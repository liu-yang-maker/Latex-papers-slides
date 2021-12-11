# Latex-papers-slides
> 关于如何使用Latex写论文和PPT



LaTeX 将文章的排版以代码的形式呈现，这种方式很符合程序员以及科学工作者的审美和工作习惯，但如果强调太多LaTeX不常用的特性，会导致很多初学者望而却步，早早弃坑回归难用的word。同时，网上关于LaTeX的文档极多，还有大量多年未更新的博客，内容早已过时无法兼容现在的版本，很容易造成误导增加学习成本。

## 编辑器

流行的 TeX 发行，比如 CTeX 和 TeX Live, 都自带有一些用于编辑文档的编辑器。这些编辑器差异还是很大的，从简单的 TeXworks 到复杂的 WinEdt, 各种各样。但是不管是什么样的编辑器，他们都是用来编辑纯文本的而已（.tex 就是纯文本），换言之他们只是 Windows 自带的记事本程序的加强版而已，**他们本身并不是 TeX 系统的一部分**。

**我使用的是TeXworks**

TeXworks 为我们预设了若干排版工具（pdfTeX, pdfLaTeX, XeTeX, XeLaTeX 等），他们分别代表什么实在太过复杂并且也不是当前需要讲明白的。本文中需要用到的排版工具主要是**XeLaTeX**，关于这些工具的介绍，可以参看后文。当你对 TeX 系统相当熟悉之后，也可以不适用 TeXworks 预设的工具，自己配置排版工具。

TeXworks 默认的排版工具是 pdfLaTeX，如果你希望更改这个默认值，可以在编辑 - 首选项 - 排版 - 处理工具 - 默认 中修改。

## Hello, world!

在编辑框中，输入

```latex
\documentclass{article}
% 这里是导言区
\begin{document}
Hello, world!
\end{document}
```

