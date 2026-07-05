# Roboseasy Studio v0.5.1-0.0.1

## 빠른 설치

### Windows 10/11 (64-bit)

1. [roboseasy-studio-setup_v0.5.1_v0.0.1_win64.exe](https://github.com/roboseasy/roboseasy-studio-deploy/releases/download/v0.5.1-0.0.1/roboseasy-studio-setup_v0.5.1_v0.0.1_win64.exe) 다운로드 (~38 MB)
2. 더블클릭 → SmartScreen "추가 정보" → "실행"
3. Inno Setup 마법사 진행 (5~30분, 인터넷 연결 필수)

설치 가이드: [install_ko.md](https://github.com/roboseasy/roboseasy-studio-deploy/blob/main/install_ko.md)

### Ubuntu 24.04+ (.deb)

```bash
wget https://github.com/roboseasy/roboseasy-studio-deploy/releases/download/v0.5.1-0.0.1/roboseasy-studio_0.5.1-0.0.1_amd64.deb
sudo apt install ./roboseasy-studio_0.5.1-0.0.1_amd64.deb
```

설치 가이드: [install_ko.md](https://github.com/roboseasy/roboseasy-studio-deploy/blob/main/install_ko.md)

## 변경 사항

- 첫 릴리즈
- Linux .deb (정통 Debian 패키징, 설치 시 venv + pip install)
- Windows 인스톨러 (Inno Setup, Python 자동 설치 + venv + pip install + 위저드 안 진행 표시)

### Linux .deb 업데이트 (2026-06-14)

- EEF ↔ 텔레오퍼레이션 속도 분리 (Goal_Velocity decouple — EEF 속도 설정이 텔레오퍼레이션 추종을 느리게 하던 문제 해결)
- EEF 관절 제어 UI 개선 (관절 grid 스크롤 + 현재 직교좌표 한 줄 표시)
- EEF·텔레오퍼레이션 연결 버튼을 캘리브레이션식 "🔌 연결" 단일 토글로 통합
- Supabase 로그인 B안(Edge Function) 이관 — 약관 1회 동의 후 반복 안 함, 앱/.deb 에 키 미포함

### Windows 인스톨러 업데이트 (2026-07-05)

- **설치 중 오류가 나도 설치 창을 닫을 수 있도록 수정** (진행 표시를 비동기 타이머 방식으로 재구조화 — 이전에는 설치가 멈추면 창이 응답하지 않던 문제)
- 순정 Windows(파이썬 미설치) 설치 시 Microsoft Store python 스텁 오탐으로 설치가 중단되던 문제 수정
- USB 시리얼 넘버 기반 포트 자동 매핑 (재부팅/재연결로 COM 번호가 바뀌어도 팔을 올바르게 인식)
- 텔레옵/데이터수집/추론/캘리브레이션의 포트 재연결 안정화 (Windows 포트 핸들 해제 지연 방어)

## 시스템 요구사항

| 항목 | Windows | Linux |
|------|---------|-------|
| OS | Windows 10/11 (64-bit) | Ubuntu 24.04 LTS |
| Python | 3.10+ (없으면 인스톨러가 자동 설치) | 3.12+ |
| 인터넷 | 첫 설치 시 필수 (lerobot/torch 1~2GB 다운로드) | 동일 |
| 디스크 | ~5GB | ~5GB |

## 무결성 검증

### Windows (PowerShell)

```powershell
Get-FileHash roboseasy-studio-setup_v0.5.1_v0.0.1_win64.exe -Algorithm SHA256
```

### Linux

```bash
sha256sum -c roboseasy-studio_0.5.1-0.0.1_amd64.deb.sha256
```

### 체크섬

- `.deb` SHA256: `04f85282a046461a5d938be202bdc4b530e5148754bf3cf41718d1733ad67f94`
- `.exe` SHA256: `5adca3c7f9eb32447de67ee2f75f20c54ff3e12945912e81a8e5bf85756ea429`
