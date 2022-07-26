# Jenkins 세팅

- apt 업데이트
`apt-get update`

- jdk8 설치
`sudo apt-get install openjdk-8-jdk`

- jenkins 저장소 key 다운로드
`wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -`

`Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).`
경고 문구에 주의

- sources.list에 추가
`echo deb http://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list`