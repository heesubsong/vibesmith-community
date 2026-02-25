# Sync Management

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## Sync Settings

![Sync Settings](images/sync-01-settings.png)

Manage local and global component synchronization at **Settings** > **Sync**.

## Local vs Global

### Local Components
- **Location**: `.cursor/`, `.claude/`
- **Scope**: Current project only
- **Purpose**: Project-specific components

### Global Components
- **Location**: `~/.cursor/`, `~/.claude/`
- **Scope**: All projects
- **Purpose**: Reusable general-purpose components

## Sync Direction

- **Local → Global**: Promote project skill to global
- **Global → Local**: Copy global skill to project
- **Bidirectional**: Auto sync (change detection)

## Manual Sync

![Manual Sync](images/sync-02-manual.png)

![Manual Sync Demo](gifs/sync-demo.gif)

Click the **Sync** button to manually execute synchronization.

## Sync Process

1. **Detect Changes**: Check local and global differences
2. **Check Conflicts**: Check for duplicate components
3. **Preview**: Show items to be synced
4. **Execute**: Sync after confirmation

## Sync Options

- **Overwrite**: Overwrite existing files
- **Merge**: Merge contents
- **Skip**: Skip conflicting items
- **Backup**: Backup existing files before sync

## Conflict Resolution

![Conflict Resolution](images/sync-03-conflicts.png)

If conflicts are found during sync, a **Conflict Resolution** window appears.

## Conflict Types

### 1. Name Conflict
- Same-named component exists in both local and global
- **Solution**: Rename one side or set priority

### 2. Content Conflict
- Same component modified differently in local and global
- **Solution**: Manual merge or choose one side

### 3. Dependency Conflict
- Dependency chain has circular reference
- **Solution**: Restructure dependencies

## Conflict Resolution Strategies

- **Local Priority**: Keep local changes
- **Global Priority**: Apply global changes
- **Manual Merge**: Choose manually
- **Backup then Overwrite**: Safe choice

## Auto Sync

![Auto Sync](images/sync-04-auto.png)

Turn on **Settings** > **Sync** > **Auto Sync** to automatically sync on file changes.

## Auto Sync Behavior

- **File Watch**: Monitor local/global directories
- **Change Detection**: Detect file create/modify/delete
- **Auto Sync**: Auto sync according to set rules
- **Conflict Notification**: Notify on conflict

## Sync Rules

- **Local Priority**: Auto push local changes to global
- **Global Priority**: Auto pull global changes to local
- **Bidirectional**: Based on latest changes
- **Manual Confirm**: Request user confirmation on conflict

## Sync Interval

- **Immediate**: Immediately on file change (not recommended)
- **5 minutes**: Every 5 minutes (default)
- **10 minutes**: Every 10 minutes
- **Manual**: Turn off auto sync

### ⚠️ Warnings

⚠️ Auto sync may cause unintended overwrites.
⚠️ Backup is recommended before important changes.
⚠️ Auto sync may be slow on network drives.

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0