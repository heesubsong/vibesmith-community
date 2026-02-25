# Managing Rules

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## Navigate to Rules Page

![Navigate to Rules Page](images/rules-01-list.png)

Click **Components** > **Rules** in the left sidebar to see all project rules.

Rules are guidelines that AI agents must follow when writing code.

## Rule Types

- **Coding Style**: Naming, formatting, structure
- **Architecture**: Package structure, dependency rules
- **Security**: Security guidelines
- **Performance**: Optimization guidelines
- **Testing**: Test writing rules
- **Documentation**: Documentation rules

### 💡 Useful Tips

💡 Rules make AI automatically follow team coding conventions.
💡 You can apply rules to specific files using file patterns.
💡 You can emphasize important rules by setting priorities.

## Create New Rule

![Create New Rule](images/rules-02-new-modal.png)

Click the **+ New Rule** button to open the rule creation modal.

## Writing Rules

1. **Rule Name**: Clear name (e.g., `react-conventions`)
2. **Description**: Scope where rule applies
3. **Content**: Specific guidelines
4. **File Pattern**: Files to apply (globs)

## Example: React Component Rules

```markdown
# React Conventions

## File Structure
- Components in PascalCase
- Hooks as useXxx
- Utils in camelCase

## Props
- children as last prop
- Use ? for optional props

## Styling
- Prefer Chakra UI components
- Avoid inline styles
```

## Rule Priority

![Rule Priority](images/rules-03-priority.png)

You can set priority for rules.

## Priority Levels

- **High**: Important rules that always apply
- **Medium**: General rules
- **Low**: Recommendations

## Conflict Resolution

When multiple rules conflict:
1. Higher priority rules take precedence
2. More specific rules take precedence (file pattern)
3. Local rules take precedence over global rules

## File Patterns

```
**/*.tsx          # All TSX files
src/components/** # Entire components directory
**/*.test.ts      # All test files
```

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0