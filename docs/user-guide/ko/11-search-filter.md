# 검색 및 필터

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## 전역 검색

![전역 검색](images/search-01-global.png)

![전역 검색 데모](gifs/search-demo.gif)

**전역 검색(Global Search)**은 모든 컴포넌트를 빠르게 찾을 수 있는 강력한 도구입니다.

### 검색 열기

- **키보드**: `Cmd+K` (Mac) / `Ctrl+K` (Windows)
- **마우스**: 상단 헤더의 검색 아이콘 클릭
- **메뉴**: View > Search

## 검색 범위

### 기본 검색 필드

- **이름** (Name): 컴포넌트의 고유 식별자
  - 예: `react-component-generator`
- **설명** (Description): 컴포넌트 설명
  - 예: "React 컴포넌트를 자동 생성"
- **태그** (Tags): 분류 태그
  - 예: `code-gen`, `react`, `testing`
- **경로** (Path): 파일 시스템 경로
  - 예: `.cursor/skills/`, `~/.cursor/skills/`
- **내용** (Content): 파일 전체 내용
  - `SKILL.md`, `AGENT.md` 등

### 검색 팁

```
✅ 좋은 예시:
"react component"     → 정확한 구문 검색
/^test-.*$/          → 정규식으로 패턴 매칭
tag:testing          → 특정 태그로 필터링

❌ 피해야 할 것:
단일 문자 (a, b)     → 너무 많은 결과
너무 일반적인 단어     → 관련 없는 결과 다수
```

## 검색 모드

### 1. 퍼지 검색 (기본)
**특징**: 오타를 허용하는 스마트 검색

**예시**:
```
입력: "recat compnent"
결과: "react component" 찾음 ✅
```

**알고리즘**: Levenshtein Distance 기반

### 2. 정확한 검색
**사용법**: 따옴표로 감싸기

**예시**:
```
"react-component-generator"  → 정확히 일치하는 항목만
"API integration"            → 구문 전체가 일치해야 함
```

### 3. 정규식 검색
**사용법**: 슬래시로 감싸기

**예시**:
```
/^test-.*$/          → test-로 시작하는 모든 항목
/.*-generator$/      → -generator로 끝나는 항목
/(react|vue)-.*$/    → react- 또는 vue-로 시작
```

**정규식 참고**:
- `.` : 임의의 문자 1개
- `*` : 0개 이상 반복
- `+` : 1개 이상 반복
- `^` : 시작
- `$` : 끝
- `|` : OR
- `[]` : 문자 클래스

### 4. 고급 필터 검색
**사용법**: `필드:값` 형식

**예시**:
```
tag:testing           → testing 태그가 있는 항목
path:local            → 로컬 경로의 항목
type:agent            → 에이전트 타입만
status:active         → 활성 상태만
author:@username      → 특정 작성자
```

**조합 가능**:
```
tag:react type:skill status:active
→ React 관련 활성 스킬만 검색
```

## 키보드 단축키

### 기본 단축키
- `Cmd+K` / `Ctrl+K`: 검색 열기
- `↑` `↓`: 결과 탐색
- `Enter`: 선택한 항목 열기
- `Cmd+Enter`: 새 탭에서 열기
- `Esc`: 검색 닫기

### 고급 단축키
- `Cmd+Shift+K`: 필터 토글
- `Tab`: 다음 섹션
- `Shift+Tab`: 이전 섹션
- `/`: 검색 모드 변경

## 고급 필터

![고급 필터](images/search-02-filters.png)

**필터** 버튼을 클릭하면 고급 필터 옵션이 나타납니다.

## 필터 옵션

### 타입별 필터
- Skills
- Agents
- Commands
- Hooks
- Rules

### 경로별 필터
- 로컬 (.cursor/)
- 글로벌 (~/.cursor/)

### 태그별 필터
- 여러 태그 선택 가능
- AND/OR 조건 선택

### 날짜별 필터
- 최근 수정일
- 생성일
- 최근 1주일, 1개월, 3개월

## 정렬

- **이름**: 알파벳 순
- **최근 수정**: 최신순
- **사용 빈도**: 많이 사용된 순
- **의존성**: 의존성 많은 순

## 저장된 검색

![저장된 검색](images/search-03-saved.png)

자주 사용하는 검색 조건을 저장하여 빠르게 재사용할 수 있습니다.

### 검색 저장하기

1. 원하는 검색 조건 설정
2. **저장** 버튼 클릭 (⭐ 아이콘)
3. 검색 이름 및 설명 입력
4. **확인**

### 저장된 검색 관리

**불러오기**:
- 검색창의 **저장된 검색** 탭 (📚)
- 원하는 검색 클릭
- 즉시 적용

**편집**:
- 저장된 검색 위에 호버
- ✏️ 편집 아이콘 클릭
- 조건 수정 후 저장

**삭제**:
- 저장된 검색 위에 호버
- 🗑️ 삭제 아이콘 클릭

### 실용적인 저장 검색 예시

#### 개발 워크플로우
```
📌 "오늘 작업"
   → 로컬 + 최근 24시간 + status:active

📌 "테스트 필요"
   → tag:testing + status:pending

📌 "리뷰 대기"
   → tag:review + 최근 1주일
```

#### 프로젝트별
```
📌 "React 프로젝트"
   → tag:react + path:local

📌 "백엔드 스킬"
   → tag:backend + tag:api

📌 "공통 유틸"
   → tag:utility + path:global
```

#### 유지보수
```
📌 "오래된 스킬"
   → 최근 수정 6개월 이상

📌 "사용 안 함"
   → 사용 횟수 0회

📌 "의존성 많음"
   → 의존성 10개 이상
```

## 검색 최적화 팁

### 1. 점진적 검색
```
Step 1: 광범위한 키워드 → "component"
Step 2: 필터 추가        → tag:react
Step 3: 범위 좁히기      → path:local
```

### 2. 부울 연산 활용
```
AND: 모든 조건 만족
  react component testing

OR: 하나라도 만족
  react|vue|angular

NOT: 제외
  component -deprecated
```

### 3. 와일드카드 사용
```
*      : 모든 문자
test-* : test-로 시작
*-util : -util로 끝남
*core* : core 포함
```

### 4. 검색 속도 향상
```
✅ 빠른 검색:
- 구체적인 키워드 사용
- 필드 지정 (tag:, path:)
- 저장된 검색 활용

❌ 느린 검색:
- 너무 일반적인 단어
- 복잡한 정규식
- 전체 내용 검색
```

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0
