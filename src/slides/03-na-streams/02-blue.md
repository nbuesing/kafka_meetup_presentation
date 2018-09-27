## Streams - blue

```groovy
@Bean
public KStream<String, Record> blue() {
  return streamsBuilder
    .stream("blue",
      Consumed.with(Serdes.String(), recordSerde));
}
```
