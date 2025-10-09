# 01. 왜 Kafka를 공부를 시작했는가?

> 보상 트랜잭션을 구현하기 위해서(정확히는 Coreography SAGA을 구현하기 위해) 아니면 DDD 이론을 배우다가 Aggregate를 나누는 기준 중 하나가 Event라는 말을 듣고 EDA -> Message/queue로 넘어가서(?) 사실 기억이 가물가물함

# 02. 준비물(지식) / 진행과정

-   **Kafka Server(Broker)**

    -   Design

        -   Producer
        -   Message Delivery Semantics
        -   Consumer
        -   Transation
        -   Replication
        -   Log Compaction

    -   Opeartion

    -   Security

        -   SSL (○)
        -   SASL (△)
        -   ACLs (X)

-   **Zookeeper 또는 KRaft Mode로 동작하는 Controller**

-   **Kafka Client API(Node.js의 경우 KafkaJS)**

    -   Outbox 패턴 구현
        CDC툴 필요함
    -   EoS 구현
        inbox 테이블 운영?
    -   일괄 처리 구현
        Producer -> Broker로 메시지를 보낼 때, size 또는 message 개수에 따라서

-   **Kafka Connect API**

    -   학습중...
    -   독립형 vs 분산 모드
    -   Plugin과 Connector
    -   Worker 설정과 Connector 설정
    -   REST API
    -   Source Connector 그리고 Sink Connector

-   **~~Kafka Streams~~<일단 보류>**<br>
    Kafka Streams API가 Java 언어 기반으로 알고 있음(Java 문법을 배워야함) 지금 당장 ESP 방식을 사용하기 보다 Batch processing 방식으로 데이터 파이프라인을 구현하는게 우선적으로 보임

# 03. 각종 설정값

## 03-1. apache/kafka Docker설정

-   Partition key 사용 여부(Optional)
-   Listener 통신 방법(SSL 및 SASL인증), INTERNAL/EXTERNAL 통신망 설정

    -   Broker Listener 옵션

        -   KAFKA_LISTENERS
        -   KAFKA_ADVERTISED_LISTENERS
        -   KAFKA_INTER_BROKER_LISTENER_NAME
        -   KAFKA_CONTROLLER_LISTENER_NAMES
        -   KAFKA_LISTENER_SECURITY_PROCOTOL_MAP
        -   KAFKA_CONTROLLER_QUORUM_VOTERS

    -   Broker 필수 SSL 옵션

        -   KAFKA_SSL_KEYSTORE_LOCATION
        -   KAFKA_SSL_KEYSTORE_PASSWORD
        -   KAFKA_SSL_TRUSTRSTORE_LOCATION
        -   KAFKA_SSL_TRUSTSTORE_PASSWORD
        -   KAFKA_SSL_KEY_PASSWORD

    -   Broker 선택 SSL 옵션

        -   KAFKA_SSL_CLIENT_AUTH= none | requested | required
        -   KAFKA_ENABLED_PROTOCOLS= TLSv1.2, TLSv1.3
        -   KAFKA_KEYSTORE_TYPE= PKCS12
        -   KAFKA_TRUSTSTORE_TYPE... 등등

-   Producer -> Server 간 EOS 달성을 위한 Transaction ID 사용 옵션

    -   Broker Config
        -   isolation.level= read_committed
        -   read_committed= false

-   Replication 관련 설정

    -   min.insync.replicas(ISR, Kafbat-ui에서 설정 가능)
    -   replica.lag.time.max.ms(지연 복제 판단?)

-   로그 삭제 방법 판단(Time or Size / Log Compaction)

    -   cleanup.policy= compact | delete
    -   Broker Config(Compact)
        -   min.compaction.lag.ms - 메시지 기록 후 압축되기까지 경과해야하는 최소 시간
        -   max.compaction.lag.ms - 메시지 기록 시점과 압축 가능 시점 사이의 최대 지연 시간
    -   Broker Config(Delete)
        -   retension.ms(Kafbat-ui에서 설정 가능)
        -   retension.bytes(Kafbat-ui에서 설정 가능)
        -   Etc...
    -   Compact와 Delete 혼합 사용 가능한듯?

-   KafkaJS 설정

    -   Client Config

        -   brokers 설정(Listener)
        -   SSL(암호화) 및 SASL/ACLs(인증)
        -   Connection Timeout 및 Request Timeout
        -   Retry(재시도)
        -   Logging

-   Kafka Connector API 설정

    -   독립 vs 분산 모드
    -   Worker 설정
        -   bootstrap.servers
        -   plugin.path
        -   group.id
        -   config.storage.topic
        -   offset.storage.topic
        -   status.storage.topic

-   Debezium for MariaDB Connector 설정
    -   ???
