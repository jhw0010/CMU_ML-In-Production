# Lab 2: Kafka for Data Streaming

## 🎯 Learning Objectives

- Understand Apache Kafka architecture (topics, offsets, partitions, brokers)
- Implement producer-consumer patterns for real-time data streaming
- Use Kafka CLI tools (kcat) for topic management and monitoring
- Explore offset management and consumer group concepts

## 🛠️ Technical Setup

**Environment:**
- WSL2 (Ubuntu 24.04)
- Apache Kafka 3.9.0
- Python 3.12 with kafka-python library
- kcat CLI tool

**Architecture:**
- Local Kafka broker running on `localhost:9092`
- ZooKeeper for cluster coordination
- Single partition topic for weather data streaming

## 📝 What I Built

### Producer Mode
- Created a Kafka producer that generates weather data
- Published 10 messages to topic `weather-wujinho1`
- Messages contain: timestamp, city, temperature
- Cities: Toronto, Guangzhou, Fuzhou

### Consumer Mode
- Implemented a Kafka consumer with `auto_offset_reset='earliest'`
- Read all messages from the topic
- Saved output to `kafka_log.csv`
- Demonstrated offset management and message persistence

### CLI Tools (kcat)
- Listed all topics and broker metadata
- Consumed messages from earliest offset using command line
- Verified message delivery and topic configuration

## 🔑 Key Concepts Learned

**Topics:** Named channels for organizing message streams

**Offsets:** Sequential message IDs that enable fault-tolerant consumption. If a consumer disconnects, it can resume from its last committed offset.

**auto_offset_reset Tradeoffs:**
- `earliest`: Reads all historical messages (good for reprocessing, bad for large backlogs)
- `latest`: Only reads new messages (good for real-time, bad if you need history)

**Partitions:** Enable parallel processing and scalability (this lab used 1 partition)

## 📂 Files

- `KafkaDemo.ipynb` - Jupyter notebook with producer/consumer implementation
- `kafka_log.csv` - Sample output from consumer

## 🚀 How to Run

1. Start Kafka services:
```bash
# Terminal 1: ZooKeeper
bin/zookeeper-server-start.sh config/zookeeper.properties

# Terminal 2: Kafka Broker
bin/kafka-server-start.sh config/server.properties
```

2. Run the notebook:
```bash
jupyter notebook KafkaDemo.ipynb
```

3. Use kcat to verify:
```bash
kcat -b localhost:9092 -t weather-wujinho1 -C -o earliest
```

## 💡 Key Takeaways

- Kafka provides durable, fault-tolerant message streaming
- Producer/consumer decoupling enables scalable architectures
- Offset management is critical for exactly-once processing guarantees
- CLI tools are essential for debugging and monitoring production systems

---

*Part of self-study coursework based on CMU's Machine Learning in Production course*
