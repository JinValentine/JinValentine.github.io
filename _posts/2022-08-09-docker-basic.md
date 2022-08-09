---
layout: single
title: "[Docker] Docker 이해하기 (기본)"
categories: Docker
tag: Docker
published: true
---

# Docker란 무엇일까? 기본 명령어와 기능들에 대해 알아보았다.

## Docker란?

- Docker는 vmware, virtualbox와 같은 가상 머신처럼 독립된 실행환경을 제공한다.
- 운영체제가 Window, MacOS여도 Docker가 가상머신을 만들어주고 리눅스 환경을 만들어준다.
- 컴퓨터에 직접 애플리케이션을 설치한 것과 같이 빠르다.
- apt, npm, pip 처럼 명령어 한줄로 원하는 앱이 포함된 실행환경을 손쉽게 설치할 수 있는 개발환경을 제공한다.

## Docker에서 쓰이는 용어

**docker hub**: 필요한 소프트웨어를 찾을 수 있는 곳

**image** : 다운(pull)받은 소프트웨어

**container** : image를 실행(run)하면 생성되는 공간

## 명령어들

```shell
docker images # pull한 image들 확인

docker run (image) # 실행(run)해서 container로 만들기

docker stop (컨테이너 ID or 이름) # 실행중인 container를 중단

docker start (이름) # Exited 된 container를 실행

docker ps # run중인 image들 확인

docker ps -a # 실행, 중단중인 container 확인

docker logs (이름) # 로그 출력

docker logs -f (이름) # 로그 실시간 출력

docker rm (이름) # container 삭제 (실행중이라면 삭제되지 않는다.)

docker rm --force (이름) # container가 실행중이여도 강제 삭제

docker rmi (image 이름) # image 삭제

docker exec (컨테이너 이름)(명령어) # host에서 컨테이너안의 명령어를 사용할 때

docker exec -it (컨테이너 이름) /bin/sh # 컨테이너와 지속적으로 연결하는 것
# (bash 쉘은 /bin/bash)
# 이때부터는 CLI는 해당 컨테이너를 대상으로 해서 명령어를 내리는 것이다.
# pwd할 경우 해당 컨테이너의 디렉토리를 알려준다.
# exit할 경우 해당 컨테이너에서 빠져나온다.
```

---

## Apache의 경우

Docker에서 Apache의 image이름은 **httpd**이다.

Docker에서 Web Server를 구축할 때는 Container의 Port와 Host의 Port는 별도로 되어있다.

### Docker에서 Port

보통 http://example.com:80/index.html로 접속하면 포트번호 80의 index.html을 불러오지만
Docker환경에서는 Host안에 Container가 있기 때문에 아파치 Web Server가 들어있는 컨테이너의 index.html를
불러오기 위해서는 Host의 포트번호와 Container의 포트번호를 연결시켜야 index.html을 불러올 수 있다.

```shell
docker run -p (Host의 포트번호):(Container의 포트번호) httpd # port forwarding이라고 부른다.
```

해당 명령어를 통해 Host의 포트번호와 Container의 포트번호를 연결시켜줄 수 있다.

Apache(httpd)의 index.html은 컨테이너 안 /usr/local/apache2/htdocs/ 경로에 있다.

index.html를 수정하기 위해서는 에디터가 직접 설치해야한다. (컨테이너는 저용량을 추구하기 때문에 에디터가 없다.)

```shell script
apt -update
apt install (에디터)
```

명령어를 통해 에디터 중 하나를 설치해서 index.html을 수정할 수 있다.

## Docker의 volume을 사용해보자

volume을 사용하게 되면 Host의 파일 시스템과 Container의 파일을 연결하여 파일시스템에 변경이 있을 시에 컨테이너 파일도 같이 변경되게 할 수 있다.

### volume의 명령어

```shell
docker run -it -v (호스트 디렉토리):(컨테이너의 volume 디렉토리) (이미지) /bin/bash
```

### 실습

volume을 활용해 새로운 Apache 컨테이너를 생성하고 Host 파일시스템과 연결하여 index.html의 내용을 변경해보았다.

```shell
docker run -p 8001:80 -v C:\Users\(유저이름)\Desktop\htdocs:/usr/local/apache2/htdocs/ httpd
```

나는 윈도우를 사용하기 때문에 명령 프롬프트에 해당 명령어를 입력했다.
이후 파일시스템 경로에 있는 index.html의 내용을 VsCode로 변경하였고 컨테이너 안의 index.html의 내용이 바뀐 것을 확인할 수 있었다.

![33](https://user-images.githubusercontent.com/77107216/183675219-f704ca76-962c-4f5e-88dd-e06e3176dd30.png)

---

### 참조

https://opentutorials.org/course/4781

**잘못된 정보 또는 오타가 기재되어있을 경우 피드백해주시면 감사하겠습니다!**
