# Frequently Asked Questions (FAQ)

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## General Questions

### Is VibeSmith free?

Yes, VibeSmith is completely free for personal and commercial use.

### Can I use VibeSmith commercially?

Yes, you can use it completely freely. No license fees, user limits, or project restrictions.

### Which AI tools does VibeSmith support?

Currently supported AI tools:
- **Cursor** (VS Code-based IDE)
- **Claude Code** (Anthropic's AI editor)

More tools like GitHub Copilot and Codeium will be supported in the future.

### What's the difference between Cursor and Claude Code?

| Comparison | Cursor | Claude Code |
|------------|--------|-------------|
| **Base** | VS Code | Independent editor |
| **AI Model** | GPT-4, Claude | Claude only |
| **Price** | Paid ($20/month) | Free (Claude Pro) |
| **Usability** | IDE-friendly | AI conversation-focused |

VibeSmith perfectly supports both tools.

### What are VibeSmith's main features?

- **Skills Management**: Reusable commands for AI agents
- **Agents Management**: Complex workflow automation
- **Commands Management**: Quick execution with slash commands
- **Hooks Management**: Git operation automation
- **Rules Management**: Apply team coding conventions
- **Dependency Graph**: Visualize component relationships
- **Advanced Search**: Fuzzy search, regex, filter search
- **Sync**: Synchronize local ↔ global components

### Do I need Cursor/Claude Code installed to use VibeSmith?

Yes, VibeSmith is a tool for managing Cursor or Claude Code configuration files. 
The AI tool must be installed first.

## Data and Security

### Where is data stored?

All data is stored **locally on your computer only**:

```
~/.vibesmith/               # VibeSmith data
├── db.sqlite              # Project index database
├── config.json            # App settings
├── backups/               # Auto backup files
└── logs/                  # App logs

.cursor/                   # Project-specific components
├── skills/
├── agents/
├── commands/
├── hooks/
└── rules/

~/.cursor/                 # Global components
├── skills/
├── agents/
└── ...
```

**Important**: **No data** is transmitted to external servers.

### Is my code sent externally?

No! VibeSmith works **completely locally**. 
- No network connection required
- No cloud servers
- No personal information collection

### Can I use VibeSmith at my company?

Yes, it's completely safe:
- All data stored locally only
- No external network communication
- Easy to comply with security policies

### How do I backup?

#### Auto Backup (Recommended)
```
Settings > General > Auto Backup
- Backup interval: Daily (default)
- Backup location: ~/.vibesmith/backups/
- Retention period: 30 days
```

#### Manual Backup
```bash
# 1. Backup VibeSmith data
tar -czf vibesmith-backup.tar.gz ~/.vibesmith

# 2. Backup project skills (Git recommended)
git add .cursor/
git commit -m "backup: save cursor components"

# 3. Backup global skills
cp -r ~/.cursor/skills ~/cursor-skills-backup
```

#### Restoration
```bash
# Restore VibeSmith data
tar -xzf vibesmith-backup.tar.gz -C ~/

# Restore from Git
git checkout HEAD -- .cursor/
```

## Project Management

### What's the difference between project-specific and global components?

| Category | Local (Project-specific) | Global |
|----------|-------------------------|--------|
| **Path** | `.cursor/skills/` | `~/.cursor/skills/` |
| **Scope** | Current project only | All projects |
| **Purpose** | Project-specific skills | General skills |
| **Git** | Include recommended | Don't include |
| **Priority** | High (overwrites) | Low |

**Usage Examples**:
- **Local**: React project-specific component creation skill
- **Global**: Commit message generation, code review skills

### Can I manage multiple projects simultaneously?

Yes, VibeSmith supports multi-project:
- Can open multiple project windows simultaneously
- Each project managed independently
- Global components shared across all projects

**Tip**: 
```
File > New Window (Cmd+Shift+N)
→ Open another project
```

### How do I add a project?

**Method 1: Open Directly**
```
File > Open Project (Cmd+O)
→ Select project root directory
```

**Method 2: Drag and Drop**
```
Drag project folder into VibeSmith window
```

**Method 3: Recent Projects**
```
File > Recent Projects
→ Select from list
```

### How do I remove a project?

```
Right-click in project list > Remove
```

**Note**: 
- Only removes from list (files not deleted)
- Use Finder/Explorer to delete actual files

## Skills, Agents, Commands

### What's the difference between Skills and Agents?

| Category | Skills | Agents |
|----------|--------|--------|
| **Invocation** | `@skill-name` | `@agent-name` |
| **Complexity** | Simple (1-5 steps) | Complex (multi-step workflow) |
| **Execution Time** | Immediate (seconds) | Long (minutes) |
| **Output** | Code, text | Reports, issues, PRs |
| **Example** | Component creation | Spec → Implementation → Test → PR |

**When to use Skills?**
- Code snippet generation
- File formatting
- Simple transformations

**When to use Agents?**
- Full feature implementation
- Automated workflows
- Tasks requiring multiple steps

### How are Commands different?

**Commands** are quick actions starting with slash (`/`).

```
/spec-create login page
/auto-implement login-spec.md
/daily-log
```

**Differences**:
- Skills: Invoke with `@`, use in AI context
- Commands: Invoke with `/`, immediate execution
- Agents: Long-running, background

### How do I share Skills?

#### Method 1: Team Sharing via Git (Recommended)
```bash
# Include .cursor in Git
git add .cursor/skills/
git commit -m "feat: add component generation skill"
git push

# Team members automatically get it on pull
```

#### Method 2: File Copy
```bash
# Copy to another project
cp -r .cursor/skills/my-skill /other/project/.cursor/skills/

# Move to global (use in all projects)
cp -r .cursor/skills/my-skill ~/.cursor/skills/
```

#### Method 3: Community Sharing
```markdown
1. Upload to GitHub Gist
2. Write installation instructions in README
3. Share with community
```

### Agents are too slow

**Causes**:
- Complex workflows
- Large projects
- AI model response time

**Solutions**:
1. **Check logs**: Identify which step is slow
2. **Optimize steps**: Remove unnecessary steps
3. **Reduce scope**: Specific directories instead of full scan
4. **Use faster model**: GPT-4 → GPT-3.5

### Rules not applying

**Checklist**:
- [ ] Is the rule enabled?
- [ ] Are file patterns (globs) correct?
- [ ] Is there a higher priority rule?
- [ ] Is local rule overwriting global rule?

**Debug Method**:
```
1. Ask AI directly:
   "What rules are currently applied?"

2. Check rule logs:
   Settings > Advanced > Rule Application Log

3. Test:
   Request simple code generation and verify rule application
```

## Search and Filtering

### Search is slow

**Causes**:
- Large project
- Index is old
- Too broad search

**Solutions**:
```
1. Rebuild index:
   Settings > Advanced > Rebuild Index

2. Add exclusion paths:
   Settings > Scan > Exclusion Paths
   - node_modules
   - .git
   - dist
   - build

3. Narrow search scope:
   - Search specific type only (type:skill)
   - Search specific path only (path:src/)
```

### What is fuzzy search?

**Fuzzy Search** is smart search that allows typos.

**Example**:
```
Input: "usrprofil"
Results:
- ✅ user-profile
- ✅ UserProfile
- ✅ user_profile_component
```

**Use Cases**:
- When you don't know exact name
- When there are typos
- Finding similar names

### How do I use regex search?

**Regex Search** finds complex patterns.

**Activate**:
```
Search box > Options > Regex (.*) icon click
```

**Examples**:
```regex
# All hooks starting with use
^use[A-Z].*

# Date format (YYYY-MM-DD)
\d{4}-\d{2}-\d{2}

# API endpoints
\/api\/v\d+\/.*

# Specific tag combinations
tag:(api|hook).*tag:react
```

### How do I use saved searches?

**Save**:
```
1. Enter search
2. Click star (⭐) icon
3. Enter name and save
```

**Load**:
```
Search box > Bookmark icon > Select from list
```

**Manage**:
```
Settings > Search > Manage Saved Searches
- Edit
- Delete
- Reorder
```

**Usage Examples**:
```
- "My skills": author:me type:skill
- "Last week": modified:7d
- "Test related": tag:test OR tag:testing
- "React components": type:skill tag:react path:components/
```

## Dependency Graph

### How do I interpret the dependency graph?

**Nodes**:
- **Circle**: Each component
- **Size**: Number of dependencies (larger = more dependencies)
- **Color**: Component type
  - 🔵 Blue: Skill
  - 🟢 Green: Agent
  - 🟡 Yellow: Command
  - 🔴 Red: Hook
  - 🟣 Purple: Rule

**Edges**:
- **Arrow**: Dependency direction
- **Thickness**: Dependency strength (thicker = more usage)
- **Color**: Dependency type

**Example**:
```
A → B: A uses B
A ↔ B: Circular dependency (caution!)
```

### How do I find circular dependencies?

```
Dependency Graph > Filter > Show circular only
```

**Resolution**:
1. Identify circular path
2. Remove intermediate component or
3. Reverse dependency direction

### Graph is too complex to read

**Simplification Methods**:
```
1. Use filters:
   - Show specific type only
   - Center on specific component

2. Change layout:
   - Hierarchical
   - Circular
   - Force-directed

3. Limit depth:
   - Show 1 level only
   - Show direct dependencies only
```

### How do I save graph as image?

```
Dependency Graph > Right-click > Export as Image
- PNG (high quality)
- SVG (vector, scalable)
- PDF (for documents)
```

## Synchronization

### When should I use sync?

**Scenario 1: Local → Global**
```
When a project-specific skill is useful and
you want to use it in other projects
```

**Scenario 2: Global → Local**
```
When you want to customize a global skill
for a specific project
```

**Scenario 3: Bidirectional**
```
Develop locally and sync to global
when stable
```

### What if conflicts occur during sync?

**Conflict Resolution Strategies**:
```
1. Overwrite:
   - Completely replace target with source
   - Caution: Target changes lost

2. Merge:
   - Combine both changes
   - Manual verification needed

3. Skip:
   - Exclude conflicting files only
   - Sync rest

4. Backup:
   - Create backup before conflict
   - Safe attempt
```

**Recommended**:
```
1. Backup first
2. Try merge
3. Manual review
4. Apply after testing
```

### How do I set up auto-sync?

```
Settings > Sync > Auto Sync
- Enable
- Interval: 1 hour (recommended)
- Direction: Bidirectional or unidirectional
- Conflict handling: Always ask (recommended)
```

**Caution**:
- Set auto-sync carefully
- Recommend manual confirmation on conflicts
- Enable backup automation together

## Performance and Optimization

### App is slow

**Performance Checklist**:
```
1. Project size:
   - 1000+ components: Add exclusion paths
   
2. Scan settings:
   - Auto-scan interval: 5min → 10min
   - Exclusion paths: node_modules, dist, .git
   
3. Cache:
   - Settings > Advanced > Optimize Cache
   - Periodically clear cache
   
4. Memory:
   - Close multiple project windows
   - Close dependency graph window (uses much memory)
```

### High memory usage

**Monitoring**:
```
Help > System Info
- Check memory usage
- Check CPU usage
```

**Optimization**:
```
1. Close unused windows
2. Stop unnecessary background tasks
3. Clear cache
4. Restart app
```

### Database got large

**Cleanup Method**:
```bash
# 1. Backup
cp ~/.vibesmith/db.sqlite ~/.vibesmith/db.sqlite.bak

# 2. Optimize
sqlite3 ~/.vibesmith/db.sqlite "VACUUM;"

# 3. Delete old data
sqlite3 ~/.vibesmith/db.sqlite "DELETE FROM scan_history WHERE created_at < date('now', '-30 days');"
```

**Auto Cleanup**:
```
Settings > Advanced > Auto Database Cleanup
- Enable
- Retention period: 30 days
```

## Additional Help

### Need more help?

**Documentation**:
- [Troubleshooting Guide](98-troubleshooting.md)
- [User Guide](README.md)

**Community**:
- [GitHub Issues](https://github.com/heesubsong/vibesmith-community/issues) - Bug reports
- [Discussions](https://github.com/heesubsong/vibesmith-community/discussions) - Questions, ideas
- [Discord](https://discord.gg/vibesmith) - Real-time chat (TBD)

### How do I request a feature?

```
1. GitHub Discussions > Ideas category
2. Title: [Feature Request] Feature name
3. Content:
   - Problem description
   - Proposed solution
   - Alternatives
   - Additional context
```

### I found a bug

```
1. GitHub Issues > New Issue
2. Select bug template
3. Include required info:
   - Reproduction steps
   - Expected behavior
   - Actual behavior
   - Screenshots
   - System info (Help > System Info)
   - Log files
```

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0
