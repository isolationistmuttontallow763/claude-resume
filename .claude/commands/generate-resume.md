根据目标岗位生成定制化简历。

## 输入

$ARGUMENTS

输入可以是以下任意一种：
1. `jobs/` 文件夹下的 JD 文件路径（如 `jobs/bytedance-backend.md`）
2. 直接粘贴的岗位名称或描述（如 "后端开发工程师"）
3. 如果为空，请询问用户目标岗位

## 执行步骤

### 第一步：读取素材

读取以下所有文件：
- `experiences/profile.md` — 个人信息和教育经历
- `experiences/work/` 下的所有 `.md` 文件 — 工作详历
- `experiences/projects.md` — 个人项目
- `experiences/skills.md` — 完整技能清单
- `experiences/honors.md` — 荣誉和量化指标
- `resume.cls` — LaTeX 可用命令

如果 $ARGUMENTS 是文件路径，也读取该 JD 文件。

### 第二步：分析岗位需求

根据 JD 或岗位名称，确定：
1. **核心技术要求**：岗位最看重的技术能力
2. **经历优先级**：哪些工作经历最相关，应该详写
3. **呈现角度**：同一段经历在不同岗位下的不同包装方式
4. **内容取舍**：是否需要个人项目 section、哪些经历可以精简

### 第三步：定制化策略

根据岗位需求，调整以下维度：
- **核心定位**：一句话概括，匹配目标岗位的关键词
- **项目排序**：最相关的经历放前面，详写；低相关的精简或省略
- **呈现角度**：同一段经历根据岗位方向调整强调重点（如同一个平台项目，投架构岗强调设计，投业务岗强调交付）
- **技能重组**：按岗位需求重新排列技能分类和优先级
- **个人项目**：与岗位强相关则保留，弱相关则省略以节省版面

### 第四步：生成简历

生成 `resume.tex` 文件（中文版），遵循以下规则：

1. **严格使用 resume.cls 定义的命令**：
   - `\name{}`, `\basicInfo{}`, `\email{}`, `\phone{}`, `\wechat{}`, `\homepage[]{}`
   - `\section{}`, `\datedsubsection{}{}`, `\role{}{}`, `\rolewithdate{}{}{}`
   - 使用 `itemize` 环境，`[parsep=0.25ex]` 控制间距

2. **控制在 1 页内**（重要！）：
   - 通常 5-6 个 section：核心定位、教育经历、工作经历、（个人项目）、技能、荣誉、致谢
   - 每个项目 3-5 个 bullet points
   - 早期实习精简到每个 1-2 行
   - 如果内容太多，优先砍掉早期实习和低相关性的 bullet points

3. **LaTeX 注意事项**：
   - 使用 `\textbf{【xxx】}` 格式标记每个 bullet 的关键词
   - `&` 需要转义为 `\&`
   - `%` 需要转义为 `\%`
   - `#` 在 LaTeX 中有特殊含义
   - 使用 `\href{url}{text}` 做超链接

4. **文件头部**：
   ```latex
   \documentclass{resume}
   \usepackage{xeCJK}
   \setCJKmainfont{SourceHanSerifSC-Medium}
   \setCJKsansfont{SourceHanSerifSC-Medium}
   \setCJKmonofont{SourceHanSerifSC-Medium}
   ```

### 第五步：向用户展示计划

在生成 .tex 之前，先向用户展示：
1. 目标定位（一句话）
2. 内容取舍（包含/省略哪些经历）
3. 核心差异化（相比通用简历的关键变化）

等待用户确认后再生成文件。

### 第六步：输出

用户确认后：

1. 备份当前 `resume.tex` 到 `.history/resume_$(date +%Y%m%d%H%M%S).tex`
2. 将生成的内容写入 `resume.tex`
3. 运行 `make en` 构建 PDF
4. 复制 PDF 到 `output/` 并按岗位命名

### 第七步：如需英文版

如果用户要求英文版：
1. 去掉 xeCJK 相关的三行（CJK 字体设置）
2. 将所有内容翻译为英文
3. 构建 PDF
