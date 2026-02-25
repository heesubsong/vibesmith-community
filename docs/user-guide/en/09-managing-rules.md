# Managing Rules

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## What are Rules?

**Rules** are guidelines that AI agents should follow when writing or reviewing code. They make AI automatically learn and apply your team's coding conventions.

### Why Rules are Needed

| Problem | Rule Solution |
|---------|---------------|
| AI generates code with different team style | Provide style guide through rules |
| Repeating same feedback | Automatically apply through rules |
| Recurring security vulnerability patterns | Prevent in advance with security rules |
| Using performance anti-patterns | Guide optimization with performance rules |

### Advantages of Rules

- **Consistency**: Entire team uses same patterns
- **Automation**: Reduce review time
- **Education**: Transfer best practices to new developers
- **Prevention**: Block issues in advance

## Navigate to Rules Page

![Navigate to Rules Page](images/rules-01-list.png)

Click **Components** > **Rules** in the left sidebar to see all project rules.

## Rule Types

### 1. Coding Style Rules

#### Naming Rules
```markdown
# Naming Conventions

## File Names
- Components: PascalCase (UserProfile.tsx)
- Hooks: camelCase, use prefix (useAuth.ts)
- Utils: camelCase (formatDate.ts)
- Types: PascalCase (User.types.ts)
- Constants: UPPER_SNAKE_CASE (API_BASE_URL)

## Variable Names
- boolean: is/has prefix (isLoading, hasError)
- Functions: start with verb (getUserData, handleClick)
- Event handlers: handle/on prefix (handleSubmit, onClose)
```

#### Format Rules
```markdown
# Formatting Rules

## Indentation
- 2 spaces (no tabs)

## Quotes
- Single quotes for strings
- Double quotes for JSX attributes

## Semicolons
- Always use semicolons

## Line Length
- Max 100 characters
- Break long chains into multiple lines
```

### 2. Architecture Rules

#### Package Structure Rules
```markdown
# Package Structure

## Directory Structure
```
src/
├── features/        # Feature modules
│   └── auth/
│       ├── components/
│       ├── hooks/
│       ├── api/
│       └── types/
├── shared/          # Shared utilities
│   ├── components/
│   ├── hooks/
│   └── utils/
└── api/             # API client
```

## Dependency Rules
- Features cannot import from other features
- Only shared/ can be imported globally
- No circular dependencies
```

#### Component Structure Rules
```markdown
# Component Structure

## File Organization
```typescript
// 1. Imports (external → internal)
import React from 'react';
import { Box, Button } from '@chakra-ui/react';
import { useAuth } from '@/hooks/useAuth';

// 2. Types
interface UserProfileProps {
  userId: string;
}

// 3. Component
export const UserProfile: React.FC<UserProfileProps> = ({ userId }) => {
  // 3-1. Hooks
  const auth = useAuth();
  
  // 3-2. State
  const [loading, setLoading] = useState(false);
  
  // 3-3. Effects
  useEffect(() => {}, []);
  
  // 3-4. Handlers
  const handleClick = () => {};
  
  // 3-5. Render
  return <Box>...</Box>;
};

// 4. Styled Components (if any)
// 5. Helper functions (if any)
```
```

### 3. Security Rules

```markdown
# Security Rules

## API Keys
❌ NEVER hardcode API keys
✅ Use environment variables

```typescript
// ❌ Bad
const API_KEY = 'sk_live_1234567890';

// ✅ Good
const API_KEY = import.meta.env.VITE_API_KEY;
```

## Authentication
✅ Always validate tokens on the server
✅ Use HttpOnly cookies for sensitive tokens
❌ Never store tokens in localStorage

## Input Validation
✅ Validate all user inputs
✅ Sanitize HTML content
✅ Use parameterized queries

## Dependencies
✅ Regularly update dependencies
✅ Audit with `npm audit`
✅ Pin major versions
```

### 4. Performance Rules

```markdown
# Performance Rules

## React Optimization
```typescript
// ✅ Memoize expensive computations
const filtered = useMemo(() => 
  data.filter(item => item.active), 
  [data]
);

// ✅ Memoize callbacks
const handleClick = useCallback(() => {
  // ...
}, [deps]);

// ✅ Code splitting
const Dashboard = lazy(() => import('./Dashboard'));

// ❌ Don't inline object/array props
// Bad
<Component style={{ margin: 10 }} />

// Good
const style = { margin: 10 };
<Component style={style} />
```

## Bundle Size
- Lazy load routes
- Tree-shake unused code
- Compress images
- Use dynamic imports

## API Calls
- Use React Query for caching
- Debounce search inputs
- Implement pagination
- Cancel pending requests
```

### 5. Testing Rules

```markdown
# Testing Rules

## Coverage Requirements
- Unit tests: 80% coverage
- Critical paths: 100% coverage
- New features: Tests required

## Test Structure
```typescript
describe('UserProfile', () => {
  // 1. Setup
  beforeEach(() => {
    // ...
  });
  
  // 2. Happy path
  it('should render user data', () => {
    // ...
  });
  
  // 3. Edge cases
  it('should handle loading state', () => {
    // ...
  });
  
  // 4. Error cases
  it('should display error message', () => {
    // ...
  });
  
  // 5. Cleanup
  afterEach(() => {
    // ...
  });
});
```

## Best Practices
- Test behavior, not implementation
- Use data-testid for selectors
- Mock external dependencies
- Test accessibility
```

### 6. Documentation Rules

```markdown
# Documentation Rules

## Code Comments
```typescript
// ✅ Good: Explain WHY
// Using debounce to reduce API calls from search input
const debouncedSearch = useDebouncedValue(query, 300);

// ❌ Bad: Explain WHAT (obvious from code)
// Set loading to true
setLoading(true);

// ✅ Complex logic needs explanation
// Calculate compound interest using A = P(1 + r/n)^(nt)
const interest = principal * Math.pow(1 + rate / frequency, frequency * years);
```

## JSDoc
```typescript
/**
 * Fetches user data from the API
 * @param userId - The unique identifier of the user
 * @returns A promise that resolves to the user data
 * @throws {NotFoundError} If the user doesn't exist
 * @example
 * const user = await fetchUser('123');
 */
async function fetchUser(userId: string): Promise<User> {
  // ...
}
```

## README
- Every feature folder needs README.md
- Document setup steps
- Include usage examples
- List dependencies
```

## Create New Rule

![Create New Rule](images/rules-02-new-modal.png)

Click the **+ New Rule** button to open rule creation modal.

### Rule Writing Guide

#### 1. Rule Name
```
✅ Good Examples:
react-conventions
typescript-best-practices
security-checklist

❌ Bad Examples:
rules (too generic)
my-rule (meaningless)
RULES_V2 (version not needed)
```

#### 2. Description
```markdown
Write clearly and specifically

Example:
"Coding conventions and best practices to follow when writing React components. 
Includes file structure, naming, type definitions, error handling, etc."
```

#### 3. Content
```markdown
# Rule Title

## Section 1
- Specific guidelines
- Example code (Good/Bad)
- Reason explanation

## Section 2
...
```

#### 4. File Patterns (Globs)
```bash
# TypeScript files only
**/*.ts
**/*.tsx

# Specific directory only
src/components/**
src/features/**

# Test files only
**/*.test.ts
**/*.spec.ts

# Exclude pattern (! prefix)
**/*.ts
!**/*.test.ts  # Exclude test files
```

## Rule Priority

![Rule Priority](images/rules-03-priority.png)

Rules can have priority settings.

### Priority Levels

#### High
**Purpose**: Rules that must never be violated

**Examples**:
- Security rules (no API key exposure)
- Critical bug pattern prohibition
- Essential team conventions

**AI Behavior**:
- Always apply first
- Warning message on violation
- Suggest auto-fix

#### Medium
**Purpose**: Recommended best practices

**Examples**:
- Performance optimization patterns
- Code readability rules
- Test writing guidelines

**AI Behavior**:
- Generally applied
- Flexible depending on situation

#### Low
**Purpose**: Optional recommendations

**Examples**:
- Code style preferences
- Comment writing style
- File structure suggestions

**AI Behavior**:
- Used as reference
- Can be ignored when conflicting with other rules

### Priority Resolution on Conflict

```
1. Priority (High > Medium > Low)
2. Specificity (Specific pattern > Generic pattern)
3. Scope (Local > Global)
4. Recency (Recently created > Older rules)
```

**Example Scenario**:
```
Situation: Editing src/components/Button.tsx

Applicable rules:
- [High] security-rules            (**/*.tsx)
- [High] react-conventions          (src/components/**)
- [Medium] performance-optimization (**/*.tsx)
- [Low] code-style-guide            (**/*.*)

Result:
1. security-rules (High + match)
2. react-conventions (High + more specific)
3. performance-optimization (Medium)
4. code-style-guide (Low)
```

## Rule Management Tips

### 1. Rule Separation Strategy

```markdown
# ❌ Bad: One huge rule
all-project-rules.md (500 lines)

# ✅ Good: Separate by topic
- react-conventions.md
- security-checklist.md
- performance-guide.md
- testing-standards.md
```

**Reasons**:
- AI can reference only relevant rules
- Easier maintenance
- Better pattern matching accuracy

### 2. Include Specific Examples

```markdown
# ❌ Bad: Abstract guidelines
"Write components simply"

# ✅ Good: Specific examples
"Keep components under 200 lines. 
Split into sub-components if exceeding 200 lines.

Example:
```typescript
// ❌ Bad: 300 lines
export const Dashboard = () => {
  // Too much logic...
};

// ✅ Good: Split into sub-components
export const Dashboard = () => {
  return (
    <>
      <DashboardHeader />
      <DashboardContent />
      <DashboardFooter />
    </>
  );
};
```
```

### 3. Version Control

```markdown
# Rule file header
# React Conventions

**Version**: 2.1.0
**Last Updated**: 2026-02-25
**Changelog**:
- 2.1.0: Added React 18 support
- 2.0.0: Made TypeScript mandatory
- 1.0.0: Initial version

---

## Rule Content
...
```

### 4. Periodic Review

```markdown
## Rule Review Checklist

Every quarter:
- [ ] Remove rules no longer valid
- [ ] Add recurring review feedback as rules
- [ ] Reflect new tech stack
- [ ] Collect team member feedback
- [ ] Update example code
```

## Advanced Rule Patterns

### Conditional Rules

```markdown
# Conditional Security Rules

## Production Environment
```typescript
if (import.meta.env.MODE === 'production') {
  // ✅ Must use HTTPS
  // ✅ Disable debug logs
  // ✅ Remove source maps
}
```

## Development Environment
```typescript
if (import.meta.env.MODE === 'development') {
  // ✅ Enable hot reload
  // ✅ Detailed error messages
  // ✅ Use React DevTools
}
```
```

### Gradual Rule Application

```markdown
# Migration Strategy

## Phase 1 (Current): Warning
Apply to new code only, show warning for existing code

## Phase 2 (After 2 weeks): Enforce for new files
New files must comply with rules

## Phase 3 (After 1 month): Full enforcement
Apply rules to all code
```

### Exception Handling

```markdown
# Exception Handling

## Allow Rule Exceptions

Cases where rules need not be followed:

```typescript
// eslint-disable-next-line @typescript-eslint/no-explicit-any
const legacyData: any = await fetchLegacyAPI();
```

**Exception Requirements**:
1. Clear reason comment required
2. PR review approval needed
3. Plan refactoring as soon as possible
```

## Rule Testing

### Rule Verification Methods

```bash
# 1. Test directly with AI
"Create a React component. Name it UserProfile."

# Expected result:
- ✅ react-conventions rule applied
- ✅ File name in PascalCase
- ✅ TypeScript used
- ✅ Props type defined

# 2. Provide rule-violating code
"Review this code"
```typescript
// Rule-violating code example
const userprofile = () => {  // Wrong naming
  return <div>test</div>
}
```

# Expected result:
- ❌ Point out naming rule violation
- ✅ Suggest correct pattern
```

### Measure Rule Effectiveness

```markdown
## Before/After Rule Application Comparison

### Before
- Code review time: Average 2 hours
- Repeated feedback: File names, naming, structure
- New hire onboarding: 2 weeks

### After
- Code review time: Average 30 minutes (75% reduction)
- Repeated feedback: Almost none
- New hire onboarding: 3 days (AI learns rules)
```

## Rule Sharing and Reuse

### Team Rule Templates

```bash
# Manage templates in project repository
rules/templates/
├── react-conventions.md
├── security-checklist.md
├── performance-guide.md
└── testing-standards.md

# When starting new project
cp rules/templates/* .cursor/rules/
```

### Community Rules

```markdown
## Popular Rule Repositories

- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)
- [React Best Practices](https://github.com/facebook/react/wiki/Best-Practices)

Convert these guides into VibeSmith rules for use
```

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0
