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