All of these assumptions are wrong

1.   There are always 24 hours in a day.
2.   Months have either 30 or 31 days.
3.   Years have 365 days.
4.   February is always 28 days long.
5.   Any 24-hour period will always begin and end in the same day (or week, or month).
6.   A week always begins and ends in the same month.
7.   A week (or a month) always begins and ends in the same year.
8.   The machine that a program runs on will always be in the GMT time zone.
9.   Ok, that’s not true. But at least the time zone in which a program has to run will never change.
10.  Well, surely there will never be a change to the time zone in which a program hast to run in production.
11.  The system clock will always be set to the correct local time.
12.  The system clock will always be set to a time that is not wildly different from the correct local time.
13.  If the system clock is incorrect, it will at least always be off by a consistent number of seconds.
14.  The server clock and the client clock will always be set to the same time.
15.  The server clock and the client clock will always be set to around the same time.
16.  Ok, but the time on the server clock and time on the client clock would never be different by a matter of decades.
17.  If the server clock and the client clock are not in synch, they will at least always be out of synch by a consistent number of seconds.
18.  The server clock and the client clock will use the same time zone.
19.  The system clock will never be set to a time that is in the distant past or the far future.
20.  Time has no beginning and no end.
21.  One minute on the system clock has exactly the same duration as one minute on any other clock
22.  Ok, but the duration of one minute on the system clock will be pretty close to the duration of one minute on most other clocks.
23.  Fine, but the duration of one minute on the system clock would never be more than an hour.
24.  You can’t be serious.
25.  The smallest unit of time is one second.
26.  Ok, one millisecond.
27.  It will never be necessary to set the system time to any value other than the correct local time.
28.  Ok, testing might require setting the system time to a value other than the correct local time but it will never be necessary to do so in production.
29.  Time stamps will always be specified in a commonly-understood format like 1339972628 or 133997262837.
30.  Time stamps will always be specified in the same format.
31.  Time stamps will always have the same level of precision.
32.  A time stamp of sufficient precision can safely be considered unique.
33.  A timestamp represents the time that an event actually occurred.
34.  Human-readable dates can be specified in universally understood formats such as 05/07/11.
35.  The offsets between two time zones will remain constant.
36.  OK, historical oddities aside, the offsets between two time zones won’t change in the future.
37.  Changes in the offsets between time zones will occur with plenty of advance notice.
38.  Daylight saving time happens at the same time every year.
39.  Daylight saving time happens at the same time in every time zone.
40.  Daylight saving time always adjusts by an hour.
41.  Months have either 28, 29, 30, or 31 days.
42.  The day of the month always advances contiguously from N to either N+1 or 1, with no discontinuities.
43.  There is only one calendar system in use at one time.
44.  There is a leap year every year divisible by 4.
45.  Non leap years will never contain a leap day.
46.  It will be easy to calculate the duration of x number of hours and minutes from a particular point in time.
47.  The same month has the same number of days in it everywhere!
48.  Unix time is completely ignorant about anything except seconds.
49.  Unix time is the number of seconds since Jan 1st 1970.
50.  The day before Saturday is always Friday.
51.  Continguous timezones are no more than an hour apart. (aka we don’t need to test what happens to the avionics when you fly over the International Date Line)
52.  Two timezones that differ will differ by an integer number of half hours.
53.  Okay, quarter hours.
54.  Okay, seconds, but it will be a consistent difference if we ignore DST.
55.  If you create two date objects right beside each other, they’ll represent the same time. (a fantastic Heisenbug generator)
56.  You can wait for the clock to reach exactly HH:MM:SS by sampling once a second.
57.  If a process runs for n seconds and then terminates, approximately n seconds will have elapsed on the system clock at the time of termination.
58.  Weeks start on Monday.
59.  Days begin in the morning.
60.  Holidays span an integer number of whole days.
61.  The weekend consists of Saturday and Sunday.
62.  It’s possible to establish a total ordering on timestamps that is useful outside your system.
63.  The local time offset (from UTC) will not change during office hours.
64.  Thread.sleep(1000) sleeps for 1000 milliseconds.
65.  Thread.sleep(1000) sleeps for >= 1000 milliseconds.
66.  There are 60 seconds in every minute.
67.  Timestamps always advance monotonically.
68.  GMT and UTC are the same timezone.
69.  Britain uses GMT.
70.  Time always goes forwards.
71.  The difference between the current time and one week from the current time is always 7 \* 86400 seconds.
72.  The difference between two timestamps is an accurate measure of the time that elapsed between them.
73.  24:12:34 is a invalid time
74.  Every integer is a theoretical possible year
75.  If you display a datetime, the displayed time has the same second part as the stored time
76.  Or the same year
77.  But at least the numerical difference between the displayed and stored year will be less than 2
78.  If you have a date in a correct YYYY-MM-DD format, the year consists of four characters
79.  If you merge two dates, by taking the month from the first and the day/year from the second, you get a valid date
80.  But it will work, if both years are leap years
81.  If you take a w3c published algorithm for adding durations to dates, it will work in all cases.
82.  The standard library supports negative years and years above 10000.
83.  Time zones always differ by a whole hour
84.  If you convert a timestamp with millisecond precision to a date time with second precision, you can safely ignore the millisecond fractions
85.  But you can ignore the millisecond fraction, if it is less than 0.5
86.  Two-digit years should be somewhere in the range 1900-2099
87.  If you parse a date time, you can read the numbers character for character, without needing to backtrack
88.  But if you print a date time, you can write the numbers character for character, without needing to backtrack
89.  You will never have to parse a format like ---12Z or P12Y34M56DT78H90M12.345S
90.  There are only 24 time zones
91.  Time zones are always whole hours away from UTC
92.  Daylight Saving Time (DST) starts/ends on the same date everywhere
93.  DST is always an advancement by 1 hour
94.  Reading the client’s clock and comparing to UTC is a good way to determine their timezone
95.  The software stack will/won’t try to automatically adjust for timezone/DST
96.  My software is only used internally/locally, so I don’t have to worry about timezones
97.  My software stack will handle it without me needing to do anything special
98.  I can easily maintain a timezone list myself
99.  All measurements of time on a given clock will occur within the same frame of reference.
100.  The fact that a date-based function works now means it will work on any date.
101.  Years have 365 or 366 days.
102.  Each calendar date is followed by the next in sequence, without skipping.
103.  A given date and/or time unambiguously identifies a unique moment.
104.  Leap years occur every 4 years.
105.  You can determine the time zone from the state/province.
106.  You can determine the time zone from the city/town.
107.  Time passes at the same speed on top of a mountain and at the bottom of a valley.
108.  One hour is as long as the next in all time systems.
109.  You can calculate when leap seconds will be added.
110. The precision of the data type returned by a getCurrentTime() function is the same as the precision of that function.
111. Two subsequent calls to a getCurrentTime() function will return distinct results.
112. The second of two subsequent calls to a getCurrentTime() function will return a larger result.
113.  The software will never run on a space ship that is orbiting a black hole.
