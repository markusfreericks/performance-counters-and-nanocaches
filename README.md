# Performance Counters and Nanocaches

## Tools for optimizing performance

### measuring time

timers are essential for effective performance optimizations. ideally, 
- we want to see how often a block of code is called, and 
- how long the invocations take (min/max/avg)

these timers should be available when the software is deployed, so that realistic measurements can be gathered. in my $WORK projects, i always include timers, and i usually provide an actuator endpoint to show the accumulated timers. this has been quite helpful in debugging real live performance issues.

timers need to be easy to add, and they have to be extremly lightweight: a timer start/stop should not consume any memory, and it should block due to synchronization.

### caching

when performance issues are found, and there is no easy way to improve the algorithm, a cache is needed. we have to differentiate between internal and external caches:

internal caches
- store the objects themselves (not a serialized form)
- require that the cached objects are effectively immutable
- can store objects of any size in constant time
- should have minimal overhead

an internal cache should return a cached answer in <<0.1ms

external caches
- store a serialized form of the objcets (often JSON)
- create a copy of the object when reading
- require measurable time for store (serialization+transmit)
- require measurable time for read (transmit+deserialization)

an external cache will rarely return a cached answer in <1ms

## Tools for optimizing performance

goal of this project

- set up some benchmarks for timers and caches
- compare common implementations
- see whether my own implementations (EasyTimer/IntervalTimer and NanoCache) can compete
