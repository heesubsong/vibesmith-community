# Frequently Asked Questions (FAQ)

## General Questions

### What is VibeSmith?

VibeSmith is an **AI Agent Components Manager** for Cursor and Claude Code. It helps you manage, organize, and optimize your skills, agents, commands, hooks, and rules in one unified dashboard.

### Is VibeSmith free?

Yes! VibeSmith has a **free tier** that includes:
- Unlimited skills/agents/commands management
- Up to 3 projects
- Dependency graph (up to 100 nodes)
- Conflict detection
- Basic context optimizer

**Pro tier** ($9.99/month) adds:
- Unlimited projects
- Unlimited dependency graph nodes
- Team collaboration (10 members)
- Cloud sync
- AI recommendations
- Priority support

### Does VibeSmith require an internet connection?

**No!** VibeSmith works **100% offline** for the free tier. All your data stays on your local machine.

Pro features (cloud sync, team collaboration) require internet.

### Is my data secure?

**Yes!** VibeSmith is **local-first**:
- All data stored on your machine
- No data sent to our servers (free tier)
- Pro cloud sync is optional and encrypted

---

## Installation & Setup

### Where does VibeSmith install?

- **macOS:** `/Applications/VibeSmith.app`
- **Windows:** `C:\Program Files\VibeSmith`
- **Linux:** `/opt/vibesmith` or `~/.local/share/vibesmith`

### Can I use VibeSmith with both Cursor and Claude Code?

**Yes!** VibeSmith supports both:
- Set global path to `~/.cursor/` or `~/.claude/`
- Switch between them in Settings
- Pro tier: Sync between both tools

### Do I need to restart my AI tool after using VibeSmith?

**No!** VibeSmith makes changes directly to your skill files. Your AI tool (Cursor/Claude Code) will pick up changes automatically.

---

## Features

### What is the Dependency Graph?

The Dependency Graph visualizes relationships between your components:
- Which skills depend on each other
- Circular dependencies (infinite loops)
- Broken references (missing skills)

**Example:** Skill A → imports → Skill B → imports → Skill C

### What is Conflict Detection?

Conflict Detection finds duplicate or overlapping components:
- **Global vs Project:** Same skill name in both locations
- **Cross-Project:** Same skill in multiple projects
- **Naming Conflicts:** Similar names causing confusion

**Example:** You have a `git-commit` skill in both `~/.cursor/skills/` and `~/my-project/.cursor/skills/`.

### What is the Context Optimizer?

Context Optimizer helps reduce token usage:
- **Oversized Skills:** Skills > 2000 tokens
- **Tech Mismatches:** Python skill in React project
- **Unused Globals:** Skills enabled but never used
- **Duplicates:** Multiple skills doing the same thing

**Result:** Save 30-50% on tokens!

### What is Smart Toggle?

Smart Toggle lets you enable/disable components without deleting them:
- **Per-Project:** Enable different skills for each project
- **Bulk Operations:** Enable/disable multiple skills at once
- **Instant:** No file system changes needed

---

## Troubleshooting

### VibeSmith won't start on macOS

**Solution:**
1. Right-click VibeSmith in Applications
2. Select "Open"
3. Click "Open" in the security dialog
4. Go to System Preferences → Security & Privacy → Allow VibeSmith

### Scan is not finding my skills

**Check:**
1. Global path is correct (Settings → Global Path)
2. Skills are in the right directory:
   - Cursor: `~/.cursor/skills/`
   - Claude Code: `~/.claude/skills/`
3. Skills follow the correct format (SKILL.md)

### Components are not showing in AI tool

**Solution:**
1. Restart your AI tool (Cursor/Claude Code)
2. Check if components are enabled (green toggle)
3. Re-scan project (Cmd/Ctrl + R)

### Dependency Graph is empty

**Reasons:**
1. No components have dependencies yet
2. Components don't reference each other
3. Scan hasn't completed (wait 10-30 seconds)

### Context Optimizer shows no suggestions

**This is good!** It means your skills are already optimized. 🎉

---

## Billing & Pricing

### How do I upgrade to Pro?

1. Go to Settings → Account
2. Click "Upgrade to Pro"
3. Enter payment details
4. Start using Pro features immediately

### Can I cancel anytime?

**Yes!** Cancel anytime, no questions asked. You'll keep Pro features until the end of your billing period.

### Do you offer refunds?

Yes! Full refund within **30 days** of purchase, no questions asked.

### Is there a student/nonprofit discount?

Yes! Email us at support@vibesmith.com with proof of student/nonprofit status for **50% off Pro**.

---

## Team & Collaboration

### How does team collaboration work? (Pro)

Pro tier includes:
- **Shared Skills:** Team library of approved skills
- **Sync:** Auto-sync skills across team members
- **Permissions:** Read/Write access control
- **Activity:** See who made changes

### Can free users share skills?

Yes! Use the **Export/Import** feature:
1. Select skill → Export → Save `.json` file
2. Share file with teammate
3. Teammate: Import → Select `.json` file

---

## Technical

### What data does VibeSmith collect?

**Free tier:** Zero data collection. Everything stays local.

**Pro tier (optional):**
- Email (for account)
- Usage analytics (anonymous)
- Crash reports (anonymous, opt-in)

We **never** collect:
- Your skill contents
- Project names/paths
- Personal information

### Can I use VibeSmith in a corporate environment?

**Yes!** VibeSmith is perfect for teams:
- **Local-first:** No data leaves your network (free tier)
- **Pro tier:** Optional cloud sync (encrypted)
- **Enterprise:** Contact us for custom deployment

### Does VibeSmith work with custom AI tools?

Not yet, but we're working on it! Currently supports:
- Cursor
- Claude Code

**Coming Soon:**
- GitHub Copilot
- Tabnine
- Custom tools (via plugin API)

---

## Plugin & Customization

### Can I create custom plugins?

**Yes!** See [Plugin Development Guide](plugin-development.md).

### Can I customize the UI?

**Yes!** See [Theme Development Guide](theme-development.md).

### Where can I find community plugins?

Check out [plugins/](../plugins/) for examples.

---

## Still Have Questions?

- 💬 [Discord Community](https://discord.gg/vibesmith) - Real-time chat
- 💭 [GitHub Discussions](https://github.com/aroido-bigcat/vibesmith-community/discussions) - Q&A
- 📧 [Email Support](mailto:support@vibesmith.com) - Pro users only
- 🐛 [Report Bug](https://github.com/aroido-bigcat/vibesmith-community/issues/new?template=1-bug_report.yml)

---

**Last Updated:** 2026-02-23
