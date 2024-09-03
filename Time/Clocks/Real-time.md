# Real-time Clocks
[Wikipedia](https://en.wikipedia.org/wiki/Real-time_clock)
> A real-time clock (RTC) is an electronic device (most often in the form of an integrated circuit) that measures the passage of time.
> 
> Although the term often refers to the devices in personal computers, servers and embedded systems, RTCs are present in almost any electronic device which needs to keep accurate time of day.

## Accuracy
> Typical crystal RTC accuracy specifications are from ±100 to ±20 parts per million (**8.6 to 1.7 seconds per day**), but temperature-compensated RTC ICs are available accurate to less than 5 parts per million. In practical terms, this is good enough to perform celestial navigation, the classic task of a chronometer. In 2011, chip-scale atomic clocks became available. Although vastly more expensive and power-hungry (120 mW vs. <1 μW), they keep time within 50 parts per trillion (5×10−11).

[What else can cause PC clock delay, if CMOS battery and RTC module seems OK? - Super User](https://superuser.com/questions/1002756/what-else-can-cause-pc-clock-delay-if-cmos-battery-and-rtc-module-seems-ok)
> Nothing, a low battery can only cause the RTC to stop completely. The RTC works on a crystal, it either works and is accurate (less inaccurate than 1 minute a day would be my guess) or it simply does not work. This behavior sounds to me like a broken RTC.

## CMOS
[CMOS - OSDev Wiki](https://wiki.osdev.org/CMOS)
- Century register

[An overview of the PC Real Time Clock (RTC) -- Phoxis](https://phoxis.org/2016/01/02/an-overview-of-the-pc-real-time-clock-rtc/)

[RTC Timekeeping Registers - Raspberry Pi Forums](https://forums.raspberrypi.com/viewtopic.php?t=261412)

Rust:
- ~~[noahrinehart/cmos: A utility to read, write CMOS and RTC data. Standard library not required.](https://github.com/noahrinehart/cmos)~~ (broken)
  - [Veliania/cmos: A utility to read, write CMOS and RTC data. Standard library not required.](https://github.com/Veliania/cmos)

[assembly - Are the "out" and "in" instructions privileged instructions? - Stack Overflow](https://stackoverflow.com/questions/44576612/are-the-out-and-in-instructions-privileged-instructions)

[I want to attempt to execute 'in' and 'out' instructions in the x86 instruction set from user space to see if I can trigger an illegal instruction exception. How do I do this? - Quora](https://www.quora.com/I-want-to-attempt-to-execute-in-and-out-instructions-in-the-x86-instruction-set-from-user-space-to-see-if-I-can-trigger-an-illegal-instruction-exception-How-do-I-do-this)

```
error: process didn't exit successfully: `target\debug\cmos.exe` (exit code: 0xc0000096, STATUS_PRIVILEGED_INSTRUCTION)
```