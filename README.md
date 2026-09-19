> ## 🆕 최신 Linux 릴리즈: [v0.6.0-0.0.17](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.17) (2026-09-17)
>
> ```bash
> wget https://github.com/roboseasy/physical-labs-app-deploy/releases/download/v0.6.0-0.0.17/physical-labs_0.6.0-0.0.17_amd64.deb
> sudo apt install ./physical-labs_0.6.0-0.0.17_amd64.deb
> ```
> **앱 안 라이브러리 설치 경로 재점검** — 새 학습 옵션의 NVIDIA GROOT 배너 [설치] 가 관리자 권한 없이 실행돼 실패하던 문제,
> `sudo pip` 로 직접 설치한 적이 있는 PC 에서 `[Errno 13]` 으로 실패하던 문제 수정(권한 오류 시 시스템 비밀번호 창으로 자동 재시도).
> 실패 시 터미널용 `sudo …` 명령을 로그에 안내. 0.0.16 의 설치 권한 수정·0.0.12 의 FFmpeg 의존성 등 포함.
> SHA256 `2c51f04d9a17f5c6507dc224514fda14bef004a097aa6e43ec2669fc67e73d8c`.
> Windows 최신은 [v0.6.0-0.0.15](https://github.com/roboseasy/physical-labs-app-deploy/releases/tag/v0.6.0-0.0.15).

# Physical Labs — 배포 (Releases)

이 저장소는 **Physical Labs**의 배포(릴리즈) 전용 공개 저장소입니다.

> 📛 이 제품은 이전에 **Roboseasy Studio** 라는 이름이었습니다 (2026-07 리네임).
> 기존 사용자의 업그레이드 방법은 [RELEASE_NOTES.md](RELEASE_NOTES.md) 를 참고하세요.

설치 파일(.deb, .exe)은 [Releases](https://github.com/roboseasy/physical-labs-app-deploy/releases) 페이지에서 다운로드할 수 있습니다.

- Ubuntu 24.04+: `.deb` 패키지
- Windows 10/11: `.exe` 인스톨러

설치 가이드: [install_ko.md](install_ko.md)
