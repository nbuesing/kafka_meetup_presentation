#### Topology : KSQL : nearest airport

```
   Sub-topology: 0
    Source: KSTREAM-SOURCE-0000000000 (topics: [red])
      --> KSTREAM-MAPVALUES-0000000001
    Processor: KSTREAM-MAPVALUES-0000000001 (stores: [])
      --> KSTREAM-TRANSFORMVALUES-0000000002
      <-- KSTREAM-SOURCE-0000000000
    Processor: KSTREAM-TRANSFORMVALUES-0000000002 (stores: [])
      --> KSTREAM-MAPVALUES-0000000003
      <-- KSTREAM-MAPVALUES-0000000001
    Processor: KSTREAM-MAPVALUES-0000000003 (stores: [])
      --> KSTREAM-FILTER-0000000004
      <-- KSTREAM-TRANSFORMVALUES-0000000002
    Processor: KSTREAM-FILTER-0000000004 (stores: [])
      --> KSTREAM-KEY-SELECT-0000000005
      <-- KSTREAM-MAPVALUES-0000000003
    Processor: KSTREAM-KEY-SELECT-0000000005 (stores: [])
      --> KSTREAM-MAPVALUES-0000000006
      <-- KSTREAM-FILTER-0000000004
    Processor: KSTREAM-MAPVALUES-0000000006 (stores: [])
      --> KSTREAM-MAPVALUES-0000000007
      <-- KSTREAM-KEY-SELECT-0000000005
    Processor: KSTREAM-MAPVALUES-0000000007 (stores: [])
      --> KSTREAM-SINK-0000000008
      <-- KSTREAM-MAPVALUES-0000000006
    Sink: KSTREAM-SINK-0000000008 (topic: KSQL_RED_NEAREST_AIRPORT)
      <-- KSTREAM-MAPVALUES-0000000007
```
