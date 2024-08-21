# Libraries
## C++
- [std::chrono](https://en.cppreference.com/w/cpp/chrono)
  - [consider incorporating some API ideas from C++'s chrono library - Issue #3 - BurntSushi/jiff](https://github.com/BurntSushi/jiff/issues/3)

## Rust
- [std::time](https://doc.rust-lang.org/std/time/index.html)
  - [Instant](https://doc.rust-lang.org/std/time/struct.Instant.html): A monotonic (but not necessarily steady) clock
  - [SystemTime](https://doc.rust-lang.org/std/time/struct.SystemTime.html)

    > A `SystemTime` does not count leap seconds. `SystemTime::now()`'s behaviour around a leap second is the same as the operating system's wall clock. The precise behaviour near a leap second (e.g. whether the clock appears to run slow or fast, or stop, or jump) depends on platform and configuration, so should not be relied on.

- [chrono: Date and time library for Rust](https://github.com/chronotope/chrono) ([Docs.rs](https://docs.rs/chrono/latest/chrono/))
  - [`DateTime`](https://docs.rs/chrono/latest/chrono/struct.DateTime.html): ISO 8601 combined date and time with time zone
    - [`NaiveDateTime`](https://docs.rs/chrono/latest/chrono/struct.NaiveDateTime.html): ISO 8601 combined date and time without timezone
      - [`NaiveDate`](https://docs.rs/chrono/latest/chrono/struct.NaiveDate.html): ISO 8601 calendar date without timezone
      - [`NaiveTime`](https://docs.rs/chrono/latest/chrono/struct.NaiveTime.html): ISO 8601 time without timezone
    - `impl From<SystemTime> for DateTime<Local>, DateTime<Utc>`

      [Convert std::time::SystemTime to chrono::datetime::DateTime - help - The Rust Programming Language Forum](https://users.rust-lang.org/t/convert-std-time-systemtime-to-chrono-datetime-datetime/7684)

  - [chrono::format::strftime](https://docs.rs/chrono/latest/chrono/format/strftime/index.html#specifiers)
  - [Differences between this crate and `time` - Issue #1423 - chronotope/chrono](https://github.com/chronotope/chrono/issues/1423)
  - Support leap seconds

- [time: The most used Rust library for date and time handling.](https://github.com/time-rs/time)
  - > `time` uses `libc` APIs for querying the local time. These `libc` APIs may access the environment in a way that is not synchronized with Rust's standard library, which leads to a path where safe Rust code can be written to cause undefined behavior. `time` mitigates this by checking how many threads are active. If it's a value other than `1`, then `now_local()` fails.

- [jiff: A date-time library for Rust that encourages you to jump into the pit of success.](https://github.com/BurntSushi/jiff)
  - [The API design rationale for Jiff](https://github.com/BurntSushi/jiff/blob/master/DESIGN.md)
  - [Comparison with `chrono`, `time`, `hifitime` and `icu`](https://github.com/BurntSushi/jiff/blob/master/COMPARE.md)
  - Not support leap seconds: [about leap seconds - Issue #7 - BurntSushi/jiff](https://github.com/BurntSushi/jiff/issues/7)
  - [`intz` name is confusing - Issue #28 - BurntSushi/jiff](https://github.com/BurntSushi/jiff/issues/28)
  - [provide a more convenient way to (de)serialize an integer number of units since the Unix epoch - Issue #101 - BurntSushi/jiff](https://github.com/BurntSushi/jiff/issues/101)

  [r/rust](https://www.reddit.com/r/rust/comments/1e929gb/jiff_is_a_new_datetime_library_for_rust_that/?share_id=43cwkAjgT_yZqdi_S2q_x), [Hacker News](https://news.ycombinator.com/item?id=41031037)

- [hifitime: A high fidelity time management library in Rust](https://github.com/nyx-space/hifitime)

[The state of time in Rust: leaps and bounds - The Rust Programming Language Forum](https://users.rust-lang.org/t/the-state-of-time-in-rust-leaps-and-bounds/107620)
> From this review, it should be evident that none of the crates cover all common use cases without significant unresolved issues. time is sufficient for numeric date-time data based on UTC (sans the leap seconds) and validation of formatted inputs, but its support for reading local time without the unsoundness hack leaves a lot to be desired. chrono deserves praise for its implementations of local time and time zone manipulation, but its data domain is too loose for applications conscious about correctness and security. hifitime is the best fit for scientific and engineering applications which need a precise and continuous time scale, but is not designed for dealing with local time.

[chrono vs time vs std-time : r/rust](https://www.reddit.com/r/rust/comments/14n9zcy/chrono_vs_time_vs_stdtime/)

[What timestamp format is 48 bits / 6 bytes long? - Stack Overflow](https://stackoverflow.com/questions/56621877/what-timestamp-format-is-48-bits-6-bytes-long)

### Windows
- [filetime: Accessing file timestamps in a platform-agnostic fashion in Rust](https://github.com/alexcrichton/filetime)
- [win32_filetime_utils: Conversion utils from, and to Windows's FILETIME, SYSTEMTIME, etc ...](https://docs.rs/crate/win32_filetime_utils/0.2.1/source/src/lib.rs)
- [filetime_win: Windows FILETIME and SYSTEMTIME string and binary serialization](https://docs.rs/filetime_win/latest/filetime_win/index.html)

From [`FILETIME`](https://learn.microsoft.com/en-us/windows/win32/api/minwinbase/ns-minwinbase-filetime) to `std::time::SystemTime`:
```rust
use std::time::{SystemTime, Duration};

pub fn system_time_from_file_time(file_time: i64) -> SystemTime {
    const NANOS_PER_SEC: u64 = 1_000_000_000;
    const INTERVALS_PER_SEC: u64 = NANOS_PER_SEC / 100;
    const INTERVALS_TO_UNIX_EPOCH: u64 = 11_644_473_600 * INTERVALS_PER_SEC;

    SystemTime::UNIX_EPOCH
        .checked_add(Duration::from_nanos((file_time as u64 - INTERVALS_TO_UNIX_EPOCH) * 100))
        // `SystemTime` is just a wrapper to `FILETIME`, so the result must can
        // be represented in `SystemTime`.
        .unwrap()
}
```