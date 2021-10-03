# Unix Time Overview - From MySQL's Date Type

[TOC]

##### References
* https://en.wikipedia.org/wiki/Unix_time
* https://dev.mysql.com/doc/refman/8.0/en/datetime.html


## Wiki

> **Unix time** (also known as **Epoch time**, **Posix time**,[[1\]](https://en.wikipedia.org/wiki/Unix_time#cite_note-1) **seconds since the Epoch**,[[2\]](https://en.wikipedia.org/wiki/Unix_time#cite_note-single-unix-spec-4.16-2) or **UNIX Epoch time**[[3\]](https://en.wikipedia.org/wiki/Unix_time#cite_note-3)) is a system for describing a [point in time](https://en.wikipedia.org/wiki/Timestamp). It is the number of [seconds](https://en.wikipedia.org/wiki/Second) that have elapsed since the *Unix epoch*, excluding [leap seconds](https://en.wikipedia.org/wiki/Leap_second). 
>
> The Unix epoch is 00:00:00 [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) on 1 January 1970 (an arbitrary date). Unix time is nonlinear with a  leap second having the same Unix time as the second before it (or after  it, implementation dependent), so that every day is treated as if it  contains exactly 86400 seconds,[[2\]](https://en.wikipedia.org/wiki/Unix_time#cite_note-single-unix-spec-4.16-2) with no seconds added to or subtracted from the day as a result of  positive or negative leap seconds. Due to this treatment of leap  seconds, Unix time is not a true representation of UTC.
>
> Unix time is widely used in [operating systems](https://en.wikipedia.org/wiki/Operating_system) and [file formats](https://en.wikipedia.org/wiki/File_format). In [Unix-like](https://en.wikipedia.org/wiki/Unix-like) operating systems, `date` is a command which will print or set the current time; by default, it prints or sets the time in the system [time zone](https://en.wikipedia.org/wiki/Time_zone), but with the `-u` flag, it prints or sets the time in UTC and, with the `TZ` [environment variable](https://en.wikipedia.org/wiki/Environment_variable) set to refer to a particular time zone, prints or sets the time in that time zone.[[4\]](https://en.wikipedia.org/wiki/Unix_time#cite_note-4)



## Date vs Datetime vs Timestamp in MySQL

### About

> The `DATE` type is used for values with a date part but no time part. MySQL retrieves and displays `DATE` values in `'YYYY-MM-DD'` format. The supported range is `'1000-01-01'` to `'9999-12-31'`.

>  The `DATETIME` type is used for values that contain both date and time parts. MySQL retrieves and displays `DATETIME` values in *'YYYY-MM-DD hh:mm:ss'* format. The supported range is `'1000-01-01 00:00:00'` to `'9999-12-31 23:59:59'`.

>  The `TIMESTAMP` data type is used for values that contain both date and time parts. `TIMESTAMP` has a range of `'1970-01-01 00:00:01'` UTC to `'2038-01-19 03:14:07'`UTC.

### Storage Structure

> A `DATETIME` or `TIMESTAMP` value can include a trailing fractional seconds part in up to microseconds (6 digits) precision. 
>
> In particular, any fractional part in a value inserted into a `DATETIME` or `TIMESTAMP` column is stored rather than discarded. 

### Supported Range

> With the fractional part included, the format for these values is `'*YYYY-MM-DD hh:mm:ss*[.*fraction*]'`, 
>
> the range for `DATETIME` values is `'1000-01-01 00:00:00.000000'` to `'9999-12-31 23:59:59.999999'`, 
>
> and the range for `TIMESTAMP` values is `'1970-01-01 00:00:01.000000'` to `'2038-01-19 03:14:07.999999'`,
> 
> while the `DATE` only support date from `1000-01-01` to `9999-12-31`.

Guess what will happen after '2038-01-19 03:14:08' with `TIMESTAMP`?



### Main differences

> MySQL converts `TIMESTAMP` values <b style='color:red'>from the current time zone to *UTC* for storage, and back from UTC to the current time zone for retrieval</b>. 
>
> By default, the current time zone for each connection is the server's time. 

### How to decide
Briefly speaking, `DATETIME` is good enough for usage in the same time zone while globalization is not required. However, to be more general, [Epoch time](https://en.wikipedia.org/wiki/Unix_time) should be always preferred as it is precise as well as versatile.


### Performance Benchmark

```sql
# college.create_time : timestamp

-- sql1, 14234/14237 AVG = 0.0014s
SELECT id, college_name FROM college WHERE do_delete = FALSE AND UNIX_TIMESTAMP(create_time) BETWEEN UNIX_TIMESTAMP('2019-06-19 15:00:00') AND UNIX_TIMESTAMP('2019-06-19 16:00:00');
        
-- sql2, 14234/14237 AVG = 0.0026s       
SELECT id, college_name FROM college WHERE do_delete = FALSE AND create_time BETWEEN '2019-06-19 15:00:00' AND '2019-06-19 16:00:00';
```



```SQL
# msg_log.date : date
# msg_log.c_time : timestamp

-- sql1, 6/25538 AVG = 
select id from msg_log where date between '2016-06-12' and '2016-06-13';

-- sql2, 6/25538 AVG = 
select id from msg_log where c_time between '2016-06-12 00:00:00' and '2016-06-14 00:00:00';

-- sql3, 6/25538 AVG = 
select id from msg_log where unix_timestamp(c_time) between unix_timestamp('2016-06-12 00:00:00') and unix_timestamp('2016-06-14 00:00:00');
```

| epoch/time/sql | sql 1 (date) | sql 2 (timestamp) | sql 3 (timestamp) |
| -------------- | ------------ | ---------------- | ---------------- |
| 1              | 0.00065      | 0.384            | 0.076            |
| 2              | 0.00062      | 0.382            | 0.076            |
| 3              | 0.00060      | 0.383            | 0.089            |
| 4              | 0.00081      | 0.386            | 0.076            |
| 5              | 0.00060      | 0.384            | 0.076            |

```sql
# college.create_time: datetime

-- sql1, AVG = 0.0014s
SELECT id, college_name FROM college WHERE do_delete = FALSE AND UNIX_TIMESTAMP(create_time) BETWEEN 1530374400 AND 1567180800;
       
-- sql2, AVG = 0.0021s
select id, college_name from college where do_delete = false and (create_time between from_unixtime(1530374400) and from_unixtime(1567180800));
```


## Unix Time in Popular Programming Lanuages 
| Language            | Get Current Unix Time                                        | Unix Time -> String<br />ut=1633060800<br />s="2021-10-01 12:00:00" | String -> Unix Time<br />s="2021-10-01 12:00:00"<br />ut=1633060800 |
| ------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Java                | import java.util.Date;<br />Date d = new Date();<br />long ut =d.getTime() / 1000L;<br />long ut1 = System.currentTimeMillis() / 1000L;<br />import java.time.Instant;<br />long ut2= Instant.now().getEpochSecond();<br /> | DateTimeFormatter f= DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss"); <br />d.toString(f) | d=DateTime.parse(s, f);<br />LocalDate d2= LocalDate.parse(s, f);<br />long ut = d.getTime()/1000L; |
| Python              | import time <br />ut=int(time.time())                        | d=time.localtime(ut)<br />s=time.strftime(f, d)              | f="%Y-%m-%d %H:%M:%S"<br />d=time.strptime(s, f)<br />ut=int(time.mktime(d)) |
| JavaScript          | let d = Date.now() <br />let d2 = new Date() <br />let ut=Math.round(d.valueOf())<br />let ut1=Math.round(d.getTime()/1000) | // approximate output<br />let s=ut.toLocaleString()         | ut=Math.round(Date.parse(s).getTimes()/1000) // Date.parse() is not recommended as ES5 though |
| momment.js          | import * as moment from 'moment'<br />ut=moment().unix()     | let m=moment(ut)<br />let f="YYYY-MM-DD HH:hh:ss"<br />let s=m.format(f) | m = moment(s, f)                                             |
| Microsoft .NET / C# | ut= (DateTime.Now.ToUniversalTime().Ticks - 621355968000000000) / 10000000 | DateAdd("s", ut, "01/01/1970 00:00:00")                      |                                                              |
| Unix / Linux        | ut=date +%s                                                  | s=date -d "@$ut" +"%F %R:%S"                                 | date --date="$s" +%s                                         |
| MySQL               | SELECT @ut := UNIX_TIMESTAMP(NOW())                          | SELECT @s:=FROM_UNIXTIME(@ut, "%Y-%m-%d %T")                 | DATE_FORMAT(@s,"%Y-%m-%d %T")                                |
| SQL Server          | SELECT DATEDIFF(s, '1970-01-01 00:00:00', GETUTCDATE())      | DATEADD(s, ut, '1970-01-01 00:00:00')                        |                                                              |