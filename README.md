# Beamer Academic Template

一个中文友好的学术 Beamer 模板,基于 CambridgeUS 主题,带学术蓝色右上角引用系统、定理 / Block 环境、`booktabs` / `tabularx` 表格示例、以及多种图片排版示例。

**XeLaTeX 编译,零 warning,Overleaf 开箱即用**(默认配置不依赖任何系统字体)。

> Adapted from the UPVD beamer theme by Amine Najahi (2012, GPL v3).

## 特性

- **CambridgeUS 主题** + 自定义 UDL 配色(`beamer_udl_theme.sty`)
- **中文支持**:`ctex` + `fontspec`,默认使用跨平台字体 `TeX Gyre Termes` + `FandolKai`,无需额外安装
- **学术蓝色上标引用**:`\upcite{}` 自动编号,每个 section 自动重置
- **页脚紧凑文献条目**:`\citeitem{}`,与正文上标编号自动联动
- **示例 frame**:
  - 定理 / 定义 / 证明环境
  - Standard / Alert / Example 三种 Block
  - `booktabs` 三线表 + `tabularx` 自动换行表
  - 单图带标题 + 双图并排 + 图文混排
- **零警告编译**:已修复 fonttheme、ctex fontset、hyperref PDF 元数据、Fandol 字体 OpenType script 等所有常见警告

## 文件清单

发布或使用本模板需要以下文件位于**同一目录**:

| 文件                           | 必需 | 说明                                        |
| ------------------------------ | ---- | ------------------------------------------- |
| `beamer-academic-template.tex` | 是   | 主文件                                      |
| `beamer_udl_theme.sty`         | 是   | 自定义颜色主题                              |
| `amss.png`(或 `.pdf` / `.jpg`) | 否   | 封面 Logo;不需要可注释 `\titlegraphic{...}` |

图片示例 frame 使用 `mwe` 宏包提供的 `example-image-a/b/c`,这些文件 TeX Live 自带,**无需上传**。

## 环境要求

- **编译器**:XeLaTeX(必须)
- **TeX 发行版**:TeX Live 2018+ / MiKTeX / MacTeX,任何一种均可,需含 `ctex`、`xeCJK`、`fontspec`、`beamer`、`mwe` 等基础宏包
- **字体**:见下方"字体配置"小节

## 快速开始

### 本地编译

```bash
xelatex beamer-academic-template.tex
xelatex beamer-academic-template.tex   # 第二次编译以正确解析交叉引用
```

由于 `\upcite{}` 是前向引用,必须**编译两次**才能正确显示编号。

### Overleaf

1. 新建项目,把 `beamer-academic-template.tex` 与 `beamer_udl_theme.sty`(以及可选的 `amss.*` Logo)上传到根目录
2. **Menu → Settings → Compiler** 中选择 `XeLaTeX`
3. 点 **Recompile**

默认配置使用 Overleaf 自带的 `TeX Gyre Termes` 和 `FandolKai`,**不需要额外字体**就能编译。

## 字体配置

模板提供两套可切换的字体方案,在主文件导言区:

### 方案 1:跨平台(默认启用,推荐用于 Overleaf / 跨机器协作)

```latex
\setmainfont{TeX Gyre Termes}
\setsansfont{TeX Gyre Termes}
\setCJKmainfont[AutoFakeBold, AutoFakeSlant=0.2]{FandolKai-Regular.otf}
\setCJKsansfont[AutoFakeBold, AutoFakeSlant=0.2]{FandolKai-Regular.otf}
\setCJKmonofont{FandolKai-Regular.otf}
```

`TeX Gyre Termes` 与 `FandolKai` 都是 TeX Live 自带的开源字体,任何 TeX Live / Overleaf 环境都能直接用。`AutoFakeBold` 与 `AutoFakeSlant=0.2` 用于合成 FandolKai 缺失的粗体与斜体字形。

### 方案 2:本地系统字体(更精致,需手动启用)

如果在本地编译且系统已装 Times New Roman 与 KaiTi(典型如 Windows),注释方案 1、取消注释方案 2:

```latex
\setmainfont{Times New Roman}
\setsansfont{Times New Roman}
\setCJKmainfont{KaiTi}
\setCJKsansfont{KaiTi}
```

macOS 上 KaiTi 可能需写成 `Kaiti SC`。

## 使用指南

### 标题、作者、机构

```latex
\title[ML for QEM]{ML for Quantum Error Mitigation}
\author[Jinming Hu]{\texorpdfstring{Jinming Hu \\ \medskip \small hujinming@amss.ac.cn}{Jinming Hu}}
\institute[AMSS]{Academy of Mathematics and Systems Science \\
                 Chinese Academy of Sciences}
```

**重要**:方括号 `[ ]` 里是**短版本**,显示在底部栏;花括号 `{ }` 里是完整版本,显示在标题页。若省略方括号,底部栏会塞入完整内容(含邮箱、换行)导致截断,出现 `Author Name author@example.com (Institu...` 的丑态。

| 命令                 | 底部栏 | 标题页 |
| -------------------- | ------ | ------ |
| `\title[短]{长}`     | 短     | 长     |
| `\author[短]{长}`    | 短     | 长     |
| `\institute[短]{长}` | 短     | 长     |

CambridgeUS 底部栏的三格依次为:**作者短** \| **机构短 — 标题短** \| **日期 / 页码**,因此短版本建议控制在 10 个英文字符以内。

`\author{}` 的完整版本若含 `\\` 或 `\medskip`,需用 `\texorpdfstring{长版本}{用于 PDF 元数据的纯文本}` 包一层,否则 hyperref 写 PDF 元数据时会发警告。

### 引用系统

正文中使用 `\upcite{key}` 插入右上角编号:

```latex
量子误差缓解主要分为 PEC \upcite{cai2022} 与 ZNE \upcite{endo2021} 两类。
```

帧底部使用 `\citeitem{key}{作者}{题目}{期刊}` 列出条目:

```latex
\vfill
\begin{minipage}[b]{\textwidth}
  \raggedright
  \rule{0.3\textwidth}{0.3pt}\\[2pt]
  \citeitem{cai2022}{Z. Cai, et al.}{Quantum error mitigation}{Rev. Mod. Phys., 2022}
  \citeitem{endo2021}{S. Endo, et al.}{Hybrid Quantum-Classical Algorithms}{J. Phys. Soc. Jpn., 2021}
\end{minipage}
```

编号在每个 `\section` 开始时自动重置为 1。

### 图片插入

模板内置三种常见排版的可直接复制示例:

```latex
% 单图带标题
\begin{figure}[h]
  \centering
  \includegraphics[width=0.55\textwidth]{your-image}
  \caption{Your caption.}
\end{figure}

% 双图并排
\begin{columns}[T,onlytextwidth]
  \begin{column}{0.48\textwidth}
    \centering
    \includegraphics[width=\linewidth]{image-a}\\[2pt]
    {\small (a) 左图说明}
  \end{column}
  \begin{column}{0.48\textwidth}
    \centering
    \includegraphics[width=\linewidth]{image-b}\\[2pt]
    {\small (b) 右图说明}
  \end{column}
\end{columns}

% 图文混排
\begin{columns}[c]
  \begin{column}{0.42\textwidth}
    \includegraphics[width=\linewidth]{image}
  \end{column}
  \begin{column}{0.55\textwidth}
    说明文字 / itemize 列表
  \end{column}
\end{columns}
```

支持的图片格式:`.pdf`、`.png`、`.jpg`、`.jpeg`、`.eps`(需要 epstopdf 包)。`\includegraphics` 的文件名**不必带扩展名**。

### 替换 Logo

把自己的 Logo 图片(`.pdf` / `.png` / `.jpg` 均可)放到 `.tex` 同目录,修改:

```latex
\titlegraphic{\includegraphics[height=1.5cm]{你的文件名}}
```

如不需要 Logo,把整行注释掉即可。

### 含 `\verb` 的 frame

Beamer 规定**任何含 `\verb` 或 `verbatim` 环境的 frame 必须加 `[fragile]` 选项**:

```latex
\begin{frame}[fragile]{Frame Title}
  这里出现了 \verb|\toprule| 等命令。
\end{frame}
```

否则会报 `! File ended while scanning use of \beamer@checkframetitle` 之类的错误。

## 自定义

### 修改主题颜色

打开 `beamer_udl_theme.sty`,调整 `\setbeamercolor{...}` 各行。

### 修改引用颜色

在主文件导言区:

```latex
\definecolor{AcademicBlue}{RGB}{0, 0, 255}   % 改成你想要的 RGB
```

### 关闭目录自动插入

如果不想在每个 section 开始时插入目录页,但保留计数器重置功能:

```latex
\AtBeginSection[]{%
  \setcounter{mycitecounter}{0}%
  % 删除下面的 frame 块即可
}
```

**注意**:`\AtBeginSection` 是"覆盖式"钩子,**只能声明一次**。所有 section 开始时要做的事都放在这一个块里;声明两次会让前一个被覆盖。

## 许可证

本模板基于原作者 Amine Najahi 的 UPVD beamer 主题(GPL v3),因此**本模板同样以 GPL v3 协议发布**。你可以自由使用、修改、分发,但衍生作品也必须以 GPL v3(或兼容协议)发布。完整协议见 <https://www.gnu.org/licenses/gpl-3.0.html>。

## 免责声明

本模板按"原样"(AS IS)提供,不附带任何明示或暗示的担保。在任何情况下,作者均不对因使用本模板而产生的任何索赔或损害负责。

使用者应自行确认有权使用其在演示文稿中加入的所有素材,**包括但不限于机构标识、字体与参考文献内容**。模板封面默认引用的 `amss` 图像仅作示例占位,公开发布前请替换为自己有权使用的机构标识。

## 致谢

- 原始 UPVD beamer 主题:Amine Najahi <amine.najahi@univ-perp.fr>
- 中文化、引用系统、示例内容、零警告优化:Jinming Hu

## 联系

Jinming Hu — hujinming@amss.ac.cn

Academy of Mathematics and Systems Science, Chinese Academy of Sciences (AMSS, CAS)
