---
layout: single
title: "[AWS] EC2 인스턴스를 WSL2로 원격접속 해보자 "
categories: AWS
tag: [aws, wsl2, ubuntu]
published: true
---

# AWS-EC2를 WSL2에서 ubuntu를 이용해 접속해보았다.

생활코딩 강의로 AWS EC2의 인스턴스로 원격 접속하는 과정을 공부 중 보통 윈도우 환경에서는 xshell이나 putty로 원격접속을 한다. 하지만 나는 그냥 wsl2의 ubuntu를 써보고 싶어서 여기저기 조사를 통해 연결해보았다. 연결을 시도할 때 계속 UNPROTECTED PRIVATE KEY FILE! 에러가 발생해서 고생했지만 계속된 시도 끝에 성공했다!

## openssh-server 설치

```shell
sudo apt update
sudo apt install openssh-server
```

## SSH 실행

WSL2 환경에서는 systemctl 명령어가 되지 않기 때문에 service를 이용해 실행해주어야한다.

```shell
sudo service ssh start
```

---

## 원격 접속을 하기 전에 ssh의 설정을 변경하자

```shell
sudo vi /etc/ssh/sshd_config
```

**ssh 접속 포트를 다르게 변경하자**

기존 설정되어있는 22는 윈도우 자체 내장 SSH서버 포트 번호이기 때문에 변경해주어야 한다.

```shell
Port 22 # 22가 아닌 다른 포트번호로 설정하자
```

**패스워드인증 설정을 변경하자**

SSH Key를 사용할 것이기 때문에 no로 설정

```shell
PasswordAuthentication yes # no로 바꿔주자
```

**설정을 변경했으면 ssh를 재시작 해주자**

```shell
sudo service ssh restart
```

---

## 윈도우에서 키 페어 파일 권한 설정

원격접속을 할 때 키 페어 파일의 권한을 설정해주어한다.  
chmod 400를 사용해 권한을 변경 해주면 되는데 **WSL2는 chmod를 바로 지원하지 않아 따로 설정을 해주어야 한다.**

해당 명령어를 통해 chmod를 사용 가능하게 해주자

```shell
sudo umount /mnt/c
sudo mount -t drvfs C: /mnt/c -o metadata
```
/mnt/c 디렉토리에서 해당 명령어 실행시 프로세스가 이미 실행 중이기에 **target is busy**라는 메세지가 발생한다.
이 때는 cd ...으로 디렉토리 밖으로 나와서 명령어를 실행해주어야 한다.

chmod 400으로 파일 권한을 설정해주자

```shell
sudo chmod 400 keyfile.pem
```

사실 처음 권한 설정할 때 WSL2에서 chmod가 되지 않아 윈도우에서 해당 파일 속성으로 들어가 직접 권한 설정을 해주었는데
후에 chmod가 간단한 설정 변경으로 가능하다는 것을 알게되었다...

## 원격 접속하기

접속할 때 해당 키 파일이 있는 곳에서 실행해야한다.

```shell
sudo ssh -i "keyfile.pem" <user>@ip
```

![정상 실행](https://user-images.githubusercontent.com/77107216/184963721-4676a0cf-5f0c-4a6e-832e-ca9863290370.png)

정상 접속되는 것을 볼 수 있다!

---

**잘못된 정보 또는 오타가 기재되어있을 경우 피드백해주시면 감사하겠습니다!**
