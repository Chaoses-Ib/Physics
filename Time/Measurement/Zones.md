# Time Zones
[Wikipedia](https://en.wikipedia.org/wiki/Time_zone)

> Time zones are the trickiest subject in date and time manipulation. First, the definitions of time zones are subject to change; IANA maintains a not rarely updated database on the world's time zones, which is integrated by software platform vendors. Second, civil date and time computations have more surprising failure cases: a periodic job that is scheduled to run every night at 03:01 Helsinki time will not run on March 31, 2024 due to the DST transition.

> A simpler level of support for the world's time zones is to operate with numeric offsets from UTC. If the date-time value carries information on the offset, and the leap seconds are ignored, arithmetics can be performed in a simple way on the proleptic Gregorian calendar without changing the offset.

> The operating system provides information on the local time offset currently in effect, typically as a function retrieving the local time. On Unix, this is usually done with the `localtime_r` standard C library function, but it's generally unsound in Rust due to unguarded use of the process' environment variables.