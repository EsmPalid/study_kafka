# 01. 왜 Kafka를 공부를 시작했는가?

> 보상 트랜잭션을 구현하기 위해서(정확히는 Coreography SAGA을 구현하기 위해) 아니면 DDD 이론을 배우다가 Aggregate를 나누는 기준 중 하나가 Event라는 말을 듣고 EDA -> Message/queue로 넘어가서(?) 사실 기억이 가물가물함

일단, Kafka를 이용해서 보상 트랜잭션을 구현하는 것이 목적임<br>
도메인과 이벤트는 간단한 온라인 전자상거래가 적절해 보임<br>
&nbsp;&nbsp;&nbsp;&nbsp;Ex] 주문->재고->결제<br>
// 실제 결제 방식까지 들어가는건 복잡해지므로 간단하게 구현해야함<br>

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

        -   SSL
        -   SASL
        -   ACLs

    -   Config값(Docker 환경변수)

        -   Partition key 사용 여부
        -   Listener 통신 방법(SSL 및 인증) / 외부 내부 통신망 설정
        -   Producer -> Server 간 EOS 달성을 위한 Transaction ID 사용
        -   isolation.level을 read_committed로 설정
        -   enable.auto.commit을 false로 설정
        -   ISR를 위한 min.insync.replicas 설정 사용 여부
        -   지연 복제 판단 replica.lag.time.max.ms
        -   로그 삭제 방법 판단(Time or Size / Log Compaction)

-   **Zookeeper 또는 KRaft Mode로 동작하는 Controller**

-   **Kafka Client API(Node.js의 경우 KafkaJS)**

    -   Outbox 패턴 구현
    -   EoS 구현
    -   일괄 처리 구현

-   **Kafka Connect API**

    -   학습중...
    -   독립형 vs 분산 모드
    -   Plugin과 Connector
    -   Worker 설정과 Connector 설정
    -   REST API
    -   Source Connector 그리고 Sink Connector

-   **~~Kafka Streams~~<일단 보류>**<br>
    Kafka Streams API가 Java 언어 기반으로 알고 있음(Java 문법을 배워야함) 지금 당장 ESP 방식을 사용하기 보다 Batch processing 방식으로 데이터 파이프라인을 구현하는게 우선적으로 보임
