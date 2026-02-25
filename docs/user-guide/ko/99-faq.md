# 자주 묻는 질문 (FAQ)

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## 일반 질문

## VibeSmith는 무료인가요?

네, VibeSmith는 개인 및 상업적 용도로 무료로 사용할 수 있습니다.

## Cursor와 Claude Code 차이는 무엇인가요?

- **Cursor**: VS Code 기반 IDE, 상업용
- **Claude Code**: Claude AI 전용 에디터

VibeSmith는 두 도구 모두 지원합니다.

## 프로젝트별 vs 글로벌 스킬의 차이는?

- **프로젝트별 (로컬)**: `.cursor/skills/` - 현재 프로젝트에만 적용
- **글로벌**: `~/.cursor/skills/` - 모든 프로젝트에 적용

## 데이터는 어디에 저장되나요?

모든 데이터는 로컬에 저장됩니다:
- 스킬 파일: `.cursor/`, `~/.cursor/`
- 데이터베이스: `~/.vibesmith/db.sqlite`
- 설정: `~/.vibesmith/config.json`

외부로 전송되는 데이터는 없습니다.

## 여러 프로젝트를 동시에 관리할 수 있나요?

네, VibeSmith는 여러 프로젝트를 동시에 열 수 있습니다.
각 프로젝트는 별도의 창에서 관리됩니다.

## 사용 방법

## 스킬을 어떻게 공유하나요?

### 방법 1: 파일 복사
```bash
# 스킬 폴더 복사
cp -r .cursor/skills/my-skill /path/to/other/project/.cursor/skills/
```

### 방법 2: Git으로 관리
스킬을 Git 저장소에 포함시켜 팀과 공유

### 방법 3: 글로벌 스킬 사용
`~/.cursor/skills/`에 두면 모든 프로젝트에서 사용 가능

## 의존성 그래프는 어떻게 해석하나요?

- **노드**: 각 컴포넌트
- **간선**: 의존 관계
- **색상**: 컴포넌트 타입
- **크기**: 의존성 개수

클릭하면 상세 정보를 볼 수 있습니다.

## 검색이 느려요. 어떻게 하나요?

1. **재스캔**: Cmd+R (Mac) 또는 Ctrl+R (Windows)
2. **인덱스 재구축**: 설정 > 고급 > 인덱스 재구축
3. **제외 경로 추가**: 불필요한 디렉토리 제외

## 백업은 어떻게 하나요?

### 자동 백업
- 설정 > 일반 > 자동 백업 켜기
- 백업 위치: `~/.vibesmith/backups/`

### 수동 백업
```bash
# 프로젝트 스킬 백업
cp -r .cursor/skills ./skills-backup

# 글로벌 스킬 백업
cp -r ~/.cursor/skills ~/skills-backup
```

## 문제 해결

## 앱이 실행되지 않아요

### macOS
- Gatekeeper 설정 확인
- 콘솔 앱에서 로그 확인

### Windows
- Windows Defender 예외 추가
- 관리자 권한으로 실행

### Linux
- AppImage 실행 권한 확인
- 라이브러리 의존성 확인

## 스캔이 작동하지 않아요

1. Cursor/Claude Code 경로 확인
2. `.cursor/` 디렉토리 권한 확인
3. 로그 파일 확인: 도움말 > 로그 보기

## 변경사항이 반영되지 않아요

- **수동 재스캔**: Cmd+R / Ctrl+R
- **자동 스캔 확인**: 설정 > 스캔 > 자동 스캔
- **캐시 삭제**: 설정 > 고급 > 캐시 삭제

## 더 많은 도움이 필요하면?

- [문제 해결 가이드](98-troubleshooting.md)
- [GitHub Issues](https://github.com/heesubsong/vibesmith-community/issues)
- [Discussions](https://github.com/heesubsong/vibesmith-community/discussions)

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0