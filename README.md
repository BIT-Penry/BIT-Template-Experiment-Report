# BIT 实验课程报告 LaTeX 模板

本项目提供了一个适用于 **北京理工大学** 实验课程报告的 LaTeX 模板，结构清晰、样式规范、支持章节划分、图片插图、参考文献等常用功能。

> 🌱 由 BIT 自动化的小米同学自行整理与维护，旨在为同学们提供一个高效、优雅的写作环境。

---

## 📝 使用说明

本模板基于 `XeLaTeX` 编译，推荐使用 VS Code + LaTeX Workshop 插件进行编辑。

你可以将整个项目文件夹 clone 或下载下来后，直接在 VS Code 中打开并编译 `main.tex`。

---

## 💻 搭建 VS Code LaTeX 环境教程

我们推荐你参考文章：

📖 **第一章 LaTeX 与 VS Code 的相遇**  
👉 https://penry.asia/article/%E7%AC%AC%E4%B8%80%E7%AB%A0-Latex%E4%B8%8EVscode%E7%9A%84%E7%9B%B8%E9%81%87/

该文详细介绍了如何：

- 安装 TeX Live / MacTeX / MikTeX
- 配置 VS Code 插件
- 编写并编译首个 `.tex` 文档
- 设置 `settings.json` 实现一键构建、中文支持等功能
- `settings.json`配置如下：

``` json
//------------------------------LaTeX 配置----------------------------------
// 设置是否自动编译
"latex-workshop.latex.autoBuild.run":"onFileChange",
//右键菜单
"latex-workshop.showContextMenu":true,
//从使用的包中自动补全命令和环境
"latex-workshop.intellisense.package.enabled": true,
//编译出错时设置是否弹出气泡设置
"latex-workshop.message.error.show": false,
"latex-workshop.message.warning.show": false,
// 编译工具和命令
"latex-workshop.latex.tools": [
    {
        "name": "xelatex",
        "command": "D:\\1_Download_Software\\texlive\\2024\\bin\\windows\\xelatex.exe",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
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
    {
        "name": "latexmk",
        "command": "latexmk",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-pdf",
            "-outdir=%OUTDIR%",
            "%DOCFILE%"
        ]
    },
    {
        "name": "biber",
        "command": "biber",
        "args": [
            "%DOCFILE%"
        ]
    },        
    {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
            "%DOCFILE%"
        ]
    }
],
// 用于配置编译链
"latex-workshop.latex.recipes": [
    {
        "name": "XeLaTeX",
        "tools": [
            "xelatex"
        ]
    },
    {
        "name": "PDFLaTeX",
        "tools": [
            "pdflatex"
        ]
    },
    {
        "name": "BibTeX",
        "tools": [
            "bibtex"
        ]
    },
    {
        "name": "LaTeXmk",
        "tools": [
            "latexmk"
        ]
    },
    {
        "name": "xelatex -> biber -> xelatex*2",
        "tools": [
            "xelatex",
            "biber",
            "xelatex",
            "xelatex"
        ]
    },        
    {
        "name": "xelatex -> bibtex -> xelatex*2",
        "tools": [
            "xelatex",
            "bibtex",
            "xelatex",
            "xelatex"
        ]
    },
    {
        "name": "pdflatex -> bibtex -> pdflatex*2",
        "tools": [
            "pdflatex",
            "bibtex",
            "pdflatex",
            "pdflatex"
        ]
    }
],
//文件清理。此属性必须是字符串数组
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
    "*.fdb_latexmk"
],
//设置为onFaild 在构建失败后清除辅助文件
"latex-workshop.latex.autoClean.run": "onFailed",
// 默认使用的recipe编译组合
"latex-workshop.latex.recipe.default": "xelatex -> biber -> xelatex*2",
// 用于反向同步的内部查看器的键绑定。ctrl/cmd +点击(默认)或双击
"latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
"files.autoSave": "afterDelay",
"workbench.colorTheme": "Winter is Coming (Dark Blue)",
"workbench.iconTheme": "vscode-icons",
"notebook.compactView": false,
"explorer.compactFolders": false,
"pasteImage.prefix": "./",
"markdown.copyFiles.destination": {
    "**/*.md": "../../source/img/pictures_markdown/"
},
```

---

## 🛠 如何编译

编译主文件 `main.tex` 即可生成完整课程报告 PDF。

默认使用 `xelatex -> biber -> xelatex*2` 编译方式，确保支持中文和参考文献。

你可以通过以下命令（或使用 VS Code 工具栏按钮）完成编译：

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
