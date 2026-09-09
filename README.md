> ## 🆕 최신 Linux 릴리즈: [v0.6.0-0.0.12](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.12) (2026-09-09)
>
> ```bash
> wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.12/physical-labs_0.6.0-0.0.12_amd64.deb
> sudo apt install ./physical-labs_0.6.0-0.0.12_amd64.deb
> ```
> **설치 수정** — 학습 시작 시 `Could not load libtorchcodec … libavdevice.so.60` 로 죽던 문제. `.deb` 의존성에
> `ffmpeg` 추가, 설치 마지막에 영상 디코더 로드 확인. 앱 기능은 0.0.11 과 동일
> (워크스페이스 Yolo + Pick&Place, LeKiwi 와이파이 설정·바퀴 주행·Motion Record/Replay 포함).
> SHA256 `ad4057d64fd646bf86ceba596955ea0c430201128843fba7f89c52c0a447cb06`.

# Physical Labs — 배포 (Releases)

이 저장소는 **Physical Labs**의 배포(릴리즈) 전용 공개 저장소입니다.

> 📛 이 제품은 이전에 **Roboseasy Studio** 라는 이름이었습니다 (2026-07 리네임).
> 기존 사용자의 업그레이드 방법은 [RELEASE_NOTES.md](RELEASE_NOTES.md) 를 참고하세요.

설치 파일(.deb, .exe)은 [Releases](https://github.com/roboseasy/physical-labs-app-deploy/releases) 페이지에서 다운로드할 수 있습니다.

- Ubuntu 24.04+: `.deb` 패키지
- Windows 10/11: `.exe` 인스톨러

설치 가이드: [install_ko.md](install_ko.md)
