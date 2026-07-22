# Roboseasy Studio v0.6.0-0.0.1

LeRobot **0.6.0** 기반. Windows / Ubuntu 모두 지원.

## 빠른 설치

### Windows 10/11 (64-bit)

1. [roboseasy-studio-setup_v0.6.0_v0.0.1_win64.exe](https://github.com/roboseasy/roboseasy-studio-deploy/releases/download/v0.6.0-0.0.1/roboseasy-studio-setup_v0.6.0_v0.0.1_win64.exe) 다운로드 (~38 MB)
2. 더블클릭 → SmartScreen "추가 정보" → "실행"
3. Inno Setup 마법사 진행 (5~30분, 인터넷 연결 필수)

설치 가이드: [install_ko.md](https://github.com/roboseasy/roboseasy-studio-deploy/blob/main/install_ko.md)

### Ubuntu 24.04+ (.deb)

```bash
wget https://github.com/roboseasy/roboseasy-studio-deploy/releases/download/v0.6.0-0.0.1/roboseasy-studio_0.6.0-0.0.1_amd64.deb
sudo apt install ./roboseasy-studio_0.6.0-0.0.1_amd64.deb
```

기존 v0.5.1 사용자도 위 명령 그대로 업그레이드됩니다 (가상환경 유지, 변경분만 설치).

## 변경 사항 (v0.5.1 → v0.6.0)

- **버그·UX 수정 (.deb 재빌드, 2026-07-21)**
  - 텔레옵·추론·EEF·수집 연결 시 `EOFError: EOF when reading a line` 차단 — lerobot 0.6.0 이 미보정 상태에서 띄우던 콘솔 입력 프롬프트를 GUI 에서 자동 처리(저장된 보정값 자동 적용, 없으면 칼리브레이션 안내)
  - 탭·섹션 전환 시 로봇 시리얼·카메라 포트가 해제되지 않아 다음 화면에서 "포트 사용중" 오류가 나던 문제 수정
  - 칼리브레이션 3D 뷰어가 창을 키워도 커지지 않던 문제 수정
  - 사용자별 화면 해상도·배율(125/150%)에서 창이 화면을 넘던 문제 완화(창 최소 크기 화면 비율 클램프)
- **버그·UX 수정 (Windows 인스톨러 재빌드, 2026-07-22)** — 위 .deb 재빌드 수정 4건 모두 포함, 추가로:
  - **엔드이펙터 XYZ(직교) 제어가 Windows 에서 실제 동작** — 정밀 IK(placo)가 Windows 를
    지원하지 않아 동작하지 않던 것을 위치 전용 numpy 간이 IK 폴백으로 해결 (XYZ 탭에 안내 표시)
  - EEF 모션 저장 후 화면 분할 오른쪽 이동이 안 되던 문제 수정
  - 로봇 저장 후 엔드이펙터 탭에 새 로봇 설정이 반영되지 않던 문제 수정
  - 엔드이펙터 기본 탭을 Joint Control 로 변경
  - Windows 포트 콤보 라벨에 저장된 로봇팔 이름 표시
- **LeRobot 0.6.0 전환** — 런타임을 `lerobot[feetech,kinematics,dataset]==0.6.0` 으로 업그레이드 (0.6.0 의 임포트 경로 변경 대응 포함)
- **GR00T N1.7 전환** — N1.5 시절의 flash-attn 수동 빌드·PR#3182 cherry-pick 절차 제거. `lerobot[groot]==0.6.0` 설치만으로 GR00T 학습 준비 완료
- SmolVLA / X-VLA 의존성 설치를 0.6.0 핀으로 정렬 — 설치 버튼이 lerobot 을 구버전으로 다운그레이드하던 문제 예방
- **설치 안정화 (.deb 재빌드)** — pandas/numpy/pyarrow 를 wheel 로만 설치하도록 고정해, 첫 설치 시 py3.12 wheel 없는 구버전 pandas sdist 소스 빌드로 pip 가 죽던 문제 차단
- 데이터셋 포맷은 v3.0 그대로 — 기존 수집 데이터 변환 불필요

## 시스템 요구사항

| 항목 | Windows | Linux |
|------|---------|-------|
| OS | Windows 10/11 (64-bit) | Ubuntu 24.04 LTS |
| Python | 3.10+ (없으면 인스톨러가 자동 설치) | 3.12+ (기본 포함) |
| 인터넷 | 첫 설치 시 필수 (lerobot/torch 2~3GB 다운로드) | 동일 |
| 디스크 | ~5GB | ~5GB |

## 무결성 검증

### Windows (PowerShell)

```powershell
Get-FileHash roboseasy-studio-setup_v0.6.0_v0.0.1_win64.exe -Algorithm SHA256
```

### Linux

```bash
sha256sum -c roboseasy-studio_0.6.0-0.0.1_amd64.deb.sha256
```

### 체크섬

- `.exe` SHA256: `676e8a43f1a547bb81fda9301e0f96cf5e446b9e0722112f7a5795a7949de291`
- `.deb` SHA256: `0de3f9c38deec8b01460d4f122c9377337903b1d90d40e56a96f822114718292`

---

# 이전 릴리즈

## v0.5.1-0.0.1 — [릴리즈 페이지](https://github.com/roboseasy/roboseasy-studio-deploy/releases/tag/v0.5.1-0.0.1)

- 첫 릴리즈. Linux .deb (정통 Debian 패키징) + Windows 인스톨러 (Inno Setup)
- Linux .deb 업데이트 (2026-06-14): EEF↔텔레옵 속도 분리, EEF 관절 UI 개선, 연결 버튼 단일 토글 통합, Supabase 로그인 B안(Edge Function) 이관
- Windows 인스톨러 업데이트 (2026-07-05): 설치 중 창 멈춤 수정, Store python 스텁 오탐 수정, USB 시리얼 넘버 기반 포트 자동 매핑, 포트 재연결 안정화
- 체크섬: `.deb` `04f85282a046461a5d938be202bdc4b530e5148754bf3cf41718d1733ad67f94` / `.exe` `5adca3c7f9eb32447de67ee2f75f20c54ff3e12945912e81a8e5bf85756ea429`
