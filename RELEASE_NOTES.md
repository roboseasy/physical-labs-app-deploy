# Physical Labs v0.6.0-0.2.0 (Linux) — 2026-11-01 재배포

> 2026-11-01 저녁에 같은 0.2.0 으로 다시 올렸습니다 (오후 재배포 포함). **그 전에 0.2.0 을 설치했다면 `--reinstall` 을 붙여야 바뀝니다** (버전이 같아 그냥 설치하면 "이미 최신" 으로 건너뜁니다).

### 새 기능
- **새 A-Go(ROS 2 LeKiwi)에서 워크스페이스(Yolo + Pick&Place)가 열립니다** — Pick&Place 의 이동 구간은 아직 실물 재조정 중이라 처음에는 천천히 확인하며 쓰세요.
- **새 A-Go(ROS 2 LeKiwi)에서 엔드이펙터 탭을 씁니다** — 🔌 연결 · Sync 확인 · Joint · XYZ 조작 · 화살표 바퀴 · Teaching Control(자유 이동 포함) · Motion Record / Replay.
  - 속도 슬라이더가 팔이 움직이는 속도입니다 (Motion Replay 는 녹화된 속도 그대로).
  - 힘 슬라이더는 흉내입니다 — 목표가 실제 위치보다 앞설 수 있는 폭을 줄여 미는 힘 · 쥐는 힘을 약하게 합니다.
  - 자유 이동은 로봇이 명령 세션을 닫을 때까지 2초쯤 뒤에 힘이 빠집니다. 끝낼 때는 로봇이 토크를 켠 것을 확인한 뒤 '토크 켜짐' 을 알립니다.
- **Teaching Control 재생 재현율 개선 (SO-101 · A-Go)**
  - 저장한 자세가 중력 때문에 1~3° 낮게 재생되던 것 — 멈춰 있는 관절의 처짐을 메웁니다.
  - 전체 실행을 녹화하면 실제 팔 위치가 섞여 재생이 덜컥거리던 것을 고쳤습니다. Motion Record 기본 30 fps.
  - 속도 슬라이더가 3D 미리보기 · 실제 팔 · 녹화의 속도를 함께 바꿉니다.
- 모터 셋업 — 중앙(2048) 이동 통과 기준을 ±5 → ±10 으로 넓혔습니다.

### 수정
- **로봇 저장 — robot id 를 바꾸면 로봇이 로봇 창고에서 사라지고 '이미 같은 robot id' 오류가 반복되던 것** (예: lekiwi05). 같은 id 는 저장 전에 거절하고, 실패하면 원래 상태로 되돌립니다.
- 앱 아이콘을 바꿨습니다 (설치 파일이 31 MB → 19 MB 로 가벼워졌습니다).

### 설치
```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.2.0/physical-labs_0.6.0-0.2.0_amd64.deb
sudo apt install ./physical-labs_0.6.0-0.2.0_amd64.deb
# 그 전에 0.2.0 을 설치한 PC:
sudo apt install --reinstall ./physical-labs_0.6.0-0.2.0_amd64.deb
```
SHA256: `9ead9879f478b763c46f082c793bf449dee05412f29fc5ee7ff94e02456ffbf4`

Windows 최신은 [v0.6.0-0.1.7](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.1.7) 입니다 (새 A-Go · 엔드이펙터 · 워크스페이스 개선 미포함).

사용 설명서: https://roboseasy.ai/docs/physical-labs
