# Frequently Asked Questions (FAQ)

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## General Questions

## Is VibeSmith free?

Yes, VibeSmith is free for personal and commercial use.

## What's the difference between Cursor and Claude Code?

- **Cursor**: VS Code-based IDE, commercial
- **Claude Code**: Claude AI-specific editor

VibeSmith supports both tools.

## What's the difference between project-specific vs global skills?

- **Project-specific (Local)**: `.cursor/skills/` - Applied to current project only
- **Global**: `~/.cursor/skills/` - Applied to all projects

## Where is data stored?

All data is stored locally:
- Skill files: `.cursor/`, `~/.cursor/`
- Database: `~/.vibesmith/db.sqlite`
- Settings: `~/.vibesmith/config.json`

No data is sent externally.

## Can I manage multiple projects simultaneously?

Yes, VibeSmith can open multiple projects at once.
Each project is managed in a separate window.

## Usage

## How do I share skills?

### Method 1: File Copy
```bash
# Copy skill folder
cp -r .cursor/skills/my-skill /path/to/other/project/.cursor/skills/
```

### Method 2: Manage with Git
Include skills in Git repository to share with team

### Method 3: Use Global Skills
Place in `~/.cursor/skills/` to use across all projects

## How do I interpret the dependency graph?

- **Nodes**: Each component
- **Edges**: Dependency relationships
- **Color**: Component type
- **Size**: Number of dependencies

Click to see detailed information.

## Search is slow. What should I do?

1. **Rescan**: Cmd+R (Mac) or Ctrl+R (Windows)
2. **Rebuild Index**: Settings > Advanced > Rebuild Index
3. **Add Exclude Paths**: Exclude unnecessary directories

## How do I backup?

### Auto Backup
- Settings > General > Turn on Auto Backup
- Backup location: `~/.vibesmith/backups/`

### Manual Backup
```bash
# Backup project skills
cp -r .cursor/skills ./skills-backup

# Backup global skills
cp -r ~/.cursor/skills ~/skills-backup
```

## Troubleshooting

## App won't start

### macOS
- Check Gatekeeper settings
- Check logs in Console app

### Windows
- Add Windows Defender exception
- Run as administrator

### Linux
- Check AppImage execution permission
- Check library dependencies

## Scan not working

1. Check Cursor/Claude Code path
2. Check `.cursor/` directory permissions
3. Check log file: Help > View Logs

## Changes not reflected

- **Manual rescan**: Cmd+R / Ctrl+R
- **Check auto scan**: Settings > Scan > Auto Scan
- **Clear cache**: Settings > Advanced > Clear Cache

## Need more help?

- [Troubleshooting Guide](98-troubleshooting.md)
- [GitHub Issues](https://github.com/heesubsong/vibesmith-community/issues)
- [Discussions](https://github.com/heesubsong/vibesmith-community/discussions)

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0