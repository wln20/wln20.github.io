### 统一序列建模与特征交叉 —— MixFormer 精读笔记

> 文章链接：https://arxiv.org/pdf/2602.14110v1
>
> 机构：字节
>
> 发布时间：2026.02
>
> Copyright (c) <a href='https://wln20.github.io/'>Wang-Luning</a>. All Rights Reserved.

MixFormer同样致力于用一个统一的类transformer模型来统一进行序列建模和特征交叉，从而解决两个模块孤立带来的模型能力瓶颈。在系统层面，其指出在有限资源下同时scale序列建模部分和特征交叉部分会造成二者竞争，因为二者在架构上是分离的，各自有一套参数，其中一边分配的计算量扩大就会导致另一边分得的变少，因此很难在全局上达到最优的scaling设计。

**MixFormer希望通过架构设计来实现序列建模和特征交叉的co-scaling**，如果想做到这一点就需要让二者处于同一个参数空间中，从而实现同时联合优化。因此，MixFormer使用一套共享的参数来同时进行序列建模和特征交叉，从而打破严格的参数分离限制，使得二者可以互相增强，让高阶特征语义直接参与到序列建模中，同时保持细粒度的行为信号。

具体而言，**MixFormer在每个block中依次使用token mixing模块（用于非序列特征的交叉）、交叉注意力模块（用于用非序列特征生成的query来提取历史序列中的信息，实现序列建模）、Output Fusion模块（对于上面的输出结果进行Per-token FFN变换，保持各个token的语义信息）。其中第token mixing和PFFN部分来自于RankMixer，用于特征交叉和保持特征语义下的变换；交叉注意力部分类似Longer、HyFormer等类target attention的做法，用于序列建模。**另外，MixFormer在所有模块中都强调多头分离计算，从而在多个特征子空间中独立提取信息。

> 可见，MixFormer其实就是将RankMixer、Longer等工作中的特征交叉、序列建模核心模块缝合到了一个统一的模块中，从而各取精华，实现了统一的特征交叉+序列建模模型。它是近半年相关工作的集大成者。





设长度为$T$的用户历史行为序列的embeddings为$S=[s_1,\cdots,s_T]$，非序列特征（如用户画像特征、目标物品特征、上下文特征等）为$\mathcal F_{ns}=\{f_1,\cdots,f_M\}$，各自对应的embedding为$e_i\in\mathbb R^{d_i}$。

参考RankMixer中的处理方式，将所有非序列特征的embedding连接成一个统一向量：$e_{ns}=[e_1;\cdots;e_M]\in\mathbb R^{D_{ns}}$，其中$D_{ns}=\sum_{i=1}^M d_i$，这部分在后续模型中会被用作query。进一步将其分割成$N$段，每段都通过一个线性层映射成维数为$x_j\in\mathbb R^D$的向量（代表一个特征子空间，在原文中称为一个head，实际处理时就是一个token）：
$$
x_j=W_j\cdot e_{ns}[d\cdot(j-1):d\cdot j],~~ j=1,\cdots,N
$$
从而得到序列$X=[x_1;\cdots;x_N]\in\mathbb R^{N\times D}$，它就是非序列特征给到模型的输入，在模型中作为主要数据流存在（在cross-attention模块中作为query来对历史序列做attention）。

这样将embedding空间分成多份可以保持表征的多样性，使得模型捕获异质的特征语义。

![image-20260226221741601](./assets/image-20260226221741601.png)

每个MixFormer block包括3个部分：Query Mixer、Cross Attention、Output Fusion，对应了原始transformer中的self-attention、cross-attention、FFN，从而充分保持transformer架构的强大表达能力，同时实现序列建模和特征交叉的集成：

- **Query Mixer**：

  实际上就是RankMixer block，用于实现非序列特征之间的高阶交叉。

  由于RankMixer中证明了对于来自不同特征空间的异质tokens做注意力意义不大，因此这里对于非序列特征$X=[x_1,\cdots,x_N]\in\mathbb T^{N\times D}$使用HeadMixing（就是对于$x_1,\cdots,x_N$的token mixing）来进行非序列特征之间的高阶交互，然后再对每个token（head）采用独立的Per-token FFN来进行变换，从而保持各个特征子空间的异质特征：
  $$
  p=[p_1,\cdots,p_N]=\text{HeadMixing}(\text{Norm}(X))+X\\
  q_i=\text{SwiGLUFFN}_i(\text{Norm}(p_i))+p_i
  $$

- **Cross Attention**：

  用于将结构化的query表征和历史序列信号进行对齐，使用带有高阶交互信息的query来提取用户历史序列中的信息。

  Query Mixer输出的$N$个query tokens被视为交叉注意力中的$N$个heads，分别关注非序列特征空间中的一个子空间，从而使得它们关注到历史序列中的不同方面。

  历史序列$S=[s_1,\cdots,s_T]$中的每次交互行为同样被处理为同维数的多头KV，从而用于和query做多头注意力。首先将每次交互行为$s_t$通过MLP转化成一个长度为$ND$表征向量$h_t$：
  $$
  h_t=\text{SwiGLUFFN}^{(l)}(\text{Norm}(s_t))+s_t\in\mathbb R^{ND}
  $$
  然后将其切成$N$段，每段对应一个维数为$D$的head：
  $$
  h_t^i=h_t[iD:(i+1)D]\in\mathbb R^D
  $$
  再进一步生成每个head的KV：
  $$
  k_t^i=W_k^ih_t^i,~~v_t=W_v^ih_t^i
  $$
  然后即可分别和query中对应的head做多头注意力，将历史序列中各个行为交互在第$i$个head上的输出进行加和，即可得到该head上的输出：
  $$
  z_i=\sum_{i=1}^T\text{softmax}(\frac{q_i^Tk_t^i}{\sqrt D})v_t^i+q_i,~~i=1,\cdots,N
  $$
  最终得到的$\{z_1,\cdots,z_N\}$即为基于非序列特征信息提取了历史序列信息后的表征，各个$z_i$捕捉了不同方面的信息。

  

- **Output Fusion**：

  实际上就是RankMixer中的Per-token FFN，用于在保持各个token独特语义的情况下对它们进行变换

  在从Query Mixer、Cross Attention模块中得到高阶非序列表征和基于非序列特征提取的历史序列信息后，进一步在该模块中将这些信号进行深度集成，从而得到最终输出表征。由于上文得到的$z_1,\cdots,z_N$各自捕捉的是独立的head上的信息，因此它们算是异质的tokens，为了保持它们独特的语义，因此借鉴RankMixer PFFN的思路来给各个token（head）$i$使用独立的MLP参数进行变换：
  $$
  o_i=\text{SwiGLUFFN}_i(\text{Norm}(z_i))+z_i
  $$
  由此得到了模型的最终输出$\{o_1,\cdots,o_N\}$，其经过处理后送入各种任务塔即可用于预测输出。





另外，借鉴SCTA等工作中的RLB（Request Level Batching）思想，希望能够**将用户侧特征和目标物品侧特征进行解耦，从而在多个候选物品/多次请求间共享同一套计算好的用户侧表征**。然而MixFormer的原始设计中，用户和物品特征被混合为非序列特征，在Query Mixier模块中进行了充分混合，使得在后续层中完全无法分出纯粹的用户侧特征或物品侧特征，难以在计算上进行解耦。

因此，为了能够应用RLB，进一步设计了一种用户-物品解耦的MixFormer变体：

![image-20260227145413509](./assets/image-20260227145413509.png)

- 特征解耦：显式地将非序列特征分成用户侧和物品侧两个子集，分别含有$N_U,N_G$个heads（tokens），并作为MixFormer的输入。二者之和为$N_U+N_G=N$，且通常数量比例设为$N_U:N_G=1:1$

- 带mask的Query Mixer：token mixing操作会使得各个head的信息被混合，其输出不再能区分纯粹的用户侧或物品侧表征。因此，设计了一种单向的user-to-item的信息融合机制，也即：对于那些user heads，只在user侧的这些heads内部进行混合，不允许item heads的信息混合过来，而允许user侧的heads的信息混合到item heads这边来。

  如上图中的混合结果可见，混合完后的user heads中仍只有来自user侧的信息，而item heads中则混入了来自user侧的信息。这样就确保了user heads仍是完全来源于user侧的信息，而没有糅合item侧的信息，从而可以将它们和目标物品解耦，从而复用于不同目标物品/不同请求。

  具体操作上，可以先正常混合，然后再对混合结果施加一个mask，去除从item侧传递到user heads中的信息，如上图mask&reshape结果中的白色部分：
  $$
  \mathcal M[i,j]=\begin{cases}
  0,& i<N_U~\text{and}~ j\geq N_U\frac{D}{N}\\1,&else
  \end{cases}\\
  \text{HeadMixing}_{\text{decouple}}(\cdot)=\mathcal M\odot\text{HeadMixing}(\cdot)
  $$

