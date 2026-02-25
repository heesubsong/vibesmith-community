# 명령어 관리

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## 명령어 페이지 이동

![명령어 페이지 이동](images/commands-01-list.png)

왼쪽 사이드바의 **Components** > **Commands**를 클릭하면 모든 명령어 목록을 볼 수 있습니다.

명령어는 Cursor에서 `/`로 시작하는 슬래시 명령어입니다.

## 명령어 종류

- **/spec-create**: 프론트엔드 스펙 생성
- **/spec-review**: 스펙 리뷰
- **/auto-implement**: 자동 구현
- **/request-api**: API 구현 요청
- **/task-start**: 작업 시작
- **/task-done**: 작업 완료
- **/daily-log**: 일일 작업 로그

## 새 명령어 생성

![새 명령어 생성](images/commands-02-new-modal.png)

**+ New Command** 버튼을 클릭하면 명령어 생성 모달이 나타납니다.

## 명령어 구성

1. **명령어 이름**: 슬래시 없이 입력 (예: `my-command`)
2. **설명**: 명령어가 수행하는 작업
3. **프롬프트**: AI에게 전달될 지시사항
4. **인자**: 명령어가 받을 파라미터

## 사용 예시

명령어 생성 후 Cursor에서:

```
/my-command arg1 arg2
```

### 💡 유용한 팁

💡 명령어 이름은 짧고 기억하기 쉽게 작성하세요.
💡 프롬프트는 명확하고 구체적으로 작성하세요.
💡 자주 사용하는 작업을 명령어로 만들면 효율적입니다.

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0