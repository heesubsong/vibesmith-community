# Search and Filter

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## Global Search

![Global Search](images/search-01-global.png)

![Global Search Demo](gifs/search-demo.gif)

**Global Search** is a powerful tool to quickly find all components.

### Opening Search

- **Keyboard**: `Cmd+K` (Mac) / `Ctrl+K` (Windows)
- **Mouse**: Click search icon in top header
- **Menu**: View > Search

## Search Scope

### Basic Search Fields

- **Name**: Component's unique identifier
  - Example: `react-component-generator`
- **Description**: Component description
  - Example: "Auto-generate React components"
- **Tags**: Classification tags
  - Example: `code-gen`, `react`, `testing`
- **Path**: File system path
  - Example: `.cursor/skills/`, `~/.cursor/skills/`
- **Content**: Full file content
  - `SKILL.md`, `AGENT.md`, etc.

### Search Tips

```
✅ Good Examples:
"react component"     → Exact phrase search
/^test-.*$/          → Pattern matching with regex
tag:testing          → Filter by specific tag

❌ Avoid:
Single characters (a, b) → Too many results
Too generic words        → Many irrelevant results
```

## Search Modes

### 1. Fuzzy Search (Default)
**Feature**: Smart search allowing typos

**Example**:
```
Input: "recat compnent"
Result: "react component" found ✅
```

**Algorithm**: Based on Levenshtein Distance

### 2. Exact Search
**Usage**: Wrap with quotes

**Example**:
```
"react-component-generator"  → Only exact matches
"API integration"            → Entire phrase must match
```

### 3. Regex Search
**Usage**: Wrap with slashes

**Example**:
```
/^test-.*$/          → All items starting with test-
/.*-generator$/      → Items ending with -generator
/(react|vue)-.*$/    → Starting with react- or vue-
```

**Regex Reference**:
- `.` : Any single character
- `*` : 0 or more repetitions
- `+` : 1 or more repetitions
- `^` : Start
- `$` : End
- `|` : OR
- `[]` : Character class

### 4. Advanced Filter Search
**Usage**: `field:value` format

**Example**:
```
tag:testing           → Items with testing tag
path:local            → Items in local path
type:agent            → Agent type only
status:active         → Active status only
author:@username      → Specific author
```

**Combinable**:
```
tag:react type:skill status:active
→ Search only active React skills
```

## Keyboard Shortcuts

### Basic Shortcuts
- `Cmd+K` / `Ctrl+K`: Open search
- `↑` `↓`: Navigate results
- `Enter`: Open selected item
- `Cmd+Enter`: Open in new tab
- `Esc`: Close search

### Advanced Shortcuts
- `Cmd+Shift+K`: Toggle filters
- `Tab`: Next section
- `Shift+Tab`: Previous section
- `/`: Change search mode

## Advanced Filters

![Advanced Filters](images/search-02-filters.png)

Click **Filters** button to show advanced filter options.

## Filter Options

### By Type
- Skills
- Agents
- Commands
- Hooks
- Rules

### By Path
- Local (.cursor/)
- Global (~/.cursor/)

### By Tag
- Multiple tag selection available
- Select AND/OR conditions

### By Date
- Last modified
- Created date
- Last week, month, 3 months

## Sorting

- **Name**: Alphabetical order
- **Last Modified**: Newest first
- **Usage Frequency**: Most used first
- **Dependencies**: Most dependencies first

## Saved Searches

![Saved Searches](images/search-03-saved.png)

Save frequently used search criteria for quick reuse.

### Saving Searches

1. Set desired search criteria
2. Click **Save** button (⭐ icon)
3. Enter search name and description
4. **Confirm**

### Managing Saved Searches

**Load**:
- **Saved Searches** tab in search box (📚)
- Click desired search
- Apply immediately

**Edit**:
- Hover over saved search
- Click ✏️ edit icon
- Modify criteria and save

**Delete**:
- Hover over saved search
- Click 🗑️ delete icon

### Practical Saved Search Examples

#### Development Workflow
```
📌 "Today's Work"
   → Local + Last 24 hours + status:active

📌 "Need Tests"
   → tag:testing + status:pending

📌 "Awaiting Review"
   → tag:review + Last week
```

#### By Project
```
📌 "React Project"
   → tag:react + path:local

📌 "Backend Skills"
   → tag:backend + tag:api

📌 "Common Utils"
   → tag:utility + path:global
```

#### Maintenance
```
📌 "Old Skills"
   → Last modified 6+ months ago

📌 "Not Used"
   → Usage count 0

📌 "Many Dependencies"
   → Dependencies 10+
```

## Search Optimization Tips

### 1. Progressive Search
```
Step 1: Broad keyword → "component"
Step 2: Add filter    → tag:react
Step 3: Narrow scope  → path:local
```

### 2. Use Boolean Operations
```
AND: All conditions satisfied
  react component testing

OR: Any condition satisfied
  react|vue|angular

NOT: Exclude
  component -deprecated
```

### 3. Use Wildcards
```
*      : All characters
test-* : Starts with test-
*-util : Ends with -util
*core* : Contains core
```

### 4. Improve Search Speed
```
✅ Fast Search:
- Use specific keywords
- Specify fields (tag:, path:)
- Use saved searches

❌ Slow Search:
- Too generic words
- Complex regex
- Full content search
```

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0
