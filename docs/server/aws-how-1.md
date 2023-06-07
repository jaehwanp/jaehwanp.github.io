---
layout: default
title: '[AWS] AWS'
parent: aws
nav_order: 1
---

## 인스턴스 설정 (free tier)

AWS 콘솔에서 인스턴스 시작 버튼을 누름

1. 원하는 이름, 원하는 OS를 설정.

<img width="709" alt="image" src="https://user-images.githubusercontent.com/45479802/228190970-8aad6aea-600e-4117-9069-aa0337245057.png">

2. 키페어 생성

<img width="540" alt="image" src="https://user-images.githubusercontent.com/45479802/228192010-3475ac4b-49b9-4f44-8968-04587162a2f1.png">

3. 네트워크 설정

모든 IP에서 들어갈 수있게 SSH트래픽허용 (0.0.0.0/0)으로 설정함

---

주의사항

12개월 후 돈내야함

(다시 ec2 만들어서 배포하면 가능)

> 프리 티어: 첫 해에는 월별 프리 티어 AMI에 대한 t2.micro(또는 t2.micro를 사용할 수 없는 리전의 t3.micro) 인스턴스 사용량 750시간, EBS 스토리지 30GiB, IO 2백만 개, 스냅샷 1GB, 인터넷 대역폭 100GB가 포함됩니다.

---

## 에러
(Load key "***.pem": Operation not permitted)

<img width="436" alt="image" src="https://user-images.githubusercontent.com/45479802/228750675-5e6cfa9c-4344-42c4-a219-d03dd87c94d6.png">


<img width="827" alt="image" src="https://user-images.githubusercontent.com/45479802/228751090-13d3ab86-672e-4be4-ba05-043ac7355f43.png">

설정 > 개인정보 보안 및 보안 > 전체 디스크 접근 권한

<img width="827" alt="image" src="https://user-images.githubusercontent.com/45479802/228751375-30d3ed1a-6211-4865-968b-a22014d161fe.png">

터미널을 체크한다.

![image](https://user-images.githubusercontent.com/45479802/228805165-b3d56966-e4d4-47d1-9b28-1863afe4a10b.png)

연결 완료 화면

---

## docker 설치 및 설정

```sh
# yum package update
$ sudo yum -y update

# install docker
$ sudo yum install docker -y

# check docker version
$ docker -v

# start docker service
$ sudo service docker start

# 파일 권한 변경 (docker 서비스시 필요)
$ sudo chmod 666 /var/run/docker.sock

```
-y : 설치과정의 모든 질문을 yes로 입력


---

## jdk 설치

```sh
# intallable java version
$ yum search java*

# install java
$ sudo yum install java-11-amazon-corretto.x86_64 -y

# check the java version
$ java -version
```

![image](https://user-images.githubusercontent.com/45479802/228798320-b1b63c1f-58ac-4abb-92da-0dd961b05b3e.png)

<img alt="image" src="https://user-images.githubusercontent.com/45479802/228798998-01fca39f-5f18-4c1a-8fa2-028c5778822e.png">



---

## DB

DB : mariadb

왠만해서는 RDS 쓰는게 좋지만 가벼운 테스트 프로젝트이므로 docker 내 db를 설치함.

### docker volume

```sh
# docker volume 생성
# sudo docker volume create [volume명]
$ sudo docker volume create mariadb-vol
```
<details>
<summary>docker volume 명령어</summary>
<div markdown="1">

```sh
# docker volume 조회
$ docker volume ls

# 해당 볼륨 자세한 정보
$ docker volume inspect [volume명]

# 제거
$ docker volume rm [volume명]

# 사용하지않는 모든 로컬 볼륨 삭제
$ docker volume prune
```


</div>
</details>

### docker 내 DB 이미지 불러오기

```sh
# mariadb 설치
$ docker pull mariadb/server:latest

$ docker images
```
<img width="514" alt="스크린샷 2023-03-30 오후 7 32 21" src="https://user-images.githubusercontent.com/45479802/228809684-e273f64c-cff5-4c18-a8f6-0f9a9046e85e.png">

### docker 컨테이너 마운트

```sh
# mount
# docker run --name [container명] -e MARIADB_ROOT_PASSWORD=[DB비번] -d -p [ec2 port]:[docker port] mariadb:latest
$ docker run --name mariadb_cont -e MARIADB_ROOT_PASSWORD=1234 -d -p 3306:3306 mariadb:latest

# container list
$ docker ps
```

### 외부 DB tool 연결

<img width="894" alt="image" src="https://user-images.githubusercontent.com/45479802/228844197-f0af6672-cae9-41f1-8800-0ecd17da78a2.png">