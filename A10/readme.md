
To start the clusters:
```
docker compose up -d
```

run any node by using:
```
docker exec -it cassandra-seed cqlsh
docker exec -it cassandra-node1 cqlsh
docker exec -it cassandra-node2 cqlsh
```


🛠 Step 1: Create Keyspace

```
CREATE KEYSPACE weather_data WITH REPLICATION = {
  'class': 'SimpleStrategy',
  'replication_factor': 2
};
```

🛠 Step 2: Use the Keyspace
```
USE weather_data;
```

🛠 Step 3: Create Table
```
CREATE TABLE temperature_readings (
  station_id text,
  reading_time timestamp,
  temperature float,
  PRIMARY KEY (station_id, reading_time)
) WITH CLUSTERING ORDER BY (reading_time DESC);
```

🧪 Step 4: Insert Sample Data
```
INSERT INTO temperature_readings (station_id, reading_time, temperature)
VALUES ('WS001', toTimestamp(now()), 32.5);

INSERT INTO temperature_readings (station_id, reading_time, temperature)
VALUES ('WS001', toTimestamp(now()), 33.2);

INSERT INTO temperature_readings (station_id, reading_time, temperature)
VALUES ('WS002', toTimestamp(now()), 29.1);
```

🔍 Step 5: Query the Data
```
SELECT * FROM temperature_readings WHERE station_id = 'WS001';
```