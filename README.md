# Claude Code MCP Async Server

**Asynchronous MCP wrapper for Claude Code CLI**

Enable Claude Code to spawn child Claude Code sessions for parallel task execution.

## Features

- ✅ **Async execution** - Start tasks in background, continue working
- ✅ **Multi-instance parallelism** - Run multiple Claude Code sessions simultaneously
- ✅ **Automatic cleanup** - No zombie processes
- ✅ **Zero config** - Works out of the box
- ✅ **Cross-platform** - Supports Windows, Linux, and macOS
- ✅ **CI/CD ready** - GitHub Actions workflows included

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
- Linux/macOS: Run `chmod +x claudecode_mcp_async_server.py`
- Restart Claude Code

**Task stuck in "running"?**
- Wait a moment, large tasks take time
- Check task files:
  - **Linux/macOS:** `ls -la /tmp/claude_code_tasks/`
  - **Windows:** `dir %TEMP%\claude_code_tasks\`
- View logs:
  - **Linux/macOS:** `tail -f /tmp/claude_code_mcp_debug.log`
  - **Windows:** `type %TEMP%\claude_code_mcp_debug.log`

**Platform-specific notes:**
- Windows: Automatic process cleanup (no zombie processes)
- POSIX: Uses SIGCHLD handler for process cleanup
- All platforms: Uses platform-appropriate temp directories

## Requirements

- Python 3.6+
- Claude Code CLI installed

## Development

### Building from Source

Using `uv` (recommended):

```bash
# Install uv if you haven't already
pip install uv

# Build the package
uv build

# Install locally
uv pip install dist/*.whl --system
```

### GitHub Actions

This project includes automated workflows:

1. **Test Workflow** (`.github/workflows/test.yml`)
   - Runs on: Windows, Linux, macOS
   - Python versions: 3.8, 3.9, 3.10, 3.11, 3.12
   - Triggered on: push to main/develop/claude branches, pull requests
   - Actions:
     - Build with `uv`
     - Run import tests
     - Lint with flake8, black, isort

2. **Publish Workflow** (`.github/workflows/publish.yml`)
   - Builds distribution packages using `uv`
   - Publishes to PyPI on release
   - Uploads to GitHub Releases
   - Supports TestPyPI for testing

### Publishing to PyPI

**Option 1: Automatic (GitHub Release)**
1. Create a new release on GitHub
2. Workflow automatically builds and publishes to PyPI

**Option 2: Manual (TestPyPI)**
1. Go to Actions → Publish to PyPI
2. Run workflow manually
3. Set `test_pypi` to `true` for TestPyPI

**Setting up PyPI Publishing:**
1. Configure trusted publishing in your PyPI project settings
2. Add environment `pypi` to your GitHub repository
3. No API tokens needed (uses OIDC)

## License

MIT License

---

**Questions?** Open an issue on GitHub.

