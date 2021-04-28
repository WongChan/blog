---
layout: post
title:  VScode写LaTex格式论文
description: 
categories: VScode
date:   2021-04-09
tags:   LaTex
---

Windows 和 Linux 都能使用 TeXLive 和 VSCode，VSCode 是一个非常好用的编辑器

<img class="img-responsive image-center thumbnail" src="{{site.url}}/blog/img/2021-04-09-VScode写LaTex格式论文/vscode.jpg" width = "100%" alt="vscode.jpg" align=center />

<!-- more -->

## TeXLive 下载与安装

### Windows

[TeXLive 官网传送门](https://www.tug.org/texlive)  
安装时长 20 分钟左右

```
清华源：https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/
以管理员身份运行 `install-tl-windows.bat` 安装 texlive 202X，
高级系统设置-环境变量-选择path双击，
新建 添加 D:\Program Files\texlive\year\bin\win32 (安装目录)
最后重启VS Code就行了。
```

### Ubuntu
1. 安装texlive
```shell
sudo apt-get install texlive-full
```
2. 安装中文字体包
```shell
sudo apt install latex-cjk-all
```
## VSCode 下载与安装

[VSCode 官网传送门](https://code.visualstudio.com)

### LaTexWorkshop 插件安装

*   打开 VSCode
*   <Ctrl+Shift+x> 打开扩展管理，搜索 LaTeX Workshop，点击安装
*   安装完后启动插件，重启 VSCode

## 插件配置及中文支持

*   点击文件 -> 首选项 -> 设置
*   搜索`latex-workshop.latex.recipes`并点击`Edit setttings.json`，打开后左边为插件默认配置，无法修改，我们可以在右侧用户设置中定义同样的属性名称，达到修改配置的目的  


<img class="img-responsive image-center thumbnail" src="{{site.url}}/blog/img/2021-04-09-VScode写LaTex格式论文/Latex.jpg" width = "100%" alt="Latex.jpg" align=center />

所有配置如下

```json
//系统自带{

// ---------- LaTeX Workshop ----------
"latex-workshop.intellisense.package.enabled": true,
"latex-workshop.message.log.show": true,
"latex-workshop.message.badbox.show": true,

// 把 Latex Workshop 命令添加进右键菜单
"latex-workshop.showContextMenu": true,

//"latex-workshop.latex.autoBuild.run": "never",  //保存不自动编译

//	编译出错，插件会弹出两个很烦人的气泡, 设置为false则不显示
"latex-workshop.message.error.show": false,
"latex-workshop.message.warning.show": false,

/*  自动清理，清楚缓存后，单次编译会有问题。
"latex-workshop.latex.autoClean.run": "onBuilt",  //onFailed
"latex-workshop.latex.clean.fileTypes": [
  "*.aux",
  "*.bbl",
  "*.blg",
  "*.idx",
  "*.ind",
  "*.lof",
  "*.lot",
  "*.out",
  "*.toc",
  "*.acn",
  "*.acr",
  "*.alg",
  "*.glg",
  "*.glo",
  "*.gls",
  "*.ist",
  "*.fls",
  "*.log",
  "*.fdb_latexmk",
],
*/

"latex-workshop.view.pdf.viewer": "tab",

//	组合
"latex-workshop.latex.recipes": [

  {
    "name": "latexmk 🔃",
    "tools": [
      "latexmk"
    ]
  },

  {
    "name": "latexmk (latexmkrc)",
    "tools": [
      "latexmk_rconly"
    ]
  },

  {
    "name": "latexmk (lualatex)",
    "tools": [
      "lualatexmk"
    ]
  },

  {
    "name": "pdflatex ➞ bibtex ➞ pdflatex × 2",
    "tools": [
      "pdflatex",
      "bibtex",
      "pdflatex",
      "pdflatex"
    ]
  },

  {
    "name": "Compile Rnw files",
    "tools": [
      "rnw2tex",
      "latexmk"
    ]
  },

  {
    "name": "Compile Jnw files",
    "tools": [
      "jnw2tex",
      "latexmk"
    ]
  },

  {
    "name": "tectonic",
    "tools": [
      "tectonic"
  ]
  },
    
//自己设置的
  {
    "name": "xelatex",//支持中文
    "tools": [
      "xelatex"
    ]
  },

  {
    "name": "pdflatex",
    "tools": [
      "pdflatex"
    ]
  },

  {
    "name": "ptex2pdf",
    "tools": [
      "ptex2pdf"
    ]
  },

  {
    "name": "x-bib-x*2",
    "tools": [
      "xelatex",
      "bibtex",
      "xelatex",
      "xelatex"
    ]
  },  

  {
    "name": "p-bib-p*2",
    "tools": [
      "ptex2pdf",
      "bibtex",
      "ptex2pdf",
      "ptex2pdf"
    ]
}],

//	工具
"latex-workshop.latex.tools": [

  {
    "name": "latexmk",
    "command": "latexmk",
    "args": [
      "-synctex=1",
      "-interaction=nonstopmode",
      "-file-line-error",
      "-pdf",
      "%DOCFILE%"
    ]
  },  

  {
    "name": "latexmk_rconly",
    "command": "latexmk",
    "args": [
        "%DOCFILE%"
    ]
  },   

  {
    "name": "lualatexmk",
    "command": "latexmk",
    "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-lualatex",
        "-outdir=%OUTDIR%",
        "%DOCFILE%"
      ]
  },  
 
  {//	支持中文
    "name": "xelatex",
    "command": "xelatex",
    "args": [
      "-synctex=1",
      "-interaction=nonstopmode",
      "-file-line-error",
      "-pdf",
      "%DOCFILE%"
   ]
  },

  {
    "name": "pdflatex",
    "command": "pdflatex",
    "args": [
      "-synctex=1",
      "-interaction=nonstopmode",
      "-file-line-error",
      "%DOCFILE%"
    ]
  },  


  {//	
    "name": "ptex2pdf",
    "command": "ptex2pdf",
    "args": [
      "-l",
      "-ot",
      "-kanji=utf8 -synctex=1 -interaction=nonstopmode",
      "%DOCFILE%"
    ]
  },
  
  {//	bib参考文献
    "name": "bibtex",
    "command": "bibtex",
    "args": [
        "%DOCFILE%"
    ]
}],


/*
//	外置SumatraPDF
"latex-workshop.view.pdf.viewer": "external",

"latex-workshop.view.pdf.external.viewer.command": "C:/.../SumatraPDF.exe",
"latex-workshop.view.pdf.external.viewer.args": [
    "-forward-search",
    "%TEX%",
    "%LINE%",
    "-reuse-instance",
    "-inverse-search",
    "\"C:/.../Microsoft VS Code/Code.exe\" \"C:/.../Microsoft VS Code/resources/app/out/cli.js\" -gr \"%f\":\"%l\"",
    "%PDF%"
],

//	正反向搜索
"latex-workshop.view.pdf.external.synctex.command": "C:/.../SumatraPDF.exe",
"latex-workshop.view.pdf.external.synctex.args": [
    "-forward-search",
    "%TEX%",
    "%LINE%",
    "-reuse-instance",
    "-inverse-search",
    "\"C:/.../Microsoft VS Code/Code.exe\" \"C:/.../Microsoft VS Code/resources/app/out/cli.js\" -gr \"%f\":\"%l\"",
    "%PDF%",
],
*/


//
"latex-workshop.message.latexlog.exclude": [
"(Font shape `(JY1|JT1|JY2|JT2)(/.*)(sl|it|sc)'.*|Some font shapes were not available.*)"
],

//系统自带}
```

配置解释如下


*   `"latex-workshop.latex.clean.fileTypes"`删除哪些文件
*   `“latex-workshop.latex.tools”`配置排版引擎程序
*   `"latex-workshop.latex.recipes"`定义排版引擎程序调用顺序

**注意**  
默认使用排版引擎程序调用顺序配置`"latex-workshop.latex.recipes"`中的第一个进行编译排版，上述配置中第一个`xelatex`不会对 bib 形式的参考文献编译排版，如用 bib 形式的参考文献请把第三个`x-bib-x*2`移到第一个，否则会报错


### LaTeX 实例

```LaTex
\documentclass[UTF8]{ctexart}
\begin{document}
你好 world!
\end{document}
```

中文模板
```latex
%保存为UTF-8编码格式
%用xelatex编译
 
\documentclass[UTF8,a4paper,12pt]{ctexart}
\usepackage[left=2.50cm, right=2.50cm, top=2.50cm, bottom=2.50cm]{geometry} %页边距
\CTEXsetup[format={\Large\bfseries}]{section} %设置章标题字号为Large，居左
%\CTEXsetup[number={\chinese{section}}]{section}
%\CTEXsetup[name={（,）}]{subsection}
%\CTEXsetup[number={\chinese{subsection}}]{subsection}
%\CTEXsetup[name={（,）}]{subsubsection}
%\CTEXsetup[number=\arabic{subsubsection}]{subsubsection}  %以上四行为各级标题样式设置，可根据需要做修改
 
%\linespread{1.5} %设置全文行间距
 
 
%\usepackage[english]{babel}
%\usepackage{float}     %放弃美学排版图表
\usepackage{fontspec}   %修改字体
\usepackage{amsmath, amsfonts, amssymb} % 数学公式相关宏包
\usepackage{color}      % color content
\usepackage{graphicx}   % 导入图片
\usepackage{subfigure}  % 并排子图
\usepackage{url}        % 超链接
\usepackage{bm}         % 加粗部分公式，比如\bm{aaa}aaa
\usepackage{multirow}
\usepackage{booktabs}
\usepackage{epstopdf}
\usepackage{epsfig}
\usepackage{longtable}  %长表格
\usepackage{supertabular}%跨页表格
\usepackage{algorithm}
\usepackage{algorithmic}
\usepackage{changepage}
 
 
 
%%%%%%%%%%%%%%%%%%%%%%%
% -- text font --
% compile using Xelatex
%%%%%%%%%%%%%%%%%%%%%%%
% -- 中文字体 --
%\setCJKmainfont{Microsoft YaHei}  % 微软雅黑
%\setCJKmainfont{YouYuan}  % 幼圆
%\setCJKmainfont{NSimSun}  % 新宋体
%\setCJKmainfont{KaiTi}    % 楷体
\setCJKmainfont{SimSun}   % 宋体
%\setCJKmainfont{SimHei}   % 黑体
 
% -- 英文字体 --
\setmainfont{Times New Roman}
%\setmainfont{DejaVu Sans}
%\setmainfont{Latin Modern Mono}
%\setmainfont{Consolas}
%
%
\renewcommand{\algorithmicrequire}{ \textbf{Input:}}     % use Input in the format of Algorithm
\renewcommand{\algorithmicensure}{ \textbf{Initialize:}} % use Initialize in the format of Algorithm
\renewcommand{\algorithmicreturn}{ \textbf{Output:}}     % use Output in the format of Algorithm
\renewcommand{\abstractname}{\textbf{\large {摘\quad 要}}} %更改摘要二字的样式
\newcommand{\xiaosi}{\fontsize{12pt}{\baselineskip}}     %\xiaosi代替设置12pt字号命令,不加\selectfont,行间距设置无效
\newcommand{\wuhao}{\fontsize{10.5pt}{10.5pt}\selectfont}
 
\usepackage{fancyhdr} %设置全文页眉、页脚的格式
\pagestyle{fancy}
\lhead{}           %页眉左边设为空
\chead{}           %页眉中间
\rhead{}           %页眉右边
%\rhead{\includegraphics[width=1.2cm]{1.eps}}  %页眉右侧放置logo
\lfoot{}          %页脚左边
\cfoot{\thepage}  %页脚中间
\rfoot{}          %页脚右边
 
 
%%%%%%%%%%%%%%%%%%%%%%%
%  设置水印
%%%%%%%%%%%%%%%%%%%%%%%
%\usepackage{draftwatermark}         % 所有页加水印
%\usepackage[firstpage]{draftwatermark} % 只有第一页加水印
% \SetWatermarkText{Water-Mark}           % 设置水印内容
% \SetWatermarkText{\includegraphics{fig/ZJDX-WaterMark.eps}}         % 设置水印logo
% \SetWatermarkLightness{0.9}             % 设置水印透明度 0-1
% \SetWatermarkScale{1}                   % 设置水印大小 0-1
 
\usepackage{hyperref} %bookmarks
\hypersetup{colorlinks, bookmarks, unicode} %unicode
 
 
 
\title{\textbf{\Large{Carol的中文\LaTeX{}模板}}}
\author{ Carol\thanks{simmel} }
\date{\today}
 
 
 
\begin{document}
 
\maketitle
%\tableofcontents
 
\begin{abstract}
这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。
 
这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。这里是中文摘要。
\end{abstract}
 
\begin{center}
\large{\textbf{Abstract}}
\end{center}
 
\begin{adjustwidth}{1cm}{1cm}
\hspace{1.5em}Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.Here is the first par. of abstract.
 
\noindent\hspace{1.5em}Here is the second par. of abstract.Here is the second par. of abstract.Here is the second par. of abstract.Here is the second par. of abstract.Here is the second par. of abstract.Here is the second par. of abstract.Here is the second par. of abstract.Here is the second par. of abstract.
\end{adjustwidth}
 
\thispagestyle{empty}       %本页不显示页码
\newpage                    %分页
%\tableofcontents\thispagestyle{empty}
\newpage
\setcounter{page}{1}        %从下面开始编页，页脚格式为导言部分设置的格式
 
 
\section{第一部分}
这是第一部分
\subsection{第一部分的子部分}
这里是第一部分的子部分
 
\section{第二部分}
这里是第二部分
\subsection{第二部分的子部分}
这里是第二部分的子部分
 
%\section{一些工具}
%插入公式
%\begin{equation}\label{eq}
%  \gamma _2^{\text{C}} = \frac{{{P_{RT}}g}}{{{P_{BT}}d_{_{{B_2}2}}^{ - \alpha } + {N_0}}}
%\end{equation}
 
%插入图片
%\begin{figure}[H]   %*表示可跨栏，如果不需要可去掉
%\centering
%\subfigure[$\sum {{I_C}}  < {I_B}$]{
%  \includegraphics[width=7cm]{1.eps}}
%  %\hspace{0cm}      %两张图片之间的距离
%%\hfill               %撑满整行
%\centering
%\subfigure[$\sum {{I_C}}  > {I_B}$]{
%  \includegraphics[width=7cm]{2.eps}}
%\caption{系统的模式选择}\label{fig}
%\end{figure}
 
插入表格
\begin{table}[H] \wuhao             %局部字体设置大小
   \centering
  \caption{系统模型符号}\label{tab}
  \begin{tabular}{c|c}
    \toprule                  %设置为顶线默认格式 加粗
    % after \\: \hline or \cline{col1-col2} \cline{col3-col4} ...
    符号 & 说明 \\
    \hline                  %普通横线
    ${{B_1}\mbox{、}{B_2}}$ & 基站的下标表示 \\
    ${C_1}\mbox{、}{C_2}$ & 蜂窝用户的下标表示 \\
    $D$ & D2D用户的下标表示 \\
    $R$ & 中继用户的下标表示 \\
    ${P_{it}}\left( {i = B,C,D,R} \right)$ & 终端$i$的发射功率 \\
    ${d_{ij}}(i,j = {B_k},{C_k},1,2,R;i \ne j,k = 1,2)$ & 设备$i$到设备$j$的距离 \\
    ${h_{ij}}(i,j = {B_k},{C_k},1,2,R;i \ne j,k = 1,2)$ &$i$-$j$ 链路的信道系数\\
    ${n_i}\left( {{n_i}\sim N\left( {\mu ,{N_0}} \right)} \right)$ & 高斯白噪声 \\
    ${P_{ij}} = {P_{iT}}d_{ij}^{ - \alpha }$ & 终端$j$收到的终端$i$发送的信号功率\\
    $\alpha$ & 路径衰落系数 \\
    \bottomrule                %设置为底线默认格式
  \end{tabular}
\end{table}
 
引用：图\ref{fig},式\eqref{eq},表\ref{tab}
 
\end{document}

```

经过上述设置，编写好 tex 文件后，<Ctrl+s> 在保存文件的同时进行编译输出


## 插入文献bib文件

### 新建lib
在.tex同一文件夹下，新建一个.bib文件，例如ref.bib，把要引用的文献的bibtex格式复制粘贴进去，这个各大搜索引擎如谷歌学术什么的应该都有，以下是一个例子，注意其中mirowski2018learning为引用文献的变量名

```
@misc{mirowski2018learning,
    title={Learning to Navigate in Cities Without a Map},
    author={Piotr Mirowski and Matthew Koichi Grimes and Mateusz Malinowski and Karl Moritz Hermann and Keith Anderson and Denis Teplyashin and Karen Simonyan and Koray Kavukcuoglu and Andrew Zisserman and Raia Hadsell},
    year={2018},
    eprint={1804.00168},
    archivePrefix={arXiv},
    primaryClass={cs.AI}
}
```
### latex编写

新建以bib为后缀的文件，将谷歌学术的内容复制进入此文件，并在文章的最后，加入如下代码。

```LaTex
\documentclass[UTF8]{ctexart} 

\usepackage{cite} % 导入引用的包，能够使用\cite

\begin{document}

% \cite括号内为引用文献的变量名，\cite前要有一个空格
% 在正文中引用，如果不引用则在参考文献部分中不显示该文献
Learning to Navigate in Cities Without a Map \cite{mirowski2018learning}. 

\bibliography{ref} % 导入lib，ref为“ref.lib"的文件名
\bibliographystyle{ieeetr} % 参考文献排版风格，这个是IEEE transaction的，其他可以自查
\end{document}
```
### 编译显示

运行 BibTeX分为下面四步

1. 用LaTeX编译你的 .tex 文件 , 这是生成一个 .aux 的文件, 这告诉BibTeX 将使用那些引用.
2. 用BibTeX 编译 .bib 文件.
3. 再次用LaTeX 编译你的 .tex 文件, 这个时候在文档中已经包含了参考文献, 但此时引用的编号可能不正确.
4. 最后用 LaTeX 编译你的 .tex 文件, 如果一切顺利的话, 这是所有东西都已正常了.

```shell
latex references.tex  //普通编译第一次
btbtex yourfilename   //第二次编译
latex references.tex  //普通编译第三次
latex references.tex  //普通编译第四次
```
但是对于VSCode，由于latex workshop的插件，使得只需要保存就是自动执行latex编译"latex references.tex"。

注意:添加参考文献即更改lib文件之后需重新执行以上操作。







## 注意

文件所在路径和文件名不要有中文，不然会编译失败