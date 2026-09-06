# Physical Labs v0.6.0-0.0.10 (Linux)

> 이 릴리즈는 **Ubuntu 24.04+ 전용 `.deb`** 입니다. Windows 사용자는
> [v0.6.0-0.0.8](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.8)
> 의 인스톨러를 받으세요. LeRobot **0.6.0** 기반.

## 빠른 설치 — Ubuntu 24.04+

```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.10/physical-labs_0.6.0-0.0.10_amd64.deb
sudo apt install ./physical-labs_0.6.0-0.0.10_amd64.deb
```

설치 후 실행: `physical-labs` 명령 또는 GNOME 메뉴에서 **Physical Labs**.
설치 가이드: [install_ko.md](https://github.com/roboseasy/physical-labs-app-deploy/blob/main/install_ko.md)

> ⚠️ **`sudo dpkg -i` 가 아니라 `sudo apt install` 을 쓰세요.**
> 구 패키지 `roboseasy-studio` 와 `Conflicts` 관계라 `dpkg -i` 는 거부됩니다.
> 이전 Physical Labs(0.0.1 / 0.0.9)가 설치돼 있으면 `apt` 가 그대로 업그레이드합니다.

## 🔁 2026-09-06 재빌드 — 같은 버전(0.0.10)에 아래 수정을 담아 다시 올렸습니다

> 이미 0.0.10 을 설치했다면 위 명령으로 **다시 설치**하세요 (`apt` 가 같은 버전이라 건너뛰면 `sudo apt reinstall ./physical-labs_0.6.0-0.0.10_amd64.deb`).

### 🦾 LeKiwi 엔드이펙터 — 관절 키보드 조그가 끊기지 않습니다

- Q/A/W/S… 관절 조그가 0.5 초마다 규칙적으로 멈추던 문제를 고쳤습니다. 이제 PC 는 방향만 보내고
  **로봇(Pi)이 스스로 적분**합니다 — 화살표 바퀴 주행과 같은 구조라 같은 정도로 부드럽습니다.
  속도는 속도 슬라이더(`Goal_Velocity`)가 정하고, 키를 떼면 그 자리에서 섭니다 (0.5 초 워치독 포함).
- 관절을 조작할 때마다 2·3번 관절(shoulder_lift·elbow_flex)이 중력으로 조금씩 내려가던 래칫을
  고쳤습니다 — 바뀐 관절만 보내고, 목표와 실측을 분리해 처짐을 목표로 되먹이지 않습니다.

### 🛠 그 밖에

- 칼리브레이션(원격 팔): 마지막 호스트 주소를 기억하고 연결 램프로 상태를 보여 줍니다.
- 모터 셋업에 로봇 추가.
- 텔레옵 Control 행: 원격 팔로워(LeKiwi)면 Follower 포트 대신 로봇 주소 안내를 보입니다.
- 홈·다른 메뉴로 나가 호스트가 내려갈 때 로봇 설정 블록 상태가 함께 갱신됩니다.
- 로봇 설정의 기본 연결 방식이 **이더넷 직결**입니다 (킷은 랜선부터 꽂기 때문).

## 주요 변경 사항 (Linux 0.0.9 대비)

### 📶 LeKiwi 로봇 와이파이 설정 — 터미널 없이 앱에서

지금까지 LeKiwi(Pi) 를 와이파이에 붙이려면 SSH 로 들어가 `wifi <SSID> <비밀번호>`, `setip N` 을
직접 쳐야 했습니다. 이제 **로봇 설정 > 2. Lekiwi (원격)** 의 `[📶 와이파이 설정…]` 버튼 하나로
PC 에서 와이파이 고르듯 처리합니다.

1. **스캔·선택** — 로봇 주변 와이파이를 신호 세기·대역(2.4/5GHz)·보안과 함께 표시. 개방/WEP 망은 회색(미지원).
2. **비밀번호 입력 → 적용** — 로봇이 새 와이파이로 옮겨 가는 동안 앱이 기다렸다가 **실제로 붙었는지**(SSID·IP) 확인합니다.
   비밀번호가 틀리면 "붙지 못했다" 로 알려 줍니다.
3. **고정 IP 확인** — 킷 번호(N)의 `192.168.0.20N` 이 아니면 `[고정 IP 설정]` 으로 이어서 맞춥니다 (Pi 의 `setip`).
4. **와이파이로 전환** — 성공하면 한 번의 클릭으로 연결 방식·로봇 IP 가 갱신됩니다. 이후 `[연결 확인]` → `[▶ 호스트 실행]` 은 그대로.

권장 순서: **이더넷 직결 → 와이파이 설정 → 고정 IP 확인 → PC 를 같은 와이파이에 연결 → 랜선 분리**.

- 로봇 비밀번호(관리자 권한)가 필요한 킷에서만 한 번 묻고, 창을 닫으면 지웁니다. 어디에도 저장하지 않습니다.
- 마지막 설정(SSID·IP·시각)은 로봇 설정에 기록되어 다음에 다시 열면 보입니다.
- ⚠️ **핫스팟 주의**: 고정 IP `192.168.0.20N` 은 `192.168.0.x` 대역 공유기에서만 통합니다. 폰 핫스팟처럼
  다른 대역이면 로봇이 붙어도 PC 가 못 찾습니다 — 앱이 이 경우를 감지해 경고하고 `setdhcp` 안내를 띄웁니다.
- 따옴표(`"`)·백슬래시(`\`)가 든 와이파이 이름/비밀번호는 Pi 설정 스크립트가 지원하지 않아 앱이 거부합니다.

### 안정성

- 로봇이 SSH 키 검증에서 바로 연결을 끊는 경우 진짜 원인(호스트 키 변경) 대신 "입력 쓰기 실패" 만 보이던 문제 수정.
- 호스트 키가 바뀐 로봇에 와이파이 설정을 시도해도 앱 안에서 복구(키 정리 → 다시 시도)할 수 있습니다.

## 시스템 요구사항

- Ubuntu 24.04 LTS
- Python 3.12+
- 인터넷 연결 (첫 설치 시 lerobot/torch 등 1~2GB 다운로드)
- 디스크 공간 ~5GB

## 무결성 검증

```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.10/physical-labs_0.6.0-0.0.10_amd64.deb.sha256
sha256sum -c physical-labs_0.6.0-0.0.10_amd64.deb.sha256
```

SHA256: `530fc11d68b5f7faaa2a706d34460f526bd71ef4ed9183094700b43a1b6fc8da`

## 커밋 로그 (v0.6.0-0.0.9 이후, physical-labs-app main)

- Fix: 관절제어시 버그 해결 (afc6c77)
- FIX: LeKiwi 관절 조그 — 로봇 쪽 적분(JOG)으로 전환해 규칙적 끊김 제거 (2752656)
- Add: 모터셋업 추가 로봇 (f0ed11f)
- FIX: 칼리브레이션 원격 팔 — 마지막 호스트 주소 기억 + 연결 램프 (5d8193d)
- Fix: 칼리브레이션 문제 개선 (9daacd7)
- Docs: v0.6.0-0.0.10 Linux 릴리즈 작업 로그 (fea3607)
- Release: VERSION 0.0.9 → 0.0.10 (Linux .deb — LeKiwi 와이파이 설정) (172c3ac)
- Add: lekiwi wifi 새롭게 연결 세팅 (35c38f9)
- Docs: v0.6.0-0.0.9 Linux 릴리즈 작업 로그 (3cfda9b)

---

# Physical Labs v0.6.0-0.0.9 (Linux)

> 이 릴리즈는 **Ubuntu 24.04+ 전용 `.deb`** 입니다. Windows 사용자는
> [v0.6.0-0.0.8](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.8)
> 의 인스톨러를 받으세요. LeRobot **0.6.0** 기반.

## 빠른 설치 — Ubuntu 24.04+

```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.9/physical-labs_0.6.0-0.0.9_amd64.deb
sudo apt install ./physical-labs_0.6.0-0.0.9_amd64.deb
```

설치 후 실행: `physical-labs` 명령 또는 GNOME 메뉴에서 **Physical Labs**.
설치 가이드: [install_ko.md](https://github.com/roboseasy/physical-labs-app-deploy/blob/main/install_ko.md)

> ⚠️ **`sudo dpkg -i` 가 아니라 `sudo apt install` 을 쓰세요.**
> 구 패키지 `roboseasy-studio` 와 `Conflicts` 관계라 `dpkg -i` 는 거부됩니다.
> 이전 Physical Labs(0.0.1)가 설치돼 있으면 `apt` 가 그대로 업그레이드합니다.

## 주요 변경 사항 (Linux 0.0.1 · 2026-08-07 재빌드 대비)

### 🛞 LeKiwi 바퀴(모바일 베이스) 주행 — 이제 앱에서 굴립니다

이전 릴리즈는 LeKiwi 의 바퀴를 **항상 정지**로 고정했습니다. 이번 릴리즈부터 키보드로 몹니다.

| 화면 | 전진 / 후진 | 좌 / 우 이동 | 제자리 좌회전 / 우회전 | 속도 |
|---|---|---|---|---|
| 텔레오퍼레이션 | `W` / `S` | `A` / `D` | `Q` / `E` | `R` / `F` (느림·보통·빠름) |
| 엔드이펙터 | `↑` / `↓` | `←` / `→` | `Shift+←` / `Shift+→` | 느림 고정 |

- 사용법은 각 화면에 **글자로 표시**됩니다 (텔레옵: 3D 뷰 아래 상태줄, 엔드이펙터: 연결 바 아래).
- 텔레오퍼레이션은 **Real Control 탭에서 연결했을 때만** 실제 바퀴가 굴러가고, Sim Control 에서는
  3D 화면에서만 움직입니다. 엔드이펙터는 연결 직후부터(Sync 확인 전에도) 굴릴 수 있습니다.
- 3D 화면의 로봇도 베이스가 같이 이동하고 옴니휠이 돌아갑니다.
- 안전 장치: 키를 떼면 즉시 정지, 창이 비활성화되거나 탭을 바꾸거나 화면이 숨겨지면 강제 정지,
  로봇 쪽에서도 0.5 초 안에 명령이 끊기면 스스로 멈춥니다. 녹화 이름 같은 글자 입력 칸에 커서가
  있을 때는 키가 로봇으로 가지 않습니다.

### 🎞 Motion Record / Replay 가 바퀴까지 기록·재생

텔레오퍼레이션과 엔드이펙터의 모션 녹화에 바퀴 속도가 함께 저장되고, 리플레이 때 그대로 재생됩니다.
Real 재생 시 파일에 바퀴 주행이 들어 있으면 경고창에 **"로봇이 이동합니다"** 가 표시됩니다.
예전 녹화 파일은 그대로 팔만 움직입니다. 저장되는 것은 속도 지령이라 바닥·배터리 상태에 따라
경로가 조금 달라질 수 있습니다.

### 그 밖의 LeKiwi 개선

- **3D 화면에 옴니 베이스까지 그립니다** — 이전에는 팔만 떠 있었습니다. 캘리브레이션·엔드이펙터·
  텔레오퍼레이션·데이터·추론 전 화면 적용. 리더 암은 그대로 SO-101 팔로 표시됩니다.
- **캘리브레이션 탭에 [🔓 토크 해제] 버튼** — 원격 팔로워(LeKiwi)의 팔 토크를 앱에서 풉니다
  (바퀴는 건드리지 않음). 다시 켜려면 호스트를 실행하세요.
- **LeKiwi 추론 탭** 지원.

### 학습 탭

- **새 학습 탭** 추가.
- `lerobot[training]` 이 설치되지 않은 환경에서는 새 학습·학습 재개 탭 진입을 막고 설치 안내를
  띄웁니다. 환경 진단의 Accelerate 카드 표기도 `lerobot[training]` 으로 통일했습니다.

## 시스템 요구사항

- Ubuntu 24.04 LTS, Python 3.12+
- 인터넷 연결 (첫 설치 시 lerobot/torch 등 1~2GB 다운로드), 디스크 여유 ~5GB

## 무결성 검증

```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.9/physical-labs_0.6.0-0.0.9_amd64.deb.sha256
sha256sum -c physical-labs_0.6.0-0.0.9_amd64.deb.sha256
```

SHA256: `a5c4b446367c12c1651085da471a1810ec68adc9abb1f3c1c82cbd843028c9fb`

## 커밋 로그 (2026-08-07 Linux 재빌드 이후, physical-labs-app main)

- 9d78cef Release: VERSION 0.0.1 → 0.0.9
- 89b777b Add: lekiw 이동 모션도 저장 및 리플레이
- a33d542 Add: Lekiwi 키보드 이동 제어
- 5e78264 Fix: Lekiwi
- 45c23d8 Add: Lekiwi 칼리브레이션 토크 off 버튼 기능 추가
- ff6e73d ADD: lerobot[training] 미설치 시 새 학습·학습 재개 탭 진입 차단
- 3cf1317 UPDATE: 환경 진단의 Accelerate 카드 표기를 lerobot[training] 으로
- 4f31e9c Add: Lekiwi Inference
- 92ac57d Add: train tap
- e0c825b, 36be047 Add: Lekiwi Teleoperation

---

# Physical Labs v0.6.0-0.0.1

LeRobot **0.6.0** 기반. **Physical Labs 의 첫 릴리즈**입니다. Windows / Ubuntu 모두 지원.

> ## 📛 Roboseasy Studio 에서 이름이 바뀌었습니다
>
> 제품명·패키지명·실행 명령·설치 경로가 모두 **Physical Labs / `physical-labs`** 로
> 바뀌었고, 버전 라인도 새 제품의 첫 릴리즈인 `0.0.1` 부터 다시 시작합니다.
> **기존 Roboseasy Studio 사용자는 아래 "업그레이드" 절을 꼭 읽어주세요.**

## 빠른 설치 — Ubuntu 24.04+

```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.1/physical-labs_0.6.0-0.0.1_amd64.deb
sudo apt install ./physical-labs_0.6.0-0.0.1_amd64.deb
```

설치 후 실행: `physical-labs` 명령 또는 GNOME 메뉴에서 **Physical Labs**.

설치 가이드: [install_ko.md](https://github.com/roboseasy/physical-labs-app-deploy/blob/main/install_ko.md)

> ⚠️ **이미 설치돼 있다면 `--reinstall` 이 필요합니다.**
> 버전 번호(`0.6.0-0.0.1`)가 그대로라 `apt` 가 "최신 버전" 으로 보고 건너뜁니다.
> `sudo apt install --reinstall ./physical-labs_0.6.0-0.0.1_amd64.deb`

> ⚠️ **`sudo dpkg -i` 가 아니라 `sudo apt install` 을 쓰세요.**
> 구 패키지 `roboseasy-studio` 와 `Conflicts` 관계라 `dpkg -i` 는 거부됩니다.
> `apt` 를 쓰면 구 패키지 제거까지 한 번에 처리됩니다.

## 빠른 설치 — Windows 10/11 (64-bit)

1. [physical-labs-setup_0.6.0-0.0.1_win64.exe](https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.1/physical-labs-setup_0.6.0-0.0.1_win64.exe) 다운로드 (~38 MB)
2. 더블클릭 → SmartScreen "추가 정보" → "실행"
3. 설치 마법사 진행 (5~30분, 인터넷 연결 필수)

> ℹ️ **Linux `.deb` 는 2026-08-07, Windows 인스톨러는 2026-08-04 재빌드가 최신입니다.**
> **(2026-08-07 · Linux 전용) LeKiwi 로봇 전 과정 지원** — 모바일 베이스 로봇 LeKiwi 로
> 텔레오퍼레이션 · 모션 녹화/재생 · 데이터 수집 · 데이터 편집 · 학습 · 추론을 모두 앱에서
> 할 수 있습니다. 팔은 SO-101 수업과 동일하게 다루며 **바퀴 주행은 포함하지 않습니다**
> (안전상 항상 정지 고정). 함께 고친 것: 앱에서 **학습한 모델이 추론 탭에 안 뜨던 문제**
> (전 기종), 체크포인트가 목록에서 전부 같은 이름으로 보이던 문제, 정책·로봇 불일치를
> 모델 선택 시점에 차단, 추론 정지 시 팔이 시작 자세로 천천히 복귀.
> **LeKiwi 를 여러 대 쓸 때 막히던 문제 2건**도 고쳤습니다 — 두 번째 로봇 연결 시
> 비밀번호를 묻지 않고 `Permission denied` 로 실패하던 것, 다른 로봇으로 바꾸면
> "호스트 키가 바뀌었다" 경고가 뜨던 것. 이제 새 로봇은 비밀번호를 한 번 물어
> 자동 등록되고, 로봇을 다시 설치해도 스스로 복구됩니다. 로봇을 **삭제하면 그 로봇의
> SSH 기록도 함께 정리**되어, 나중에 새 로봇을 같은 자리에 등록해도 경고 없이 붙습니다.
> **⚠️ 추론 탭은 실험적입니다** — 로봇이 사람 조작 없이 스스로 움직이므로 처음에는
> 로봇 주변을 비우고 [정지] 에 손을 두고 시작하세요.
> **로그인 사용자 기록 백엔드(Supabase) 교체 반영** — 서버 데이터베이스 교체로
> 이전 빌드는 로그인 시 사용자 정보(이름·이메일) 기록이 서버에 저장되지 않았습니다
> (앱 사용에는 영향 없음). 이번 빌드부터 정상 기록됩니다.
> (2026-08-02 재빌드 포함분: **보정 실패 시 어떤 모터가 문제인지 안내** — ID 셋업
> (중앙 정렬)을 하지 않은 SO-ARM 보정 시 `Magnitude 2555 exceeds 2047` 오류만 뜨던
> 것을, 범위 초과 모터 번호·현재 위치·해결 방법을 안내하도록 개선.)
> (2026-07-30 재빌드 포함분: **Python 3.14 가 설치된 PC 에서 설치가 실패하던 문제**
> 해결 — PC 의 Python 이 64-bit 3.12/3.13 이 아니면 동봉 Python 3.12 를 자동 설치.)
> 이전에 받으셨다면 다시 받아 설치하세요.

> 아래 "주요 변경 사항" 의 성능·버그 수정 항목은 **Linux .deb 기준**입니다.
> Windows 인스톨러는 별도 빌드라 반영 범위가 다를 수 있습니다.

## 업그레이드 (기존 `roboseasy-studio` 사용자)

위 `sudo apt install ./physical-labs_*.deb` 한 줄이면 구 패키지가 자동 제거되고
새 패키지가 설치됩니다. 사용자 데이터는 **첫 실행 시 자동으로 이관**됩니다.

| 항목 | 이관 여부 |
|---|---|
| 약관 동의 (`terms.json`) | ✅ 유지 — 다시 묻지 않음 |
| 로봇 설정 (`robots.json`) | ✅ 유지 — 포트·카메라 재설정 불필요 |
| API 키 (HuggingFace / Wandb) | ✅ OS 키링에서 자동 복사 |
| 녹화 모션 (`~/.cache/`) | ✅ 자동 복사 |
| 구글 로그인 | ⚠️ **재로그인 1회 필요** |

- 재로그인 1회는 **설계상 정상 동작**입니다. 설치마다 새로 발급되는 설치
  식별자(install_id)가 바뀌면 저장된 토큰을 폐기하도록 되어 있습니다
  (기존 버전 업그레이드 때와 동일한 동작).
- 구 데이터(`~/.config/Roboseasy/`)는 **삭제하지 않고 그대로 둡니다** — 문제가
  생기면 언제든 되돌릴 수 있습니다. 정리하려면 `rm -rf ~/.config/Roboseasy`.
- 수동으로 설치했던 흔적(`/opt/roboseasy-studio`)이 남아 있으면 설치 마지막에
  안내가 출력됩니다. 자동 삭제하지 않으니 직접 정리하세요.

## 주요 변경 사항

### 제품명 전면 리네임
- 패키지 `physical-labs`, 실행 명령 `physical-labs`, 설치 경로 `/opt/physical-labs`
- 설정 디렉토리 `~/.config/PhysicalLabs`, 캐시 `~/.cache/physical-labs`
- 창 제목·GNOME 런처 표시명 **Physical Labs**
- 이용약관·개인정보처리방침의 제품명도 **Physical Labs** 로 갱신 (동의 버전은 그대로라 재동의 불필요)
- 유저 데이터 자동 이관 (원본 비삭제·멱등)

### 새 로봇 생성 기종 개편
- **SO-101 / SO-102(7 DoF) / Lekiwi / reBot(7 DoF) / Dual SO-101 / Dual SO-102** 6종으로 재구성
- 현재 선택 가능한 기종은 **SO-101** 이며, 나머지는 "준비 중" 표시

### 로봇 불러오기 속도 대폭 개선
- 로봇 선택 후 워크플로우 진입이 **약 6초 → 1초 내외**로 단축
  - 엔드이펙터·텔레오퍼레이션이 **같은 URDF 를 각각 파싱**하던 중복 제거 (kinematics 공유)
  - URDF 파싱을 앱 시작 직후 백그라운드로 이동
  - 7개 탭을 한꺼번에 만들던 것을 **해당 탭을 처음 열 때** 만들도록 변경
- **"로봇을 불러오는 중입니다" 안내 창** 추가 — 진입·탭 최초 열기 시 표시

### 버그 수정
- **훈련이 시작되지 않던 문제** — `lerobot-train` 이 `accelerate` 없음으로 즉시 종료되던 것.
  환경 진단의 Accelerate / Wandb 설치 버튼이 이제 `lerobot[training]` 을 설치합니다
  (낱개 설치 시 lerobot 의 버전 제약을 벗어나는 문제도 함께 해소)
- **의존성 설치 버튼이 `.deb` 환경에서 항상 실패하던 문제** — 설치 위치(`/opt/physical-labs/venv`)가
  관리자 소유라 권한 오류가 나던 것. 이제 시스템 비밀번호를 한 번 입력하면 설치됩니다
- **훈련 > 환경 진단의 패키지 설치 버튼이 눌리지 않던 문제** (Flash Attention / Accelerate / Wandb)
- **새 학습이 `FileExistsError` 로 시작되지 않던 문제** — 앱이 출력 폴더를 미리 만들어
  lerobot 이 거부하던 것. 폴더를 지우고 다시 눌러도 재발했습니다
- **학습 결과 저장 위치를 `~/.PhysicalLabs/outputs/train` 으로 고정** — 이전에는 앱을
  실행한 위치에 따라 결과물이 흩어지고 '학습 재개' 가 이전 학습을 못 찾았습니다.
  기존 위치의 학습도 재개 목록에 계속 표시됩니다
- 학습 경과·남은 시간이 1시간을 넘으면 `시:분:초` 로 표기 (이전에는 `183:20` 처럼 표시)
- **데이터 > 편집에서 데이터셋을 열면 앱이 통째로 종료되던 문제** — 오류 메시지 없이
  꺼지던 크래시입니다. 데이터 수집·텔레오퍼레이션·추론·데이터셋 병합 경로에도 같은
  원인이 있어 함께 수정했습니다
- **작업 도중 화면을 옮기거나 앱을 종료할 때 강제 종료되던 문제** — 백그라운드 작업이
  남아 있는 상태에서 창이 닫히면 발생하던 크래시
- 설치 마지막 안내가 이미 `dialout` 그룹에 있는 사용자에게도 '실패' 처럼 보이던 문구 수정
- 엔드이펙터 기본 탭이 XYZ Control 로 열리던 문제 → **Joint Control** 로 변경
- 텔레오퍼레이션에서 Follower/Leader 포트가 **둘 다 같은 포트**로 잡히던 문제
  → '포트 고정하기' 심볼릭 링크를 우선 사용해 재부팅 후에도 좌우가 뒤바뀌지 않음
- 텔레오퍼레이션 Sim Control 진입 시 연결 버튼이 잘려 보이던 문제
- GR00T 모델 카드가 삭제된 N1.5 를 안내하던 문제 → **NVIDIA GROOT** 표기로 변경
- '+ New robot' 버튼 한글화 → **'+ 로봇 추가'**
- GNOME 독 아이콘 매칭 수정 — `.desktop` 파일명과 앱의 desktop file name 불일치 해소
- 작업표시줄 고정 유지(Windows) — AppUserModelID 에서 버전 세그먼트 제거

### LeRobot 0.6.0 기반 기능 (이전 제품명 시절 반영분 포함)
- **Teaching Control(직접 교시) 탭** — 자유 이동(토크 해제)으로 손으로 팔을 끌어
  포즈를 잡고 시퀀스 저장 → Motion Record 로 순차 실행·모션 저장(속도/힘 조절)
  → Motion Replay 로 재생. **Linux .deb 에는 이번에 처음 포함**됩니다.
- **GR00T N1.7 전환** — flash-attn 수동 빌드·cherry-pick 절차 제거,
  `lerobot[groot]==0.6.0` 설치만으로 학습 준비 완료
- SmolVLA / X-VLA 의존성 설치를 0.6.0 핀으로 정렬
- 텔레옵·추론·EEF·수집 연결 시 `EOFError` 차단
- 탭·섹션 전환 시 로봇 시리얼·카메라 포트 미해제 수정
- 칼리브레이션 3D 뷰어 창 크기 조절 수정, 고배율 DPI 창 클램프
- 설치 안정화 — pandas/numpy/pyarrow 를 wheel 로만 설치해 pip 빌드 실패 차단
- 데이터셋 포맷은 v3.0 그대로 — 기존 수집 데이터 변환 불필요

## 시스템 요구사항

| 항목 | Linux |
|------|-------|
| OS | Ubuntu 24.04 LTS |
| Python | 3.12+ (기본 포함) |
| 인터넷 | 첫 설치 시 필수 (lerobot/torch 2~3GB 다운로드) |
| 디스크 | ~5GB |

| 항목 | Windows |
|------|---------|
| OS | Windows 11 64-bit (10 은 동작 가능하나 미검증) |
| Python | **64-bit 3.12 / 3.13** — 없거나 범위 밖(3.11 이하·3.14 이상)이면 동봉 Python 3.12 를 자동 설치해 사용 |
| 인터넷 | 첫 설치 시 필수 (lerobot/torch 1~2GB 다운로드) |
| 디스크 | ~5GB |

## 무결성 검증

```bash
# Linux
sha256sum -c physical-labs_0.6.0-0.0.1_amd64.deb.sha256
```

```powershell
# Windows (PowerShell)
Get-FileHash physical-labs-setup_0.6.0-0.0.1_win64.exe -Algorithm SHA256
```

- `.deb` SHA256: `5201cee3208c2873db05d1d067822676069ccc0a847eac7525345fe9f0482b71`
  (2026-08-07 재빌드)
- `.exe` SHA256: `650b0a75dc7661bfc4a37d21366b02443a116974291044016a29d1048749d3a2`
  (2026-08-04 재빌드)

---

## 이전 제품(Roboseasy Studio) 릴리즈

제품이 **Physical Labs** 로 전환되면서 구 제품명으로 배포됐던 릴리즈와 산출물은
모두 정리했습니다. 앞으로는 `physical-labs` 만 배포합니다.

구 버전을 쓰고 계셨다면 위 설치 명령으로 바로 업그레이드하시면 되고,
사용자 데이터는 첫 실행 시 자동 이관됩니다.
