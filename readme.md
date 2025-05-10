
# 📈 Kafka Stock Market Data Pipeline on AWS ☁️
##Real-time stock market data simulation, streaming with Kafka, and analysis with AWS Glue & Athena

AWS
Kafka
Python
PostgreSQL

🌟 Features
✔ Real-time stock market simulation (Python)
✔ Kafka Producer (AWS EC2) pushing live stock data
✔ Kafka Consumer storing data in PostgreSQL
✔ AWS Glue Crawler for automatic schema detection
✔ Amazon Athena for SQL-based analytics

## 📊 Data Flow Architecture

## 📊 Data Flow Architecture

```mermaid
flowchart LR
    A[Python Data Simulator] -->|Feeds| B[Kafka Producer]
    B -->|Publishes| C[(Kafka Cluster\nAWS EC2)]
    C -->|Streams| D[Kafka Consumer]
    D -->|Stores in| E[(PostgreSQL DB)]
    E -->|Crawled by| F[AWS Glue]
    F -->|Query via| G[Amazon Athena]
````
    
🚀 Quick Setup



1️⃣ Kafka EC2 Setup
# Install Kafka on Amazon Linux 2023
# Better to use JDK 17
sudo yum install -y java-1.8.0

wget https://archive.apache.org/dist/kafka/3.8.0/kafka_2.12-3.8.0.tgz
tar -xzf kafka_2.12-3.8.0.tgz
cd kafka_2.12-3.8.0


2️⃣ Clone & Run
git clone https://github.com/tushar-rb/kafka-stock.git
cd kafka-stock

🛠 Usage:

📤 Start Producer (Simulate Data)
python producer/simulator.py \
  --bootstrap_servers <EC2_IP>:9092 \
  --topic stock-data \
  --interval 1  # emits every 1 sec

📥 Start Consumer (Store in DB)
python consumer/consumer.py \
  --bootstrap_servers <EC2_IP>:9092 \
  --topic stock-data \
  --db_url postgresql://user:pass@host/db

🔍 Analyze with Athena
Set up Glue Crawler → Scan PostgreSQL table

Run SQL Queries in Athena:
SELECT symbol, AVG(price) 
FROM stock_data 
WHERE ts > NOW() - INTERVAL '1' DAY 
GROUP BY symbol;

