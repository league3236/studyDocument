===============

Visual studio code가 제공하는 주요 기능

- 디버그 기능
- 구문 하이라이트
- IntelliSense
- Git과의 연계
- 태스크 자동 실행
- 확장 기능 임베디드
- 통합 터미널 기능

==============

Home-brew 패키지 매니저를 통하여 azure-cli 설치하기

```bash
$ brew update && brew install azure-cli

설치 확인
$kubectl version

Client Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.5", GitCommit:"20c265fef0741dd71a66480e35bd69f18351daea", GitTreeState:"clean", BuildDate:"2019-10-15T19:16:51Z", GoVersion:"go1.12.10", Compiler:"gc", Platform:"darwin/amd64"}
```

Azure contianer registry

azure가 제공하는 컨테이너 이미지 공유 서비스.
- 여러 리전 간에서 레지스트 관리
- 보안과 CI/CD 연계
- 컨테이너 이미지의 자동 빌드
- 



Azure login
```
$ az login
```

Azure 서비스 이용하기 위한 리소스 프로바이더 활성화
```
$ az provider register -n Microsoft.Network
$ az provider register -n Microsoft.Storage
$ az provider register -n Microsoft.Compute
$ az provider register -n Microsoft.ContainerService
```

=============
