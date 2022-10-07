---
layout: single
title: "[AWS] EC2에서 쉘 스크립트로 배포를 할 때 발생한 Unable to access jarfile 오류 "
categories: AWS
tag: [aws, linux, shell script]
published: true
---

# 쉘 스크립트로 배포를 할 때 발생한 Unable to access jarfile 오류의 원인과 해결

## 문제상황:cry:

웹 애플리케이션을 무중단 배포하기 위해 EC2 Linux 서버에 Spring Boot 프로젝트를 git clone으로 복사해 넣어주었다.  
배포를 위해 빌드 후에 nohup 명령어에 properties들의 경로를 설정해주고 터미널을 종료해도 애플리케이션이 계속 구동될 수 있도록 하였다.

마지막으로 nohup 명령어를 실행 후 정상적으로 서비스가 잘 배포되었는지 확인하기 위해 nohup.out의 로그를 확인하니 톰캣이 시작했다는 로그가 아닌 **해당 오류**가 발생한다.

![원인](https://user-images.githubusercontent.com/77107216/194506758-0298171f-fb1b-4f13-9369-89e6655dfce4.png)

jar파일에 액세스할수 없다고 한다. 무엇이 문제일까?

## 원인:joy:

오류 로그를 보니 배포를 해주는 쉘 스크립트에 문제가 있는 것 같아 계속해서 오타를 찾아보니 오타는 없었다. 그래서 검색을 통해 다른 사람들이 쉘 스크립트를 사용한 것을 보고 해결책을 찾을 수 있었다.  
**\ 문자를 사용한 후에는 엔터로 줄을 바꿔야 한다.**  
나 같은 경우는 그냥 한 줄로 다 적어버려서 생긴 문제였다.
![nohup 수정전](https://user-images.githubusercontent.com/77107216/194505100-878c1d26-e192-48a6-9fee-4d39e93f64ba.png)

## 해결:smiley:

\문자 후에 줄 바꿈으로 nohup 명령어를 수정하였다.
![nohup 수정완료](https://user-images.githubusercontent.com/77107216/194505120-7bc7e1be-1204-4cc6-8ef7-76fe169a1288.png)

쉘 스크립트를 실행 후에 nohup.out의 로그를 확인해보니 정상적으로 실행이 된 것을 확인할 수 있었다.

![해결](https://user-images.githubusercontent.com/77107216/194505125-e7747b01-d8c8-4c77-98f5-da08cfd2ef63.png)

---

**잘못된 정보 또는 오타가 기재되어있을 경우 피드백해주시면 감사하겠습니다!**
