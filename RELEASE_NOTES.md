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

- **LeRobot 0.6.0 전환** — 런타임을 `lerobot[feetech,kinematics,dataset]==0.6.0` 으로 업그레이드 (0.6.0 의 임포트 경로 변경 대응 포함)
- **GR00T N1.7 전환** — N1.5 시절의 flash-attn 수동 빌드·PR#3182 cherry-pick 절차 제거. `lerobot[groot]==0.6.0` 설치만으로 GR00T 학습 준비 완료
- SmolVLA / X-VLA 의존성 설치를 0.6.0 핀으로 정렬 — 설치 버튼이 lerobot 을 구버전으로 다운그레이드하던 문제 예방
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

- `.exe` SHA256: `f9adff14f3b211ede8c66e3621ff7c0ea076bfc71946e1219d566621b921f9d8`
- `.deb` SHA256: `94150f32625eaa47bf8b1779538e1cbc866e6a40d78fc684a2dffeefe7a844a5`

---

# 이전 릴리즈

## v0.5.1-0.0.1 — [릴리즈 페이지](https://github.com/roboseasy/roboseasy-studio-deploy/releases/tag/v0.5.1-0.0.1)

- 첫 릴리즈. Linux .deb (정통 Debian 패키징) + Windows 인스톨러 (Inno Setup)
- Linux .deb 업데이트 (2026-06-14): EEF↔텔레옵 속도 분리, EEF 관절 UI 개선, 연결 버튼 단일 토글 통합, Supabase 로그인 B안(Edge Function) 이관
- Windows 인스톨러 업데이트 (2026-07-05): 설치 중 창 멈춤 수정, Store python 스텁 오탐 수정, USB 시리얼 넘버 기반 포트 자동 매핑, 포트 재연결 안정화
- 체크섬: `.deb` `04f85282a046461a5d938be202bdc4b530e5148754bf3cf41718d1733ad67f94` / `.exe` `5adca3c7f9eb32447de67ee2f75f20c54ff3e12945912e81a8e5bf85756ea429`
