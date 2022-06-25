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