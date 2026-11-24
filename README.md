# Real-Time Financial Market Streaming Data Pipeline

An end-to-end real-time event streaming pipeline that ingests live stock market tick data from public financial REST APIs into **Apache Kafka**, processes rolling window aggregations via **PySpark Structured Streaming**, and persists raw and curated data into **MongoDB** and **MySQL**.

## Architecture
\Financial REST API\ -> \Python Kafka Producer\ -> \Apache Kafka Topic\ -> \PySpark Structured Streaming\ -> \MongoDB (Raw JSON) & MySQL (Aggregated Metrics)\

## Project Structure
- \producer/kafka_producer.py\: Polls live market quotes (with rate-limit backoff and historical replay mode) and publishes JSON events to Kafka.
- \spark_streaming/stream_processor.py\: Consumes Kafka streams, computes 5-minute rolling moving averages and volume metrics, and writes to dual sinks.
- \sql/schema.sql\: MySQL table definitions and indexes for aggregated market metrics.
- \docker-compose.yml\: Local containerized setup for Kafka, Zookeeper, MongoDB, and MySQL.
