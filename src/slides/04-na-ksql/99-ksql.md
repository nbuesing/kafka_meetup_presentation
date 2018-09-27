# KSQL

```
SET 'auto.offset.reset' = 'earliest';
```

```
create stream red with (kafka_topic='red', value_format='avro');
```

```
create stream blue with (kafka_topic='blue', value_format='avro');
```

```
create stream \
  ksql_red_nearest_airport with (PARTITIONS=8) \
  as select \
      aircraft->transponder transponder, \
      closestAirport(location->latitude, location->longitude) as airport, \
      location \
    from red \
  partition by transponder;
```

```
create table \
  ksql_red_nearest_airport_count with (PARTITIONS=8) \
  as select \
      airport, \
      count(*) as count \
    from ksql_red_nearest_airport window tumbling (size 4 hours) \
  group by airport;
```
