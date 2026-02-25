# 규칙 관리

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## 규칙이란?

**규칙(Rules)**은 AI 에이전트가 코드를 작성하거나 리뷰할 때 따라야 할 지침입니다. 팀의 코딩 컨벤션을 AI가 자동으로 학습하고 적용하게 만듭니다.

### 규칙의 필요성

| 문제 | 규칙 솔루션 |
|------|-----------|
| AI가 팀 스타일과 다른 코드 생성 | 규칙으로 스타일 가이드 제공 |
| 매번 동일한 피드백 반복 | 규칙으로 자동 적용 |
| 보안 취약점 패턴 반복 | 보안 규칙으로 사전 차단 |
| 성능 안티패턴 사용 | 성능 규칙으로 최적화 유도 |

### 규칙의 장점

- **일관성**: 팀 전체가 동일한 패턴 사용
- **자동화**: 리뷰 시간 단축
- **교육**: 신입 개발자에게 베스트 프랙티스 전달
- **예방**: 문제를 사전에 차단

## 규칙 페이지로 이동

![규칙 페이지로 이동](images/rules-01-list.png)

왼쪽 사이드바의 **Components** > **Rules**를 클릭하면 모든 프로젝트 규칙을 볼 수 있습니다.

## 규칙 유형

### 1. 코딩 스타일 규칙

#### 네이밍 규칙
```markdown
# Naming Conventions

## 파일명
- 컴포넌트: PascalCase (UserProfile.tsx)
- 훅: camelCase, use 접두사 (useAuth.ts)
- 유틸: camelCase (formatDate.ts)
- 타입: PascalCase (User.types.ts)
- 상수: UPPER_SNAKE_CASE (API_BASE_URL)

## 변수명
- boolean: is/has 접두사 (isLoading, hasError)
- 함수: 동사로 시작 (getUserData, handleClick)
- 이벤트 핸들러: handle/on 접두사 (handleSubmit, onClose)
```

#### 포맷 규칙
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

### 2. 아키텍처 규칙

#### 패키지 구조 규칙
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

#### 컴포넌트 구조 규칙
```markdown
# Component Structure

## File Organization
```typescript
// 1. Imports (외부 → 내부)
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

### 3. 보안 규칙

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

### 4. 성능 규칙

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

### 5. 테스트 규칙

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

### 6. 문서화 규칙

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

## 새 규칙 생성

![새 규칙 생성](images/rules-02-new-modal.png)

**+ New Rule** 버튼을 클릭하면 규칙 생성 모달이 나타납니다.

### 규칙 작성 가이드

#### 1. 규칙 이름
```
✅ 좋은 예시:
react-conventions
typescript-best-practices
security-checklist

❌ 나쁜 예시:
rules (너무 일반적)
my-rule (의미 없음)
RULES_V2 (버전 명시 불필요)
```

#### 2. 설명 (Description)
```markdown
명확하고 구체적으로 작성

예:
"React 컴포넌트 작성 시 따라야 할 코딩 컨벤션과 베스트 프랙티스입니다. 
파일 구조, 네이밍, 타입 정의, 에러 처리 등을 포함합니다."
```

#### 3. 내용 (Content)
```markdown
# 규칙 제목

## 섹션 1
- 구체적인 지침
- 예시 코드 (Good/Bad)
- 이유 설명

## 섹션 2
...
```

#### 4. 파일 패턴 (Globs)
```bash
# TypeScript 파일만
**/*.ts
**/*.tsx

# 특정 디렉토리만
src/components/**
src/features/**

# 테스트 파일만
**/*.test.ts
**/*.spec.ts

# 제외 패턴 (! 접두사)
**/*.ts
!**/*.test.ts  # 테스트 파일 제외
```

## 규칙 우선순위

![규칙 우선순위](images/rules-03-priority.png)

규칙에는 우선순위를 설정할 수 있습니다.

### 우선순위 레벨

#### High (높음)
**용도**: 절대 위반하면 안 되는 규칙

**예시**:
- 보안 규칙 (API 키 노출 금지)
- 크리티컬 버그 패턴 금지
- 팀 필수 컨벤션

**AI 동작**:
- 항상 우선 적용
- 위반 시 경고 메시지
- 자동 수정 제안

#### Medium (중간)
**용도**: 권장하는 베스트 프랙티스

**예시**:
- 성능 최적화 패턴
- 코드 가독성 규칙
- 테스트 작성 가이드

**AI 동작**:
- 일반적으로 적용
- 상황에 따라 유연하게

#### Low (낮음)
**용도**: 선택적 권장 사항

**예시**:
- 코드 스타일 선호
- 주석 작성 스타일
- 파일 구조 제안

**AI 동작**:
- 참고 사항으로 활용
- 다른 규칙과 충돌 시 무시 가능

### 충돌 시 우선순위 결정

```
1. 우선순위 (High > Medium > Low)
2. 구체성 (구체적 패턴 > 일반적 패턴)
3. 범위 (로컬 > 글로벌)
4. 최신성 (최근 생성 > 오래된 규칙)
```

**예시 시나리오**:
```
상황: src/components/Button.tsx 편집

적용 가능한 규칙:
- [High] security-rules            (**/*.tsx)
- [High] react-conventions          (src/components/**)
- [Medium] performance-optimization (**/*.tsx)
- [Low] code-style-guide            (**/*.*)

결과:
1. security-rules (High + 일치)
2. react-conventions (High + 더 구체적)
3. performance-optimization (Medium)
4. code-style-guide (Low)
```

## 규칙 관리 팁

### 1. 규칙 분리 전략

```markdown
# ❌ 나쁜 예: 하나의 거대한 규칙
all-project-rules.md (500 lines)

# ✅ 좋은 예: 주제별 분리
- react-conventions.md
- security-checklist.md
- performance-guide.md
- testing-standards.md
```

**이유**:
- AI가 관련 규칙만 참조 가능
- 유지보수 용이
- 패턴 매칭 정확도 향상

### 2. 구체적인 예시 포함

```markdown
# ❌ 나쁜 예: 추상적 지침
"컴포넌트는 단순하게 작성하세요"

# ✅ 좋은 예: 구체적 예시
"컴포넌트는 200줄 이하로 유지하세요. 
200줄 초과 시 하위 컴포넌트로 분리하세요.

예시:
```typescript
// ❌ Bad: 300 lines
export const Dashboard = () => {
  // 너무 많은 로직...
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

### 3. 버전 관리

```markdown
# 규칙 파일 헤더
# React Conventions

**버전**: 2.1.0
**최종 업데이트**: 2026-02-25
**변경 이력**:
- 2.1.0: React 18 지원 추가
- 2.0.0: TypeScript 필수 변경
- 1.0.0: 초기 버전

---

## 규칙 내용
...
```

### 4. 주기적 리뷰

```markdown
## 규칙 리뷰 체크리스트

매 분기마다:
- [ ] 더 이상 유효하지 않은 규칙 제거
- [ ] 반복되는 리뷰 피드백을 규칙으로 추가
- [ ] 새로운 기술 스택 반영
- [ ] 팀원 피드백 수렴
- [ ] 예시 코드 업데이트
```

## 고급 규칙 패턴

### 조건부 규칙

```markdown
# Conditional Security Rules

## Production 환경
```typescript
if (import.meta.env.MODE === 'production') {
  // ✅ 반드시 HTTPS 사용
  // ✅ 디버그 로그 비활성화
  // ✅ Source map 제거
}
```

## Development 환경
```typescript
if (import.meta.env.MODE === 'development') {
  // ✅ Hot reload 활성화
  // ✅ 상세한 에러 메시지
  // ✅ React DevTools 사용
}
```
```

### 점진적 규칙 적용

```markdown
# Migration Strategy

## Phase 1 (현재): Warning
새 코드에만 적용, 기존 코드는 경고만 표시

## Phase 2 (2주 후): Enforce for new files
새 파일은 반드시 규칙 준수

## Phase 3 (1개월 후): Full enforcement
모든 코드에 규칙 적용
```

### 예외 처리

```markdown
# Exception Handling

## 규칙 예외 허용

특정 상황에서 규칙을 따르지 않아도 되는 경우:

```typescript
// eslint-disable-next-line @typescript-eslint/no-explicit-any
const legacyData: any = await fetchLegacyAPI();
```

**예외 허용 조건**:
1. 명확한 이유 주석 필수
2. PR에서 리뷰 승인 필요
3. 가능한 빨리 리팩토링 계획 수립
```

## 규칙 테스트

### 규칙 검증 방법

```bash
# 1. AI에게 직접 테스트
"React 컴포넌트를 생성해줘. UserProfile이라는 이름으로."

# 기대 결과:
- ✅ react-conventions 규칙 적용
- ✅ 파일명 PascalCase
- ✅ TypeScript 사용
- ✅ Props 타입 정의

# 2. 규칙 위반 코드 제공
"이 코드를 리뷰해줘"
```typescript
// 규칙 위반 코드 예시
const userprofile = () => {  // 잘못된 네이밍
  return <div>test</div>
}
```

# 기대 결과:
- ❌ 네이밍 규칙 위반 지적
- ✅ 올바른 패턴 제안
```

### 규칙 효과 측정

```markdown
## 규칙 적용 전/후 비교

### 적용 전 (Before)
- 코드 리뷰 시간: 평균 2시간
- 반복 피드백: 파일명, 네이밍, 구조
- 신입 온보딩: 2주

### 적용 후 (After)
- 코드 리뷰 시간: 평균 30분 (75% 감소)
- 반복 피드백: 거의 없음
- 신입 온보딩: 3일 (AI가 규칙 학습)
```

## 규칙 공유 및 재사용

### 팀 규칙 템플릿

```bash
# 프로젝트 저장소에 템플릿 관리
rules/templates/
├── react-conventions.md
├── security-checklist.md
├── performance-guide.md
└── testing-standards.md

# 새 프로젝트 시작 시
cp rules/templates/* .cursor/rules/
```

### 커뮤니티 규칙

```markdown
## 인기 규칙 저장소

- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)
- [React Best Practices](https://github.com/facebook/react/wiki/Best-Practices)

이런 가이드를 VibeSmith 규칙으로 변환하여 사용
```

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0
