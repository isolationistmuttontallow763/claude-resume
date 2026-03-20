# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

一套简历管理系统：从结构化经历素材出发，根据不同目标岗位生成定制化 LaTeX 简历并编译为 PDF。

## Build Commands

```bash
make all     # Clean + build both English and Chinese PDFs
make en      # Build English PDF only (resume.pdf)
make zh      # Build Chinese PDF only (resume-zh.pdf)
make clean   # Remove build artifacts
```

Requires **XeLaTeX** (`brew install --cask mactex` on macOS).

## Slash Commands

- `/generate-resume [目标岗位或JD文件]` — 根据目标岗位从 `experiences/` 素材生成定制化简历，构建 PDF，输出到 `output/`
- `/add-experience [描述]` — 添加或更新经历到 `experiences/` 素材库

## Architecture

### 简历生成流程

```
experiences/  →  /generate-resume  →  resume.tex  →  make en  →  output/Name-Title.pdf
   (素材)         (AI 定制化)         (LaTeX源)      (编译)        (输出)
```

### 目录结构

- **`experiences/`** — 经历素材库（唯一真实来源），所有简历内容从这里生成
  - `profile.md` — 个人信息、联系方式、教育经历
  - `work/` — 按公司分的工作详历（含项目背景、核心工作、量化成果、技术栈）
  - `projects.md` — 个人项目
  - `skills.md` — 完整技能清单
  - `honors.md` — 荣誉 + 量化指标速查表
- **`jobs/`** — 目标岗位 JD 文件，`_template.md` 为格式模板
- **`output/`** — 生成的简历 PDF 输出目录
- **`.history/`** — 历史 .tex 版本备份（格式: `resume_YYYYMMDDHHmmss.tex`）
- **`resume.tex`** — 当前活跃的简历源文件
- **`resume.cls`** — LaTeX 类定义（布局、字体、命令），基于 [billryan/resume](https://github.com/billryan/resume)

### LaTeX 关键命令 (resume.cls)

| 命令 | 用途 |
|------|------|
| `\name{}` | 姓名居中大标题 |
| `\basicInfo{}` | 联系方式行（包裹 `\email`, `\phone`, `\wechat`, `\homepage`） |
| `\datedsubsection{}{}` | 公司/学校 + 时间 |
| `\role{}{}` | 部门 + 职位 |
| `\rolewithdate{}{}{}` | 部门 + 职位 + 时间（同公司多角色） |

CJK 字体: `SourceHanSerifSC-Medium` via `xeCJK`。英文版简历需去掉 xeCJK 相关三行。

### 重要约定

- **简历控制在 1 页内**（中文版），英文版可适当放宽
- 修改 `resume.tex` 前先备份到 `.history/`
- `experiences/` 中的素材尽量保留原始细节，精简在生成时做
- `resume-zh.tex` 由 Makefile 自动生成，不要手动编辑
- 每个 experience 文件的 frontmatter `tags` 字段用于辅助匹配岗位需求
