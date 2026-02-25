# 문제 해결

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## 앱 실행 문제

## macOS에서 앱이 열리지 않음

### 증상
- "손상되어 열 수 없습니다" 오류
- Gatekeeper 경고

### 해결 방법

**방법 1: 시스템 환경설정에서 허용**
1. **시스템 환경설정** > **보안 및 개인 정보 보호**
2. **일반** 탭에서 **확인 없이 열기** 클릭

**방법 2: 터미널에서 격리 속성 제거**
```bash
xattr -cr /Applications/VibeSmith.app
```

**방법 3: Gatekeeper 임시 비활성화 (권장하지 않음)**
```bash
sudo spctl --master-disable
```

## Windows에서 앱이 실행되지 않음

### 증상
- SmartScreen 경고
- "알 수 없는 게시자" 오류

### 해결 방법

**방법 1: SmartScreen 우회**
1. 설치 파일 우클릭 > **속성**
2. **일반** 탭에서 **차단 해제** 체크
3. **확인** 클릭

**방법 2: 관리자 권한으로 실행**
1. 앱 아이콘 우클릭
2. **관리자 권한으로 실행** 선택

## Linux에서 AppImage가 실행되지 않음

### 증상
- 권한 거부 오류
- FUSE 오류

### 해결 방법

**방법 1: 실행 권한 부여**
```bash
chmod +x VibeSmith-*.AppImage
```

**방법 2: FUSE 설치**
```bash
# Ubuntu/Debian
sudo apt-get install fuse libfuse2

# Fedora
sudo dnf install fuse fuse-libs
```

**방법 3: --no-sandbox 옵션**
```bash
./VibeSmith-*.AppImage --no-sandbox
```

## 스캔 문제

## 프로젝트 스캔이 작동하지 않음

### 원인 진단

**1. 로그 확인**
- **도움말** > **로그 보기**
- 오류 메시지 확인

**2. 경로 확인**
```bash
# .cursor 디렉토리 존재 확인
ls -la .cursor/

# 권한 확인
ls -ld .cursor/
```

**3. Cursor/Claude Code 경로 확인**
- **설정** > **일반** > **AI 도구 경로**
- 올바른 경로가 설정되어 있는지 확인

### 해결 방법

**빈 스캔 결과**
```bash
# 스킬이 실제로 존재하는지 확인
find . -name "SKILL.md"

# 글로벌 스킬 확인
ls -la ~/.cursor/skills/
```

**스캔이 느림**
- 제외 경로 추가: `node_modules`, `.git`, `dist`
- 설정 > 스캔 > 제외 경로

**스캔이 멈춤**
1. 앱 재시작
2. 캐시 삭제: 설정 > 고급 > 캐시 삭제
3. 인덱스 재구축: 설정 > 고급 > 인덱스 재구축

## 변경사항이 자동으로 감지되지 않음

### 자동 스캔 활성화 확인
- 설정 > 스캔 > 자동 스캔 켜기
- 스캔 주기: 5분 권장

### 수동 재스캔
- **Cmd+R** (Mac) 또는 **Ctrl+R** (Windows)
- 또는 **파일** > **프로젝트 재스캔**

## 성능 문제

## 앱이 느려요

### 원인

- 대규모 프로젝트 (1000+ 컴포넌트)
- 자동 스캔 주기가 너무 짧음
- 메모리 부족

### 해결 방법

**1. 제외 경로 추가**
```
설정 > 스캔 > 제외 경로
- node_modules
- .git
- dist
- build
- coverage
```

**2. 스캔 주기 조정**
- 5분 → 10분 또는 15분으로 변경
- 또는 자동 스캔 끄고 수동 스캔

**3. 캐시 최적화**
- 설정 > 고급 > 캐시 최적화
- 자동 정리 활성화

**4. 데이터베이스 정리**
```bash
# 백업 후 데이터베이스 최적화
sqlite3 ~/.vibesmith/db.sqlite "VACUUM;"
```

## 메모리 사용량이 높아요

### 모니터링
- **도움말** > **시스템 정보**
- 메모리 사용량 확인

### 최적화
- 여러 프로젝트 창 닫기
- 의존성 그래프 창 닫기 (메모리 많이 사용)
- 앱 재시작

## 데이터 문제

## 데이터가 손실되었어요

### 백업 복원

**자동 백업에서 복원**
```bash
# 백업 디렉토리 확인
ls -la ~/.vibesmith/backups/

# 최신 백업 찾기
ls -lt ~/.vibesmith/backups/ | head -5

# 백업 복원
cp ~/.vibesmith/backups/db-YYYY-MM-DD.sqlite ~/.vibesmith/db.sqlite
```

**Git에서 복원 (스킬 파일)**
```bash
# 스킬 파일 복원
git checkout HEAD -- .cursor/skills/

# 특정 스킬만 복원
git checkout HEAD -- .cursor/skills/my-skill/
```

## 충돌하는 컴포넌트가 있어요

### 중복 감지
- **도구** > **중복 컴포넌트 찾기**
- 로컬 vs 글로벌 충돌 확인

### 해결 방법
1. 한쪽 삭제
2. 이름 변경
3. 우선순위 설정 (로컬 우선 vs 글로벌 우선)

## 데이터베이스 오류

### 재구축
```bash
# 기존 데이터베이스 백업
cp ~/.vibesmith/db.sqlite ~/.vibesmith/db.sqlite.bak

# 데이터베이스 삭제 (자동 재생성됨)
rm ~/.vibesmith/db.sqlite

# 앱 재시작 및 프로젝트 재스캔
```

## 추가 도움

## 로그 수집

문제를 보고할 때 다음 정보를 포함하세요:

**1. 앱 로그**
- **도움말** > **로그 보기** > **로그 내보내기**
- 위치: `~/.vibesmith/logs/app.log`

**2. 시스템 정보**
- **도움말** > **시스템 정보** > **복사**
- OS, 버전, 메모리, CPU 등

**3. 재현 단계**
- 문제가 발생한 정확한 단계
- 스크린샷 (가능한 경우)

## 커뮤니티 지원

### GitHub Issues
- 버그 리포트: [Issues](https://github.com/heesubsong/vibesmith-community/issues)
- 버그 템플릿 사용

### Discussions
- 질문: [Q&A](https://github.com/heesubsong/vibesmith-community/discussions/categories/q-a)
- 아이디어: [Ideas](https://github.com/heesubsong/vibesmith-community/discussions/categories/ideas)

### Discord (TBD)
- 실시간 채팅 지원
- 커뮤니티 도움

## 긴급 문제

앱이 완전히 작동하지 않으면:

**1. 안전 모드로 실행**
```bash
# macOS/Linux
open -a VibeSmith --args --safe-mode

# Windows
VibeSmith.exe --safe-mode
```

**2. 설정 초기화**
```bash
# 설정 백업
cp ~/.vibesmith/config.json ~/.vibesmith/config.json.bak

# 설정 삭제 (기본값으로 재설정)
rm ~/.vibesmith/config.json
```

**3. 완전 재설치**
```bash
# 모든 데이터 백업
tar -czf vibesmith-backup.tar.gz ~/.vibesmith

# 데이터 삭제
rm -rf ~/.vibesmith

# 앱 재설치
```

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0