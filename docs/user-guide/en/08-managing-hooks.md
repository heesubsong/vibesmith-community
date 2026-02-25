# Managing Hooks

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## Navigate to Hooks Page

![Navigate to Hooks Page](images/hooks-01-list.png)

Click **Components** > **Hooks** in the left sidebar to see all Git hooks.

Git hooks are scripts that run automatically during Git operations like commit, push, etc.

## Main Git Hooks

- **pre-commit**: Run before commit (lint, format check)
- **commit-msg**: Validate commit message
- **pre-push**: Run before push (run tests)
- **post-commit**: Run after commit (notifications, etc.)

### 💡 Useful Tips

💡 Hooks are powerful tools for automating Git workflow.
💡 You can auto-check code quality with pre-commit hooks.
💡 If a hook fails, the Git operation is aborted.

## Create New Hook

![Create New Hook](images/hooks-02-new-modal.png)

Click the **+ New Hook** button to open the hook creation modal.

## Hook Configuration

1. **Select Hook Type**: pre-commit, commit-msg, pre-push, etc.
2. **Write Script**: Commands or scripts to execute
3. **Execution Conditions**: Specific file patterns, etc.

## Example: pre-commit Lint Check

```bash
#!/bin/bash
# Lint check
npm run lint

# Abort commit on failure
if [ $? -ne 0 ]; then
  echo "❌ Lint check failed. Commit aborted."
  exit 1
fi
```

### ⚠️ Warnings

⚠️ Hook scripts must have execution permission.
⚠️ Write carefully as failed hooks will abort Git operations.
⚠️ Overly complex hooks can slow down workflow.

## Enable/Disable Hook

![Enable/Disable Hook](images/hooks-03-toggle.png)

Use the toggle switch on the hook card to enable or disable hooks.

## Enabled vs Disabled

- **Enabled**: Hook runs automatically during Git operations
- **Disabled**: Hook doesn't run (temporary off)

## Usage Scenarios

**During Development**: Temporarily disable for quick testing
**Before Release**: Enable all hooks for quality verification

Toggle takes effect immediately.

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0