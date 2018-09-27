### User Defined Function

```groovy
@UdfDescription(name = "closestAirport", description = "return airport code for closest airport.")
public class ClosestAirport {
    private static final String HOST = "http://localhost:9080";
    private Geolocation geolocation = Feign.builder()
            .options(new Request.Options(200, 200))
            .encoder(new JacksonEncoder())
            .decoder(new JacksonDecoder())
            .target(Geolocation.class, HOST);
    @Udf(description = "find closest airport to given location.")
    public String closestAirport(final Double latitude, final Double longitude) {
        return geolocation.closestAirport(latitude, longitude).getCode();
    }
}
```
