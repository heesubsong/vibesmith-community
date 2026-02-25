# Managing Commands

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## Navigate to Commands Page

![Navigate to Commands Page](images/commands-01-list.png)

Click **Components** > **Commands** in the left sidebar to see all commands.

Commands are slash commands starting with `/` in Cursor.

## Command Types

- **/spec-create**: Create frontend spec
- **/spec-review**: Review spec
- **/auto-implement**: Auto implementation
- **/request-api**: Request API implementation
- **/task-start**: Start task
- **/task-done**: Complete task
- **/daily-log**: Daily work log

## Create New Command

![Create New Command](images/commands-02-new-modal.png)

Click the **+ New Command** button to open the command creation modal.

## Command Configuration

1. **Command Name**: Without slash (e.g., `my-command`)
2. **Description**: What the command does
3. **Prompt**: Instructions to pass to AI
4. **Arguments**: Parameters the command will receive

## Usage Example

After creating command, in Cursor:

```
/my-command arg1 arg2
```

### 💡 Useful Tips

💡 Keep command names short and memorable.
💡 Write prompts clearly and specifically.
💡 Creating commands for frequently used tasks is efficient.

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0