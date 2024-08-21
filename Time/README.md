# Time
[Wikipedia](https://en.wikipedia.org/wiki/Time)

[The state of time in Rust: leaps and bounds - The Rust Programming Language Forum](https://users.rust-lang.org/t/the-state-of-time-in-rust-leaps-and-bounds/107620)

> There are several different quantities used by software to represent dates and times, each with their own properties and complexities.
> 
> A *timestamp* measures the linear count of seconds since an agreed-upon moment, usually the Unix epoch (1970-01-01T00:00:00Z). For efficiency, arithmetics involving durations in uniform time units are often performed over timestamps rather than broken-down calendar time values.
> 
> A *date and time* in its simplest form refers to a date and a time of day. A date-time value has real-world meaning when it is associated with a calendar and a relationship to a standard time scale usually formulated as a fixed offset. This article will only consider the [proleptic Gregorian calendar 8](https://en.wikipedia.org/wiki/Proleptic_Gregorian_calendar) as it is the calendar that most software applications solely need to deal with, as well as the only calendar designated for worldwide communication by ISO 8601 and various Internet standards. Similarly, most applications deal with times offset from UTC, but there are complications with this time standard which are detailed below.
> 
> A *civil date and time* is date and time designated by authorities governing *time zones*. A time zone is normally defined by the principal offset from UTC and possibly a daylight saving time (DST) offset applied on a certain schedule within each year. The history of changes in the time zone definition needs to be considered for local calendar times that refer to the past. Crucially, this is the legal definition of what a local date and time e.g. "February 24, 12:34 in Helsinki" refers to.