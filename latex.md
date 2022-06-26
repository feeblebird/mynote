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
>* 标题: \title, \author\, \date 
>> 把这几个设置好之后，在正文使用\maketitle就生成了对应标题
>* 摘要/前言: abstract 环境/\chapter*
>* 目录: \tableofcontents(目录是自动生成的)
>* 章节: \chapter, \section, ...
>* 附录: \appendix + \chapter或\section ...
>* 文献: \bibliography
>* 索引: \printindex
* 文档划分
>* \frontmatter, \mainmatter, \backmatter
>> 这么分的意义在于：
>> 这三个部分的格式可能不统一，frontmatter的页码可能使用罗马数字，mainmatter可能重新开始用阿拉伯数字
>* \appendix
>> 一般的文档只需要区分一个正文和附录
>* 章节层次表
>> ![image.png](https://s2.loli.net/2022/06/25/7fKsJQcytF5TdSD.png)
>> 我们最常用的就是\section
# 磁盘文件组织
> 对于较大的文档，可以将文档分成多个文件，并划分文件目录结构：
>* 主文档，给出文档框架结构
>* 按内容章节划分不同的文件
>* 使用单独的类文件和格式文件设置格式
>* 用小文件隔离复杂的图表(意思应该是用小文件表示复杂的图表)
>> 相关命令：
>>* \documentclass: 读入文档类文件(.cls)
>>* \usepackage: 读入一个格式文件——宏包(.sty)
>>* \include: 分页，并读入章节文件(.tex)
>>* \input: 读入任意的文件
# 填写文档内容
* hello world
```latex
% 英文
\documentclass{article}
\begin{document}
Hello world.
\end{document}

% 中文
% ctexart意思是chinese tex article
\documentclass{ctexart}
\begin{document}
你今天吃了吗？
\end{document}
```
![image.png](https://s2.loli.net/2022/06/26/OCMpf3ykoRY8nLF.png)
> 如果使用pdflatex编译中文文档，那么需要指出我们使用的编码为utf-8编码
> ```latex
> \documentclass[UTF8]{ctexart}
> \begin{document}
> 今天你吃了吗？
> \end{document}
> ```
> 而XeLaTex一定是utf-8编码
# 语法结构
* 命令
> 参数总在后面花括号表示，用中括号表示可选参数
>
> \cmd{arg1}{arg2}
>
> \cmd[opt]{arg1}{arg2}
>
> LaTex的分数，1/2:fraction
>
> \frac{1}{2}
>
> Tex的分数，1/2:
>
> 1 \over 2
> 第二种这种写法一般不用，因为不好表达复杂的分式
* 环境
> 环境是一种特殊的命令
> ```latex
> \begin{env}
> ...
> \end{env}
> ```
> LaTex的矩阵就是一种环境，
>
> \begin{matrix} ... \\ ... end{matrix}
>
> 上面这是一个两行的矩阵，\\为换行命令
> Tex的矩阵,
>
> \matrix{...\cr ...\cr}
* 注释
> 以符号%开头，该行字%后面的部分
# LaTex宏；命令与环境
* LaTex中的宏可以分为命令与环境：
* 命令
> 命令通常以反斜线开头，可以带0到多个参数。
> 
> 命令也可以是直接输出某种结构；也可以改变一个状态，此时LaTex用花括号{}分组或环境作为状态改变的作用域。
> 例如\em abc改变字体以强调一些文字，得到abc；
> em为emphasize的缩写，将abc变为斜体
> 
> 而带参数的命令\emph{abc}可得到同样的效果。
* 环境
> 环境的格式为
> ```latex
> \begin{env}
> 环境的内容
> \end{env}
> % 比如右对齐
> \begin{flushright}
> 文字
> \end{flushright}
> ```
