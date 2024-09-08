# Build End-to-End Streaming Application using Flink SQL、Kafka、MySQL、Elasticsearch and Kibana.

<img width="451" alt="图片2" src="https://user-images.githubusercontent.com/5378924/79943461-838bdc80-849b-11ea-81f4-b28b31e03176.png">

You can download the data here: https://drive.google.com/file/d/1P4BAZnpCY-knMt5HFfcx3onVjykYt3et/view?usp=sharing

This is a repository to build the dockers which will be used in the tuturial.

Blog: https://flink.apache.org/2020/07/28/flink-sql-demo-building-e2e-streaming-application.html

# How to build

## build ibnummuhammad/datagen:0.2

    mvn clean package
    cp target/flink-sql-demo.jar datagen/flink-sql-demo.jar
    cd datagen/
    cp ~/Downloads/user_behavior.log ~/Documents/github/ibnummuhammad/flink-sql-demo/datagen
    docker build . --tag ibnummuhammad/datagen:0.2

## build ibnummuhammad/demo-sql-client:0.2

    cd sql-client
    docker build . --tag ibnummuhammad/demo-sql-client:0.2

## build ibnummuhammad/mysql-example:0.2

    cd mysql
    docker build . --tag ibnummuhammad/mysql-example:0.2

# How to run

    docker-compose up --detach

# How to add table

```
CREATE TABLE user_behavior (
    user_id BIGINT,
    item_id BIGINT,
    category_id BIGINT,
    behavior STRING,
    ts TIMESTAMP(3),
    proctime AS PROCTIME(),   -- generates processing-time attribute using computed column
    WATERMARK FOR ts AS ts - INTERVAL '5' SECOND  -- defines watermark on ts column, marks ts as event-time attribute
) WITH (
    'connector' = 'kafka',  -- using kafka connector
    'topic' = 'user_behavior',  -- kafka topic
    'scan.startup.mode' = 'earliest-offset',  -- reading from the beginning
    'properties.bootstrap.servers' = 'kafka:9092',  -- kafka broker address
    'format' = 'json'  -- the data format is json
);
```
