### Stream-Stream Join

```groovy
create stream redBlueJoin with (PARTITIONS=8) \
  as select \
    redBucket.transponder rt, \
    redBucket.latitude as rlat, \
    redBucket.longitude as rlong, \
    blueBucket.transponder as bt, \
    blueBucket.latitude as blat, \
    blueBucket.longitude as blong \
  from redBucket \
  inner join blueBucket within 4 hours \
    on redBucket.bucket = blueBucket.bucket;  
```
