# Physical Labs v0.6.0-0.0.2

LeRobot **0.6.0** 기반.

> ## 📛 제품명이 바뀌었습니다 — Roboseasy Studio → **Physical Labs**
>
> 패키지명·실행 명령·설치 경로가 모두 `physical-labs` 로 바뀌었습니다.
> **기존 사용자는 아래 "업그레이드" 절을 꼭 읽어주세요.**

## 빠른 설치

### Ubuntu 24.04+ (.deb)

```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.2/physical-labs_0.6.0-0.0.2_amd64.deb
sudo apt install ./physical-labs_0.6.0-0.0.2_amd64.deb
```

설치 후 실행: `physical-labs` 명령 또는 GNOME 메뉴에서 **Physical Labs**.

설치 가이드: [install_ko.md](https://github.com/roboseasy/physical-labs-app-deploy/blob/main/install_ko.md)

> ⚠️ **`sudo dpkg -i` 가 아니라 `sudo apt install` 을 쓰세요.**
> 구 패키지 `roboseasy-studio` 와 `Conflicts` 관계라 `dpkg -i` 는 거부됩니다.
> `apt` 를 쓰면 구 패키지 제거까지 한 번에 처리됩니다.

### Windows

이번 릴리즈는 **Linux .deb 만** 포함합니다. Windows 인스톨러는 다음 재빌드에서
`physical-labs` 이름으로 반영될 예정이며, 그때까지는 이전 릴리즈
[v0.6.0-0.0.1](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.1)
의 `.exe` 를 사용하세요 (기능은 동일, 이름만 구 명칭).

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

## 변경 사항 (v0.6.0-0.0.1 → v0.6.0-0.0.2)

- **제품명 전면 리네임** — `Roboseasy Studio` → `Physical Labs`
  - 패키지 `physical-labs`, 실행 명령 `physical-labs`, 설치 경로 `/opt/physical-labs`
  - 설정 디렉토리 `~/.config/PhysicalLabs`, 캐시 `~/.cache/physical-labs`
  - 창 제목·GNOME 런처 표시명 `Physical Labs`
- **유저 데이터 자동 이관** — 로그인·약관·로봇 설정·API 키·녹화 모션을 구 위치에서
  복사(원본 비삭제·멱등)
- **GNOME 독 아이콘 매칭 수정** — `.desktop` 파일명과 앱의 desktop file name 이
  어긋나 있던 기존 불일치를 정합화
- **작업표시줄 고정 유지 (Windows)** — AppUserModelID 에서 버전 세그먼트를 제거해
  릴리스마다 고정이 풀리던 문제 예방
- **Teaching Control(직접 교시) 탭이 Linux .deb 에도 포함** — 이전 .deb 에는 빠져
  있던 기능. 자유 이동(토크 해제)으로 손으로 팔을 끌어 포즈를 잡고 시퀀스 저장 →
  Motion Record 로 순차 실행·모션 저장(속도/힘 조절) → Motion Replay 로 재생

## 시스템 요구사항

| 항목 | Linux |
|------|-------|
| OS | Ubuntu 24.04 LTS |
| Python | 3.12+ (기본 포함) |
| 인터넷 | 첫 설치 시 필수 (lerobot/torch 2~3GB 다운로드) |
| 디스크 | ~5GB |

## 무결성 검증

```bash
sha256sum -c physical-labs_0.6.0-0.0.2_amd64.deb.sha256
```

### 체크섬

- `.deb` SHA256: `6d087b82267377be2f602486de6290739ea714088ff7401068d933b1ef14566b`

---

# 이전 릴리즈

## v0.6.0-0.0.1 — [릴리즈 페이지](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.1)

> 이 시점까지의 제품명은 **Roboseasy Studio** 이며, 산출물 이름도 `roboseasy-studio_*` 입니다.

- **LeRobot 0.6.0 전환** — 런타임을 `lerobot[feetech,kinematics,dataset]==0.6.0` 으로 업그레이드
- **GR00T N1.7 전환** — N1.5 시절의 flash-attn 수동 빌드·PR#3182 cherry-pick 절차 제거
- SmolVLA / X-VLA 의존성 설치를 0.6.0 핀으로 정렬
- 텔레옵·추론·EEF·수집 연결 시 `EOFError` 차단, 탭·섹션 전환 시 포트 미해제 수정,
  칼리브레이션 3D 뷰어 크기 조절 수정, 고배율 DPI 창 클램프
- Windows 인스톨러(2026-07-22): Teaching Control 탭 신규, 엔드이펙터 XYZ 제어 Windows 동작
  (numpy 간이 IK 폴백), EEF 화면 분할·로봇 설정 반영 수정
- 체크섬: `.deb` `0de3f9c38deec8b01460d4f122c9377337903b1d90d40e56a96f822114718292` /
  `.exe` `94a508e467ef6d553c01e89c2da12847c0e0f65c1233504d808521454bf87bac`

## v0.5.1-0.0.1 — [릴리즈 페이지](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.5.1-0.0.1)

- 첫 릴리즈. Linux .deb (정통 Debian 패키징) + Windows 인스톨러 (Inno Setup)
- Linux .deb 업데이트 (2026-06-14): EEF↔텔레옵 속도 분리, EEF 관절 UI 개선, 연결 버튼 단일 토글 통합, Supabase 로그인 B안(Edge Function) 이관
- Windows 인스톨러 업데이트 (2026-07-05): 설치 중 창 멈춤 수정, Store python 스텁 오탐 수정, USB 시리얼 넘버 기반 포트 자동 매핑, 포트 재연결 안정화
- 체크섬: `.deb` `04f85282a046461a5d938be202bdc4b530e5148754bf3cf41718d1733ad67f94` / `.exe` `5adca3c7f9eb32447de67ee2f75f20c54ff3e12945912e81a8e5bf85756ea429`
