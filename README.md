# cursor-session-tools

> 让每一次 Cursor 对话都不被遗忘

你有没有过这样的经历？在一个悠闲的下午，和 AI 完成了一场酣畅淋漓的coding讨论，改了十几个文件，做了无数个决策——然后第二天打开 Cursor，完全想不起昨天干了什么。

**cursor-session-tools** 就是来解决这个问题的。

## 它是什么

两个 Cursor Skill，形成完美的工作记录闭环：

| Skill | 作用 | 触发方式 |
|-------|------|----------|
| **project-init** | 初始化项目文档结构 | `/project-init` |
| **session-log** | 记录每次工作的摘要 | `/session-log` |

## 能做什么

### 1. 一键初始化项目

```bash
/project-init
```

自动创建：

```
project/
└── session-logs/
    └── my-project/
        ├── README.md      # 项目入口，看一眼就懂
        └── session-log.md # 工作日志，按时间线记录
```

### 2. 一句话记录 session

```bash
/记录一下
```

自动生成：

```markdown
## 2026-05-28 14:51

**任务**：重构用户认证模块

**做了什么**：拆分了 AuthService，移除了过期的 JWT 逻辑

**标签**：refactor, auth

**文件变更**：
修改：auth/service.ts, auth/middleware.ts
新增：auth/types.ts
```

### 3. 智能嵌套支持

大项目套小项目？没问题。自动找到**最近的**项目文档来记录。

```
root/                    → 记录到大项目
root/subprojects/        → 记录到小项目
root/subprojects/code/  → 依然记录到小项目
```

## 为什么需要它

| 痛点 | 解决 |
|------|------|
| 每次都想不起昨天做了什么 | 时间线日志，一目了然 |
| git log 太零散，看不出上下文 | 结构化记录，任务+操作+文件变更 |
| 文档散落各处 | 统一在 `session-logs/` 下管理 |
| 大项目下的小项目记录混乱 | 最近优先原则，智能嵌套 |

## 安装

把 `project-init` 和 `session-log` 两个文件夹放到你的 Cursor skill 目录：

```
~/.claude/skills/project-session/
├── project-init/
│   └── SKILL.md
└── session-log/
    └── SKILL.md
```

## 开始使用

**第一步**：初始化项目

```
/project-init
项目名：my-awesome-project
目标：做一个很棒的东西
```

**第二步**：正常工作的同时，记下关键决策

```
/记录一下
```

**第三步**：想回顾项目进度？

直接打开 `session-logs/my-awesome-project/session-log.md`，时间线清晰呈现。

## Session 条目格式

```markdown
---

## {YYYY-MM-DD HH:MM}

**任务**：{一句话描述本次目标}

**做了什么**：{操作+决策}

**标签**：{可选，用逗号分隔}

**文件变更**：
修改：{文件名}
新增：{文件名}
```

## 项目状态一目了然

每个项目都有 `README.md`：

```markdown
# my-awesome-project

## 目标
做一个很棒的东西

## 状态
- [x] 已完成核心功能
- [ ] 添加测试

## 重要进展记录
| 日期 | 进展 |
|------|------|
| 2026-05-28 | 完成用户认证模块 |

## Todo
- [ ] 性能优化
- [ ] 文档完善
```

## License

MIT 
