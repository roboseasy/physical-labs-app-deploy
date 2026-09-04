# Physical Labs 설치 가이드

> Ubuntu 24.04 LTS 사용자용 한국어 설치/실행 가이드

## 1. 소개

Physical Labs 는 Feetech STS3215 서보 모터 ID 셋업과 LeRobot SO-ARM 101 로봇팔 운용을 위한 데스크탑 GUI 도구입니다. CLI/Python 환경 지식 없이 바로 사용할 수 있도록 설계됐습니다.

## 2. 시스템 요구사항

| 항목 | 요구 |
|---|---|
| 운영체제 | **Ubuntu 24.04 LTS** (Python 3.12 기본 포함) |
| 인터넷 | 첫 설치 시 필수 (lerobot/torch 등 1~2GB 다운로드) |
| 디스크 공간 | 약 5GB (가상환경 포함) |
| 권한 | 설치 시 sudo 필요. 모터 USB 사용 시 dialout 그룹 |

> ⚠️ Ubuntu 22.04 는 미지원입니다. lerobot 0.6.0 이 Python ≥3.12 를 요구하는데 22.04 의 기본 python 은 3.10 입니다.

## 3. 다운로드

[GitHub Releases 페이지](https://github.com/roboseasy/physical-labs-app-deploy/releases) 에서 최신 `.deb` 파일을 받습니다. 또는 명령으로:

```bash
# 최신 release 의 파일명을 확인 후 (예: v0.5.1-0.0.1)
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.10/physical-labs_0.6.0-0.0.10_amd64.deb
```

### 무결성 검증 (선택)

```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.10/physical-labs_0.6.0-0.0.10_amd64.deb.sha256
sha256sum -c physical-labs_0.6.0-0.0.10_amd64.deb.sha256
# OK 출력 확인
```

## 4. 설치

```bash
sudo apt install ./physical-labs_0.6.0-0.0.10_amd64.deb
```

> ⚠️ **`sudo dpkg -i` 가 아니라 `sudo apt install` 을 쓰세요.**
> 구 패키지 `roboseasy-studio` 와 `Conflicts` 관계라 `dpkg -i` 는 거부됩니다.
> `apt` 를 쓰면 구 패키지 제거까지 한 번에 처리됩니다.

설치 단계에서 다음이 일어납니다:
1. apt 가 시스템 의존성(`python3-venv`, `libxcb-cursor0`, `libnss3` 등) 자동 설치
2. `Setting up physical-labs (...)` 출력 후 postinst 시작
3. `>>> physical-labs: 가상환경 생성 중...`
4. `>>> physical-labs: 의존성 설치 중 (5~10분 소요, lerobot/torch 등 1~2GB 다운로드 필요)...`
5. lerobot, torch, PyQt6 등 pip 진행 출력 (수백 줄)
6. `>>> physical-labs: 설치 완료. 'physical-labs' 명령 또는 GNOME 메뉴에서 실행하세요.`

## 4.1 기존 `roboseasy-studio` 사용자 (제품명 변경 안내)

제품명이 **Roboseasy Studio → Physical Labs** 로 바뀌었습니다. 위 설치 명령
한 줄이면 구 패키지가 자동 제거되고 새 패키지가 설치됩니다.
사용자 데이터는 **첫 실행 시 자동 이관**됩니다.

| 항목 | 이관 여부 |
|---|---|
| 약관 동의 | ✅ 유지 — 다시 묻지 않음 |
| 로봇 설정 (포트·카메라) | ✅ 유지 — 재설정 불필요 |
| API 키 (HuggingFace / Wandb) | ✅ OS 키링에서 자동 복사 |
| 녹화 모션 | ✅ 자동 복사 |
| 구글 로그인 | ⚠️ **재로그인 1회 필요** |

- 재로그인 1회는 **정상 동작**입니다 — 설치마다 새로 발급되는 설치 식별자가
  바뀌면 저장된 토큰을 폐기하도록 설계되어 있습니다 (기존 업그레이드 때와 동일).
- 구 데이터(`~/.config/Roboseasy/`)는 **삭제하지 않고 그대로 둡니다**.
  정리하려면 `rm -rf ~/.config/Roboseasy`.
- 실행 명령이 `roboseasy-studio` → **`physical-labs`** 로 바뀝니다.
  구 명령 심볼릭 링크는 제공하지 않습니다.

## 5. 첫 실행

GNOME 메뉴에서 "Physical Labs" 검색 후 클릭, 또는:

```bash
physical-labs
```

첫 실행 흐름:
1. **Welcome 화면** — Physical Labs 인사
2. **Google 로그인** — 기본 브라우저가 열려 OAuth 진행 → 로그인 완료 시 브라우저 탭 자동 닫기 시도
3. **약관 동의** (최초 1회만)
4. **모드 선택** — ID 셋업 / 단일 모터 테스트 / SO-ARM 101 / 워크스페이스

## 6. 주요 기능

| 기능 | 진입 |
|---|---|
| **모터 ID 셋업** | 모드 선택 → "모터 ID 셋업" 마법사 |
| **단일 모터 테스트** | 모드 선택 → "단일 모터 테스트" |
| **SO-ARM 101 제어** | 모드 선택 → "SO-ARM 101" |
| **데이터셋 창고** | 워크스페이스 → 사이드바 "데이터셋 창고" — 로컬/HuggingFace 데이터셋 통합 조회 |
| **로봇 워크플로우** | 워크스페이스 → 로봇 선택 → 캘리브레이션/텔레옵/수집/훈련/추론 탭 |

## 7. 업데이트

새 버전이 [GitHub Releases](https://github.com/roboseasy/physical-labs-app-deploy/releases) 에 올라오면:

```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/<새버전>/physical-labs_<새버전>_amd64.deb
sudo apt install --reinstall ./physical-labs_<새버전>_amd64.deb
```

기존 가상환경(`/opt/physical-labs/venv`)은 유지되며 pip 가 변경분만 설치합니다 (보통 1~3분).

### 강제 재설치 (가상환경부터 다시)

```bash
sudo rm -rf /opt/physical-labs/venv
sudo apt install --reinstall ./physical-labs_<버전>_amd64.deb
```

## 8. 제거

```bash
sudo apt remove physical-labs
```

`/opt/physical-labs/` 와 그 안의 `venv` 까지 모두 제거됩니다. 사용자 데이터(`~/.config/PhysicalLabs/` — 로그인 토큰, HuggingFace API 키, 로봇 설정 등)는 **보존**됩니다.

완전 정리가 필요하면:

```bash
rm -rf ~/.config/PhysicalLabs
```

> ⚠️ `~/.config/PhysicalLabs` 를 지우면 다시 설치할 때 Google 로그인부터 시작하고 저장된 HuggingFace 토큰도 모두 사라집니다.

## 9. 문제 해결 (FAQ)

### 9.1 `PermissionError: [Errno 13] Permission denied: '/opt/physical-labs/resource/oauth_client.json'`

원인: 일부 옛 빌드의 .deb 가 시크릿 파일을 0600 으로 설치해 일반 사용자가 못 읽음.

해결:
```bash
sudo chmod 644 /opt/physical-labs/resource/oauth_client.json
sudo chmod 644 /opt/physical-labs/resource/supabase_config.json
```

### 9.2 설치 중 `python3-venv` 또는 `python3.12-venv` 관련 에러

```bash
sudo apt update
sudo apt install python3-venv python3.12-venv python3-pip
sudo apt install --reinstall ./physical-labs_*.deb
```

### 9.3 USB 모터를 인식하지 못함 (Permission denied on /dev/ttyUSB*)

dialout 그룹에 사용자 추가 후 **재로그인** 또는 재부팅:

```bash
sudo usermod -aG dialout $USER
# 로그아웃/재로그인 또는 재부팅
```

연결 후 `ls -l /dev/ttyUSB*` 로 그룹이 dialout 인지 확인.

### 9.4 Google 로그인 후 브라우저 탭이 자동으로 안 닫힘

Firefox 의 보안 정책(`dom.allow_scripts_to_close_windows` 기본 false) 때문일 수 있습니다.

옵션:
- **권장**: Chrome / Chromium 사용
- 또는 안내 메시지가 보이면 직접 탭을 닫고 앱으로 돌아가세요. 로그인은 정상 처리됐습니다.

### 9.5 데이터셋 창고가 비어있음 (HuggingFace Hub 데이터셋이 안 보임)

설정 → 일반 → API 키 에서 HuggingFace Access Token 추가 후 "선택" 으로 활성화하세요.

### 9.6 첫 실행 후 venv 가 손상된 것 같음 (ImportError 류)

```bash
sudo rm -rf /opt/physical-labs/venv
sudo apt install --reinstall ./physical-labs_<버전>_amd64.deb
```

### 9.7 로그 위치

- 앱 로그: `~/.config/PhysicalLabs/logs/` (시나리오 로그가 활성화된 경우)
- 설치 로그: `sudo journalctl -u apt | grep physical-labs` (또는 dpkg.log)

## 10. 라이선스 / 저작권

© 로보시지 (RoboSEasy)

본 소프트웨어의 라이선스 조건은 `/opt/physical-labs/resource/terms_of_service.md` 를 참고하세요. 개인정보처리방침은 `privacy_policy.md`.
