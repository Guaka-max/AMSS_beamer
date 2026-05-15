# Beamer Academic Template

一个中文友好的学术 Beamer 模板,基于 CambridgeUS 主题,带有学术蓝色的右上角参考文献引用系统。

> Adapted from the UPVD beamer theme by Amine Najahi (2012, GPL v3).

## 特性

- **CambridgeUS 主题** + 自定义 UDL 颜色配色
- **中文支持**(`ctex` + `fontspec`,默认 Times New Roman + 楷体)
- **学术蓝色上标引用系统**:`\upcite{}` 自动编号,每个 section 重置
- **页脚参考文献列表**:`\citeitem{}` 紧凑排列,与正文上标编号联动
- 内置示例:定理/定义/证明环境、Block 环境、`booktabs` 三线表、`tabularx` 自动换行表

## 文件清单

发布或使用本模板需要以下文件位于**同一目录**:

| 文件 | 说明 |
|------|------|
| `beamer-academic-template.tex` | 主文件 |
| `beamer_udl_theme.sty`         | 自定义颜色主题 |
| `amss.png`(或 `.pdf` / `.jpg`)| 封面 Logo(可替换为自己的图) |

## 环境要求

- **编译器**:XeLaTeX(必须,因为使用了 `ctex` 与 `fontspec`)
- **TeX 发行版**:TeX Live 2015+ / MiKTeX / MacTeX,任何一种均可
- **系统字体**:
  - Times New Roman(英文)
  - KaiTi(中文楷体)

若所在系统缺少上述字体,可改为本机已装的:

| 原字体 | 跨平台替代(TeX Live 自带,无需额外安装) |
|--------|------------------------------------------|
| Times New Roman | `TeX Gyre Termes` |
| KaiTi           | `FandolKai` |

替换方式:打开 `.tex` 文件,修改导言区中相应的 `\setmainfont{}` 与 `\setCJKmainfont{}` 即可。

## 快速开始

### 本地编译

```bash
xelatex beamer-academic-template.tex
xelatex beamer-academic-template.tex   # 第二次编译以正确解析交叉引用
```

### Overleaf

1. 新建项目,把三个文件全部上传到根目录
2. 在 **Menu → Settings → Compiler** 中选择 `XeLaTeX`
3. 点 **Recompile**

> Overleaf 默认环境没有 Times New Roman 和 KaiTi,需要按上一节把字体替换为 `TeX Gyre Termes` + `FandolKai`,或上传字体文件。

## 使用指南

### 1. 修改标题、作者、机构

```latex
\title[ML for QEM]{ML for Quantum Error Mitigation}
\author[Jinming Hu]{Jinming Hu \\ \medskip \small hujinming@amss.ac.cn}
\institute[AMSS]{Academy of Mathematics and Systems Science \\
                 Chinese Academy of Sciences}
```

**重要**:方括号 `[ ]` 里的是**短版本**,显示在底部栏;花括号 `{ }` 里的是完整版本,显示在标题页。若省略方括号,底部栏会塞入完整内容(含邮箱、换行)导致截断,出现 `Author Name author@example.com (Institu...` 的丑态。

| 命令 | 底部栏 | 标题页 |
|------|--------|--------|
| `\title[短]{长}` | 短 | 长 |
| `\author[短]{长}` | 短 | 长 |
| `\institute[短]{长}` | 短 | 长 |

CambridgeUS 底部栏的三格依次为:**作者短** \| **机构短 — 标题短** \| **日期 / 页码**,因此短版本建议控制在 10 个英文字符以内。

### 2. 引用系统

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

编号在每个 `\section` 开始时自动重置为 1,无需手动管理。

### 3. 替换 Logo

把自己的 Logo 图片(`.pdf` / `.png` / `.jpg` 均可)放到 `.tex` 同目录,然后修改:

```latex
\titlegraphic{\includegraphics[height=1.5cm]{你的文件名}}
```

文件名**不必带扩展名**,XeLaTeX 会自动尝试 `.pdf`、`.png`、`.jpg`。

## 自定义

### 修改主题颜色

打开 `beamer_udl_theme.sty`,在里面调整 `\setbeamercolor{...}` 行即可。

### 修改引用颜色

在主文件导言区修改:

```latex
\definecolor{AcademicBlue}{RGB}{0, 0, 255}   % 改成你想要的 RGB
```

### 关闭目录自动插入

如果不想在每个 section 开始时插入目录页,删除或注释掉:

```latex
\AtBeginSection[]{ ... }
```

## 许可证

本模板基于原作者 Amine Najahi 的 UPVD beamer 主题(GPL v3),因此**本模板同样以 GPL v3 协议发布**。你可以自由使用、修改、分发,但衍生作品也必须以 GPL v3(或兼容协议)发布。完整协议见 <https://www.gnu.org/licenses/gpl-3.0.html>。

## 免责声明

本模板按"原样"(AS IS)提供,不附带任何明示或暗示的担保。在任何情况下,作者均不对因使用本模板而产生的任何索赔或损害负责。

使用者应自行确认有权使用其在演示文稿中加入的所有素材,**包括但不限于机构标识、字体与参考文献内容**。模板封面默认引用的 `amss` 图像仅作示例占位,公开发布前请替换为自己有权使用的机构标识。

## 致谢

- 原始 UPVD beamer 主题:Amine Najahi <amine.najahi@univ-perp.fr>
- 中文化、引用系统、示例内容:Jinming Hu

## 联系

Jinming Hu — hujinming@amss.ac.cn

Academy of Mathematics and Systems Science, Chinese Academy of Sciences (AMSS, CAS)
