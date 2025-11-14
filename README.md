# Claude Code MCP Async Server

**Asynchronous MCP wrapper for Claude Code CLI**

Enable Claude Code to spawn child Claude Code sessions for parallel task execution.

## Features

- ✅ **Async execution** - Start tasks in background, continue working
- ✅ **Multi-instance parallelism** - Run multiple Claude Code sessions simultaneously
- ✅ **Automatic cleanup** - No zombie processes
- ✅ **Zero config** - Works out of the box

## Quick Start

### 🚀 Install with UVX

Zero configuration - just run:

```bash
uvx claudecode-mcp-async
```

### Configure Claude Code

Add to your `~/.claude/settings.json`:

```json
{
  "mcpServers": {
    "claude-code-mcp": {
      "command": "uvx",
      "args": ["claudecode-mcp-async"],
      "env": {}
    }
  }
}
```

### Restart Claude Code

Reload or restart Claude Code to load the MCP server.

## Usage Examples

### 🚀 Async Execution (Game Changer!)

Start a long task and continue working immediately:

**You:**
> Please analyze the entire project code and generate a comprehensive technical report

**Claude:**
I'll analyze your entire project and generate a technical report. This is a large task, so I'll start it asynchronously...

✅ **Task Started** (Task ID: abc12345)
You can continue working on other things while it runs in the background!

**You:** (Continue working immediately)
> While the report is generating, help me write some unit tests

**Claude:**
Sure! Let me write those unit tests for you...

**You:** (A few minutes later)
> Can you check if the report task is finished?

**Claude:**
✅ **Report Complete!**

[View Detailed Technical Report]
- Project structure analysis
- Code quality assessment
- Performance optimization recommendations
- Security audit results

### ⚡ Parallel Execution

Run multiple tasks simultaneously:

**You:**
> I need to do three things at once:
> 1. Generate unit tests for utils.py
> 2. Refactor database.py to use async/await
> 3. Add type hints to all functions in api.py

**Claude:**
I'll start all three tasks in parallel!

🔄 **Task 1 Started** (Task ID: task1) - Generating unit tests
🔄 **Task 2 Started** (Task ID: task2) - Refactoring database code
🔄 **Task 3 Started** (Task ID: task3) - Adding type hints

All tasks are running in parallel...

**You:** (Later)
> Are all three tasks finished?

**Claude:**
✅ **All Complete!**

- ✅ Task 1: Unit tests for utils.py generated
- ✅ Task 2: database.py refactored to async mode
- ✅ Task 3: Type hints added to api.py functions

### 🎯 Quick Sync Tasks

For simple immediate tasks:

**You:**
> Write a Python function to validate email addresses

**Claude:**
```python
import re

def validate_email(email):
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None

# Usage examples
print(validate_email("user@example.com"))  # True
print(validate_email("invalid-email"))    # False
```

✅ **Task Complete!**

## Why Async?

**Problem:** Claude Code blocks the parent session while running.

**Solution:** This MCP server spawns child Claude Code processes that run in the background.

**Benefits:**
- 🚀 Start a task and continue working immediately
- ⚡ Run multiple tasks in parallel
- 🎯 No blocking, no waiting
- 🧹 Automatic process cleanup

## Troubleshooting

**Server not showing up?**
- Use absolute path in config
- Run: `chmod +x claudecode_mcp_async_server.py`
- Restart Claude Code

**Task stuck in "running"?**
- Wait a moment, large tasks take time
- Check: `ls -la /tmp/claude_code_tasks/`
- View logs: `tail -f /tmp/claude_code_mcp_debug.log`

## Requirements

- Python 3.6+
- Claude Code CLI installed

## License

MIT License

---

**Questions?** Open an issue on GitHub.

