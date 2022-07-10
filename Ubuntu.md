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

