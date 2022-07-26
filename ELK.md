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
- 빌드 및 실행
`docker-compose build && docker-compose up -d`

- 종료
`docker-compose down -v`

- 로그
`docker-compose logs`

- 시작 / 정지
`docker-compose start/stop`

- 포트 표시
`docker-compose port` >> ??

#### 접속
Elasticsearch : 9200 / 9300
Logstash : 5000 / 9600
Kibana : 5601

#### elasticsearch에 nori 플러그인 설치
#####  elasticsearch의 Dockerfile에 아래 코드를 추가해도 문제 없다.
`RUN elasticsearch-plugin install analysis-nori`

- bash shell 접근
```
docker exec -it docker_elk_elasticsearch_1 /bin/bash
```

- analysis-nori plug-in 설치
```
cd /usr/share/elasticsearch/bin/
./elasticsearch-plugin install analysis-nori
```

- user_dictionary 파일 생성
```
cd /usr/share/elasticsearch/config
vi userdict_ko.txt
```

- curl 명령을 이용해서 es 클러스터 조회
`curl -XGET -u [elasticID]:[elasticPW] "localhost:9200"`

- curl 명령을 이용해서 노리 실행 예시
curl -XPOST "[서버ip:elastic_port]/_analyze?pretty" -H 'Content-Type: application/json' -d'
{"analyzer":"nori", "text":"우리는 차를 살 수 있을까"}'

- 또는 kibana의 dev Tools를 사용해서 쿼리를 날린다.

- Index analyzer 생성
kibana로 들어가서 Management > Dev Tools > Console에 아래 내용 입력
세팅을 설정할 때, mappings도 같이 설정해 주면 되나, 만약 어려울 경우 PUT 인덱스명/_mapping 을 사용해 추가할 수 있다.
단 자동으로 필드가 추가되지 않았을 경우에!
```
PUT my_index
{
  "settings": {
    "index": {
      "number_of_shards": "3",
      "number_of_replicas": "0",
      "analysis": {
        "tokenizer": {
          "nori_user_dict": {
            "type": "nori_tokenizer",
            "decompound_mode": "mixed",
            "user_dictionary": "userdict_ko.txt"
          }
        },
        "analyzer": {
          "my_analyzer": {
            "type": "custom",
            "tokenizer": "nori_user_dict"
          }
        }
      }
    }
  }
}
```

- 도큐먼트 입력
```
PUT my_index/_doc/1
{
  "title": "별 헤는 밤",
  "author": "윤동주",
  "category": "시",
  "publish_date": "1948-01-01T00:00:00",
  "content": """계절이 지나가는 하늘에는
가을로 가득 차 있습니다.

나는 아무 걱정도 없이
가을 속의 별들을 다 헤일 듯합니다.

가슴 속에 하나 둘 새겨지는 별을
이제 다 못 헤는 것은
쉬이 아침이 오는 까닭이요,
내일 밤이 남은 까닭이요,
아직 나의 청춘이 다하지 않은 까닭입니다.

별 하나에 추억과
별 하나에 사랑과
별 하나에 쓸쓸함과
별 하나에 동경과
별 하나에 시와
별 하나에 어머니, 어머니,

어머님, 나는 별 하나에 아름다운 말 한마디씩 불러 봅니다. 소학교 때 책상을 같이 했던 아이들의 이름과, 패, 경, 옥, 이런 이국 소녀들의 이름과, 벌써 아기 어머니 된 계집애들의 이름과, 가난한 이웃 사람들의 이름과, 비둘기, 강아지, 토끼, 노새, 노루, '프랑시스 잠[1]', '라이너 마리아 릴케[2]' 이런 시인의 이름을 불러 봅니다.

이네들은 너무나 멀리 있습니다.
별이 아스라이 멀듯이.

어머님,
그리고 당신은 멀리 북간도에 계십니다.

나는 무엇인지 그리워
이 많은 별빛이 내린 언덕 위에
내 이름자를 써 보고
흙으로 덮어 버리었습니다.

따는 밤을 새워 우는 벌레는
부끄러운 이름을 슬퍼하는 까닭입니다.

그러나 겨울이 지나고 나의 별에도 봄이 오면
무덤 위에 파란 잔디가 피어나듯이
내 이름자 묻힌 언덕 위에도
자랑처럼 풀이 무성할 거외다.
"""
}
```

#### Elastic search 가용 용량 확인
`curl -XGET -u [elastic]:[PW] "http://localhost:9200/_cat/allocation?v"`

#### 나중에 참고해볼만한 내용
https://utto.tistory.com/35
