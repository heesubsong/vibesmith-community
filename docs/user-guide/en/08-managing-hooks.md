# Managing Hooks

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## What are Git Hooks?

**Git Hooks** are scripts that run automatically during Git operations (commit, push, etc.). They can automatically verify code quality and standardize team workflows.

### Why Hooks are Needed

| Problem | Hook Solution |
|---------|---------------|
| Committing code with lint errors | Automatic check in pre-commit |
| Wrong commit message format | Validation in commit-msg |
| Pushing code with failing tests | Run tests in pre-push |
| Accidentally committing sensitive info | Scan in pre-commit |

### Advantages of Hooks

- **Automation**: No manual checking needed
- **Consistency**: Same rules applied across team
- **Early Detection**: Find issues locally first
- **Quality Improvement**: Automatically ensure code quality

## Navigate to Hooks Page

![Navigate to Hooks Page](images/hooks-01-list.png)

Click **Components** > **Hooks** in the left sidebar to see all Git hooks.

## Types of Git Hooks

### Client-Side Hooks

#### pre-commit
**Execution Time**: Before commit (just before Cmd+K Enter)

**Use Cases**:
- Lint check (ESLint, Prettier)
- Type check (TypeScript)
- Run tests (fast unit tests)
- Scan sensitive data (.env, API keys)
- File size check

**Example Scenario**:
```bash
# Block commit if lint errors exist
npm run lint
# Block commit if TypeScript errors exist
npm run type-check
# Block commit if sensitive info exists
git diff --cached | grep -i "api_key\|password\|secret"
```

#### commit-msg
**Execution Time**: Right after writing commit message

**Use Cases**:
- Commit message format validation
- Conventional Commits rule check
- Verify issue number inclusion
- Minimum length validation

**Example Scenario**:
```bash
# Conventional Commits format validation
# Correct: feat(api): add user API
# Wrong: updated code

# Issue number required
# Correct: feat: add feature #123
# Wrong: feat: add feature
```

#### pre-push
**Execution Time**: Before push (just before git push)

**Use Cases**:
- Run full test suite
- Build verification
- Full lint check
- Security vulnerability scan

**Example Scenario**:
```bash
# Run all tests (thorough even if slow)
npm test
# Verify production build
npm run build
# Scan security vulnerabilities
npm audit
```

#### post-commit
**Execution Time**: Right after commit completes

**Use Cases**:
- Send notifications
- Collect statistics
- Auto-generate documentation
- Record logs

**Example Scenario**:
```bash
# Slack notification
curl -X POST $SLACK_WEBHOOK -d "New commit: $(git log -1 --oneline)"
# Update work log
echo "$(date): Commit completed" >> .work-log
```

### Server-Side Hooks

#### pre-receive
**Execution Time**: Before server receives push

**Use Cases**:
- Verify branch protection rules
- Permission check
- Enforce policies

#### post-receive
**Execution Time**: After server receives push

**Use Cases**:
- Trigger CI/CD
- Automate deployment
- Send notifications

## Create New Hook

![Create New Hook](images/hooks-02-new-modal.png)

Click the **+ New Hook** button to open hook creation modal.

### Hook Components

#### 1. Select Hook Type
```
✅ pre-commit   - Quick checks (lint, format)
✅ commit-msg   - Message validation
✅ pre-push     - Slow checks (tests, build)
✅ post-commit  - Notifications, logs
```

#### 2. Write Script
```bash
#!/bin/bash

# Script must start with Shebang
# Exit code determines success/failure:
#   0 = success (continue)
#   1 = failure (abort)

exit 0  # success
exit 1  # failure
```

#### 3. Set Execution Conditions
```bash
# Check only specific files
if git diff --cached --name-only | grep -q "\.tsx\?$"; then
  # Execute only when TypeScript files changed
  npm run type-check
fi

# Execute only on specific branches
BRANCH=$(git rev-parse --abbrev-ref HEAD)
if [ "$BRANCH" = "main" ]; then
  # Execute only on main branch
  npm test
fi
```

## Real-World Examples

### Example 1: Lint + Format Check (pre-commit)

```bash
#!/bin/bash

echo "🔍 Running pre-commit checks..."

# Check only changed files (fast)
FILES=$(git diff --cached --name-only --diff-filter=ACM | grep -E '\.(ts|tsx|js|jsx)$')

if [ -z "$FILES" ]; then
  echo "✅ No files to check"
  exit 0
fi

# ESLint check
echo "Running ESLint..."
npx eslint $FILES
if [ $? -ne 0 ]; then
  echo "❌ ESLint failed. Please fix errors."
  exit 1
fi

# Prettier check
echo "Running Prettier..."
npx prettier --check $FILES
if [ $? -ne 0 ]; then
  echo "❌ Prettier failed. Run 'npm run format' to fix."
  exit 1
fi

echo "✅ Pre-commit checks passed"
exit 0
```

### Example 2: Commit Message Validation (commit-msg)

```bash
#!/bin/bash

COMMIT_MSG_FILE=$1
COMMIT_MSG=$(cat $COMMIT_MSG_FILE)

# Conventional Commits format validation
PATTERN="^(feat|fix|docs|style|refactor|test|chore)(\(.+\))?: .{1,50}"

if ! echo "$COMMIT_MSG" | grep -qE "$PATTERN"; then
  echo "❌ Invalid commit message format"
  echo ""
  echo "Expected format:"
  echo "  type(scope): subject"
  echo ""
  echo "Examples:"
  echo "  feat(api): add user endpoint"
  echo "  fix(ui): resolve button click issue"
  echo "  docs: update README"
  exit 1
fi

# Check for issue number
if ! echo "$COMMIT_MSG" | grep -qE "#[0-9]+"; then
  echo "⚠️  Warning: No issue number found"
  echo "Consider adding issue number: #123"
  # Only warning, pass through
fi

echo "✅ Commit message validated"
exit 0
```

### Example 3: Run Tests (pre-push)

```bash
#!/bin/bash

echo "🧪 Running tests before push..."

# Check branch
BRANCH=$(git rev-parse --abbrev-ref HEAD)
echo "Current branch: $BRANCH"

# Stricter for main/develop branches
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "develop" ]; then
  echo "Protected branch detected. Running full test suite..."
  
  # Full tests
  npm run test:ci
  if [ $? -ne 0 ]; then
    echo "❌ Tests failed. Cannot push to $BRANCH."
    exit 1
  fi
  
  # Verify build
  npm run build
  if [ $? -ne 0 ]; then
    echo "❌ Build failed. Cannot push to $BRANCH."
    exit 1
  fi
else
  # Only fast tests for feature branches
  npm run test:unit
  if [ $? -ne 0 ]; then
    echo "❌ Unit tests failed."
    exit 1
  fi
fi

echo "✅ All checks passed. Pushing..."
exit 0
```

### Example 4: Sensitive Data Scan (pre-commit)

```bash
#!/bin/bash

echo "🔒 Scanning for sensitive data..."

# Search for sensitive patterns
SENSITIVE_PATTERNS=(
  "api[_-]?key"
  "secret[_-]?key"
  "password"
  "private[_-]?key"
  "access[_-]?token"
  "bearer"
  "-----BEGIN.*PRIVATE KEY-----"
)

for pattern in "${SENSITIVE_PATTERNS[@]}"; do
  if git diff --cached | grep -iE "$pattern"; then
    echo "❌ Potential sensitive data detected: $pattern"
    echo "Please remove sensitive information before committing."
    exit 1
  fi
done

# Check .env file
if git diff --cached --name-only | grep -q "\.env$"; then
  echo "⚠️  Warning: .env file detected"
  echo "Make sure you're not committing secrets."
  
  # .env warning only (may allow commit depending on project)
  read -p "Continue? (y/n) " -n 1 -r
  echo
  if [[ ! $REPLY =~ ^[Yy]$ ]]; then
    exit 1
  fi
fi

echo "✅ No sensitive data detected"
exit 0
```

## Enable/Disable Hooks

![Enable/Disable Hooks](images/hooks-03-toggle.png)

Toggle hooks on/off with the toggle switch on hook cards.

### Enabled vs Disabled

| State | Action | Use Case |
|-------|--------|----------|
| **Enabled** | Auto-execute | Normal development, release prep |
| **Disabled** | Don't execute | Quick prototypes, emergency hotfix |

### Temporary Disable Methods

```bash
# Method 1: Toggle in UI (recommended)
# Click toggle switch in VibeSmith

# Method 2: Bypass via CLI
git commit --no-verify  # Skip all hooks
git push --no-verify    # Skip pre-push hook

# Method 3: Environment variable
SKIP_HOOKS=1 git commit -m "message"
```

### ⚠️ Cautions

⚠️ Use `--no-verify` only in emergencies.
⚠️ CI will still perform checks.
⚠️ Code bypassing hooks may be rejected in PR.

## Hook Management Best Practices

### 1. Performance Optimization

```bash
# ❌ Bad: Check all files
npm run lint

# ✅ Good: Check only changed files
git diff --cached --name-only | xargs npx eslint

# ❌ Bad: Slow E2E tests
npm run test:e2e  # in pre-commit

# ✅ Good: Fast unit tests
npm run test:unit  # in pre-commit
npm run test:e2e   # in pre-push or CI
```

### 2. Clear Error Messages

```bash
# ❌ Bad
echo "Failed"
exit 1

# ✅ Good
echo "❌ ESLint failed"
echo ""
echo "Please fix the following errors:"
npx eslint --format=stylish
echo ""
echo "Run 'npm run lint:fix' to auto-fix"
exit 1
```

### 3. Gradual Adoption

```bash
# Step 1: Warning only
echo "⚠️  Please run 'npm run lint'"

# Step 2: Fail but bypassable
read -p "Continue anyway? (y/n) " -n 1 -r

# Step 3: Enforce
exit 1
```

### 4. Document Team Rules

```markdown
# .git/hooks/README.md

## Project Git Hooks

### pre-commit
- ESLint: Changed files only
- Prettier: Auto-format verification
- Execution time: ~2 seconds

### pre-push
- Unit tests: Full suite
- Build: Production build
- Execution time: ~30 seconds

### Bypass Method
Emergency only: `git commit --no-verify`
```

## Debugging Hooks

### When Hooks Don't Execute

```bash
# 1. Check execution permissions
ls -l .git/hooks/pre-commit
# -rwxr-xr-x (execution permission required)

# 2. Grant execution permission
chmod +x .git/hooks/pre-commit

# 3. Verify Shebang
head -1 .git/hooks/pre-commit
# #!/bin/bash (required)

# 4. Manual execution test
.git/hooks/pre-commit
```

### Check Hook Execution Logs

```bash
# Run in debug mode
bash -x .git/hooks/pre-commit

# Save to log file
.git/hooks/pre-commit 2>&1 | tee hook.log
```

### Common Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| Permission denied | No execution permission | `chmod +x` |
| Command not found | PATH issue | Use absolute path |
| Slow execution | Checking all files | Check changed files only |
| Windows error | CRLF line ending | Convert to LF |

## Hook Sharing and Deployment

### Using Husky (Recommended)

```json
// package.json
{
  "scripts": {
    "prepare": "husky install"
  },
  "devDependencies": {
    "husky": "^8.0.0"
  }
}
```

```bash
# Add hooks
npx husky add .husky/pre-commit "npm run lint"
npx husky add .husky/pre-push "npm test"

# Include in Git repository (.husky/ directory)
# Team members get hooks automatically with npm install
```

### Manual Deployment

```bash
# Include hook scripts in project
mkdir -p scripts/git-hooks
cp .git/hooks/pre-commit scripts/git-hooks/

# Installation script
echo '#!/bin/bash
cp scripts/git-hooks/* .git/hooks/
chmod +x .git/hooks/*
' > scripts/install-hooks.sh

# Add to README
echo "Run \`./scripts/install-hooks.sh\` after clone" >> README.md
```

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0
