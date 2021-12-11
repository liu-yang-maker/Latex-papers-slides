# Latex-papers-slides
> 关于如何使用Latex写论文和PPT

我们给了一个Datawhale的模版供大家参考 https://github.com/liu-yang-maker/datawhale-beamer-zh-CN

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

很容易发现，输入进编辑框的五行文字，在最终输出的 pdf 档中只显示了 1 行。事实上，交付 TeX 处理的文档内容，并不会全部输出。

此处的第一行`\documentclass{article}`中包含了一个控制序列（或称命令 / 标记）。所谓控制序列，是以反斜杠`\`开头，以第一个**空格或非字母** 的字符结束的一串文字，他们并不被输出，但是他们会影响输出文档的效果。这里的控制序列是`documentclass`，它后面紧跟着的`{article}`代表这个控制序列有一个必要的参数，该参数的值为`article`. 这个控制序列的作用，是调用名为 “article” 的文档类。

只有在 “document” 环境中的内容，才会被正常输出到文档中去或是作为控制序列对文档产生影响。因此，在`\end{document}`之后插入任何内容都是无效的。`\begin{document}`与`\documentclass{article}`之间的部分被称为导言区。导言区中的控制序列，通常会影响到整个输出文档。

## 中英文混排

除掉成功生成第一个文档，实现中文输出（或者说是中英文混排）恐怕是困扰中国的 TeX 使用者的第二个普遍问题。众所周知，TeX 系统是高教授开发的，当初并没有考虑到亚洲文字的问题。因此早期的 TeX 系统并不能直接支持中文，必须要用其他工具先处理一下（或者是一些宏包之类的）。

但是现在，XeTeX 原生支持 Unicode，并且可以方便地调用系统字体。可以说解决了困扰中国 TeX 使用者多年的大问题。

此外，除去中文支持，中文的版式处理和标点禁则也是不小的挑战。好在由吴凌云和江疆牵头，现在主要由刘海洋和李清（还有我打个酱油）维护的 `ctex` 宏包 / 文档类一次性解决了这些问题。`ctex` 宏包和文档类的优势在于，它适用于多种编译方式；在内部处理好了中文和中文版式的支持，隐藏了这些细节；并且，提供了不少中文用户需要的功能接口。

为了和原有的日志对接，这里分别用两种方法来介绍中英文混排。当然，老方法只是为了「兼容性」存在的，推荐使用新方法。

在 TeXworks 编辑框中输入以下内容，保存，使用 XeLaTeX 编译：

```latex
\documentclass[UTF8]{ctexart}
\begin{document}
你好，world!
\end{document}
```

相较于之前的例子，这份代码只有细微的差异：

1. 文档类从 `article` 变为 `ctexart`；
2. 增加了文档类选项 `UTF8`。

`ctex` 宏包和文档类的默认配置是为使用简体中文 Windows 系统的用户配置的，在 Linux 或 Unix 系统（包括 OS X）下使用会遇到一点困难。对此，项目组官方给出了一个 wiki 来解释说明。参见：https://code.google.com/p/ctex-kit/wiki/UnixFonts

## 组织你的文章

### 作者、标题、日期

```latex
\documentclass[UTF8]{ctexart}
\title{你好，world!}
\author{Liam}
\date{\today}
\begin{document}
\maketitle
你好，world!
\end{document}
```

### 章节和段落

```latex
\documentclass[UTF8]{ctexart}
\title{你好，world!}
\author{Liam}
\date{\today}
\begin{document}
\maketitle
\section{你好中国}
中国在 East Asia.
\subsection{Hello Beijing}
北京是 capital of China.
\subsubsection{Hello Dongcheng District}
\paragraph{Tian'anmen Square}
is in the center of Beijing
\subparagraph{Chairman Mao}
is in the center of 天安门广场。
\subsection{Hello 山东}
\paragraph{山东大学} is one of the best university in 山东。
\end{document}
```

### 插入目录

```latex
\documentclass[UTF8]{ctexart}
\title{你好，world!}
\author{Liam}
\date{\today}
\begin{document}
\maketitle
\tableofcontents
\section{你好中国}
中国在 East Asia.
\subsection{Hello Beijing}
北京是 capital of China.
\subsubsection{Hello Dongcheng District}
\paragraph{Tian'anmen Square}
is in the center of Beijing
\subparagraph{Chairman Mao}
is in the center of 天安门广场。
\subsection{Hello 山东}
\paragraph{山东大学} is one of the best university in 山东。
\end{document}
```

## 插入数学公式

为了使用 AMS-LaTeX 提供的数学功能，我们需要在导言区加载`amsmath`宏包：

```latex
\usepackage{amsmath}
```

### 数学模式

LaTeX 的数学模式有两种：行内模式 (inline) 和行间模式 (display)。前者在正文的行文中，插入数学公式；后者独立排列单独成行。

在行文中，使用`$ ... $`可以插入行内公式，使用`\[ ... \]`可以插入行间公式，如果需要对行间公式进行编号，可以使用`equation`环境： \begin{equaion} … \end{equation}

> 行内公式也可以使用`\(...\)`来插入，略嫌麻烦。无编号的行间公式也可以使用`$$ ... $$`来插入，但是这样做会改变行文的默认行间距，不推荐。

### 上下标

```latex
\documentclass{article}
%
% 数学环境支持
% %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\usepackage{amsmath}
\begin{document}
Einstein 's $E=mc^2$.

\[ E=mc^2. \]

\begin{equation}
E=mc^2.
\end{equation}
\end{document}
```

## 插入图片和表格

### 图片

在 LaTeX 中插入图片，有很多种方式。最好用的应当属利用`graphicx`宏包提供的`\includegraphics`命令。比如你在你的 TeX 源文件同目录下，有名为 a.jpg 的图片，你可以用这样的方式将它插入到输出文档中：

```latex
\documentclass{article}
\usepackage{graphicx}
\begin{document}
\includegraphics{a.jpg}
\end{document}
```

图片可能很大，超过了输出文件的纸张大小，或者干脆就是你自己觉得输出的效果不爽。这时候你可以用

`\includegraphics`控制序列的可选参数来控制。比如

```latex
\includegraphics[width = .8\textwidth]{a.jpg}
```

这样图片的宽度会被缩放至页面宽度的百分之八十，图片的总高度会按比例缩放。

> `\includegraphics`控制序列还有若干其他的可选参数可供使用，一般并用不到。感兴趣的话，可以去查看[该宏包的文档](http://texdoc.net/texmf-dist/doc/latex/graphics/graphicx.pdf)。

### 表格

`tabular`环境提供了最简单的表格功能。它用`\hline`命令表示横线，`|`表示竖线；用`&`来分列，用`\\`来换行；每列可以采用居中、居左、居右等横向对齐方式，分别用`l`、`c`、`r` 来表示。

```latex
\begin{tabular}{|l|c|r|}
 \hline
操作系统& 发行版& 编辑器\\
 \hline
Windows & MikTeX & TexMakerX \\
 \hline
Unix/Linux & teTeX & Kile \\
 \hline
Mac OS & MacTeX & TeXShop \\
 \hline
通用& TeX Live & TeXworks \\
 \hline
\end{tabular}
```

### 浮动体

插图和表格通常需要占据大块空间，所以在文字处理软件中我们经常需要调整他们的位置。`figure`和`table`环境可以自动完成这样的任务；这种自动调整位置的环境称作浮动体 (float)。我们以`figure`为例。

```latex
\begin{figure}[htbp]
\centering
\includegraphics{a.jpg}
\caption{有图有真相}
\label{fig:myphoto}
\end{figure}
```

“htbp” 选项用来指定插图的理想位置，这几个字母分别代表 here, top, bottom, float page，也就是就这里、页顶、页尾、浮动页 (专门放浮动体的单独页面) 。`\centering`用来使插图居中；`\caption`命令设置插图标题，LaTeX 会自动给浮动体的标题加上编号。注意`\label`应该放在标题之后。

## 版面设置

### 页边距

设置页边距，推荐使用`geometry`宏包。可以在[这里](http://texdoc.net/texmf-dist/doc/latex/geometry/geometry.pdf)查看它的说明文档。

比如我希望，将纸张的长度设置为 20cm、宽度设置为 15cm、左边距 1cm、右边距 2cm、上边距 3cm、下边距 4cm，可以在导言区加上这样几行：

```latex
\usepackage{geometry}
\geometry{papersize={20cm,15cm}}
\geometry{left=1cm,right=2cm,top=3cm,bottom=4cm}
```

### 页眉页脚

设置页眉页脚，推荐使用`fancyhdr`宏包。可以在[这里](http://texdoc.net/texmf-dist/doc/latex/fancyhdr/fancyhdr.pdf)查看它的说明文档。

比如我希望，在页眉左边写上我的名字，中间写上今天的日期，右边写上我的电话；页脚的正中写上页码；页眉和正文直接有一道宽为 0.4pt 的横线分割，可以在导言区加上如下几行：

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\lhead{\author}
\chead{\date}
\rhead{152xxxxxxxx}
\lfoot{}
\cfoot{\thepage}
\rfoot{}
\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\headwidth}{\textwidth}
\renewcommand{\footrulewidth}{0pt}
```

### 首行缩进

中国人写文章，习惯每一段的段首都空出两个中文汉字的长度。美国人没有这个习惯，他们每一小节的段首都顶格。为了解决这个问题，我们可以在导言区调用`\usepackage{indentfirst}`.

就算是这样，首行缩进的长度，仍然不符合中国人的习惯。我们可以在导言区添加这样的控制序列`\setlength{\parindent}{2.45em}`来调整首行缩进的大小。这里的 2.45em 是中文小四号字大小两个中文字的长度。

### 行间距

我们可以通过`setspace`宏包提供的命令来调整行间距。比如在导言区添加如下内容，可以将行距设置为 1.5 倍：

```latex
\usepackage{setspace}
\onehalfspacing
```

具体可以查看该宏包的[文档](http://texdoc.net/texmf-dist/doc/latex/setspace/README)。

### 段间距

我们可以通过修改计数器`\parskip`的值来调整段间距。例如在导言区添加以下内容

```latex
\addtolength{\parskip}{.4em}
```

则可以在原有的基础上，增加段间距 0.4em. 如果需要减小段间距，只需将该数值改为负值即可。
