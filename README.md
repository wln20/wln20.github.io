# Luning's Blog

- pdf文件：挂在`./files/`下，通过`https://wln20.github.io/files/XXX.pdf`在浏览器端直接显示
- posts：若希望直接让md渲染成的html中正确显示数学公式，则在开头指定`math: true`
- posts：若希望md渲染成的html中具有目录，则：

  开头指定：`layout: single`和`toc: true`
  
  在内容之前写：
  ```
  ## 目录
  {: .no_toc}
  
  * TOC
  {:toc}
  ```
  后续可通过`##`、`###`等md中的目录来对应章节
- publications：仿照`./publications/`下的md文件
