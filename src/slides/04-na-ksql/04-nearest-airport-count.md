## Streams - count

```groovy
create table \
  ksql_red_nearest_airport_count with (PARTITIONS=8) \
  as select \
      airport, \
      count(*) as count \
    from ksql_red_nearest_airport window tumbling (size 4 hours) \
  group by airport;
```

```groovy
@Bean
public KStream<String, Count> nearestAirportCount() {
  KStream<String, Count> bean = nearestAirport()
    .selectKey((key, value) -> value.getAirport())
    .groupByKey()
    .windowedBy(TimeWindows.of(WINDOW))
    .aggregate(
      () -> 0,
      (key, value, aggregate) -> aggregate + 1,
      Materialized.with(Serdes.String(), Serdes.Integer())
    ).toStream((wk, v) -> wk.key())
    .mapValues(Count::new)
    .through("red.nearest.airport.count", Produced.with(Serdes.String(), countSerde)
  );
  return bean;
}
```
