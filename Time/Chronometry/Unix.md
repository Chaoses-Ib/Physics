# Unix Time
[Wikipedia](https://en.wikipedia.org/wiki/Unix_time)

> POSIX timestamps represent the number of seconds since the Unix epoch. Unix standard library functions converting between timestamps and broken-down calendar time ignore leap seconds.
> 
> For a variety of mostly historical reasons, leap seconds have been solved on Unix systems by setting the wall-clock time back by a second. The wall clock is generally allowed by POSIX to make discontinuous jumps in either direction, so this is not a new concern; Unix programs using system wall-clock timestamps to measure elapsed time should be prepared to gracefully handle the non-monotonic clock. However, if an application expects the clock to be synchronized via NTP, leap seconds become "dangerous time" when the system clock abruptly deviates from UTC by up to a second, yet there is no way to get information about this through standard APIs. Linux provides the OS-specific `adjtimex` system call, which works if the time synchronization daemon supports the feature and is able to get the information on the upcoming leap second in time.

Unix time | UTC tiem
--- | ---
`i32::MIN` | 1901-12-13 20:45:52
`i32::MAX` | [2038-01-19 03:14:07](https://en.wikipedia.org/wiki/Year_2038_problem)
`u32::MAX` | 2106-02-07 06:28:15
10000000000 | 2286-11-20 <br/> [The 2286 Bug. Unix timestamps represent time as... \| by Nathan Smith \| Medium](https://medium.com/@nate510/the-2286-bug-65697bb1b908)

## Libraries
Rust:
- `std::time::SystemTime::now().duration_since(std::time::UNIX_EPOCH)`
- [unix-ts: Unix timestamp manipulation and conversion in Rust.](https://github.com/lukesneeringer/unix-ts)
- [unix-time: A minimalist Rust crate to play with UNIX epoch-based Instant](https://github.com/qdeconinck/unix-time)