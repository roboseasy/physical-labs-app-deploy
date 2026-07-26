# Physical Labs v0.6.0-0.0.1

LeRobot **0.6.0** 기반. **Physical Labs 의 첫 릴리즈**입니다.

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

> ⚠️ **`sudo dpkg -i` 가 아니라 `sudo apt install` 을 쓰세요.**
> 구 패키지 `roboseasy-studio` 와 `Conflicts` 관계라 `dpkg -i` 는 거부됩니다.
> `apt` 를 쓰면 구 패키지 제거까지 한 번에 처리됩니다.

## Windows

이번 릴리즈는 **Linux .deb 만** 포함합니다.
Windows 인스톨러는 다음 재빌드에서 `physical-labs` 이름으로 제공될 예정입니다.

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
- 유저 데이터 자동 이관 (원본 비삭제·멱등)

### 새 로봇 생성 기종 개편
- **SO-101 / SO-102 / Lekiwi / reBot / Dual SO-101 / Dual SO-102** 6종으로 재구성
- 현재 선택 가능한 기종은 **SO-101** 이며, 나머지는 "준비 중" 표시

### 버그 수정
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

## 무결성 검증

```bash
sha256sum -c physical-labs_0.6.0-0.0.1_amd64.deb.sha256
```

- `.deb` SHA256: `6a28608f954d1defb7b97d95f0b067523db19af1723b6a54f8cfd4f642da7a81`

---

## 이전 제품(Roboseasy Studio) 릴리즈에 대해

Physical Labs 로 리네임하면서 구 제품명으로 배포됐던 릴리즈
(`v0.6.0-0.0.1` · `v0.5.1-0.0.1`)는 **정리했습니다**. 해당 버전을 쓰고 계셨다면
위 설치 명령으로 바로 업그레이드하시면 됩니다.

구 산출물이 필요한 경우 이 저장소의 git 히스토리에서 받을 수 있습니다:

```bash
git clone https://github.com/roboseasy/physical-labs-app-deploy
cd physical-labs-app-deploy
git log --all --oneline -- linux/dist window/dist   # 해당 커밋 확인
git checkout <commit> -- linux/dist window/dist
```
