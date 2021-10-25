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
