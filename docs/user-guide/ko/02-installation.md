# 설치 가이드

> 📝 이 문서는 자동으로 생성되었습니다. 내용이 부정확하거나 누락된 부분이 있다면 [Issue](https://github.com/heesubsong/vibesmith-community/issues)로 제보해주세요.

## macOS 설치

## Homebrew를 통한 설치 (권장)

Homebrew를 사용하면 가장 쉽게 설치할 수 있습니다.

```bash
# Homebrew Tap 추가
brew tap heesubsong/vibesmith

# VibeSmith 설치
brew install --cask vibesmith
```

설치 후 애플리케이션 폴더에서 VibeSmith를 실행하세요.

## DMG 파일로 설치

1. [GitHub Releases](https://github.com/heesubsong/vibesmith/releases)에서 최신 `.dmg` 파일 다운로드
2. DMG 파일을 열기
3. VibeSmith 아이콘을 Applications 폴더로 드래그
4. Applications 폴더에서 VibeSmith 실행

## 보안 설정

macOS Gatekeeper 경고가 나타나면:

1. **시스템 환경설정** > **보안 및 개인 정보 보호** 열기
2. **일반** 탭에서 **확인 없이 열기** 클릭
3. 또는 앱 아이콘을 Control + 클릭 > **열기** 선택

### ⚠️ 주의사항

⚠️ 첫 실행 시 macOS에서 보안 경고가 나타날 수 있습니다.
⚠️ Apple Silicon (M1/M2) Mac에서도 정상 작동합니다.

## Windows 설치

## 설치 파일로 설치

1. [GitHub Releases](https://github.com/heesubsong/vibesmith/releases)에서 최신 `.exe` 파일 다운로드
2. 다운로드한 설치 파일 실행
3. 설치 마법사 지시 따라 진행
4. 설치 완료 후 시작 메뉴에서 VibeSmith 실행

## Portable 버전

설치 없이 사용하고 싶다면:

1. Portable 버전 (`.zip`) 다운로드
2. 원하는 폴더에 압축 해제
3. `VibeSmith.exe` 실행

## 권한 설정

Windows Defender SmartScreen 경고가 나타나면:

1. **추가 정보** 클릭
2. **실행** 버튼 클릭

## Linux 설치

## AppImage로 설치

1. [GitHub Releases](https://github.com/heesubsong/vibesmith/releases)에서 최신 `.AppImage` 파일 다운로드
2. 실행 권한 부여:
   ```bash
   chmod +x VibeSmith-*.AppImage
   ```
3. AppImage 실행:
   ```bash
   ./VibeSmith-*.AppImage
   ```

## .deb 패키지 (Ubuntu/Debian)

```bash
# 다운로드한 .deb 파일 설치
sudo dpkg -i vibesmith_*.deb

# 의존성 문제 해결
sudo apt-get install -f
```

## .rpm 패키지 (Fedora/RHEL)

```bash
# 다운로드한 .rpm 파일 설치
sudo rpm -i vibesmith-*.rpm
```

## 소스에서 빌드

개발자용 설치 방법입니다.

## 사전 요구사항

- **Node.js**: 18 이상
- **npm**: 8 이상
- **Python**: 3.11 이상

## 빌드 단계

```bash
# 저장소 클론
git clone https://github.com/heesubsong/vibesmith.git
cd vibesmith

# 의존성 설치
make setup

# 데스크톱 앱 빌드
make dist-desktop

# 빌드된 앱 위치:
# - macOS: packages/desktop/dist/VibeSmith.dmg
# - Windows: packages/desktop/dist/VibeSmith.exe
# - Linux: packages/desktop/dist/VibeSmith.AppImage
```

자세한 빌드 가이드는 [개발자 문서](../developer-guide/)를 참고하세요.

## 설치 확인

설치가 완료되면 다음을 확인하세요:

## 1. 앱 실행

VibeSmith를 실행하면 다음 화면이 나타나야 합니다:
- 대시보드 메인 화면
- 왼쪽 사이드바 (Navigation)
- 상단 헤더

## 2. 버전 확인

**도움말** > **VibeSmith 정보**에서 버전을 확인할 수 있습니다.

현재 최신 버전: **0.1.0**

## 3. 문제 발생 시

설치 중 문제가 발생하면:
- [문제 해결 가이드](98-troubleshooting.md)
- [GitHub Issues](https://github.com/heesubsong/vibesmith-community/issues)
- 설치 로그 확인 (앱 내 **도움말** > **로그 보기**)

### 💡 유용한 팁

💡 자동 업데이트가 활성화되어 있으면 새 버전이 자동으로 다운로드됩니다.
💡 설치 위치를 변경하고 싶다면 Portable 버전을 사용하세요.
💡 여러 버전을 동시에 설치할 수 있습니다 (테스트용).

---

**최종 업데이트**: 2026-02-25  
**버전**: 0.1.0