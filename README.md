> ## 🆕 최신 Linux 릴리즈: [v0.6.0-0.2.0](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.2.0) (2026-11-01 재배포)
>
> ```bash
> wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.2.0/physical-labs_0.6.0-0.2.0_amd64.deb
> sudo apt install ./physical-labs_0.6.0-0.2.0_amd64.deb
> ```
> **새 A-Go(ROS 2 LeKiwi)에서 엔드이펙터 · 워크스페이스(Yolo + Pick&Place)가 열립니다**, **Teaching Control 재생 재현율 개선** (SO-101 · A-Go), **로봇 저장 시 robot id 중복 오류 수정** (예: lekiwi05).
> 2026-11-01 저녁에 같은 0.2.0 으로 다시 올렸습니다 — 그 전 0.2.0 을 설치했다면 `sudo apt install --reinstall ./physical-labs_0.6.0-0.2.0_amd64.deb`. 사용 설명서: https://roboseasy.ai/docs/physical-labs
> SHA256 `9ead9879f478b763c46f082c793bf449dee05412f29fc5ee7ff94e02456ffbf4`.
> Windows 최신은 [v0.6.0-0.1.7](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.1.7) (2026-10-22) —
> [physical-labs-setup_0.6.0-0.1.7_win64.exe](https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.1.7/physical-labs-setup_0.6.0-0.1.7_win64.exe),
> SHA256 `7988c028ba155571284f5212d20f77d3f8e716fcdbb8269b898967f2cff6a775`.

# Physical Labs — 배포 (Releases)

이 저장소는 **Physical Labs**의 배포(릴리즈) 전용 공개 저장소입니다.

> 📛 이 제품은 이전에 **Roboseasy Studio** 라는 이름이었습니다 (2026-07 리네임).
> 기존 사용자의 업그레이드 방법은 [install_ko.md](install_ko.md) 4.1절을 참고하세요.

설치 파일(.deb, .exe)은 [Releases](https://github.com/roboseasy/physical-labs-app-deploy/releases) 페이지에서 다운로드할 수 있습니다.

- Ubuntu 24.04+: `.deb` 패키지
- Windows 10/11: `.exe` 인스톨러

설치 가이드: [install_ko.md](install_ko.md)
