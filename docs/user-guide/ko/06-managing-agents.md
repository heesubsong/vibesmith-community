# 에이전트 관리

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## 에이전트 페이지 이동

![에이전트 페이지 이동](images/agents-01-list.png)

왼쪽 사이드바의 **Components** > **Agents**를 클릭하면 모든 에이전트 목록을 볼 수 있습니다.

에이전트는 특정 작업을 자동으로 수행하는 AI 서브에이전트입니다.

## 에이전트 유형

- **Task Manager**: GitHub Projects 태스크 관리
- **Spec Writer**: 프론트엔드 스펙 작성
- **Spec Reviewer**: 스펙 리뷰 및 검증
- **Test Writer**: 자동 테스트 코드 작성
- **UI Implementer**: UI 컴포넌트 구현
- **QA Fixer**: Quality Gate 자동 수정
- **API Integrator**: API 연동 자동화
- **Daily Reporter**: 일일 보고서 생성

### 💡 유용한 팁

💡 에이전트는 복잡한 작업을 자동화하는 특수 스킬입니다.
💡 Cursor의 Task 도구를 통해 호출됩니다.
💡 각 에이전트는 독립적으로 실행되며 결과를 반환합니다.

## 새 에이전트 생성

![새 에이전트 생성](images/agents-02-new-modal.png)

**+ New Agent** 버튼을 클릭하면 에이전트 생성 모달이 나타납니다.

## 필수 입력 항목

1. **에이전트 이름**: kebab-case (예: `my-agent`)
2. **설명**: 에이전트가 수행하는 작업
3. **서브에이전트 타입**: Cursor Task 타입 선택
4. **모델**: fast, alpha, beta 등
5. **도구**: 에이전트가 사용할 도구 목록

## 서브에이전트 타입

- `generalPurpose`: 일반 작업
- `explore`: 코드베이스 탐색
- `shell`: 커맨드 실행
- `browser-use`: 브라우저 자동화

## 에이전트 상세 보기

![에이전트 상세 보기](images/agents-03-detail.png)

에이전트 카드를 클릭하면 상세 정보를 볼 수 있습니다.

## 상세 페이지

- **메타데이터**: 이름, 설명, 타입
- **설정**: 모델, 도구, 옵션
- **프롬프트**: 에이전트에게 전달되는 지시사항
- **실행 이력**: 최근 실행 기록
- **성능 지표**: 성공률, 평균 실행 시간

## 에이전트 실행

Cursor에서 에이전트를 실행하려면:

```
@task-manager 다음 작업을 추천해줘
@spec-writer 로그인 기능 스펙을 작성해줘
@test-writer UserProfile 컴포넌트 테스트 작성해줘
```

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0