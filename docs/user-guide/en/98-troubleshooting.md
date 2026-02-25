# Troubleshooting

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## App Launch Issues

## App won't open on macOS

### Symptoms
- "Cannot be opened because it is damaged" error
- Gatekeeper warning

### Solutions

**Method 1: Allow in System Preferences**
1. **System Preferences** > **Security & Privacy**
2. Click **Open Anyway** in **General** tab

**Method 2: Remove quarantine attribute in Terminal**
```bash
xattr -cr /Applications/VibeSmith.app
```

**Method 3: Temporarily disable Gatekeeper (not recommended)**
```bash
sudo spctl --master-disable
```

## App won't run on Windows

### Symptoms
- SmartScreen warning
- "Unknown publisher" error

### Solutions

**Method 1: Bypass SmartScreen**
1. Right-click installer > **Properties**
2. Check **Unblock** in **General** tab
3. Click **OK**

**Method 2: Run as administrator**
1. Right-click app icon
2. Select **Run as administrator**

## AppImage won't run on Linux

### Symptoms
- Permission denied error
- FUSE error

### Solutions

**Method 1: Grant execution permission**
```bash
chmod +x VibeSmith-*.AppImage
```

**Method 2: Install FUSE**
```bash
# Ubuntu/Debian
sudo apt-get install fuse libfuse2

# Fedora
sudo dnf install fuse fuse-libs
```

**Method 3: --no-sandbox option**
```bash
./VibeSmith-*.AppImage --no-sandbox
```

## Scan Issues

## Project scan not working

### Diagnosis

**1. Check Logs**
- **Help** > **View Logs**
- Check error messages

**2. Check Paths**
```bash
# Check if .cursor directory exists
ls -la .cursor/

# Check permissions
ls -ld .cursor/
```

**3. Check Cursor/Claude Code Path**
- **Settings** > **General** > **AI Tool Path**
- Verify correct path is set

### Solutions

**Empty Scan Results**
```bash
# Check if skills actually exist
find . -name "SKILL.md"

# Check global skills
ls -la ~/.cursor/skills/
```

**Slow Scan**
- Add exclude paths: `node_modules`, `.git`, `dist`
- Settings > Scan > Exclude Paths

**Scan Hangs**
1. Restart app
2. Clear cache: Settings > Advanced > Clear Cache
3. Rebuild index: Settings > Advanced > Rebuild Index

## Changes not auto-detected

### Check Auto Scan Enabled
- Settings > Scan > Turn on Auto Scan
- Scan interval: 5 minutes recommended

### Manual Rescan
- **Cmd+R** (Mac) or **Ctrl+R** (Windows)
- Or **File** > **Rescan Project**

## Performance Issues

## App is slow

### Causes

- Large projects (1000+ components)
- Auto scan interval too short
- Insufficient memory

### Solutions

**1. Add Exclude Paths**
```
Settings > Scan > Exclude Paths
- node_modules
- .git
- dist
- build
- coverage
```

**2. Adjust Scan Interval**
- Change 5min → 10min or 15min
- Or turn off auto scan and use manual scan

**3. Cache Optimization**
- Settings > Advanced > Cache Optimization
- Enable auto cleanup

**4. Database Cleanup**
```bash
# Optimize database after backup
sqlite3 ~/.vibesmith/db.sqlite "VACUUM;"
```

## High memory usage

### Monitoring
- **Help** > **System Info**
- Check memory usage

### Optimization
- Close multiple project windows
- Close dependency graph window (uses lots of memory)
- Restart app

## Data Issues

## Data loss

### Restore from Backup

**Restore from auto backup**
```bash
# Check backup directory
ls -la ~/.vibesmith/backups/

# Find latest backup
ls -lt ~/.vibesmith/backups/ | head -5

# Restore backup
cp ~/.vibesmith/backups/db-YYYY-MM-DD.sqlite ~/.vibesmith/db.sqlite
```

**Restore from Git (skill files)**
```bash
# Restore skill files
git checkout HEAD -- .cursor/skills/

# Restore specific skill only
git checkout HEAD -- .cursor/skills/my-skill/
```

## Conflicting components

### Duplicate Detection
- **Tools** > **Find Duplicate Components**
- Check local vs global conflicts

### Solutions
1. Delete one side
2. Rename
3. Set priority (local priority vs global priority)

## Database Error

### Rebuild
```bash
# Backup existing database
cp ~/.vibesmith/db.sqlite ~/.vibesmith/db.sqlite.bak

# Delete database (auto-recreated)
rm ~/.vibesmith/db.sqlite

# Restart app and rescan project
```

## Additional Help

## Collect Logs

Include the following information when reporting issues:

**1. App Logs**
- **Help** > **View Logs** > **Export Logs**
- Location: `~/.vibesmith/logs/app.log`

**2. System Info**
- **Help** > **System Info** > **Copy**
- OS, version, memory, CPU, etc.

**3. Reproduction Steps**
- Exact steps where problem occurred
- Screenshots (if possible)

## Community Support

### GitHub Issues
- Bug reports: [Issues](https://github.com/heesubsong/vibesmith-community/issues)
- Use bug template

### Discussions
- Questions: [Q&A](https://github.com/heesubsong/vibesmith-community/discussions/categories/q-a)
- Ideas: [Ideas](https://github.com/heesubsong/vibesmith-community/discussions/categories/ideas)

### Discord (TBD)
- Real-time chat support
- Community help

## Critical Issues

If app completely doesn't work:

**1. Run in Safe Mode**
```bash
# macOS/Linux
open -a VibeSmith --args --safe-mode

# Windows
VibeSmith.exe --safe-mode
```

**2. Reset Settings**
```bash
# Backup settings
cp ~/.vibesmith/config.json ~/.vibesmith/config.json.bak

# Delete settings (reset to defaults)
rm ~/.vibesmith/config.json
```

**3. Complete Reinstall**
```bash
# Backup all data
tar -czf vibesmith-backup.tar.gz ~/.vibesmith

# Delete data
rm -rf ~/.vibesmith

# Reinstall app
```

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0