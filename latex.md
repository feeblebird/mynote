# cmd调出符号文档
* 命令为:
> texdoc symbols

# 组织文档结构
* latex文档基本结构
> 以**document**环境为界，**document**环境前是导言部分(**preamble**)；环境内部是正文部分；环境之后的部分被忽略。
```latex
%%% 简单文档
% 导言：格式设置
\documentclass{ctexart}
\usepackage[b5paper]{geometry}
% 正文：填写内容
\begin{document}
使用 \LaTex
\end{document}
```
> %是注释
>
> b5paper是设置纸张大小为b5
>
> begin{document}就是正文的开始
* 文档部件
> * 标题: \title, \author\, \date 
    > 把这几个设置好之后，在正文使用\maketitle就生成了对应标题
> * 摘要/前言: abstract 环境/\chapter*
> * 目录: \tableofcontents(目录是自动生成的)
> * 章节: \chapter, \section, ...
> * 附录: \appendix + \chapter或\section ...
> * 文献: \bibliography
> * 索引: \printindex
* 文档划分
> * \frontmatter, \mainmatter, \backmatter
> 
> 这么分的意义在于：
>
> 这三个部分的格式可能不统一，frontmatter的页码可能使用罗马数字，mainmatter可能重新开始用阿拉伯数字