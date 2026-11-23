# Physical Labs v0.6.0-0.2.1 (Linux) — 2026-11-23

### 새 기능
- **워크스페이스 "물류지능화" (새 A-Go · ROS 2 LeKiwi)** — 블록을 이어 흐름을 만들고 실제 로봇으로 실행합니다.
  - 블록: 코드(명령 실행) · 자율주행 켜기/끄기 · YOLO 판정(팔레트 기다리기 · ACT 끝내기) · 모션 · 정책 · 조건.
  - 코드 블록의 출력을 변수에 담아 조건 갈래를 고를 수 있습니다.
  - 바퀴 토크가 꺼져 멈추면 한 실행에 두 번까지 스스로 복구합니다. 비상 정지 · 연결 끊김은 스스로 풀지 않습니다.
  - 흐름은 `~/.PhysicalLabs/flows/` 에 저장됩니다.
- **Dual SO-102 기종 추가** — 로봇 설정(리더 2대) · 캘리브레이션 · 텔레옵 · 모션 녹화/재생 · 데이터 수집 · 학습 · 추론. 엔드이펙터 탭은 아직 지원하지 않습니다.
- **YOLO-ACT (act_bbox)**
  - 데이터 수집: '입력 데이터 추가' 로 YOLO bbox 를 함께 기록합니다 (카메라 박스 표시 · 클래스별 conf 임계값 · 편집 탭 재생).
  - 훈련: ACT 입력 데이터를 RGB / bbox 중에서 고릅니다.
  - 추론: YOLO-ACT 실행, YOLO 가중치 직접 고르기, LeKiwi 는 [바퀴도 정책이 몰기].
- **클라우드 GPU 학습** — 클라우드에서 학습을 돌리고 작업 목록 · 진행 상태를 보고 결과 모델을 내려받습니다. 설정에서 계정별 GPU 사용량 · 차감 내역을 봅니다.
- **훈련 탭 조기 종료** — loss 가 정한 step 수 동안 낮아지지 않으면 그 체크포인트를 저장하고 멈춥니다.
- **데이터 수집** — 새 데이터셋을 수집하기 전에 기록 방식을 고릅니다 (텔레옵-레코딩 / 티칭-레코딩은 준비 중).
- **SO-101 엔드이펙터** — 중력 처짐 보정, Teaching Sync 에 속도 · 힘 반영.
- 단일 모터 화면 — 스캔 범위를 ID 0~30 으로 넓혔습니다.

### 수정
- **학습 재개** — 목표 step 전에 멈춘 학습을 원래 목표 step 까지 이어서 돌릴 수 있습니다.
- **데이터 수집 끝 알림** — 저장소 이름이 빈칸이고 에피소드 수가 늘 0개로 뜨던 것.
- 데이터 수집 일시정지 / 재녹화 오류.
- 로그인 세션이 유지되지 않던 것.
- 클라우드에서 학습한 모델을 GPU 없는 PC 에서 추론하지 못하던 것.

### 설치
```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.2.1/physical-labs_0.6.0-0.2.1_amd64.deb
sudo apt install ./physical-labs_0.6.0-0.2.1_amd64.deb
```
SHA256: `81a8f96979c84f749abe55d28574471758a94c818db46cb134326f12244379cf`

> ⚠️ Dual SO-102 로봇을 등록한 PC 에서는 0.2.0 이하로 되돌리지 마세요 — 옛 버전은 그 로봇을 SO-101 로 잘못 봅니다.

Windows 최신은 [v0.6.0-0.1.7](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.1.7) 입니다 (이번 릴리즈 내용 미포함).

사용 설명서: https://roboseasy.ai/docs/physical-labs

---

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
