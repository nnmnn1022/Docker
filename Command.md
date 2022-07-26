# Docker Command

1.  `docker ps [-a]` :
docker 에 돌아가는 모든 컨테이너 확인

2. `docker images` :
docker 에 있는 모든 이미지 확인

3. `docker system df` :
docker 내 이미지들 용량 확인

4. `docker pull CNAME_IMAGE` :
이미지 다운로드

5. `docker search CNAME_IMAGE` :
이미지 검색

6. `docker run [--name 이름] [-d(백그라운드)] [-p(포트) 80:80] CNAME_IMAGE`
도커에 있는 이미지를 이름 지정, 포트 지정하여 백그라운드에 실행
앞에 포트는 docker HOST port / 뒤에 포트는 docker Container port 

7. `docker rmi CNAME_IMAGE` :
이미지 삭제

8. `docker stop CONTAINER` :
컨테이너 중지

9. `docker start CONTAINER` :
중지했던 컨테이너 실행

10. `docker rm [--force] CONTAINER` : 
컨테이너 삭제

11. `docker logs [-f(지속적으로 보기)] CONTAINER` :
도커 로그 확인

12. `docker exec [OPTIONS] CONTAINER COMMAND`
도커 컨테이너에 실행하고 싶은 내용 전달

13. `docker exec -it CONTAINER /bin/bash(sh)` :
shell 프로그램이 사용자가 입력한 내용을 전달받아 운영체제에게 전달
-it 옵션이 지속적으로 전달 가능하도록 함.
exit 을 통해 나갈 수 있음

14. `docker run -p 80:80 -v ~/host경로:~/container안의 경로/ CONTAINER`
HOST 환경을 사용하여 작업을 할 수 있는 서버 설정

15. 

## Docker build 파일 만들기
1. docker build (`-t 이름`) `PATH` > 이미지 만들기

2. docker run ~~~ > Container 만들기

- `docker commit CONTAINER IMAGE_NAME` 사용하여 이미지로 만들 수 있다.

## Dockerfile 명령어
1. FROM : 운영체제를 가져오는 듯

2. RUN : linux 명령어 실행 // 빌드가 되는 시점에 실행

3. WORKDIR : 디렉토리 없으면 만들고, 사용자를 이동하고, 이제부터 시작하는 RUN / ENTRY POINT / 등이 실행될 때 저 곳에서 실행.

4. CMD : [] 대괄호 안에 넣어서 // 컨테이너 실행 시에 실행

5. 명령어를 자동으로 실행되지 않게 하려면, docker run 명령을 입력할 때 맨 뒤에 pwd라고 입력하면, cmd 대신 명령을 입력할 수 있음 (like overriding)