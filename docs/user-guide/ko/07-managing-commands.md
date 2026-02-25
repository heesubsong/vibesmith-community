# 명령어 관리

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## 명령어란?

**명령어(Commands)**는 Cursor에서 `/`로 시작하는 슬래시 명령어입니다. 복잡한 작업을 간단한 명령어 하나로 실행할 수 있습니다.

### 명령어 vs 스킬 vs 에이전트

| 구분 | 명령어 | 스킬 | 에이전트 |
|------|--------|------|----------|
| **호출** | `/command` | `@skill` | `@agent` |
| **용도** | 빠른 액션 | 재사용 패턴 | 복잡한 워크플로우 |
| **인자** | ✅ 지원 | 제한적 | 프롬프트 기반 |
| **출력** | 즉시 | 즉시 | 다단계 보고서 |

### 명령어의 장점

- **빠른 실행**: 타이핑만으로 즉시 실행
- **인자 전달**: 파라미터로 유연한 제어
- **자동완성**: IDE에서 자동완성 지원
- **일관성**: 팀 전체가 동일한 명령어 사용

## 명령어 페이지로 이동

![명령어 페이지로 이동](images/commands-01-list.png)

왼쪽 사이드바의 **Components** > **Commands**를 클릭하면 모든 명령어 목록을 볼 수 있습니다.

## 기본 제공 명령어

### 워크플로우 명령어

#### /spec-create
**용도**: 프론트엔드 기능 스펙 생성

**사용법**:
```
/spec-create 로그인 페이지
/spec-create dashboard --issue 123
```

**생성 파일**:
- `docs/specs/login-page.md`
- Issue 연동 (선택)

#### /spec-review
**용도**: 스펙 문서 리뷰

**사용법**:
```
/spec-review docs/specs/login-page.md
```

**검증 항목**:
- ✅ 완전성
- ✅ 명확성
- ✅ 실현가능성
- ✅ 일관성

#### /auto-implement
**용도**: 스펙 기반 자동 구현

**사용법**:
```
/auto-implement docs/specs/login-page.md
/auto-implement login --test
```

**생성 파일**:
- 컴포넌트 코드
- 테스트 코드
- 스타일 파일

### API 관련 명령어

#### /request-api
**용도**: 백엔드에 API 구현 요청

**사용법**:
```
/request-api 사용자 정보 조회
/request-api POST /users --spec user-spec.md
```

**생성 결과**:
- GitHub Issue 생성
- Mock 데이터 준비
- API 인터페이스 정의

#### /integrate-api
**용도**: API 연동 코드 생성

**사용법**:
```
/integrate-api /users
/integrate-api /auth --with-msw
```

**생성 파일**:
```
src/api/
├── client.ts
├── types.ts
├── hooks/
│   └── useUser.ts
└── mocks/
    └── handlers.ts
```

### 태스크 관리 명령어

#### /task-start
**용도**: 새 작업 시작

**사용법**:
```
/task-start #123
/task-start "로그인 페이지 구현"
```

**실행 작업**:
- Issue 상태 변경
- 브랜치 생성
- 작업 로그 기록

#### /task-done
**용도**: 작업 완료

**사용법**:
```
/task-done
/task-done --commit --push
```

**실행 작업**:
- 변경사항 커밋
- PR 생성
- Issue 완료 처리

#### /daily-log
**용도**: 일일 작업 로그 생성

**사용법**:
```
/daily-log
/daily-log --yesterday
```

**생성 내용**:
- 완료된 작업
- 진행 중인 작업
- 블로킹 이슈
- 다음 계획

## 새 명령어 생성

![새 명령어 생성](images/commands-02-new-modal.png)

**+ New Command** 버튼을 클릭하면 명령어 생성 모달이 나타납니다.

### 명령어 구성 요소

#### 1. 명령어 이름
```
✅ 좋은 예시:
/create-component
/run-tests
/format-code

❌ 나쁜 예시:
/c (너무 짧음)
/createReactComponentWithTests (너무 김)
/create_component (언더스코어 사용)
```

#### 2. 설명
```markdown
명령어가 수행하는 작업을 명확하게 설명

예:
"React 함수형 컴포넌트를 생성하고 기본 테스트 파일을 추가합니다."
```

#### 3. 프롬프트
```markdown
AI에게 전달될 상세한 지시사항

예:
"""
다음 조건으로 React 컴포넌트를 생성하세요:
- 함수형 컴포넌트
- TypeScript
- Props 타입 정의 포함
- Chakra UI 스타일링
- 기본 테스트 파일 포함
"""
```

#### 4. 인자 (Arguments)
```yaml
arguments:
  - name: componentName
    type: string
    required: true
    description: "컴포넌트 이름 (PascalCase)"
    
  - name: withTest
    type: boolean
    required: false
    default: true
    description: "테스트 파일 생성 여부"
```

## 명령어 실전 예시

### 예시 1: 컴포넌트 생성 명령어

**명령어 정의**:
```yaml
name: create-component
description: "React 컴포넌트를 생성합니다"
prompt: |
  {componentName}이라는 이름의 React 함수형 컴포넌트를 생성하세요.
  - TypeScript 사용
  - Chakra UI로 스타일링
  - Props 인터페이스 정의
  {withTest ? "- Vitest 테스트 파일 포함" : ""}
```

**사용**:
```
/create-component UserProfile
/create-component LoginForm --withTest=false
```

### 예시 2: 테스트 실행 명령어

**명령어 정의**:
```yaml
name: run-tests
description: "특정 파일의 테스트를 실행합니다"
arguments:
  - name: file
    type: string
    required: false
    description: "테스트할 파일 경로"
```

**사용**:
```
/run-tests
/run-tests src/components/UserProfile.test.tsx
```

### 예시 3: 문서 생성 명령어

**명령어 정의**:
```yaml
name: generate-docs
description: "코드에서 자동으로 문서를 생성합니다"
arguments:
  - name: target
    type: string
    required: true
  - name: format
    type: enum
    values: [markdown, html, jsdoc]
    default: markdown
```

**사용**:
```
/generate-docs src/utils/
/generate-docs src/api/ --format=jsdoc
```

## 명령어 관리 팁

### 1. 네이밍 컨벤션
```
✅ 동사로 시작: create-, run-, generate-
✅ 간결하지만 명확: deploy-prod (O), dp (X)
✅ 일관성 유지: create-component, create-hook
```

### 2. 프롬프트 작성 팁
```markdown
✅ 구체적으로:
  "TypeScript로 React 함수형 컴포넌트 생성"

✅ 조건 명시:
  "Props가 있으면 인터페이스 정의"

✅ 예외 처리:
  "파일이 이미 존재하면 에러"
```

### 3. 인자 설계
```
✅ 필수 인자는 최소한으로
✅ 기본값 제공
✅ 타입 명확히 지정
✅ 설명 상세하게
```

### 4. 테스트
```bash
# 명령어 생성 후 반드시 테스트
/my-command test-arg
/my-command --help
/my-command (인자 없이)
```

### ⚠️ 주의사항

⚠️ 명령어 이름은 생성 후 변경할 수 없습니다.
⚠️ 너무 복잡한 로직은 에이전트로 분리하는 것이 좋습니다.
⚠️ 인자 검증을 반드시 포함하세요.
⚠️ 에러 메시지는 사용자 친화적으로 작성하세요.

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0
