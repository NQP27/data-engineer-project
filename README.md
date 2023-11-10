## Table of Contents
- [Introduction](#introduction)
- [System Architecture](#system-architecture)
- [Technologies](#technologies)
- [Getting Started](#getting-started)

## Introduction
An nd-to-end data engineering pipeline project utilizing Apache Airflow, Python, Apache Kafka, Apache Zookeeper, Apache Spark, and Cassandra. Everything is containerized using Docker.


## System Architecture
![System Architecture](https://github.com/NQP27/data-engineer-project/blob/main/images/system_architecture.png)

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
    venv\Scripts\activate
    ```

3. Create necessary folders:
    ```bash
    mkdir dags
    mkdir script
    mkdir requirements
    ```
4. Create kafka_stream.py in dags folder, this file will stream api's data to kafka via airflow.
5. Create spark_stream in root folder, this file will get data from kafka and load them to cassandra.
6. Create requirements.txt in requirements folder, this file contain necessary dependencies while using docker. 
7. Create entrypoint.sh in script folder, used to install dependencies on requirements.txt and initialize sirflow application as a web server.
8. Create docker-compose.yml in root folder, docker-compose.yml is a tool for managing and deploying containers in a Docker environment.
9. We need 2 java files: spark-sql-kafka-0-10_2.12:3.5.0,jar, spark-cassandra-connector_2.13:3.4.1.jar to run spark_stream.py. I downloaded them from https://mvnrepository.com and located them in E:\worksapce\data-engineer\venv\Lib\site-packages\pyspark\jars
10. In root folder, use this command to run docker environment
    ```bash
    docker-compose up -d
    ```
    ![Run Docker](https://github.com/NQP27/data-engineer-project/blob/main/images/docker-compose-up.png)
11. Wait a few minutes then go to http://localhost:8080/ (Airlow UI) to run dags
      ![Airflow UI](https://github.com/NQP27/data-engineer-project/blob/main/images/airflow-ui.png)
      ![Airflow run Dags](https://github.com/NQP27/data-engineer-project/blob/main/images/airflow-run.png)
12. Go to http://localhost:9021/ (Kafka Control Center), we can see data streamed from API via airflow
      ![DKafka Control Center](https://github.com/NQP27/data-engineer-project/blob/main/images/control-center.png)
13. Back to the terminal, run this command to load data from kafka to cassandra:
   ```bash
   spark-submit --master spark://localhost:7077 --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.0,com.datastax.spark:spark-cassandra-connector_2.13:3.4.1 spark_stream.py
   ```
13. Spark is running and you can see it in http://localhost:9090/    
14. Check the data in cassandra: 
    - Run this command to access cassandra:
    ```bash
       docker exec -it cassandra cqlsh -u cassandra -p cassandra localhost 9042
    ```
    - To querry the data:
    ```bash
       select * from spark_streams.created_users;
    ```

                                                


    
