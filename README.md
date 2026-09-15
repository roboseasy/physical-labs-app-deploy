> ## 🆕 최신 Linux 릴리즈: [v0.6.0-0.0.16](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.16) (2026-09-16)
>
> ```bash
> wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.16/physical-labs_0.6.0-0.0.16_amd64.deb
> sudo apt install ./physical-labs_0.6.0-0.0.16_amd64.deb
> ```
> **앱 안 라이브러리 설치 수정** — 워크스페이스 Yolo + Pick&Place 의 [설치](ultralytics)와 학습 탭 SmolVLA / X-VLA /
> NVIDIA GROOT 의존성 설치가 `[Errno 13] Permission denied` 로 실패하던 문제. 이제 시스템 비밀번호 창으로 설치합니다.
> ultralytics 8.4.153 고정. 0.0.12 의 FFmpeg 의존성·Yolo + Pick&Place 워크스페이스 등 포함.
> SHA256 `a2d7d1d88796e9828f15c6c753c62926ea802f1b815da019707d219bb47870ad`.
> Windows 최신은 [v0.6.0-0.0.15](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.15).

# Physical Labs — 배포 (Releases)

이 저장소는 **Physical Labs**의 배포(릴리즈) 전용 공개 저장소입니다.

> 📛 이 제품은 이전에 **Roboseasy Studio** 라는 이름이었습니다 (2026-07 리네임).
> 기존 사용자의 업그레이드 방법은 [RELEASE_NOTES.md](RELEASE_NOTES.md) 를 참고하세요.

설치 파일(.deb, .exe)은 [Releases](https://github.com/roboseasy/physical-labs-app-deploy/releases) 페이지에서 다운로드할 수 있습니다.

- Ubuntu 24.04+: `.deb` 패키지
- Windows 10/11: `.exe` 인스톨러

설치 가이드: [install_ko.md](install_ko.md)
