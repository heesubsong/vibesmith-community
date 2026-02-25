# 훅 관리

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## Git 훅이란?

**Git 훅(Hooks)**은 Git 작업(커밋, 푸시 등) 시 자동으로 실행되는 스크립트입니다. 코드 품질을 자동으로 검증하고 팀의 워크플로우를 표준화할 수 있습니다.

### 훅의 필요성

| 문제 | 훅 솔루션 |
|------|-----------|
| 린트 에러가 있는 코드 커밋 | pre-commit에서 자동 검사 |
| 잘못된 커밋 메시지 형식 | commit-msg에서 검증 |
| 테스트 실패한 코드 푸시 | pre-push에서 테스트 실행 |
| 민감 정보 실수로 커밋 | pre-commit에서 스캔 |

### 훅의 장점

- **자동화**: 수동 검사 불필요
- **일관성**: 팀 전체가 동일한 규칙 적용
- **조기 발견**: 문제를 로컬에서 먼저 발견
- **품질 향상**: 자동으로 코드 품질 보장

## 훅 페이지로 이동

![훅 페이지로 이동](images/hooks-01-list.png)

왼쪽 사이드바의 **Components** > **Hooks**를 클릭하면 모든 Git 훅 목록을 볼 수 있습니다.

## Git 훅 종류

### 클라이언트 사이드 훅

#### pre-commit
**실행 시점**: 커밋 전 (Cmd+K Enter 직전)

**용도**:
- 린트 검사 (ESLint, Prettier)
- 타입 검사 (TypeScript)
- 테스트 실행 (빠른 단위 테스트)
- 민감 정보 스캔 (.env, API 키)
- 파일 크기 검사

**예시 시나리오**:
```bash
# 린트 에러가 있으면 커밋 차단
npm run lint
# TypeScript 에러가 있으면 커밋 차단
npm run type-check
# 민감 정보가 있으면 커밋 차단
git diff --cached | grep -i "api_key\|password\|secret"
```

#### commit-msg
**실행 시점**: 커밋 메시지 작성 직후

**용도**:
- 커밋 메시지 형식 검증
- Conventional Commits 규칙 검사
- Issue 번호 포함 여부 확인
- 최소 길이 검증

**예시 시나리오**:
```bash
# Conventional Commits 형식 검증
# 올바른 형식: feat(api): 사용자 API 추가
# 잘못된 형식: updated code

# Issue 번호 필수
# 올바른 형식: feat: 기능 추가 #123
# 잘못된 형식: feat: 기능 추가
```

#### pre-push
**실행 시점**: 푸시 전 (git push 직전)

**용도**:
- 전체 테스트 실행
- 빌드 검증
- 린트 전체 검사
- 보안 취약점 스캔

**예시 시나리오**:
```bash
# 모든 테스트 실행 (느려도 철저하게)
npm test
# 프로덕션 빌드 검증
npm run build
# 보안 취약점 스캔
npm audit
```

#### post-commit
**실행 시점**: 커밋 완료 직후

**용도**:
- 알림 전송
- 통계 수집
- 자동 문서 생성
- 로그 기록

**예시 시나리오**:
```bash
# Slack 알림
curl -X POST $SLACK_WEBHOOK -d "새 커밋: $(git log -1 --oneline)"
# 작업 로그 업데이트
echo "$(date): 커밋 완료" >> .work-log
```

### 서버 사이드 훅

#### pre-receive
**실행 시점**: 서버가 푸시 받기 전

**용도**:
- 브랜치 보호 규칙 검증
- 권한 검사
- 정책 강제

#### post-receive
**실행 시점**: 서버가 푸시 받은 후

**용도**:
- CI/CD 트리거
- 배포 자동화
- 알림 전송

## 새 훅 생성

![새 훅 생성](images/hooks-02-new-modal.png)

**+ New Hook** 버튼을 클릭하면 훅 생성 모달이 나타납니다.

### 훅 구성 요소

#### 1. 훅 타입 선택
```
✅ pre-commit   - 빠른 검사 (린트, 포맷)
✅ commit-msg   - 메시지 검증
✅ pre-push     - 느린 검사 (테스트, 빌드)
✅ post-commit  - 알림, 로그
```

#### 2. 스크립트 작성
```bash
#!/bin/bash

# 스크립트는 반드시 Shebang으로 시작
# 종료 코드로 성공/실패 결정:
#   0 = 성공 (작업 계속)
#   1 = 실패 (작업 중단)

exit 0  # 성공
exit 1  # 실패
```

#### 3. 실행 조건 설정
```bash
# 특정 파일만 검사
if git diff --cached --name-only | grep -q "\.tsx\?$"; then
  # TypeScript 파일이 변경되었을 때만 실행
  npm run type-check
fi

# 특정 브랜치에서만 실행
BRANCH=$(git rev-parse --abbrev-ref HEAD)
if [ "$BRANCH" = "main" ]; then
  # main 브랜치에서만 실행
  npm test
fi
```

## 훅 실전 예시

### 예시 1: 린트 + 포맷 검사 (pre-commit)

```bash
#!/bin/bash

echo "🔍 Running pre-commit checks..."

# 변경된 파일만 검사 (빠름)
FILES=$(git diff --cached --name-only --diff-filter=ACM | grep -E '\.(ts|tsx|js|jsx)$')

if [ -z "$FILES" ]; then
  echo "✅ No files to check"
  exit 0
fi

# ESLint 검사
echo "Running ESLint..."
npx eslint $FILES
if [ $? -ne 0 ]; then
  echo "❌ ESLint failed. Please fix errors."
  exit 1
fi

# Prettier 검사
echo "Running Prettier..."
npx prettier --check $FILES
if [ $? -ne 0 ]; then
  echo "❌ Prettier failed. Run 'npm run format' to fix."
  exit 1
fi

echo "✅ Pre-commit checks passed"
exit 0
```

### 예시 2: 커밋 메시지 검증 (commit-msg)

```bash
#!/bin/bash

COMMIT_MSG_FILE=$1
COMMIT_MSG=$(cat $COMMIT_MSG_FILE)

# Conventional Commits 형식 검증
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

# Issue 번호 확인
if ! echo "$COMMIT_MSG" | grep -qE "#[0-9]+"; then
  echo "⚠️  Warning: No issue number found"
  echo "Consider adding issue number: #123"
  # Warning만 표시하고 통과
fi

echo "✅ Commit message validated"
exit 0
```

### 예시 3: 테스트 실행 (pre-push)

```bash
#!/bin/bash

echo "🧪 Running tests before push..."

# 브랜치 확인
BRANCH=$(git rev-parse --abbrev-ref HEAD)
echo "Current branch: $BRANCH"

# main/develop 브랜치는 더 엄격하게
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "develop" ]; then
  echo "Protected branch detected. Running full test suite..."
  
  # 전체 테스트
  npm run test:ci
  if [ $? -ne 0 ]; then
    echo "❌ Tests failed. Cannot push to $BRANCH."
    exit 1
  fi
  
  # 빌드 검증
  npm run build
  if [ $? -ne 0 ]; then
    echo "❌ Build failed. Cannot push to $BRANCH."
    exit 1
  fi
else
  # 기능 브랜치는 빠른 테스트만
  npm run test:unit
  if [ $? -ne 0 ]; then
    echo "❌ Unit tests failed."
    exit 1
  fi
fi

echo "✅ All checks passed. Pushing..."
exit 0
```

### 예시 4: 민감 정보 스캔 (pre-commit)

```bash
#!/bin/bash

echo "🔒 Scanning for sensitive data..."

# 민감한 패턴 검색
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

# .env 파일 확인
if git diff --cached --name-only | grep -q "\.env$"; then
  echo "⚠️  Warning: .env file detected"
  echo "Make sure you're not committing secrets."
  
  # .env는 경고만 (프로젝트에 따라 커밋 허용 가능)
  read -p "Continue? (y/n) " -n 1 -r
  echo
  if [[ ! $REPLY =~ ^[Yy]$ ]]; then
    exit 1
  fi
fi

echo "✅ No sensitive data detected"
exit 0
```

## 훅 활성화/비활성화

![훅 활성화/비활성화](images/hooks-03-toggle.png)

훅 카드의 토글 스위치로 훅을 활성화하거나 비활성화할 수 있습니다.

### 활성화 vs 비활성화

| 상태 | 동작 | 사용 시나리오 |
|------|------|---------------|
| **활성화** | 자동 실행 | 정상 개발, 릴리즈 준비 |
| **비활성화** | 실행 안 함 | 빠른 프로토타입, 긴급 핫픽스 |

### 일시적 비활성화 방법

```bash
# 방법 1: UI에서 토글 (권장)
# VibeSmith에서 토글 스위치 클릭

# 방법 2: CLI로 우회
git commit --no-verify  # 모든 훅 건너뛰기
git push --no-verify    # pre-push 훅 건너뛰기

# 방법 3: 환경 변수
SKIP_HOOKS=1 git commit -m "message"
```

### ⚠️ 주의사항

⚠️ `--no-verify`는 긴급 상황에만 사용하세요.
⚠️ CI에서는 여전히 검사가 수행됩니다.
⚠️ 훅을 우회한 코드는 PR에서 거부될 수 있습니다.

## 훅 관리 베스트 프랙티스

### 1. 성능 최적화

```bash
# ❌ 나쁜 예: 모든 파일 검사
npm run lint

# ✅ 좋은 예: 변경된 파일만 검사
git diff --cached --name-only | xargs npx eslint

# ❌ 나쁜 예: 느린 E2E 테스트
npm run test:e2e  # pre-commit에서

# ✅ 좋은 예: 빠른 단위 테스트
npm run test:unit  # pre-commit
npm run test:e2e   # pre-push 또는 CI
```

### 2. 명확한 에러 메시지

```bash
# ❌ 나쁜 예
echo "Failed"
exit 1

# ✅ 좋은 예
echo "❌ ESLint failed"
echo ""
echo "Please fix the following errors:"
npx eslint --format=stylish
echo ""
echo "Run 'npm run lint:fix' to auto-fix"
exit 1
```

### 3. 점진적 적용

```bash
# 1단계: Warning만 표시
echo "⚠️  Please run 'npm run lint'"

# 2단계: 실패하지만 우회 가능
read -p "Continue anyway? (y/n) " -n 1 -r

# 3단계: 강제 적용
exit 1
```

### 4. 팀 규칙 문서화

```markdown
# .git/hooks/README.md

## 프로젝트 Git 훅

### pre-commit
- ESLint: 변경된 파일만
- Prettier: 자동 포맷 검증
- 실행 시간: ~2초

### pre-push
- Unit tests: 전체
- Build: 프로덕션 빌드
- 실행 시간: ~30초

### 우회 방법
긴급 상황에만: `git commit --no-verify`
```

## 훅 디버깅

### 훅이 실행되지 않을 때

```bash
# 1. 실행 권한 확인
ls -l .git/hooks/pre-commit
# -rwxr-xr-x (실행 권한 필요)

# 2. 실행 권한 부여
chmod +x .git/hooks/pre-commit

# 3. Shebang 확인
head -1 .git/hooks/pre-commit
# #!/bin/bash (필수)

# 4. 수동 실행 테스트
.git/hooks/pre-commit
```

### 훅 실행 로그 확인

```bash
# 디버그 모드로 실행
bash -x .git/hooks/pre-commit

# 로그 파일로 저장
.git/hooks/pre-commit 2>&1 | tee hook.log
```

### 일반적인 문제

| 문제 | 원인 | 해결 |
|------|------|------|
| 권한 거부 | 실행 권한 없음 | `chmod +x` |
| 명령어 없음 | PATH 문제 | 절대 경로 사용 |
| 느린 실행 | 전체 검사 | 변경 파일만 검사 |
| 윈도우 에러 | CRLF 라인 엔딩 | LF로 변환 |

## 훅 공유 및 배포

### Husky 사용 (권장)

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
# 훅 추가
npx husky add .husky/pre-commit "npm run lint"
npx husky add .husky/pre-push "npm test"

# Git 저장소에 포함 (.husky/ 디렉토리)
# 팀원이 npm install하면 자동 적용
```

### 수동 배포

```bash
# 훅 스크립트를 프로젝트에 포함
mkdir -p scripts/git-hooks
cp .git/hooks/pre-commit scripts/git-hooks/

# 설치 스크립트
echo '#!/bin/bash
cp scripts/git-hooks/* .git/hooks/
chmod +x .git/hooks/*
' > scripts/install-hooks.sh

# README에 안내
echo "Run \`./scripts/install-hooks.sh\` after clone" >> README.md
```

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0
