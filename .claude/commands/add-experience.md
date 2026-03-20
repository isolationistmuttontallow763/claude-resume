添加或更新经历到 experiences/ 素材库。

## 输入

$ARGUMENTS

用户可能提供：
1. 一段新的工作/项目经历描述
2. 对现有经历的更新或补充
3. 新的技能、荣誉、量化指标

## 执行步骤

### 第一步：理解输入

分析用户提供的内容属于哪种类型：
- **新工作经历** → 创建或更新 `experiences/work/` 下的文件
- **新个人项目** → 更新 `experiences/projects.md`
- **新技能** → 更新 `experiences/skills.md`
- **新荣誉/成果** → 更新 `experiences/honors.md`
- **个人信息变更** → 更新 `experiences/profile.md`

### 第二步：读取现有文件

读取要更新的目标文件，了解当前内容和格式。

### 第三步：更新内容

遵循以下格式规范：

**工作经历文件** (`experiences/work/*.md`)：
```markdown
---
company: 公司名
company_en: English Name
url: https://...
location: 城市
period: YYYY/MM -- YYYY/MM
department: 部门
role: 角色
tags: [tag1, tag2, ...]
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

**关键原则**：
- 尽量记录原始细节，不要过早精简（精简在生成简历时做）
- tags 要覆盖核心技术和业务领域关键词
- 量化成果尽量具体，包含数字

### 第四步：确认更新

向用户展示变更内容（diff），确认后写入文件。

### 第五步：同步提示

如果新增的经历可能影响现有简历，提醒用户：
"经历已更新。如需重新生成简历，请运行 /generate-resume [目标岗位]"
