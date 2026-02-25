# Managing Skills

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## What are Skills?

**Skills** are reusable command sets that enable AI agents to perform specific tasks.

### Advantages of Skills

- **Reusability**: Write once, use across multiple projects
- **Consistency**: Entire team works with same patterns
- **Automation**: Automate repetitive tasks
- **Sharing**: Share best practices with community

### Skill Usage Examples

#### 1. Code Generation Skill
```
@react-component-generator
  - Component name: UserProfile
  - Type: Functional
  - Styling: Chakra UI
```

#### 2. Refactoring Skill
```
@code-refactoring
  - Target: legacy/user-service.ts
  - Pattern: Class → Functional
  - Include tests: true
```

#### 3. Documentation Skill
```
@auto-documentation
  - Target: src/utils/
  - Language: English + Korean
  - Format: JSDoc
```

## Navigate to Skills Page

![Navigate to Skills Page](images/skills-01-list.png)

Click **Skills** menu in the left sidebar to view all skills.

### Skill List Information

Each skill card displays:

- **Name**: Unique identifier (kebab-case)
- **Description**: Brief explanation of what the skill does
- **Tags**: Category and purpose classification
  - `code-gen`: Code generation
  - `refactoring`: Refactoring
  - `testing`: Testing
  - `docs`: Documentation
  - `analysis`: Analysis
- **Path**: 
  - 🏠 **Local**: Apply to current project only
  - 🌍 **Global**: Apply to all projects
- **Status**:
  - ✅ **Active**: Currently available
  - ⏸️ **Inactive**: Temporarily disabled
- **Recent Use**: Last invocation time
- **Usage Count**: Total invocation count

### List View Options

- **Card View**: Visually rich card format (default)
- **List View**: Concise list format
- **Grid View**: View more skills at once

### 💡 Useful Tips

💡 Use search box to quickly find desired skills.
💡 Click tags to filter skills by that tag.
💡 List can be sorted by name, last modified, usage frequency, or category.
💡 Set favorites (⭐) for quick access to frequently used skills.

## Search for Skills

![Search for Skills](images/skills-02-search.png)

![Search for Skills Demo](gifs/skills-search-demo.gif)

Type keywords in the search box to filter skills in real-time.

Search capabilities:
- **Name search**: Search within skill names
- **Description search**: Search within descriptions
- **Tag search**: Search within tags
- **Fuzzy search**: Smart search allowing typos

## Create New Skill

![Create New Skill](images/skills-03-new-modal.png)

Click the **+ New Skill** button in the top right to open skill creation modal.

Items to configure in modal:
1. **Skill Name** (required)
2. **Description** (required)
3. **Type** selection (Skill, Agent, Command, Hook, Rule)
4. **Path** selection (local/global)
5. **Tags** addition (optional)

### ⚠️ Cautions

⚠️ Skill names must be in kebab-case. (e.g., `my-awesome-skill`)
⚠️ Names cannot be changed after creation, so enter carefully.
⚠️ Global skills are used in all projects, so caution is needed.

## Enter Skill Information

![Enter Skill Information](images/skills-04-form-filled.png)

Fill in each field in order:

### 1. Skill Name
- Enter in kebab-case format
- Example: `my-awesome-skill`, `react-component-generator`
- No spaces or special characters

### 2. Description
- Clearly describe what the skill does
- Example: "Skill that automatically generates React components"

### 3. Type Selection
- **Skill**: General AI skill
- **Agent**: Automated agent
- **Command**: Slash command
- **Hook**: Git hook
- **Rule**: Project rule

### 4. Path Selection
- **Local**: Apply to current project only
- **Global**: Apply to all projects

### 💡 Useful Tips

💡 Write description in detail as it's important for later searches.
💡 Adding tags makes finding related skills easier.

## Skill Creation Complete

![Skill Creation Complete](images/skills-05-created.png)

Click the **Create** button to create the skill.

After creation:
- New skill appears in skill list
- Automatically navigate to skill detail page
- Skill file created in file system

File Location:
- **Local**: `.cursor/skills/{skill-name}/SKILL.md`
- **Global**: `~/.cursor/skills/{skill-name}/SKILL.md`

### 📝 Note

📝 Created skill files are immediately available in Cursor AI.
📝 You can also directly edit skill files.

## View Skill Details

![View Skill Details](images/skills-06-detail.png)

Click skill card to view detailed information.

Information available on detail page:
- Skill metadata (name, description, tags)
- Skill content (SKILL.md)
- Usage statistics
- Related dependencies
- Recent modification history

Possible actions:
- ✏️ **Edit**: Modify skill content
- 📋 **Copy**: Copy to another project
- 🗑️ **Delete**: Delete skill
- 🔄 **Sync**: Synchronize local ↔ global

## Edit Skill

![Edit Skill](images/skills-07-edit.png)

Click **Edit** button to modify skill content.

Edit modes:
- **Visual Editor**: Form-based editing
- **Markdown Editor**: Direct markdown editing
- **Live Preview**: Immediately confirm changes

Click **Save** button after editing to save changes.

### 💡 Useful Tips

💡 Quickly save with Cmd+S (Mac) or Ctrl+S (Windows).
💡 View format help with Cmd+/ in markdown editor.

## Delete Skill

![Delete Skill](images/skills-08-delete-confirm.png)

Click **Delete** button to show confirmation dialog.

When deleting:
- Skill file completely removed from file system
- Cannot be recovered, so choose carefully
- Deleting global skill affects all projects

Click **Delete** button after confirmation to complete deletion.

### ⚠️ Cautions

⚠️ Deleted skills cannot be recovered.
⚠️ Deleting global skills removes them from all projects.
⚠️ Consider deactivating instead.

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0
