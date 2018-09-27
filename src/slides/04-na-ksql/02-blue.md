## KSQL - blue

```groovy
create stream blue with (kafka_topic='blue', value_format='avro');
```

```groovy
@Bean
public KStream<String, Record> blue() {
  return streamsBuilder
    .stream("blue",
      Consumed.with(Serdes.String(), recordSerde));
}
```
