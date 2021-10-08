## Handy Date Time in Python | Pendulum.py

[TOC]

### Built-in Date Time in Python Recap

Python provides classes `date`, `datetime`, `time`, `timedelta` and `timezone` for datetime scenarios and `calendar` for calendar scenarios.

```Python
import datetime
import time

#### Instantiation

#### Localization and Time Zones

#### Attributes

#### String Formatting

#### String Parsing 

#### Arithmetics


```

### [Pendulum.py](https://pendulum.eustace.io/)

#### Introduction

> Drop-in replacement for the standard datetime class.


#### Installation

```Python
# recommended for conda users
conda install pendulum 

# for all python users
pip install pendulum 
```

#### Import

```python
# global import for the following demo, with the alias pm
import pendulum as pm
```



#### Instantiation

```python
# datetime helper
dt = pendulum.datetime(2021, 10, 8)
### DateTime(2021, 10, 8, 0, 0, 0, tzinfo=Timezone('UTC'))


# local timezone helper 
## Just an alias for datetime(..., tz='local'). 
## See next section for more timezone info
dt = pendulum.local(2021, 10, 8)
### DateTime(2021, 10, 8, 0, 0, 0, tzinfo=Timezone('Asia/Shanghai'))


# semantic helper
now = pendulum.now()
### DateTime(2021, 10, 8, 10, 32, 19, 617067, tzinfo=Timezone('Asia/Shanghai'))

today = pendulum.today()
### DateTime(2021, 10, 8, 0, 0, 0, tzinfo=Timezone('Asia/Shanghai'))

yesterday = pendulum.yesterday()
### DateTime(2021, 10, 7, 0, 0, 0, tzinfo=Timezone('Asia/Shanghai'))

tomorrow = pendulum.tomorrow()
### DateTime(2021, 10, 9, 0, 0, 0, tzinfo=Timezone('Asia/Shanghai'))


# parse from string. See the "String Parsing" section for more parsing info
dt = pendulum.from_format('2021-10-08 12:00:00', 'YYYY-MM-DD HH:mm:ss')
### DateTime(2021, 10, 8, 12, 0, 0, tzinfo=Timezone('UTC'))


# unix timestamp
"""
from_timestamp() will create a DateTime instance equal to the given timestamp and will set the timezone as well or default it to UTC.
"""
dt = pendulum.from_timestamp(-1)
### DateTime(1969, 12, 31, 23, 59, 59, tzinfo=Timezone('UTC'))

dt = pendulum.from_timestamp(0)
### DateTime(1970, 1, 1, 8, 0, 0, tzinfo=Timezone('UTC'))

dt = pendulum.from_timestamp(0, tz='Asia/Shanghai')
### DateTime(1970, 1, 1, 8, 0, 0, tzinfo=Timezone('Asia/Shanghai'))

```

#### Localization and Time Zones

Time zones comes out when globalization occurs, such as instantiation and string parsing with the **keyword argument `tz`**. 

The `tz` argument is keyword-only. Supported strings for `tz` are provided by the [IANA time zone database](https://www.iana.org/time-zones).

```python
dt = pendulum.local(2021, 10, 8)
print(dt.timezone.name)
### 'Asia/Shanghai'
```



##### Background of [Time Zones](https://simple.wikipedia.org/wiki/Time_zone)

> Time zones give specific areas on the Earth a time of day that is earlier or later than the neighboring time zones. This is because when it is daytime on one side of the earth, it is night-time on the other side. 
>
> There are **24 time zones** dividing the earth into different times, each with its own name, like the *North American Eastern(ET)* Time Zone. 
>
> [Greenwich Mean Time](https://simple.wikipedia.org/wiki/Greenwich_Mean_Time) (GMT) began in 1675. It is now called UTC ([Coordinated Universal Time](https://simple.wikipedia.org/wiki/Coordinated_Universal_Time)). UTC is the time standard of the world. All other parts of the world are offset (plus or minus) according to their longitude. Most of the zones  are offset by a full hour, but there are some offset by half an hour or 45 minutes.
>
> The time zones are numbered in relation to the UTC, so in [Los Angeles](https://simple.wikipedia.org/wiki/Los_Angeles) the time zone will be UTC−8, in [London](https://simple.wikipedia.org/wiki/London) UTC+0, in [Rome](https://simple.wikipedia.org/wiki/Rome) UTC+1, and in [New Delhi](https://simple.wikipedia.org/wiki/New_Delhi) UTC+5:30.
>
> GMT was a standard reference for time keeping when each city kept a different local time.





![time zones](https://upload.wikimedia.org/wikipedia/commons/thumb/8/88/World_Time_Zones_Map.png/600px-World_Time_Zones_Map.png)



##### Practical Cases

###### datetime()

The `datetime()` helper sets the time to 00:00:00 if it's not specified, and the timezone (the `tz` keyword argument) to **UTC**. 
Otherwise it can be a `Timezone` instance or simply a string timezone value such as 'Asia/Shanghai'.

```Python
pendulum.datetime(2021, 10, 8)
### DateTime(2021, 10, 8, 0, 0, 0, tzinfo=Timezone('UTC'))

pendulum.datetime(2021, 10, 8, tz='Asia/Shanghai')
### DateTime(2021, 10, 8, 0, 0, 0, tzinfo=Timezone('Asia/Shanghai'))
```

###### local()

`local()` is similar to `datetime()` but automatically sets the timezone to the **local timezone**.

```python
dt = pendulum.local(2021, 10, 8)
print(dt.timezone.name)
### 'Asia/Shanghai'
```

###### from_format()

`from_format()`, is similar to the native `datetime.strptime()` function but uses custom tokens to create a `DateTime` instance.

It also accepts a `tz` keyword argument to specify the timezone:

```python
pendulum.from_format('2021-10-08 12:00:00', 'YYYY-MM-DD HH:mm:ss')
### DateTime(2021, 10, 8, 12, 0, 0, tzinfo=Timezone('UTC'))
```

###### from_timestamp()

`from_timestamp()` set the timezone default to UTC unless `tz` argument is given.

```python
d0 = pendulum.from_timestamp(0)
d8 = pendulum.from_timestamp(60*60*8, tz='Asia/Shanghai')
```

**QUESTION**: Are they equivalent, `d0==d8`?

```python
dt0 = pendulum.from_timestamp(0)
dt8 = pendulum.from_timestamp(0, tz='Asia/Shanghai')
```

**QUESTION**: Now, are they equivalent, `dt0==dt8`?



**SOLUTION**

| variable | declaration                                   | value                                                        |
| :------: | --------------------------------------------- | ------------------------------------------------------------ |
|    d0    | from_timestamp(0)                             | DateTime(1970, 1, 1, 0, 0, 0, tzinfo=Timezone('UTC'))        |
|    d8    | from_timestamp(60\*60\*8, tz='Asia/Shanghai') | DateTime(1970, 1, 1, 16, 0, 0, tzinfo=Timezone('Asia/Shanghai')) |
|   dt0    | from_timestamp(0)                             | DateTime(1970, 1, 1, 0, 0, 0, tzinfo=Timezone('UTC'))        |
|   dt8    | from_timestamp(0, tz='Asia/Shanghai')         | DateTime(1970, 1, 1, 8, 0, 0, tzinfo=Timezone('Asia/Shanghai')) |

d0 = dt0 = dt8 != d8


<strong style="color: red">CRITICAL</strong>

A `timestamp` ([Unix time](https://en.wikipedia.org/wiki/Unix_time)) is a number **ALWAYS** relative to **UTC**!

> **Unix time** (also known as **Epoch time**, **Posix time**,[[1\]](https://en.wikipedia.org/wiki/Unix_time#cite_note-1) **seconds since the Epoch**,[[2\]](https://en.wikipedia.org/wiki/Unix_time#cite_note-single-unix-spec-4.16-2) or **UNIX Epoch time**[[3\]](https://en.wikipedia.org/wiki/Unix_time#cite_note-3)) is a system for describing a [point in time](https://en.wikipedia.org/wiki/Timestamp). It is the number of [seconds](https://en.wikipedia.org/wiki/Second) that have elapsed since the *Unix epoch*, excluding [leap seconds](https://en.wikipedia.org/wiki/Leap_second). The Unix epoch is 00:00:00 [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) on 1 January 1970 (an arbitrary date).

When `tz` argument is given, it actually means **THE INSTANCE** created by `from_timestamp()` with the **TIMESTAMP** is later **FORMATTED**  to the given time zone for display.

#### Attributes

```python
dt=pendulum.local(2021, 10, 8, 8, 1, 2, 3)
```
```python
dt.year					### 2021
dt.month				### 10
dt.day					### 8
dt.hour					### 8
dt.minute				### 1
dt.second 				### 2
dt.microsecond 			### 3

dt.day_of_week 			### 5
dt.day_of_year 			### 281
dt.days_in_month		### 31 ATTENTION: it is the total number of days in this month
dt.week_of_month		### 2
dt.week_of_year			### 40
dt.quarter				### 4

dt.timestamp()			### 1633651262.000003  = dt.float_timestamp()
dt.float_timestamp()	### 1633651262.000003  = dt.timestamp()
dt.int_timestamp()		### 1633651262 integer


dt.offset_hours			### 8.0 (UTC+8)
# Returns an int of seconds difference from UTC (+/- sign included)
dt.offset				### 28800 = 60 * 60 * 8 (UTC+8)

dt.tz					### Timezone('Asia/Shanghai')
dt.timezone				### Timezone('Asia/Shanghai')
dt.timeinfo				### Timezone('Asia/Shanghai')
dt.timezone_name		### 'Asia/Shanghai'
dt.timezone.name		### 'Asia/Shanghai'

dt.date()				### Date(2021, 10, 8)
dt.time()				### Time(8, 1, 2, 3)
dt.timetz()				### datetime.time(8, 1, 2, 3, tzinfo=Timezone('Asia/Shanghai'))

```



#### String Formatting

#### String Parsing 

#### Arithmetics






