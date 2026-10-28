# Releases와 Packages

## 일반 설치: Releases

[최신 Release](https://github.com/kkt9102/NetMaru/releases/latest)에서 `NetMaru-arm64.dmg`를 받으세요. 최신 버전의 고정 다운로드 주소는 다음과 같습니다.

[NetMaru-arm64.dmg](https://github.com/kkt9102/NetMaru/releases/latest/download/NetMaru-arm64.dmg)

각 Release에는 DMG·ZIP·SHA256SUMS·MIT LICENSE·개인정보 및 외부 구성요소 고지가 함께 있습니다. GitHub Packages 계정 인증이나 Docker가 없어도 Release 설치파일을 받을 수 있습니다.

## 고급 배포: GitHub Packages

패키지: `ghcr.io/kkt9102/netmaru`

이 이미지는 **macOS 설치파일과 고지를 보관하는 배포 이미지**입니다. Linux에서 NetMaru를 실행하는 컨테이너가 아닙니다. 일반 사용자는 Releases를 사용하세요.

Releases를 게시하면 `.github/workflows/publish-package.yml`이 Release 파일의 SHA-256을 검증한 뒤 GHCR에 버전 태그와 `latest`를 게시합니다. 작업 권한은 해당 저장소의 `contents: read`, `packages: write`로 제한합니다. 개인 PAT를 저장소나 workflow에 넣지 않고 GitHub가 실행마다 발급하는 토큰을 사용합니다.

패키지 공개 후 Docker로 설치파일만 꺼내려면 컨테이너를 실행하지 않고 다음과 같이 복사할 수 있습니다.

```sh
docker pull ghcr.io/kkt9102/netmaru:1.1.2
docker create --name netmaru-installer ghcr.io/kkt9102/netmaru:1.1.2 /not-executed
docker cp netmaru-installer:/bundle/NetMaru-arm64.dmg ./NetMaru-arm64.dmg
docker rm netmaru-installer
```

이미지는 GitHub의 Linux x86_64 실행기에서 생성됩니다. 다른 CPU에서 추출할 때는 `docker pull`과 `docker create`에 `--platform linux/amd64`를 지정할 수 있습니다. 컨테이너를 시작할 필요가 없습니다.

GitHub는 개인 계정의 새 Packages를 기본적으로 비공개로 생성합니다. 최초 게시 후 패키지 설정의 공개 상태를 확인해야 하며, 비공개 상태에서는 소유자 또는 읽기 권한이 있는 계정의 인증이 필요합니다. 저장소가 공개라고 패키지까지 자동으로 공개되는 것은 아닙니다.

공식 문서: [지원 형식](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages), [공개 범위 설정](https://docs.github.com/en/packages/learn-github-packages/configuring-a-packages-access-control-and-visibility).
