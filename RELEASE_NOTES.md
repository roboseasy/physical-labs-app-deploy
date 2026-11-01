# Physical Labs v0.6.0-0.2.0 (Linux)

### 바뀐 점
- **모터 셋업 — 중앙(2048) 이동 통과 기준을 ±5 → ±10 으로 넓혔습니다.** 모터가 중앙 근처에서 멈췄는데도 오차 몇 칸 때문에 '실패' 로 나오던 경우가 줄어듭니다.
- 0.1.9 의 모든 기능(ROS 2 LeKiwi · SO-102 · 데이터 수집 업로드 수정)이 그대로 들어 있습니다.
- 배포 저장소의 지난 릴리즈를 정리했습니다. 0.1.x 이하를 설치한 PC 도 아래 명령으로 그대로 업데이트됩니다.

### 설치
```bash
wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.2.0/physical-labs_0.6.0-0.2.0_amd64.deb
sudo apt install ./physical-labs_0.6.0-0.2.0_amd64.deb
```
SHA256: `eb82c75489af9d5e1b8c9943ec2cd05686f27e882a387c0e14768abb9fe89e0a`

Windows 최신은 [v0.6.0-0.1.7](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.1.7) 입니다.

사용 설명서: https://roboseasy.ai/docs/physical-labs
