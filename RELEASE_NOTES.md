# Physical Labs v0.6.0-0.2.0 (Linux) — 2026-11-01 재배포

> 2026-11-01 오후에 같은 0.2.0 으로 다시 올렸습니다. **오전에 0.2.0 을 이미 설치했다면 `--reinstall` 을 붙여야 바뀝니다** (버전이 같아 그냥 설치하면 "이미 최신" 으로 건너뜁니다).

### 새 기능
- **새 A-Go(ROS 2 LeKiwi)에서 엔드이펙터 탭을 씁니다** — 🔌 연결 · Sync 확인 · Joint · XYZ 조작 · 화살표 바퀴 · Teaching Control(자유 이동 포함) · Motion Record / Replay.
  - 속도 슬라이더가 팔이 움직이는 속도입니다 (Motion Replay 는 녹화된 속도 그대로).
  - 힘 슬라이더는 흉내입니다 — 목표가 실제 위치보다 앞설 수 있는 폭을 줄여 미는 힘 · 쥐는 힘을 약하게 합니다.
  - 자유 이동은 로봇이 명령 세션을 닫을 때까지 2초쯤 뒤에 힘이 빠집니다. 끝낼 때는 로봇이 토크를 켠 것을 확인한 뒤 '토크 켜짐' 을 알립니다.
- **Teaching Control 재생 재현율 개선 (SO-101 · A-Go)**
  - 저장한 자세가 중력 때문에 1~3° 낮게 재생되던 것 — 멈춰 있는 관절의 처짐을 메웁니다.
  - 전체 실행을 녹화하면 실제 팔 위치가 섞여 재생이 덜컥거리던 것을 고쳤습니다. Motion Record 기본 30 fps.
  - 속도 슬라이더가 3D 미리보기 · 실제 팔 · 녹화의 속도를 함께 바꿉니다.
- 모터 셋업 — 중앙(2048) 이동 통과 기준을 ±5 → ±10 으로 넓혔습니다.

### 설치
```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.2.0/physical-labs_0.6.0-0.2.0_amd64.deb
sudo apt install ./physical-labs_0.6.0-0.2.0_amd64.deb
# 오전에 0.2.0 을 설치한 PC:
sudo apt install --reinstall ./physical-labs_0.6.0-0.2.0_amd64.deb
```
SHA256: `284496ec8441876b92c4ee16f8dfb46018d29d8bc1d74d40e3171f36cd7fe1a8`

Windows 최신은 [v0.6.0-0.1.7](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.1.7) 입니다 (새 A-Go · 엔드이펙터 개선 미포함).

사용 설명서: https://roboseasy.ai/docs/physical-labs
