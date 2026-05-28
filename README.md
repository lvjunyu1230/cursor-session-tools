# cursor-session-tools

Session logging tools for Cursor AI IDE. Includes two skills for initializing project documentation and recording session logs.

## Skills

### project-init

Initialize project documentation structure. Creates `README.md` and `session-log.md` in `session-logs/{project-name}/`.

**Trigger**: `/project-init`, "初始化项目", "新建项目"

### session-log

Record current session work log. Searches upward from current directory to find the nearest `session-logs/{project-name}/session-log.md` and appends a structured entry.

**Trigger**: `/session-log`, "记录 session", "记录一下", "log session"

## Features

- **Universal**: Works in any directory, no hardcoded paths
- **Nested projects**: Supports parent-child project structure with "nearest wins" search
- **Structured format**: Task, actions, tags, and file changes
- **Tags**: Optional tags for filtering and aggregation

## Quick Start

1. Run `/project-init` to initialize a project
2. Work on your project
3. Run `/session-log` to record your session

## Session Entry Format

```markdown
---

## {YYYY-MM-DD HH:MM}

**任务**：{task description}

**做了什么**：{actions and decisions}

**标签**：{optional tags}

**文件变更**：
修改：{modified files}
新增：{new files}
```

## License

MIT
