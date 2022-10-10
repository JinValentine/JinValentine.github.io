---
layout: single
title: "[AWS] CodeDeploy 배포 오류 발생과 해결 "
categories: AWS
tag: [aws, linux, codedeploy]
published: true
---

# CodeDeploy로 배포할 때 발생한 오류 해결하기

## 문제상황😥

CI/CD를 위해 Github Action으로 S3에 zip파일을 저장, 보관하고 CodeDeploy로 배포를 하는 과정이였다.  
Github Action에서는 무사히 성공했다고 나오지만 EC2 서버에는 배포되어야할 파일이 디렉토리를 확인해보니 없었다..
![github action 성공](https://user-images.githubusercontent.com/77107216/194939456-0886d54c-5057-48d1-aa2b-64b1cbee6888.png)
문제를 찾기 위해 AWS에 접속해 CodeDeploy 배포 과정을 살펴보니 배포 중에 오류가 발생한 것이였다.
![오류발생](https://user-images.githubusercontent.com/77107216/194933621-5647842b-c26c-47df-88eb-84f9c09d837e.png)

원인을 찾아봐야겠다

## 원인😂

원인을 찾기 위해서 우선 EC2서버에 codedeploy-agent가 실행 중인 것부터 확인해보았다.

```linux
sudo service codedeploy-agent status
```

잘 실행 되고 있다.

```linux
The AWS CodeDeploy agent is running as PID
```

이번에는 codedeploy의 log를 봐야겠다는 생각에 log를 볼 수 있는 경로로 가보았다.

```linux
/var/log/aws/codedeploy-agent/codedeploy-agent.log
```

tail 명령어로 log를 확인해보았다.
apppspec.yml을 찾을 수 없다는 내용의 log들
![log확인](https://user-images.githubusercontent.com/77107216/194933627-9c053147-577f-4ee3-8322-efb1dcda3557.png)

배포를 할 때 AWS CodeDeploy의 설정이 담겨져 있는 appspec.yml을 인식하지 못하고 있는 것 같다. 그래서 appspec.yml의 위치를 재확인하고 오타도 재확인 하고 다시 배포해보았지만 여전히 발생하는 오류..

원인을 찾기 위해 공식문서를 참조하고 검색을 계속 해보았다.
그 결과 **배포단계에서 오류가 날 경우 계속 배포 시도를 해도 마지막에 성공했던 배포 내용을 참조한다는 것**을 알게 되었다.

해당 위치로 가서 배포 내용을 참조하는 경로를 알아보았다.

```linux
cd /opt/codedeploy-agent/deployment-root/deployment-instructions/
```

명령어를 통해 deployment-archive 내에 배포내용의 경로를 알 수 있었다.

```linux
cat ****.****.****_last_successful_install
```

찾아가보니 문제의 appspec.yml을 발견

![문제발견](https://user-images.githubusercontent.com/77107216/194933629-3e6d74bb-3710-49ef-bdd1-7f15ed0020dc.png)

appspec.yml의 오타로 인해 배포를 하여도 계속 이 경로를 참조하고 있어 제대로 된 appspec.yml을 인식하지 못해 계속해서 오류가 발생했던 것이였다.😱

## 해결😀

해당 yml을 수정하고 나서 실패했던 배포가 무사히 배포되어 성공하였고 EC2 서버에도 파일이 들어왔다.
![성공](https://user-images.githubusercontent.com/77107216/194933630-0ea93b38-44af-4254-8818-b1bf8dc7d9d7.png)

## 추가해결방법😲

CodeDeploy에서 원인을 찾기 힘든 오류가 발생할 때는 EC2 서버의 codedeploy-agent를 삭제해주고 재설치해주면 되는 경우도 있었다.  
혹시 모르니 한번 시도해보자!

---

**잘못된 정보 또는 오타가 기재되어있을 경우 피드백해주시면 감사하겠습니다!**
