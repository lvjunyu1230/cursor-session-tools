---
name: session-log
description: 记录当前 session 工作日志。查找当前目录向上最近的 session-logs/{项目名}/session-log.md，生成结构化条目并追加。触发词：记录 session、session-log、记录一下、log session。
---

# Session Log

## Overview

查找当前项目的 session-log.md，生成结构化 session 条目并追加记录。

## Core Logic

1. **查找 session-log.md**：
   - 从当前工作目录向上逐级搜索 `session-logs/*/session-log.md`
   - 找到第一个即为目标（**最近优先原则**，支持嵌套项目）
   - 如找不到，提示用户先运行 `/project-init`
2. **确定项目上下文**：根据找到的路径确定项目名和所属关系
3. **获取文件变更**：运行 `git diff --stat HEAD` 和 `git status --short`
4. **生成摘要**：基于本次对话上下文生成结构化条目
5. **追加记录**：追加到 session-log.md 末尾
6. **手动判断**：不自动更新 README.md 的「重要进展记录」，仅追加到 session-log.md

## Workflow

### Step 1: 查找 session-log.md

从当前工作目录向上搜索 `session-logs/*/session-log.md`：
```
./session-logs/*/session-log.md → 找到则停止
../session-logs/*/session-log.md → 找到则停止
../../session-logs/*/session-log.md → ...
```

- 如果找到：继续下一步
- 如果未找到：提示"未找到 session-log.md，请先运行 /project-init 初始化项目"

### Step 2: 获取文件变更

运行以下命令：
```bash
git diff --stat HEAD
git status --short
```

记录修改和新增的文件。

### Step 3: 生成 Session 条目

基于本次对话上下文，生成以下格式的条目：

```markdown
---

## {YYYY-MM-DD HH:MM}

**任务**：{一句话描述本次目标}

**做了什么**：{最终操作+决策}

**思考过程**：{可选，记录纠结和反复的思路}
- 纠结点1：{描述}
- 纠结点2：{描述}
- 放弃的思路：{描述}

**标签**：{可选标签，用逗号分隔，如：skill-design, refactor}

**文件变更**：
修改：{文件名，多个用逗号分隔}
新增：{文件名，多个用逗号分隔}
```

### Step 3.5: 捕捉思考过程

回顾本次对话，识别：
- 用户提出了哪些备选方案或纠结点
- 哪些思路被放弃及原因
- 关键的决策时刻和最终选择
- 过程中修正了哪些观点
- 有哪些「最初想...但后来发现...」的转折

将以上内容整理成「思考过程」字段。如果本次对话没有太多纠结，可标注"无"或省略此字段。

### Step 4: 追加到 session-log.md

将生成的条目追加到 `session-logs/{项目名}/session-log.md` 末尾。

### Step 5: 报告完成

回复：
```
Session 日志已更新。

项目：{项目名}
位置：{session-log.md 完整路径}

条目已追加，包含：
- 任务：{一句话描述}
- 思考过程：{有/无}
- 文件变更：修改 {N} 个，新增 {M} 个

如需查看，运行 /project-readme 查看项目状态。
```

## 标签建议

常用标签分类：
- **工作类型**：`design`, `implement`, `research`, `review`, `fix`
- **领域**：`skill`, `frontend`, `backend`, `docs`, `config`
- **状态**：`in-progress`, `blocked`, `done`

## 大项目嵌套小项目模式

在嵌套项目中，自动找到最近的项目文档：
- 在 `root/subprojects/small-project/code/` 下工作 → 记录到 small-project
- 在 `root/subprojects/` 下工作 → 记录到 big-project

## 注意事项

- 如果 git diff 无输出（无文件变更），「文件变更」部分可留空或标注"无"
- 标签和思考过程均为可选项，如无相关内容可标注"无"
- 不自动更新 README.md，由用户手动判断是否值得记录到「重要进展记录」
- 思考过程是最有价值的部分——记录当时的纠结和决策，比记录结果更有意义
