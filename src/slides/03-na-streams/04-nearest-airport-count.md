## Streams - count

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
