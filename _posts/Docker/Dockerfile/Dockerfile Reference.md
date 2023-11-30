Dockerfile은 Docker 이미지 (image)를 만들기 위한 명령어 스크립트 정도로 볼 수 있다.
아래 내용은 정리하면서 기억하기 위해 작성한 내용들이다.
- [원본링크](https://docs.docker.com/engine/reference/builder/)
### Format 샘플

```dockerfile
# Comment
INSTRUCTION arguments
```
명령어는 대소문자를 구분하지는 않지만 일반적으로는 대문자로 쓰는 것이 관례이다. 

### FROM 명령어

```dockerfile
FROM [--platform=<platform>] <image> [AS <name>]
```

```dockerfile
FROM [--platform=<platform>] <image>[:<tag>] [AS <name>]
```

```dockerfile
FROM [--platform=<platform>] <image>[@<digest>] [AS <name>]
```

`FROM` 명령어는 Docker 이미지를 만들기 위한 부모 이미지 (사용 할 이미지) 정보를 기입한다.
> `--plafrom` 파라미터는 Docker 컨테이너를 특정 플랫폼에 대한 이미지로 빌드할 때 사용되는 옵션이다. (e.g OS)

```dockerfile
FROM ubuntu:latest
```
- 간략한 `FROM` 예시

`FROM` 명령어보다 먼저 올 수 있는 것들로는 **parser directives, comments** 와 전역으로 설정한 **ARGs** 정도이다. 

Dockerfile에서 유효한 **parser directives** 가 아니라면 `#`으로 시작하는 라인은 주석으로 처리 하게 된다. 다른 라인 속 `#`은 **arguments** 로서 처리가 된다.

```dockerfile
# Comment
RUN echo 'we are running some # of cool things'
```
- 실제 Dockerfile이 실행 될 때 모든 주석들은 제거 후 실행 된다.

```dockerfile
        # this is a comment-line
    RUN echo hello
RUN echo world
```

```dockerfile
# this is a comment-line
RUN echo hello
RUN echo world
```
- 위 둘의 Dockerfile은 공백을 무시하고 동일한 기능을 수행하겠지만, 공백은 넣지 않는게 좋다.

### 환경 변수
