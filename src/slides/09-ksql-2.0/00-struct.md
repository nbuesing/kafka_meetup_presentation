### Struct

**->**

```groovy
select aircraft->transponder, location from red;
```

```groovy
select location->latitude, location->longitude from blue;
```

```groovy
select * from blue where aircraft->callsign='DAL665  ';
```
