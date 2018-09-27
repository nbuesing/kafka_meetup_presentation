## Streams - nearest airport

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
