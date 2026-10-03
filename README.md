> ## 🆕 최신 Linux 릴리즈: [v0.6.0-0.1.2](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.1.2) (2026-10-03)
>
> ```bash
> wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.1.2/physical-labs_0.6.0-0.1.2_amd64.deb
> sudo apt install ./physical-labs_0.6.0-0.1.2_amd64.deb
> ```
> **일부 PC 에서 학습이 시작 직후 멈추던 문제 수정** — GPU 버전 PyTorch 의 영상 디코더가 쓰는 NVIDIA NPP 라이브러리를 함께 설치하고,
> 훈련 탭 › 환경 진단에 "영상 디코더" 확인·설치 항목을 추가했습니다. LeKiwi 호스트가 정지되지 않을 때 앱 안 [강제 정지] 버튼 포함.
> SHA256 `69b3f6577e51378e5eb79a328f3eddcfe51b78bb80e17be64f277f708fc11297`.
> Windows 최신은 [v0.6.0-0.1.1](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.1.1).

# Physical Labs — 배포 (Releases)

이 저장소는 **Physical Labs**의 배포(릴리즈) 전용 공개 저장소입니다.

> 📛 이 제품은 이전에 **Roboseasy Studio** 라는 이름이었습니다 (2026-07 리네임).
> 기존 사용자의 업그레이드 방법은 [RELEASE_NOTES.md](RELEASE_NOTES.md) 를 참고하세요.

설치 파일(.deb, .exe)은 [Releases](https://github.com/roboseasy/physical-labs-app-deploy/releases) 페이지에서 다운로드할 수 있습니다.

- Ubuntu 24.04+: `.deb` 패키지
- Windows 10/11: `.exe` 인스톨러

설치 가이드: [install_ko.md](install_ko.md)
