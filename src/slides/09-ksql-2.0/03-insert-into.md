### Insert Into

```groovy
create stream blueBucket \
  as select \
    bucketLocation(location->latitude, location->longitude, 3.0) as bucket, \
    aircraft->transponder as transponder, aircraft->callsign as callsign, \
    location->latitude as latitude, location->longitude as longitude \
  from blue partition by bucket;
```

```groovy
create stream blueBucket_w \
  as select \
    bucketLocation(location->latitude, location->longitude, 3.0, 'w') as bucket, \
    aircraft->transponder as transponder, aircraft->callsign as callsign, \
    location->latitude as latitude, location->longitude as longitude \
  from blue partition by bucket;
```

```groovy
insert into blueBucket select * from blueBucket_w;
```
