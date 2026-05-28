---
name: project-init
description: 初始化项目文档结构。在当前目录或指定目录下创建 session-logs/{项目名}/ 文件夹，包含 README.md 和 session-log.md。触发词：初始化项目、project-init、新建项目。
---

# Project Init

## Overview

在指定目录下初始化项目文档结构，创建两个文件：
- `README.md`：项目入口文档
- `session-log.md`：Session 日志（含格式模板）

## Core Logic

1. **接收参数**：项目名、目标描述、可选项目根目录（默认当前工作目录）
2. **检测已存在**：在指定目录下查找 `session-logs/{项目名}/`，存在则报告"无需重复初始化"
3. **创建目录结构**：`session-logs/{项目名}/`
4. **初始化文件内容**：写入 README.md 和 session-log.md

## Workflow

### Step 1: 获取项目信息

询问用户以下信息（如果未提供）：
- 项目名
- 项目目标（一句话描述）
- 项目根目录（可选，默认为当前工作目录）

### Step 2: 检测是否已初始化

查找 `项目根目录/session-logs/{项目名}/` 是否存在。

- 如果存在：报告"项目已初始化，无需重复初始化"，结束
- 如果不存在：继续下一步

### Step 3: 创建目录结构

创建 `项目根目录/session-logs/{项目名}/`

### Step 4: 创建 README.md

```markdown
# {项目名}

## 目标
{一句话描述}

## 状态
- [ ] 进行中

## 重要进展记录

| 日期 | 进展 |
|------|------|
| | |

## 关键文件
| 文件 | 说明 |
|------|------|
| | |

## Todo
（待填写）
```

### Step 5: 创建 session-log.md

```markdown
# {项目名} — Session Log

<!-- 新条目追加在下方 -->

---

## {YYYY-MM-DD HH:MM}

**任务**：

**做了什么**：{操作+决策}

**标签**：

**文件变更**：
修改：{文件名}
新增：{文件名}
```

### Step 6: 报告完成

回复：
```
项目初始化完成。

项目名：{项目名}
位置：{项目根目录}/session-logs/{项目名}/

文件：
- README.md（项目入口）
- session-log.md（Session 日志）

触发 /session-log 开始记录工作日志。
```

## 大项目嵌套小项目模式

支持大项目下包含小项目的嵌套结构。在子目录下运行 `/project-init` 会创建独立的子项目文档，不影响父项目。

嵌套时建议在父项目的 README.md 中添加「关联项目」字段，便于跳转。
