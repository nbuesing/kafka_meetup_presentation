## Streams - red

```groovy
@Bean
public KStream<String, Record> red() {
  return streamsBuilder
    .stream("red",
      Consumed.with(Serdes.String(), recordSerde));
}
```
