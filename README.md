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

# How to run

    docker-compose up --detach
