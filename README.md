# Kafka_foot
The project is to build a football based event with the help of kafka system
This is a new project

## Add a connector to Kafka Connect

1 - Add a volume to store plugin configs for connect in the docker-compose.yml

2 - Add the connector within the container : 
```
docker exec -it connect confluent-hub install confluentinc/kafka-connect-elasticsearch:5.4.0 --no-prompt
```
3 - Restart the connect container : 
```
docker restart connect
```
4 - Check in the control center that the plugin has been added

5 - Add the connector as follow : (for JSON format values)
```
curl -X POST http://localhost:8083/connectors -H "Content-Type: application/json" -d '{
  "name": "simple-elasticsearch-connector",
  "config": {
    "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
    "tasks.max": "1",
    "key.converter": "org.apache.kafka.connect.json.JsonConverter",
    "value.converter": "org.apache.kafka.connect.json.JsonConverter",
    "transforms": "insertTS, TimestampConverter",
    "topics": "test4",
    "transforms.insertTS.type": "org.apache.kafka.connect.transforms.InsertField$Value",
    "transforms.insertTS.timestamp.field": "timestamp",
    "transforms.TimestampConverter.type": "org.apache.kafka.connect.transforms.TimestampConverter$Value",
    "transforms.TimestampConverter.target.type": "unix",
    "transforms.TimestampConverter.field": "timestamp",
    "transforms.TimestampConverter.format": "yyyy-MM-dd HH:mm:ss",
    "connection.url": "http://10.0.0.175:9200",
    "type.name": "_doc",
    "key.ignore": "true",
    "schema.ignore": "true",
    "key.converter.schemas.enable": "false",
    "value.converter.schemas.enable": "false"
  }
}'
```
6 - Check the connect container logs to see if the worker started properly !
