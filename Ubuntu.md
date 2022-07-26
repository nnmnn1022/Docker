# Ubuntu
## sudo 설치
- sudo를 따로 설치해야 되는지 몰랐음.

1. sudo 설치
`apt-get update && apt-get install -y sudo`

2. 사용자 계정 추가
```
adduser --disabled-password --gecos "" umoo \
&& echo 'umoo:umoo' | chpasswd \
&& adduser umoo sudo \
&& echo 'umoo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
```

3. 비밀번호 설정
- `sudo passwd`

참고자료 : https://yongho1037.tistory.com/720

## apt 업데이트

1. `sudo apt update`
2. `sudo apt-get install software-properties-common`


## yum 업데이트
`apt install yum` 으로 yum을 설치

`E: Unable to locate package yum`
위 에러는 ubuntu에서 package를 다운로드 받지 못해서 나오는 에러.

`cd /etc/apt` 이동 후 sources.list 백업.
`sudo cp sources.list sources.list.back`

`vim sources.list`
```
deb http://archive.ubuntu.com/ubuntu bionic main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu bionic-security main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu bionic-updates main restricted universe multiverse
```
추가

## vim 다운로드
`apt-get update`
`apt-get install vim`
