# Troubleshooting Guide

Common issues and solutions for VibeSmith.

## 🚨 Installation Issues

### macOS: "VibeSmith can't be opened because it is from an unidentified developer"

**Solution:**
1. Right-click **VibeSmith.app** in Applications
2. Select **"Open"**
3. Click **"Open"** in the security dialog

**Alternative:**
1. Go to **System Preferences → Security & Privacy**
2. Click **"Open Anyway"** next to the VibeSmith warning
3. Restart VibeSmith

### macOS: Application is damaged and can't be opened

**Solution:**
```bash
# Remove quarantine attribute
xattr -cr /Applications/VibeSmith.app

# Restart VibeSmith
```

### Windows: SmartScreen prevented an unrecognized app

**Solution:**
1. Click **"More info"**
2. Click **"Run anyway"**

---

## 🔍 Scanning Issues

### Scan is not finding my skills/agents

**Check:**

1. **Global path is correct**
   - Settings → Global Path
   - Cursor: `~/.cursor/`
   - Claude Code: `~/.claude/`

2. **Skills directory exists**
   ```bash
   # Check if directory exists
   ls -la ~/.cursor/skills/
   ls -la ~/.claude/skills/
   ```

3. **Skills follow correct format**
   - Skill: `skills/my-skill/SKILL.md`
   - Agent: `agents/my-agent/AGENT.md`
   - Command: `commands/my-command/COMMAND.md`

4. **File permissions**
   ```bash
   # Fix permissions
   chmod -R 755 ~/.cursor/skills/
   ```

### Scan is taking too long

**Normal scan times:**
- Small (< 50 components): 5-10 seconds
- Medium (50-200 components): 10-30 seconds
- Large (200+ components): 30-60 seconds

**If longer:**
1. Check CPU usage (Activity Monitor/Task Manager)
2. Close other apps
3. Restart VibeSmith
4. Try manual scan (Cmd/Ctrl + R)

### Scan fails with error

**Common errors:**

1. **"Permission denied"**
   ```bash
   # Fix permissions
   sudo chmod -R 755 ~/.cursor/
   ```

2. **"Directory not found"**
   - Check global path in Settings
   - Create directory if missing:
     ```bash
     mkdir -p ~/.cursor/skills/
     ```

3. **"Invalid format"**
   - Check SKILL.md format
   - Validate with [Skill Validator](../plugins/example-skill-generator/)

---

## 🔄 Sync Issues

### Components not showing in AI tool (Cursor/Claude)

**Solution:**

1. **Restart AI tool**
   - Quit and restart Cursor/Claude Code

2. **Check if enabled**
   - Open VibeSmith
   - Check toggle is green (enabled)

3. **Re-scan project**
   - VibeSmith → Scan Project (Cmd/Ctrl + R)

4. **Check file path**
   ```bash
   # Verify file exists
   ls -la ~/.cursor/skills/my-skill/SKILL.md
   ```

5. **Check file contents**
   - Open SKILL.md in editor
   - Verify format is correct

### Changes in VibeSmith not reflecting in AI tool

**Solution:**

1. **Wait 5-10 seconds** (AI tool auto-refreshes)
2. **Manual refresh:**
   - Cursor: Cmd/Ctrl + Shift + P → "Reload Window"
   - Claude Code: Restart app
3. **Check file was actually saved** (check modified date)

### AI tool changes not showing in VibeSmith

**Solution:**

1. **Manual re-scan:**
   - VibeSmith → Scan Project (Cmd/Ctrl + R)

2. **Enable auto-scan:**
   - Settings → Enable "Auto-scan on file change"

3. **Check file watcher:**
   - Settings → Advanced → "Reset file watcher"

---

## 📊 UI Issues

### Dashboard is empty

**Check:**

1. **Projects added?**
   - Click "Add Project" to scan first project

2. **Components exist?**
   - Check `~/.cursor/skills/` has files

3. **Database corrupted?**
   - Settings → Advanced → "Reset Database"
   - Warning: This will re-scan all projects

### Dependency Graph is empty

**Reasons:**

1. **No dependencies** (components don't reference each other)
2. **Scan not complete** (wait 10-30 seconds)
3. **Filter too restrictive** (clear filters)

**Solution:**
- Create a skill that references another skill
- Re-scan project
- Check "Show all" in graph filters

### Context Optimizer shows no suggestions

**This is good!** Your skills are already optimized. 🎉

**To test it:**
1. Create a large skill (> 2000 tokens)
2. Re-scan
3. Check Context Optimizer

### Search not working

**Solution:**

1. **Clear search field**
2. **Try different keywords**
3. **Check filters** (may be hiding results)
4. **Re-index search:**
   - Settings → Advanced → "Rebuild search index"

---

## ⚙️ Performance Issues

### VibeSmith is slow/laggy

**Solution:**

1. **Too many components?**
   - Disable unused skills
   - Archive old projects

2. **Large dependency graph?**
   - Filter to specific project/type
   - Use "Overview mode" for 100+ nodes

3. **Low RAM?**
   - Close other apps
   - Restart VibeSmith
   - Upgrade to 8GB+ RAM (recommended)

4. **Clear cache:**
   - Settings → Advanced → "Clear cache"

### High CPU usage

**Solution:**

1. **Disable auto-scan:**
   - Settings → Disable "Auto-scan on file change"

2. **Reduce scan frequency:**
   - Settings → Scan Interval → "Manual only"

3. **Check for infinite loops:**
   - Dependency Graph → Look for circular dependencies

---

## 🔐 Security & Privacy

### Is my data safe?

**Yes!** VibeSmith is local-first:
- All data on your machine
- No cloud sync (free tier)
- Optional cloud sync (Pro tier, encrypted)

### Can I block telemetry?

**Yes!**
1. Settings → Privacy
2. Disable "Anonymous usage analytics"
3. Disable "Crash reports"

---

## 🐛 Crashes & Errors

### VibeSmith crashes on startup

**Solution:**

1. **Check logs:**
   - macOS: `~/Library/Logs/VibeSmith/`
   - Windows: `%APPDATA%\VibeSmith\logs\`
   - Linux: `~/.local/share/vibesmith/logs/`

2. **Reset settings:**
   ```bash
   # macOS/Linux
   rm -rf ~/.config/vibesmith/
   
   # Windows
   rmdir /s %APPDATA%\VibeSmith
   ```

3. **Reinstall:**
   - Uninstall VibeSmith
   - Download latest version
   - Reinstall

4. **Report bug:**
   - [Create issue](https://github.com/aroido-bigcat/vibesmith-community/issues/new?template=1-bug_report.yml)
   - Attach log files

### "Cannot read property of undefined" error

**Solution:**
1. Settings → Advanced → "Reset Database"
2. Re-scan projects
3. If persists, report bug with logs

### Database locked error

**Solution:**
1. Close all VibeSmith instances
2. Wait 10 seconds
3. Restart VibeSmith
4. If persists:
   ```bash
   # macOS/Linux
   rm ~/.local/share/vibesmith/db.lock
   ```

---

## 🌐 Network Issues (Pro)

### Cloud sync not working

**Check:**

1. **Internet connection:**
   - Open browser, check internet
2. **Account status:**
   - Settings → Account → Check "Pro" badge
3. **Sync enabled:**
   - Settings → Sync → Enable "Auto-sync"
4. **Firewall:**
   - Allow VibeSmith through firewall

### Team collaboration not syncing

**Solution:**

1. **All team members on Pro?**
2. **Same team ID?**
   - Settings → Team → Check team ID matches
3. **Permissions:**
   - Check if you have "Write" access
4. **Manual sync:**
   - Settings → Team → "Force sync"

---

## 📱 Platform-Specific

### macOS: Homebrew installation fails

**Solution:**
```bash
# Update Homebrew
brew update

# Try again
brew install --cask vibesmith

# If fails, try direct download
# https://github.com/aroido-bigcat/vibesmith-community/releases
```

### Windows: Installation blocked by antivirus

**Solution:**
1. Add VibeSmith to antivirus whitelist
2. Temporarily disable antivirus
3. Install VibeSmith
4. Re-enable antivirus

### Linux: AppImage won't execute

**Solution:**
```bash
# Make executable
chmod +x VibeSmith-*.AppImage

# Run
./VibeSmith-*.AppImage

# Or install to system
./VibeSmith-*.AppImage --install
```

---

## 🆘 Still Need Help?

### Before asking for help:

1. ✅ Check this troubleshooting guide
2. ✅ Search [GitHub Issues](https://github.com/aroido-bigcat/vibesmith-community/issues)
3. ✅ Check [FAQ](faq.md)
4. ✅ Try [Discord search](https://discord.gg/vibesmith)

### Get support:

- 💬 **Discord** (fastest): https://discord.gg/vibesmith
- 💭 **Discussions**: https://github.com/aroido-bigcat/vibesmith-community/discussions
- 🐛 **Bug Report**: [Create Issue](https://github.com/aroido-bigcat/vibesmith-community/issues/new?template=1-bug_report.yml)
- 📧 **Email** (Pro only): support@vibesmith.com

### When reporting issues:

Include:
- VibeSmith version (`Help → About`)
- OS and version
- Steps to reproduce
- Error logs (if any)
- Screenshots

---

**Last Updated:** 2026-02-23
