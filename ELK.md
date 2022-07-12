# ELK Stack 설치

## JAVA 설치

1. `sudo apt-get update`
2. `sudo apt-get install openjdk-8-jdk`
3. 환경 변수 설정
4. `vim /etc/profile` // root에 설치
profile 가장 아래에 아래 내용 추가
```
export JAVA_HOME=/usr/lib/[java-8-openjdk-amd64]
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=$CLASSPATH:$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar
```
5. `source /etc/profile` 

3-1. `vim ~/.bashrc` // 특정 계정에 적용
```
export JAVA_HOME=/usr/lib/jvm/[java-8-openjdk-amd64]
export PATH=${PATH}:${JAVA_HOME}/bin
```
3-2. `source ~/.bashrc`


## ELK Stack 다운로드 및 설치
#### 다운로드
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.3.deb
wget https://artifacts.elastic.co/downloads/logstash/logstash-5.4.3.deb
wget https://artifacts.elastic.co/downloads/kibana/kibana-5.4.3-amd64.deb
wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-5.4.3-amd64.deb
```
#### 설치
```
sudo dpkg -i elasticsearch-5.4.3.deb && \
sudo dpkg -i logstash-5.4.3.deb && \
sudo dpkg -i kibana-5.4.3-amd64.deb && \
sudo dpkg -i filebeat-5.4.3-amd64.deb
```

오류가 많다..
현재 문제 : NAT 관련 세팅이 되어있지 않아 ELK 설치가 진행되지 않음.

>>> Docker-compose를 사용해서 깔려 있는 최신 ELK stack을 사용하기로 함.

#### Git clone
`git clone https://github.com/deviantony/docker-elk`

#### Elasticsearch에서 X-pack(유료) X
해당 내용 제거

#### Docker 빌드 & 실행, 종료
- 실행
`docker-compose build && docker-compose up -d`

- 종료
`docker-compose down -v`

#### 접속
Elasticsearch : 9200 / 9300
Logstash : 5000 / 9600
Kibana : 5601