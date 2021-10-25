# Kafka_foot
The project is to build a football based event with the help of kafka system
This is a new project

## Add a connector to Kafka Connect

1 - Add a volume to store plugin configs for connect in the docker-compose.yml

2 - Add the connector within the container : 
```
docker exec -it connect confluent-hub install confluentinc/kafka-connect-elasticsearch:5.4.0
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
   "connection.url": "http://10.0.0.175:9200",
   "tasks.max": "1",
   "topics": "simple.elasticsearch.data",
   "type.name": "_doc",
   "value.converter": "org.apache.kafka.connect.json.JsonConverter", 
   "value.converter.schemas.enable": "false",
   "schema.ignore": "true",
   "key.ignore": "true"
 }
}'
```
