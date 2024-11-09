Dockerfile →(build)→ Docker Image →(run)→ Docker Container

**도커 이미지** : 하둡/스파크/스톰/MySQL 등

**도커 컨테이너**: → 이미지의 목적에 맞는 파일이 들어 있는 파일 시스템과 격리된 시스템 자원 및 네트워크 사용할 수 있는 독립된 공간이 생성되고 도커 컨테이너가 됨! 

- 컨테이너는 이미지에 영향을 주지 X
- 컨테이너는 호스트와 분리
- 컨테이너 간은 분리

```json
#버전 확인
docker -v

#이미지 빌드 
docker run -i -t 저장소/이미지이름:태그
(로컬에서 못찾으면 중앙에서 내려받음)

ls

exit

#이미지 내려받기
docker pull centos:7

#이미지 목록 확인
docker images 

#컨테이너 생성(컨테이너 안으로 들어가진 X)
docker create -i -t --name mycentos centos:7

	#컨테이너 시작
	docker start mycentos

	#컨테이너 진입
	docerk attach mycentos
	
#생성시작진입 한 번에 하려면 run해주면되는거같음

#컨테이너 목록 확인
docker ps

#컨테이너 정지
docker stop angry_morse

#컨테이너 삭제 
docker rm angry_morse

#삭제확인
docker ps -a

#모든 컨테이너 삭제
docker container prune

#포트에 바인딩(호스트포트:컨테이너포트) (특정IP:호스트포트:컨테이너)
docker run -i -t --name mywebserver -p 80:80 ubuntu:14.04
docker run -i -t -p 3306:3306 -p 192.168.0.100:7777:80 ubuntu:14.04

#컨테이너 생성해서 내부로 들어가서 아파치 웹 서버 실행
apt-get update
apt-get install apache2 -y
service apache2 start
```

![image](https://github.com/user-attachments/assets/d3e1c6f5-e04a-4b1a-bc04-15a20297dc0d)
![image](https://github.com/user-attachments/assets/1572c52a-f88f-4054-8eda-712e05e50a47)

**컨테이너 애플리케이션 구축**
![image](https://github.com/user-attachments/assets/a59e41d4-b7b6-45fc-b098-541a8c8708aa)

- 왼편보다는 오른편이 원래 도커의 목적

**도커 볼륨**

- mysql 컨테이너 삭제하면 컨테이너 계층에 저장돼있던 DB 정보도 삭제된다는 치명적 단점을 보완하고자 나온 것
- 호스트와 볼륨 공유할 수도 있고 볼륨 컨테이너 활용할 수도 있음

## 도커 이미지

```json
#도커 이미지 만들 컨테이너 생성
docker run -i -t --name commit_test ubuntu:14.04

#docker commit 명령어로 컨테이너를 이미지로 만들기
docker commit [OPTIONS] CONTAINER [REPOSITORY:TAG]]

#이미지 생성
docker commit \ -a "alicek106"(작성자데이터) -m "my first commit"(부가설명) \ commit_test \ commit_test:first
```

## docker file
![image](https://github.com/user-attachments/assets/95361a34-7ef5-45a5-961a-b3e68a77d32e)

from 베이스 이미지

maintainer 개발자 정보

label 메타데이터

run 컨테이너 내부의 명령어

add 파일을 이미지에 추가workdir 명령어 실행할 디렉터리

expose 노출할 포트

cmd실행할 명령어 커맨드 설정 한번만 사용할수 있음. 

```json
docker build -t mybuild:0.0 ./

# -t는 이미지 이름 설정. mybuild:0.0 이미지 이름 
```
