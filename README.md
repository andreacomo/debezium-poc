# Debezium POC
Implementation based on:

https://debezium.io/documentation/reference/1.6/tutorial.html

https://github.com/debezium/debezium-examples/tree/master/tutorial

To setup MySql connector: (see https://debezium.io/documentation/reference/configuration/topic-auto-create-config.html)

* go to http://localhost:9002
* create a new MySql connector with config:

```
name=inventory-connector
connector.class=io.debezium.connector.mysql.MySqlConnector
database.user=debezium
database.server.id=184054
tasks.max=1
database.hostname=mysql
database.password=dbz
database.history.kafka.bootstrap.servers=kafka:9092
database.history.kafka.topic=schema-changes.inventory
database.server.name=dbserver1
database.port=3306

topic.creation.default.replication.factor=1
topic.creation.default.partitions=1
topic.creation.default.cleanup.policy=delete

topic.creation.groups=inventory
topic.creation.inventory.include=dbserver1\.inventory.*
topic.creation.inventory.partitions=10
topic.creation.inventory.cleanup.policy=compact
topic.creation.inventory.delete.retention.ms=7776000000
```

# Consumer

`debezium-events-consumer` is a sample consumer application based on MuleSoft 4.3