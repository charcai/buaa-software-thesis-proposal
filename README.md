# 北航软件学院本科毕设开题报告 LaTeX 模板

依据《软件学院本科毕设开题报告》Word 模板制作，适用于北京航空航天大学软件学院本科毕业设计（论文）开题报告。保留原模板的章节结构和说明文字，使用 XeLaTeX 编译。

封面、页眉页脚、字体和字号依据原 DOC 设置。正文采用标准 LaTeX 语法，标点处理使用 xeCJK，引用使用 cite 宏包，目录保留贴近原 Word 的点线、缩进与字体样式。

[查看模板 PDF](proposal.pdf) · [查看综合示例 PDF](example.pdf)

## 快速开始

安装包含 XeLaTeX 和 latexmk 的 TeX 发行版，例如 TeX Live 或 MacTeX，并准备下文列出的字体。模板使用 fontspec、xeCJK、geometry、graphicx、xcolor、eso-pic、cite 和 hyperref，综合示例还使用 amsmath 和 booktabs。

打开 `proposal.tex`，填写顶部的封面信息，再将说明文字替换为自己的报告内容。

~~~latex
\newcommand{\ReportTitle}{你的毕业设计题目}
\newcommand{\StudentName}{你的姓名}
\newcommand{\StudentID}{你的学号}
\newcommand{\SchoolSupervisor}{学院指导老师}
\newcommand{\CompanySupervisor}{}
\newcommand{\SupervisorCompany}{}
\newcommand{\ReportYear}{2026}
\newcommand{\ReportMonth}{11}
\newcommand{\ReportDay}{18}
~~~

在主文件所在目录运行以下命令，生成 `proposal.pdf`。latexmk 自动执行目录和交叉引用所需的多轮编译。

~~~sh
latexmk -xelatex proposal.tex
~~~

VS Code 的 LaTeX Workshop 可选择 `latexmk (xelatex)` 编译配方。项目附带 `.latexmkrc`，编译引擎使用 XeLaTeX。复制模板时保留样式文件、图片及所需字体的相对位置。

## 字体

模板依次查找项目目录中的指定字体文件、系统已安装的同名字体、macOS 中 Microsoft Word 自带的对应字体文件。缺少所需字体时编译停止。

| 字体 | 项目根目录中的文件名 |
| --- | --- |
| Times New Roman | `TimesNewRoman.ttf` |
| 宋体（SimSun） | `SimSun.ttc` |
| 黑体（SimHei） | `SimHei.ttf` |
| 华文新魏（STXinwei） | `STXinwei.ttf` |
| 楷体_GB2312（KaiTi_GB2312） | `KaiTi_GB2312.ttf` |
| Arial | `Arial.ttf` |

Windows、Linux 和在线编译环境也需要提供这些字体。文件名区分大小写的平台应使用表中的名称。楷体_GB2312、楷体和华文楷体是不同字体。

| 用途 | 中文字体 | 西文及数字 |
| --- | --- | --- |
| 封面大标题 | 华文新魏，36 磅 | Times New Roman |
| 封面填写栏 | 黑体，14 磅，加粗 | Times New Roman，14 磅，加粗 |
| 封面标签 | 黑体，14 磅 | Times New Roman，14 磅 |
| 学院行、日期 | 宋体，14 磅 | Times New Roman，14 磅 |
| 页眉、页脚校名 | 楷体_GB2312，9 磅 | 同一款楷体_GB2312 |
| 页脚页码 | 连接号为宋体，9 磅 | Times New Roman，9 磅 |
| 一级、二级标题 | 黑体，15 / 14 磅 | Times New Roman，15 / 14 磅 |
| 三级标题 | 黑体，12 磅 | 黑体，12 磅，编号为 14 磅加粗黑体 |
| 正文、参考文献 | 宋体，12 磅 | Times New Roman，12 磅 |
| 一级目录 | 黑体，12 磅 | 标题编号为 Times New Roman，页码为 Arial |
| 二级目录 | 宋体，12 磅 | Times New Roman，12 磅 |
| 三级目录 | 宋体，10 磅，斜体 | Times New Roman，10 磅，斜体 |
| 引用上标 | 宋体，6 磅 | 宋体，6 磅 |

字号使用 bp 单位。粗体和斜体通过 fontspec、xeCJK 的字体设置处理，宋体和黑体的部分效果使用内置的合成粗体、倾斜功能，字形可能与 Word 有细微差异。

## 封面

在主文件顶部填写题目、姓名、学号、两位指导老师及单位。短填写项居中，长填写项按原字号左对齐折行，横线位于末行下方，后续栏目和日期相应下移。封面内容需要容纳在一页内，长填写项请检查预览。

日期由 `\ReportYear`、`\ReportMonth`、`\ReportDay` 组成，整体居中。需要自定义完整日期时，在封面信息后写 `\renewcommand{\ReportDate}{2026 年 11 月 18 日}`。

## 正文与标题

~~~latex
\section{论文背景与意义}
\subsection{选题来源与背景}
本小节的第一段。

同一小节的后续段落。

\subsubsection{进一步讨论}
三级标题下的正文。
~~~

标题支持到标准 `\subsubsection`（三级）。

普通文字用空行分段。所有段落使用同一套 xeCJK 标点规则，带颜色、加粗的文字和列表也按该规则处理。默认使用全角式 `PunctStyle=quanjiao`，可在导言区用 `\xeCJKsetup{PunctStyle=kaiming}` 等切换。

正文为 24 磅首行缩进、24.4 磅基本行距、零额外段间距。高公式可以撑开行距。字号和行距通过标准 `\normalsize` 生效。原样文部分段落的西文也指定为宋体，用局部分组保留，例如 `{\songlatin 文字。\par}`。

标题支持标准星号形式和目录短标题，例如 `\section*{说明}` 和 `\section[目录短标题]{正文长标题}`。章节引用使用 `\label`、`\ref` 和 `\nameref`。

~~~latex
\subsection{技术方案}\label{sec:method}
方案详见第 \ref{sec:method} 节（\nameref{sec:method}）。
~~~

## 目录

使用标准 `\tableofcontents` 入口。标题、页码和链接由 LaTeX 自动写入，目录行保留贴近原 Word 的字体、缩进、点线和固定宽度，支持长条目换行。

默认显示三级标题。在 `\tableofcontents` 前设置 `\setcounter{tocdepth}{1}` 可只显示一级标题，设为 `2` 显示到二级标题。

## 图表、公式与列表

使用标准 figure、table、equation、enumerate 和 itemize 环境。graphicx 已加载，可使用 `\includegraphics`。数学公式可加载 amsmath，三线表可加载 booktabs。

~~~latex
本研究计划分为以下步骤。
\begin{enumerate}
  \item 文献阅读与需求分析。
  \item 系统实现与实验验证。
\end{enumerate}

随后分析实验结果。
~~~

图表的位置由 LaTeX 根据浮动参数和页面空间安排。编号与交叉引用使用 `\label`、`\ref`，公式引用可使用 amsmath 提供的 `\eqref`。

## 参考文献

~~~latex
相关研究已讨论这一问题\cite{method}。
同时引用多篇文献\cite{method,experiment}。

\begin{thebibliography}{99}
  \bibitem{method} 作者. 文献题名. 年份.
  \bibitem{experiment} 另一位作者. 另一篇文献. 年份.
\end{thebibliography}
~~~

使用标准 `\cite`、thebibliography 和 `\bibitem`。环境自动生成“主要参考文献”标题及目录项，条目左顶格显示。参数 `99` 为两位数编号预留标签宽度。

文献按条目顺序自动编号，文献键需要唯一。正文用相同的键引用，增删或重排条目后运行 latexmk，编号与跳转链接自动更新。文献内容和列表顺序由作者填写。

cite 宏包将引用排成带方括号的上标，并自动排序和压缩连续编号，例如 [1–3]。重复引用同一文献得到同一编号。缺失的文献键显示为问号，并产生未解析引用警告。带附注的 `\cite[附注]{method}` 使用 cite 宏包默认的行内引用形式。

也可采用标准 BibTeX 工作流，在同目录准备 `references.bib`，在主文件中使用以下命令。latexmk 会调用 BibTeX 并更新引用。

~~~latex
\bibliographystyle{unsrt}
\bibliography{references}
~~~

手写 thebibliography 和 BibTeX 是两种可选写法，条目格式由作者或所选 BibTeX 样式决定。

## 综合示例与文件结构

`example.tex` 演示长题目封面、普通段落、公式、嵌套列表、图片、表格、交叉引用、长目录项及连续正文分页。

~~~sh
latexmk -xelatex example.tex
~~~

示例使用通用题目、姓名和学号占位内容。

| 文件 | 用途 |
| --- | --- |
| `proposal.tex` | 主文件，填写封面与正文 |
| `buaa-proposal.sty` | 字体与排版样式 |
| `.latexmkrc` | XeLaTeX 编译配置 |
| `assets/school-logo.jpeg` | 封面学院标识 |
| `example.tex` | 综合示例 |
| `README.md` | 编译、写作与维护说明 |
| `proposal.pdf`、`example.pdf` | 编译预览 |

## 维护与旧版迁移

样式文件按字体加载、样式与常用尺寸、封面页眉页脚、正文、标题、引用和目录组织。

- 内部命令使用 `buaa@` 前缀，字体解析结果与样式配置分别命名。
- 字体字号、行距、标题间距和常用宽度集中定义，封面及页眉页脚的绝对坐标放在绘制代码旁，单位为 bp，文字位置表示基线。
- 封面填写栏的下移量在单个封面的局部分组内累计。
- 正文标点使用 xeCJK，引用与编号使用 cite 和标准文献环境，目录行使用贴近原 Word 的排版实现。

旧版大写标题命令、`\BodyText`、`\ContinueText`、`\ReportContents`、`\ReportBodyStart` 和 `\ReportCitation` 保留为兼容入口。`\ReferenceItem{键}{内容}` 转为 `\bibitem`，需要放在 thebibliography 环境内。旧文件应将原来的参考文献标题及条目替换成上面的标准环境。

## 验证范围

当前版本在本机 XeLaTeX 环境下验证。字体、封面与页眉页脚尽量贴近学院原 DOC，正文使用标准规则自动换行和分页。Word 与 XeLaTeX 的字形合成、标点间距、断行和浮动图表分页可能不同，修改内容后请检查最终 PDF，并结合学院当年的要求确认提交格式。

报告问题时，请提供最小可复现的内容、编译环境、错误日志或问题页截图。
