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
# 正文文本
* 直接输入正文文本
> 用空格分开单词。一个换行符等同于一个空格，多个空格的效果和一个相同。
> 也就是说换行符也等同于空格。（这一点和github上的markdown一样）
> 
> 自然段分段是空一行。
# 正文符号
* 有一些符号被LaTex宏语言所占用，需要以命令形式输入：
> ```latex
> \# \$ \% \& \{ \} \textbackslash
> ```
> \# $ % & { } \
* 键盘上没有的符号用命令输入。
> ```latex
> \S \dag \ddag \P \copyright
> % dag为分节符
> \textbullet \textregistered
> \texttrademark \pounds
> ```
* 更多的符号需要使用符号字体包。（看symbols文档）
# 公式
* 数学模式下字体、符号、间距与正文都不同，一切数学公式（包括单个符号n, π）都要在数学模式下输入。
* 行内（inline）公式：
> 使用一对符号$$来表示。如$a+b=c$
* 显示（display）公式：
> * 简单的不编号公式用命令\[和\]表示。（不要使用双美元符号`$$ $$`）
> * 基本的编号的公式用equation环境。
> * 更复杂的结构，使用amsmath宏包提供的专门的数学环境。（不要使用eqnarray环境）
* 上标与下标
> ^ 和 _ 表示
* 上下画线与花括号
> \overline, \underline, \overbrace, \underbrace
* 分式
> \frac{分子}{分母}
* 根式
> \sqrt[次数]{根号下}
* 矩阵
> 使用amsmath宏包提供的专门的矩阵环境matrix, pmatrix, bmatrix等。特别复杂的矩阵（如带线条）使用array环境作为表格画出。
* 数学符号
    * 数学字母a, b, α，数学字体\mathbb(实数R)、\mathcal等
    * 普通符号，\infty(无穷)，\angle(角度)
    * 二元运算符，a+b, a-b, a点加b
    * 二元关系符，a=b, a≤b
    * 括号，<a, b>, 使用\left, \right放大
    > 大公式用大括号
    * 标点，逗号、分号(\colon)
# amsmath和mathtools
* amsmath是基本的数学工具包，在包含数学公式的文档中几乎无处不在。mathtools则对amsmath做了一些补充和增强。
> 示例
> ```latex
> \documentclass{article}
> \usepackage{amsmath}
> \usepackage{mathtools}
> 
> \begin{document}
> \begin{align*}
> 2^5 &= (1+1)^5 \\
> &= \begin{multlined}[t]
> \binom{5}{0} \cdot{1^5} + \binom{5}{1} \cdot{1^4} \cdot{1}
> + \binom{5}{2} \cdot{1^3} \cdot{1^2} \\
> + \binom{5}{3} \cdot{1^2} \cdot{1^3}
> + \binom{5}{4} \cdot{1} \cdot{1^4} + \binom{5}{5} \cdot{1^5}
> \end{multlined} \\
> &= \binom{5}{0} + \binom{5}{1} + \binom{5}{2} + \binom{5}{3}
> + \binom{5}{4} + \binom{5}{5}
> \end{align*}
> 
> \end{document}
> ```
> ![image.png](https://s2.loli.net/2022/06/26/NeHWdkuz5g4YQmS.png)
> `multlined`环境应该是多行显示的时候有缩进
>
> `&=`让多个等号对齐
# 科技功能
* siunitx: 数字单位的一揽子解决方案
> ```latex
> `\num{-1.235e96} \\
> \SI{299792458}{m/s} \\
> \SI{2×7×3.5}{m}
> ```
> ![image.png](https://s2.loli.net/2022/06/26/gANLEvn6akKTfYI.png)
> 第一个科学计数法；第二个需要用千分符，大概半个空格那么宽；
> 
> 数字个位对齐
> ```latex
> begin{tabular}{|S|}
> \hline
> -234531 \\ 13.55 \\ .9e37km \\
> \hline
> \end{tabular}
> ```
> ![image.png](https://s2.loli.net/2022/06/26/Bqon3by6agzI4GC.png)
> `\hline`是上下各加了一个横线
# 列表环境
* enumerate 编号
> ```latex
> \documentclass{article}
> 
> \begin{document}
> \begin{enumerate}
> 	\item aaa
> 	\item bbb
> 	\item ccc
> \end{enumerate}
> \end{document}
> ```
> ![image.png](https://s2.loli.net/2022/06/26/EGvtqFdAXz2ksOR.png)
* itemize 不编号
* description 有标题
# 定理类环境
* `\newtheorem`定义定理类环境，如
> `\newtheorem{thm}{定理}[section]
* 使用定理类环境，如
> ```latex
> \begin{thm}
> 一个定理
> \end{thm}
> ```
> ![image.png](https://s2.loli.net/2022/06/26/CSotNGHPjxqFwr5.png)
# 引文
* quote
* quotation
# 抄录代码
* `\verb`命令，如
> `\verb|#include <stdio.h>|
> ![image.png](https://s2.loli.net/2022/06/26/hLH9MGkVBWyfKs6.png)
* `verbatim`环境，如
> ```latex
> \begin{verbatim}
> #include <stdio.h>
> int main(){
>     print("hello world.");
> }
> \end{verbatim}
> ```
> ![image.png](https://s2.loli.net/2022/06/26/rLobI25fiYeQwAu.png)
* 使用listings宏包（带语法高亮）
> 设置起来比较麻烦
* minted宏包（调用python的Pygment）
# 算法结构（伪代码）
* clrscode宏包（算法导论）
> cmd里`texdoc clrscode`查询文档
* algorithm2e宏包
* algorithmicx宏包的algpseudocode格式
# 图表与浮动环境
* 使用tabular环境画表格
> ```latex
> \documentclass{article}
> \usepackage{xeCJK}
> \begin{document}
> 	
> 	\begin{tabular}[UTF8]{|rr|}
> 		\hline
> 		输入 & 输出 \\
> 		\hline
> 		$-2$ & 4 \\
> 		0 & 0 \\
> 		2 & 4 \\
> 		\hline
> 	\end{tabular}	
> 
> \end{document}
> ```
> 因为要输出中文，所以要把编译器切换为XeLaTex，然后又报错了，又要加上`\usepackage{XeCJK}`才可以
> `{|rr|}`生成表格竖线
> 可以使用一些工具生成表格代码，例如
> `https://www.tablesgenerator.com/latex_tables
# 功能各异的表格宏包
* 单元格处理
> `multirow`, `makecell`
>
> 前者是合并单元格，后者是拆分单元格
* 长表格
> `longtable`, `xtab` 
>
> 前者用地多一些，后者用地少一些
>
> 如果表格的内容很长，如果不使用宏包，则
> 表格不会自动换行。
* 定宽表格
> `xtabular`
>
> 用地比较少，这里的定宽**不是**说单元格的宽度，而是确定了表格的宽度。内容长了就自动换行。
* 表线控制
> `booktabs`, `diagbox`, `arydshln`
>
> 前两个是常用的
>
> 第一个是是画**三线表**的；
> 第二个是斜线宏包
> 
> ![image.png](https://s2.loli.net/2022/06/26/WI1wC2hlBtn7ODx.png)
* 表列格式
> `array`
* 综合应用
> `tabu`
# 插图
* 使用`graphicx`宏包提供的`\includegraphics`命令
> `\includegraphics[width=2cm]{pkulogo.pdf}
# 代码画图
* 优先使用外部工具画图，特别是可视化工具，例如一般的矢量图用`Inkscape`, `Illustrator(收费)`甚至`PowerPoint(保存为pdf格式)`，数学图形用`MATLAB`, `matplotlib`之类。
* 如果有合适的宏包，某些特定类型的图形也可以用LaTex代码作图。现代LaTex绘图宏包很多基于`TikZ`。
# 浮动体
* 图表都要额外地再塞到一个环境中
> 插入的一幅图或者一个表格在LaTex中其实默认是按照一个字符来使用的，就相当于一个很大的方块，它会随着文本的移动而移动，但是我们有时不希望这样。
> 
> ![image.png](https://s2.loli.net/2022/06/26/ZfgL8TxqF61sSAJ.png)
* `figure`环境, `table`环境
* 其他环境可以使用`float`宏包得到
> 浮动体的标题用`\caption`命令得到，自动编号
# 自动化工具
* 目录
> 需要编译两次
* 交叉引用
> 需要编译两次
* PDF的链接和书签
> `hyperref`宏包来实现
> 
> `hyperref`产生链接和书签的原理与普通的交叉引用相同。`hyperref`会在PDF中写入相应的“锚点”代码，在其他地方引用。交叉引用的代码并入`.aux`文件，目录的的代码并入`.toc`文件，PDF书签则产生单独的`.out`文件。
# BiBTex的使用
```latex
\bibliographystyle{plain}
% 写参考文献的格式是什么，plain表示最普通的格式
```
> 文章中的引用通过`\cite{name}`命令引用
>
> 在文章末尾通过`bibliography{}`输出参考文献列表
>
> 排版的时候，先用bibtex编译一下，在用xelatex编译两下就可以了。
> 
> 也有一键排版的工具，名字好像是`latexmk`
# 参考文献格式设置
* 选用合适的`.bst`格式，比如`plainnat`, `gbt7714-plain`。
* `batbib`宏包支持作者，年的格式
* 利用`custom-bib`产生定制的格式文件
* `biblatex`+`Biber`文献处理的新方式
# 设计文档格式
* 为了做到格式与内容分离，要做到只是用与内容相关的命令和环境。
> 比如强调一个词时，推荐使用
> `\emph{important}`
> 不推荐使用`\textit{important}
> 因为后者就把格式固定死了，为斜体。那么就可能不符合论文要求，而前者会根据不同的模板显示不同的效果。
# 使用宏包定制格式
* `forest`宏包
```latex
\documentclass{article}
\usepackage{forest}
\begin{document}
	\begin{forest}
		[A [B [TT [BB] [C]]] [SS [D] [D] [E]]]
	\end{forest}
\end{document}
```
![image.png](https://s2.loli.net/2022/06/26/R4kUilBcdVHaJwL.png)
# 格式控制功能
* 字体
> * \rmfamily, \textrm{...}
> * \sffamily, \textsf{...}
> * \ttfamily, \texttt{...}
* 字号
> `\Huge, \LARGE, \Large, \large, \normalsize, \small, \footnotesize, \scriptsize, \tiny`
* 中文字号
> `\zihao{5}, \zihao{-3}`
* 对齐
> `\centering, \raggedleft, \raggedright`
>
> 分别为居中、左对齐、右对齐，默认是两端对齐
* 空白间距
> `\hspace{2cm}, \vspace{3mm}
>
> 水平空格2cm，垂直空格3mm
* 版面布局
> `geometry`宏包，设置纸张大小，版心的大小
>
> `fancyhdr`宏包，设置章节标题、页码、页眉、也叫的格式
* 分页断行
> `\linebreak, \\`
> 
> `\\`只在画表格的时候用，写正文的时候从来不用
>
> `\pagebreak, \newpage, \clearpage, \cleardoublepage`
* 盒子
> `mbox{内容}`，只占一行的盒子
>
> `\parbox{4em}{内容|}, minipage`，占多行的盒子
# 格式应用于文档
> 如果预定义的格式不符合需要，就需要设置修改。经常文档作者本人就是格式设计者，此时更应该主义不要把格式和内容混在一起。
>
> 直接设置相关参数。如设置`\parindent`（设置段首缩进量，`parskip`（两段之间的垂直间距），`\linespread`（设置行间距，默认一倍行距），`\pagestyle`（设置有无页眉页脚等）。
>
> 修改部分命令的定义。如`\thesection, \labelenumi, \descriptionlabel, \figurename`。
>
> 利用工具宏包完成设置。如使用`ctex`宏包设置中文格式，使用`tocloft`宏包设置目录格式。
# 自定义的命令和环境
* 对于LaTex没有直接提供的格式，可以使用自定义的命令和环境实现语义的接口
> 例如，为程序名称定义一个命令：
>
> `\newcommand\prg[1]{\textsf{#1}}`，定义这个新命令，使用无衬线字体显示。这样如果想改成都用蓝色字体显示的话就会很方便。
>
> `prg`是新命令的名字，下面为示例
> ```latex
> \documentclass{article}
> \usepackage{xeCJK}
> \newcommand\prg[1]{\textsf{#1}}
> % #1的意思就是说第一个参数
> \begin{document}
> 程序\prg{sort}很有用。
> \end{document}
> ```
> ![image.png](https://s2.loli.net/2022/06/26/4yfmXRDAnS9OF6l.png)
> 
> 如果我们想改一下显示效果，则直接修改即可
> ```latex
> \documentclass{article}
> \usepackage{xeCJK}
> \newcommand\prg[1]{\textbf{\Huge #1}}
> \begin{document}
> 程序\prg{sort}很有用。
> \end{document}
> ```
> ![image.png](https://s2.loli.net/2022/06/26/nJgYytoIDawR7xu.png)
>
> **各种直接修改输出格式的命令，如字体、字号、对齐、间距的命令，都应该放在文档格式设置或自定义的命令、环境中，而避免在正文中直接使用。**
# 章节标题
* `ctex`宏包及文档类，用`\ctexset`定制。西文用`titlesec`等。
# 浮动标题
* `caption`宏包
# 列表环境
* `enumitem`宏包
> ```latex
> \usepackage{enumitem}
> \setlist{nosep}
> ```
> 将中文列表设置为普通正文的行间距
>
> ![image.png](https://s2.loli.net/2022/06/26/5E6mcs9SgevVNXA.png)