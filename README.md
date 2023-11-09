# data-engineer-project
## Table of Contents
- [Introduction](#introduction)
- [System Architecture](#system-architecture)
- [Technologies](#technologies)
- [Getting Started](#getting-started)

## Introduction
An nd-to-end data engineering pipeline project utilizing Apache Airflow, Python, Apache Kafka, Apache Zookeeper, Apache Spark, and Cassandra. Everything is containerized using Docker.


## System Architecture
![System Architecture](https://github.com/NQP27/data-engineer-project/blob/main/system_architecture.png)

The project is designed with the following components:

- **Data Source**: I use `randomuser.me` API to generate random user data for our pipeline.
- **Apache Airflow**: Responsible for orchestrating the pipeline and storing fetched data in a PostgreSQL database.
- **Apache Kafka and Zookeeper**: Used for streaming data from PostgreSQL to the processing engine.
- **Control Center and Schema Registry**: Helps in monitoring and schema management of our Kafka streams.
- **Apache Spark**: For data processing with its master and worker nodes.
- **Cassandra**: Where the processed data will be stored.

## Technologies

- Apache Airflow
- Python
- Apache Kafka
- Apache Zookeeper
- Apache Spark
- Cassandra
- PostgreSQL
- Docker

## Getting Started

1. Create folder data-engineer:
    ```bash
    mkdir data-engineer
    cd data-engineer
    ```

2. Create virtual environment:
    ```bash
    python -m venv venv
    ```

3. Create file dags and script:
    ```bash
    mkdir dags
    mkdir script
    ```
