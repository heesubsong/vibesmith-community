# Getting Started with VibeSmith

Welcome to VibeSmith! This guide will help you install and set up VibeSmith on your system.

## 📥 Installation

### macOS

#### Option 1: Homebrew (Recommended)

```bash
# Add the VibeSmith tap
brew tap aroido-bigcat/vibesmith

# Install VibeSmith
brew install --cask vibesmith
```

#### Option 2: Direct Download

1. Download the latest `.dmg` file from [Releases](https://github.com/aroido-bigcat/vibesmith-community/releases)
2. Open the `.dmg` file
3. Drag **VibeSmith** to your Applications folder
4. Launch VibeSmith from Applications

**Note:** On first launch, you may need to allow the app in System Preferences → Security & Privacy.

### Windows

⏳ **Coming Soon!** 

[Sign up for Windows beta](https://github.com/aroido-bigcat/vibesmith-community/issues/new?template=4-beta_request.yml)

### Linux

⏳ **Coming Soon!**

[Sign up for Linux beta](https://github.com/aroido-bigcat/vibesmith-community/issues/new?template=4-beta_request.yml)

---

## 🎯 First Launch

### 1. Set Global Path

On first launch, VibeSmith will ask you to set your global AI agent path:

- **Cursor:** `~/.cursor/`
- **Claude Code:** `~/.claude/`

You can change this later in Settings.

### 2. Scan Your First Project

1. Click **"Add Project"**
2. Select your project directory
3. VibeSmith will automatically scan for:
   - Skills (`.cursor/skills/`, `.claude/skills/`)
   - Agents (`.cursor/agents/`, `.claude/agents/`)
   - Commands (`.cursor/commands/`, `.claude/commands/`)
   - Hooks (`settings.json`)
   - Rules (`.cursor/rules/`, `.claude/rules/`)

### 3. Explore the Dashboard

The dashboard shows:
- **Statistics:** Total components, active/inactive counts
- **Recent Activity:** Recently modified components
- **Quick Actions:** Create, scan, and manage components
- **Context Optimizer:** Token usage and optimization suggestions

---

## 🎓 Quick Tour (5 Minutes)

### Component List

View all your skills, agents, commands, hooks, and rules in one place.

**Features:**
- 🔍 **Search:** Find components instantly
- 🏷️ **Filter:** By type, project, tag, or status
- 📊 **Sort:** By name, date, or usage
- 🎯 **Toggle:** Enable/disable components

### Dependency Graph

Visualize relationships between components.

**Features:**
- 🔗 **See Dependencies:** Which skills depend on each other
- 🔴 **Detect Cycles:** Find circular dependencies
- ⚠️ **Broken Links:** Find missing references
- 🎯 **Filter:** By project, type, or risk

### Conflict Detection

Find duplicate or overlapping components.

**Features:**
- 🔍 **Auto-Detection:** Finds conflicts automatically
- 🌍 **Global vs Project:** Detects name collisions
- 🎯 **One-Click Fix:** Disable, rename, or delete
- 📊 **Reports:** Export conflict reports

### Context Optimizer

Reduce token usage and improve AI performance.

**Features:**
- 📈 **Token Analysis:** See which components use most tokens
- ⚠️ **Oversized Skills:** Find skills that are too large
- 🔍 **Tech Mismatches:** Python skill in React project
- 🎯 **Suggestions:** Get actionable optimization tips

---

## ⚙️ Configuration

### Settings

Access settings via **VibeSmith → Settings** (macOS) or **File → Settings** (Windows/Linux).

**Options:**
- **Global Path:** Change your global AI agent directory
- **Projects:** Manage project list
- **Theme:** Switch between light/dark mode
- **Language:** Change UI language (English/Korean)
- **Auto-Scan:** Enable/disable automatic scanning

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Cmd/Ctrl + K` | Quick Search |
| `Cmd/Ctrl + N` | Create New Component |
| `Cmd/Ctrl + R` | Rescan Project |
| `Cmd/Ctrl + ,` | Settings |
| `Cmd/Ctrl + Q` | Quit |

---

## 🆘 Need Help?

- 📚 [User Guide](user-guide.md) - Detailed feature documentation
- 🔧 [Troubleshooting](troubleshooting.md) - Common issues
- ❓ [FAQ](faq.md) - Frequently asked questions
- 💬 [Discord](https://discord.gg/vibesmith) - Community support
- 🐛 [Report Bug](https://github.com/aroido-bigcat/vibesmith-community/issues/new?template=1-bug_report.yml)

---

## 📝 Next Steps

1. ✅ Install VibeSmith
2. ✅ Scan your first project
3. 📖 Read the [User Guide](user-guide.md)
4. 🔌 Explore [Plugins](plugin-development.md)
5. 💬 Join our [Discord Community](https://discord.gg/vibesmith)

---

**Need help?** Ask in our [Discord](https://discord.gg/vibesmith) or [GitHub Discussions](https://github.com/aroido-bigcat/vibesmith-community/discussions)!
