flowchart LR
    A[Python Data Simulator] -->|Feeds| B[Kafka Producer]
    B -->|Publishes| C[(Kafka Cluster\nAWS EC2)]
    C -->|Streams| D[Kafka Consumer]
    D -->|Stores in| E[(PostgreSQL DB)]
    E -->|Crawled by| F[AWS Glue]
    F -->|Query via| G[Amazon Athena]
