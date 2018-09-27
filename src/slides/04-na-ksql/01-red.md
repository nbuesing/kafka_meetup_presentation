## KSQL - red

```groovy
create stream red with (kafka_topic='red', value_format='avro');
```

```groovy
@Bean
public KStream<String, Record> red() {
  return streamsBuilder
    .stream("red",
      Consumed.with(Serdes.String(), recordSerde));
}
```
