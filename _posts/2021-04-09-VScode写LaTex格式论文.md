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

/*  自动清理，清除缓存后，单次编译有时候会有问题。
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

[中文模板](https://github.com/WongChan/blog/tree/main/img/2021-04-09-VScode%E5%86%99LaTex%E6%A0%BC%E5%BC%8F%E8%AE%BA%E6%96%87/cn.tex)  

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