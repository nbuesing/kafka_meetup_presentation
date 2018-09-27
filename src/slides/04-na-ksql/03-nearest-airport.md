## Streams - nearest airport

```groovy
create stream \
  ksql_red_nearest_airport with (PARTITIONS=8) \
  as select \
      aircraft->transponder transponder, \
      closestAirport(location->latitude, location->longitude) as airport, \
      location \
    from red \
  partition by transponder;
```

```groovy
@Bean
public KStream<String, NearestAirport> nearestAirport() {
  return red().map((key, value) -> {
    String airport = geolocation.closestAirport(
      value.getLocation().getLatitude(),
      value.getLocation().getLongitude()
    ).getCode();

    return KeyValue.pair(
      key,
      new NearestAirport(
        airport,
        value.getLocation().getLatitude(),
        value.getLocation().getLongitude()
      )
    );
  }).through(
      "red.nearest.airport",
      Produced.with(Serdes.String(), nearestAirportSerde)
  );
}
```
