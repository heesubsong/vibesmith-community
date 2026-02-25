# Sync Management

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## What is Sync?

**Sync** is a feature that automatically aligns local and global components. You can efficiently manage project-specific and global components.

### Why is Sync Needed?

**Problem Situation**:
```
Project A: skill-x (v1.0) ← Modified
Project B: skill-x (v0.9) ← Old version!
Project C: skill-x None   ← Not added yet!
```

**After Sync**:
```
Project A: skill-x (v1.0) ✅
Project B: skill-x (v1.0) ✅ Auto-updated
Project C: skill-x (v1.0) ✅ Auto-added
```

## Sync Settings

![Sync Settings](images/sync-01-settings.png)

Manage sync at **Settings** > **Sync**.

## Local vs Global

### Local Components
**Location**: `.cursor/`, `.claude/`

**Features**:
- Apply to current project only
- Project-specific logic
- Quick experimentation and testing

**Example**:
```
.cursor/skills/
├── project-specific-skill/
├── custom-workflow/
└── temp-experiment/
```

### Global Components
**Location**: `~/.cursor/`, `~/.claude/`

**Features**:
- Apply to all projects
- Generic skills
- Reusable patterns

**Example**:
```
~/.cursor/skills/
├── react-component-generator/
├── code-formatter/
└── test-writer/
```

### When to Use Which?

#### Keep Local
```
✅ Project-specific coding rules
✅ Specific domain logic
✅ Experimental skills
✅ Contains secrets

Example: "customer-api-wrapper" → This project only
```

#### Promote to Global
```
✅ Use in multiple projects
✅ Verified patterns
✅ Share with entire team
✅ Generic functionality

Example: "react-component-generator" → All projects
```

## Sync Directions

### 1. Local → Global (Promote)
**When to Use**: When you want to use useful skills in other projects

**Example**:
```
Develop locally → Test → Verify complete → Promote to global
```

**Method**:
1. Open skill detail page
2. Click **Promote to Global** button
3. Confirm

### 2. Global → Local (Copy)
**When to Use**: Customize global skill for project

**Example**:
```
Copy global skill → Modify locally → Project-specific
```

**Method**:
1. Select global skill
2. Click **Copy to Local** button
3. Modify if needed

### 3. Bidirectional (Auto)
**When to Use**: Automatically maintain latest version

**Action**:
- Local modification → Auto-reflect in global
- Global modification → Auto-reflect in local
- Notify user on conflict

## Manual Sync

![Manual Sync](images/sync-02-manual.png)

![Manual Sync Demo](gifs/sync-demo.gif)

Click **Sync** button to manually synchronize.

### Sync Process

#### Step 1: Detect Changes
```
🔍 Comparing local and global...
  - Newly added files: 3
  - Modified files: 2
  - Deleted files: 1
```

#### Step 2: Check Conflicts
```
⚠️  Conflicts found:
  - skill-x: Both local and global modified
  - skill-y: Local deleted, global modified
```

#### Step 3: Preview
```
📋 Scheduled to sync:
  ✅ skill-a: Local → Global
  ✅ skill-b: Global → Local
  ⚠️  skill-x: Conflict resolution needed
```

#### Step 4: Execute
```
🔄 Syncing...
  ✅ skill-a updated
  ✅ skill-b updated
  ⏭️  skill-x skipped (conflict)

✅ Complete! 2 synced, 1 skipped
```

## Sync Options

### Conflict Handling
- **Overwrite**: Replace existing file
- **Merge**: Combine contents
- **Skip**: Ignore conflicting items
- **Backup then Overwrite**: Safe choice ✅

### Scope Settings
- **All**: All components
- **By Type**: Skills only, Agents only, etc.
- **Selected**: Only manually selected items

### Backup
- **Auto Backup**: Automatic backup before sync
- **Backup Retention**: Keep last 10
- **Restore**: Restore to previous version anytime

## Conflict Resolution

![Conflict Resolution](images/sync-03-conflicts.png)

**Conflict Resolution** window appears when conflicts are found.

### Conflict Types

#### 1. Name Conflict
**Situation**: Different components with same name in local and global

**Resolution**:
```
Option A: Rename one
  local-skill-x, global-skill-x

Option B: Set priority
  Local priority → Keep local only
  Global priority → Keep global only
```

#### 2. Content Conflict
**Situation**: Same component modified in both local and global

**Resolution**:
```
Option A: Local priority
  ← Keep local changes

Option B: Global priority
  → Keep global changes

Option C: Manual merge
  ↔ Select only needed parts from both
```

#### 3. Dependency Conflict
**Situation**: Circular reference in dependency chain

**Resolution**:
```
Before: A → B → C → A (❌ Circular)
After:  A → B → C (✅ Normal)

Method: Restructure dependencies
```

### Conflict Resolution Strategies

#### Safe Strategy (Recommended)
```
1. Create backup
2. Review conflict items
3. Judge importance
4. Resolve one by one
5. Test
```

#### Quick Strategy
```
1. Apply local priority in bulk
2. Fetch from global later if needed
```

## Auto Sync

![Auto Sync](images/sync-04-auto.png)

Turn on **Settings** > **Sync** > **Auto Sync** to auto-sync on file changes.

### Auto Sync Behavior

#### File Watching
```
🔍 File system monitoring
  - Local: .cursor/, .claude/
  - Global: ~/.cursor/, ~/.claude/
  
Detect:
  - File creation
  - File modification
  - File deletion
  - Rename
```

#### On Change Detection
```
1. Detect changes
2. Identify impact scope
3. Check conflicts
4. Auto-sync or notify
```

#### Conflict Notification
```
💬 Notification:
   "Conflict found in skill-x.
    Please resolve manually."

[Resolve] [Later] [Ignore]
```

### Sync Rules

#### Local Priority Rule
**Setting**: Auto-reflect local changes in global

**Action**:
```
Local modification → Auto-update global
Global modification → Notify only (manual approval needed)
```

**When to Use**: During project development

#### Global Priority Rule
**Setting**: Auto-reflect global changes in local

**Action**:
```
Global modification → Auto-update local
Local modification → Notify only (manual approval needed)
```

**When to Use**: Stable project

#### Bidirectional Rule
**Setting**: Auto-update with latest changes

**Action**:
```
Local modification → Update global
Global modification → Update local
Simultaneous modification → Conflict notification
```

**When to Use**: Team collaboration

#### Manual Confirm Rule
**Setting**: Manually approve all changes

**Action**:
```
All changes → Notification + Wait for approval
```

**When to Use**: Critical project

## Sync Interval

- **Immediate**: Immediately on file change (not recommended)
- **5 minutes**: Every 5 minutes (default)
- **10 minutes**: Every 10 minutes
- **30 minutes**: Every 30 minutes
- **Manual**: Turn off auto-sync

### Interval Selection Guide

```
✅ 5 min: Active development
✅ 10 min: General work
✅ 30 min: Stable project
✅ Manual: Network drive or large volume
```

## Best Practices

### 1. Enable Backup
```
✅ Always turn on auto-backup
✅ Backup retention: 30 days
✅ Manual backup before important changes
```

### 2. Prevent Conflicts
```
✅ Sync before work
✅ Sync after work
✅ Clear naming
✅ Minimize dependencies
```

### 3. Progressive Sync
```
Step 1: Develop & test locally
Step 2: Promote to global after verification
Step 3: Use in other projects
```

### 4. Regular Cleanup
```
Monthly: Remove unused components
Quarterly: Optimize dependencies
Semi-annually: Review entire structure
```

### ⚠️ Cautions

⚠️ Auto-sync can cause unintended overwrites.
⚠️ Always backup before important changes.
⚠️ Auto-sync may be slow on network drives.
⚠️ Ignoring conflicts can lead to data loss.

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0
