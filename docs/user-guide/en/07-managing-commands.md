# Managing Commands

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## What are Commands?

**Commands** are slash commands starting with `/` in Cursor. You can execute complex tasks with a single simple command.

### Commands vs Skills vs Agents

| Feature | Commands | Skills | Agents |
|---------|----------|--------|--------|
| **Invocation** | `/command` | `@skill` | `@agent` |
| **Purpose** | Quick actions | Reusable patterns | Complex workflows |
| **Arguments** | ✅ Supported | Limited | Prompt-based |
| **Output** | Immediate | Immediate | Multi-step reports |

### Advantages of Commands

- **Quick Execution**: Execute immediately with just typing
- **Argument Passing**: Flexible control with parameters
- **Auto-completion**: IDE supports auto-completion
- **Consistency**: Entire team uses the same commands

## Navigate to Commands Page

![Navigate to Commands Page](images/commands-01-list.png)

Click **Components** > **Commands** in the left sidebar to see all commands.

## Built-in Commands

### Workflow Commands

#### /spec-create
**Purpose**: Create frontend feature specification

**Usage**:
```
/spec-create login page
/spec-create dashboard --issue 123
```

**Generated Files**:
- `docs/specs/login-page.md`
- Issue integration (optional)

#### /spec-review
**Purpose**: Review spec document

**Usage**:
```
/spec-review docs/specs/login-page.md
```

**Validation Items**:
- ✅ Completeness
- ✅ Clarity
- ✅ Feasibility
- ✅ Consistency

#### /auto-implement
**Purpose**: Auto-implementation based on spec

**Usage**:
```
/auto-implement docs/specs/login-page.md
/auto-implement login --test
```

**Generated Files**:
- Component code
- Test code
- Style files

### API-Related Commands

#### /request-api
**Purpose**: Request API implementation from backend

**Usage**:
```
/request-api fetch user info
/request-api POST /users --spec user-spec.md
```

**Result**:
- GitHub Issue created
- Mock data prepared
- API interface defined

#### /integrate-api
**Purpose**: Generate API integration code

**Usage**:
```
/integrate-api /users
/integrate-api /auth --with-msw
```

**Generated Files**:
```
src/api/
├── client.ts
├── types.ts
├── hooks/
│   └── useUser.ts
└── mocks/
    └── handlers.ts
```

### Task Management Commands

#### /task-start
**Purpose**: Start new task

**Usage**:
```
/task-start #123
/task-start "Implement login page"
```

**Actions**:
- Change issue status
- Create branch
- Record work log

#### /task-done
**Purpose**: Complete task

**Usage**:
```
/task-done
/task-done --commit --push
```

**Actions**:
- Commit changes
- Create PR
- Mark issue as done

#### /daily-log
**Purpose**: Generate daily work log

**Usage**:
```
/daily-log
/daily-log --yesterday
```

**Generated Content**:
- Completed tasks
- In-progress tasks
- Blocking issues
- Next plans

## Create New Command

![Create New Command](images/commands-02-new-modal.png)

Click the **+ New Command** button to open the command creation modal.

### Command Components

#### 1. Command Name
```
✅ Good Examples:
/create-component
/run-tests
/format-code

❌ Bad Examples:
/c (too short)
/createReactComponentWithTests (too long)
/create_component (underscore usage)
```

#### 2. Description
```markdown
Clearly describe what the command does

Example:
"Creates a React functional component and adds a basic test file."
```

#### 3. Prompt
```markdown
Detailed instructions to pass to AI

Example:
"""
Create a React component with the following conditions:
- Functional component
- TypeScript
- Include Props type definition
- Chakra UI styling
- Include basic test file
"""
```

#### 4. Arguments
```yaml
arguments:
  - name: componentName
    type: string
    required: true
    description: "Component name (PascalCase)"
    
  - name: withTest
    type: boolean
    required: false
    default: true
    description: "Whether to create test file"
```

## Real-World Examples

### Example 1: Component Creation Command

**Command Definition**:
```yaml
name: create-component
description: "Creates a React component"
prompt: |
  Create a React functional component named {componentName}.
  - Use TypeScript
  - Style with Chakra UI
  - Define Props interface
  {withTest ? "- Include Vitest test file" : ""}
```

**Usage**:
```
/create-component UserProfile
/create-component LoginForm --withTest=false
```

### Example 2: Test Execution Command

**Command Definition**:
```yaml
name: run-tests
description: "Runs tests for a specific file"
arguments:
  - name: file
    type: string
    required: false
    description: "File path to test"
```

**Usage**:
```
/run-tests
/run-tests src/components/UserProfile.test.tsx
```

### Example 3: Documentation Generation Command

**Command Definition**:
```yaml
name: generate-docs
description: "Automatically generates documentation from code"
arguments:
  - name: target
    type: string
    required: true
  - name: format
    type: enum
    values: [markdown, html, jsdoc]
    default: markdown
```

**Usage**:
```
/generate-docs src/utils/
/generate-docs src/api/ --format=jsdoc
```

## Command Management Tips

### 1. Naming Convention
```
✅ Start with verb: create-, run-, generate-
✅ Concise but clear: deploy-prod (O), dp (X)
✅ Maintain consistency: create-component, create-hook
```

### 2. Prompt Writing Tips
```markdown
✅ Be specific:
  "Create React functional component with TypeScript"

✅ State conditions:
  "Define interface if Props exist"

✅ Handle exceptions:
  "Error if file already exists"
```

### 3. Argument Design
```
✅ Minimize required arguments
✅ Provide defaults
✅ Specify types clearly
✅ Describe in detail
```

### 4. Testing
```bash
# Always test after creating command
/my-command test-arg
/my-command --help
/my-command (without arguments)
```

### ⚠️ Cautions

⚠️ Command names cannot be changed after creation.
⚠️ Too complex logic should be separated into agents.
⚠️ Always include argument validation.
⚠️ Write error messages to be user-friendly.

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0
