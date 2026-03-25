# claude-resume

[English](README.md) | 中文

AI 驱动的简历管理系统 — 一份素材，N 份定制简历。

> 不只是一个 Skill，而是一个用 Claude Code Skill 构建完整工作流的示范项目。

<p align="center">
  <img src="demo-output.png" alt="生成的 PDF 示例" width="600">
</p>

基于 [Claude Code](https://claude.ai/code) Skill 体系，从结构化经历素材出发，根据不同目标岗位自动生成定制化 LaTeX 简历。

## 工作流程

```
┌─────────────────────────────────────────────────────────┐
│  初始化 (/resume init)                                   │
│                                                         │
│  粘贴简历  ──→  自动解析  ──→  experiences/*.md          │
│       或                                                │
│  问答引导  ──→  逐步填写  ──→  experiences/*.md          │
└──────────────────────────┬──────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│  生成 (/resume generate "后端开发工程师")                  │
│                                                         │
│  读取素材  →  分析 JD  →  定制化重组                      │
│                                                         │
│  → resume.tex  →  make en  →  output/姓名-岗位.pdf       │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│  维护 (/resume add)                                      │
│                                                         │
│  "升职了" / "做了新项目" / "拿了证书"                      │
│  → 自动更新 experiences/*.md                              │
└─────────────────────────────────────────────────────────┘
```

## 特性

- **零配置上手** — 粘贴现有简历或回答几个问题即可，无需手动编辑 Markdown
- **素材驱动** — 经历、技能、荣誉存储在 Markdown 文件中，与简历呈现分离
- **AI 定制化** — 根据 JD 自动选择经历、调整呈现角度、重排优先级
- **多岗位适配** — 同一段经历在不同方向下有不同包装（后端/云原生/AI 方向等）
- **自然语言维护** — 用自然语言添加经历、技能、证书
- **LaTeX 输出** — 专业排版，编译为 PDF，基于 [billryan/resume](https://github.com/billryan/resume) 模板
- **版本追踪** — `.history/` 每次生成前自动备份

## 前置条件

- **Claude Code CLI** — 已安装并认证
- **XeLaTeX** — macOS: `brew install --cask mactex`（[下载](https://tug.org/mactex/)）

## 快速开始

### 1. 安装

**方式 A：作为 Skill 安装（推荐）**

```bash
npx skills add deusyu/claude-resume --yes
```

然后在任意目录：

```
/resume init
```

Skill 会自动搭建项目结构（复制 `resume.cls`、`Makefile`，创建 `experiences/` 目录）。

**方式 B：克隆仓库**

```bash
git clone https://github.com/deusyu/claude-resume.git
cd claude-resume
claude
```

### 2. 初始化素材库

**问答引导（推荐新用户）**

```
/resume init
```

Skill 会逐步引导你填写 — 姓名、教育、工作经历、项目、技能 — 一次问一个问题。

**导入现有简历**

```
/resume init <粘贴你的简历或经历文本>
```

自动解析并结构化为 `experiences/` 文件。

### 3. 生成简历

```
/resume generate 后端开发工程师
```

或指定 JD 文件：

```
/resume generate jobs/bytedance-backend.md
```

Skill 会展示定制化方案（保留/舍弃哪些经历、如何重新包装），确认后生成。

### 4. 持续更新

```
/resume add 最近做了一个实时数据管道项目，处理 100 万事件/秒
/resume add 拿到了 AWS Solutions Architect Professional 认证
```

## 项目结构

| 路径 | 用途 |
|------|------|
| `skills/resume/SKILL.md` | Skill 定义 — 所有工作流（init、generate、add） |
| `skills/resume/assets/` | 打包资产（resume.cls、Makefile、模板） |
| `skills/resume/references/` | LaTeX 命令参考 |
| `experiences/` | 经历素材库（唯一数据源） |
| `jobs/_template.md` | 目标岗位 JD 模板 |
| `resume.tex` | 当前 LaTeX 源文件 |
| `resume.cls` | LaTeX 样式类（布局、字体、命令） |
| `Makefile` | 构建命令（`make en`、`make zh`、`make all`、`make clean`） |
| `.history/` | .tex 历史版本备份 |
| `output/` | 生成的 PDF 输出目录 |

## 子命令

### `/resume init [可选：粘贴简历文本]`

初始化。两种模式：

- **无参数** → 问答引导，一次问一个问题（姓名 → 教育 → 工作 → 项目 → 技能 → 荣誉）
- **带文本** → 解析你的现有简历或 LinkedIn 导出，自动生成 `experiences/` 结构化文件

### `/resume generate [岗位名称或 JD 文件路径]`

核心工作流，完整流水线：

1. **读取** `experiences/` 下所有素材文件
2. **分析** 岗位需求 — 提取核心技能、优先级
3. **方案** — 选择经历、决定排序和侧重、确定保留/舍弃的 section
4. **确认** — 展示方案给用户，等待确认
5. **生成** — 使用 `resume.cls` 命令写入 `resume.tex`
6. **构建** — `make en` → 复制 PDF 到 `output/`

### `/resume add [描述]`

用自然语言更新经历素材：

```
/resume add 做了一个开源 RAG 项目，用 LlamaIndex 实现，200+ Stars
/resume add 拿到了 AWS Solutions Architect 认证
```

## 自定义

### 经历素材格式

工作经历文件使用 YAML frontmatter + Markdown：

```markdown
---
company: 公司名
period: 2024/01 -- 至今
department: 部门
role: 角色
tags: [go, kubernetes, distributed-system]
---

# 项目名称
> 时间 | 角色

## 项目背景
...

## 核心工作
...

## 量化成果
...

## 技术栈
...
```

`tags` 字段帮助 AI 在生成时匹配岗位需求。

### LaTeX 样式

修改 `resume.cls` 可自定义布局、字体、间距。当前基于 [billryan/resume](https://github.com/billryan/resume)。

## 致谢

- LaTeX 模板基于 [billryan/resume](https://github.com/billryan/resume) 和 [imtsuki/resume](https://github.com/imtsuki/resume)
- 简历生成由 [Claude Code](https://claude.ai/code) Skill 驱动

## License

[MIT](LICENSE)
