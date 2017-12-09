---
layout: post
title: Datetime module - working with date and time
tags: python datetime
---
Among many built-in modules in Python one module we use frequently is **datetime** module. So , today I’m gonna share what I’ve learned about **datetime** module and how to use it.

Why should we use **datetime** module ? This question may have arrived in your mind, the ans is-  if you want to work with date and time , manipulate them and format them for better user experiences in Python , you should get your hands dirty working with this specific module.

Okay, first let’s import the **datetime** module


```python
import datetime 
```

Now, if you want to output  any arbitrary date in the standard form like: **yy-mm-dd** ; then we will need to work with **datetime.date()** which is basically a class which is derived from **datetime** module and takes the arguments as year, month and date respectively,

```python
import datetime
date_1 = datetime.date(2017, 12, 7)
print(date_1)
```

in the 2nd line we're passing the arguments- 2017, 12 and 7 which are  year, month and date respectively ; at the 3rd line we’re printing that and the result is something like this:

```python
>>> 2017-12-07
```

What about you don’t remember what is date of today ? No need to worry, cause **datetime.date.today()** can do that for you! 

```python
tday = datetime.date.today()
print(tday)

>>> 2017-12-07
```

We want to know which weekday is today ,there are two classes **weekday() and isoweekday()** to do that work for us. In Python each weekday is equal to a specific number.  The **weekday()** class considers day as (mon=0, tue=1, wed=2, thu=3, fri=4, sat= 5, sun=6) but **isoweekday()** class do as (mon=1, tue=2, wed=3, thu=4, fri=5, sat= 6, sun=7).

```python
print(tday.weekday())
>>> 3 # the date is 2017-12-07 and day is Thursday and which is equal to 3

print(tday.isoweekday())
>>> 4 # as this class considers Thursday=4
```

To find out the difference between two date and time we can use **datetime.timdelta()** ,

```python
tday = datetime.date.today()
tdelta = datetime.timedelta(days=7)

print(tday)
print(tday – tdelta)
>>> 2017-12-08
>>> 2017-12-01
```

you can use to find out how many days are remained till birthday like below one

```python
birthday = datetime.date(2018, 1, 1)
till_birthday = birthday – tday

print(“Days remained till birthday: {}”.format(till_birthday.days))
>>> Days remained till birthday: 24
```

the result we get from the above is actually **timedelta!**

When you need to access both date and time at the same time , we can use **datetime.datetime()** ,

```python
dt = datetime.datetime(2017, 12, 8, 9, 30, 15, 100000)

print(dt)
print(“Date: {}”.format(dt.date()))
print(“Time: ”.format(dt.time()))
>>> 2017-12-08 09:30:15.100000
>>> Date: 2017-12-08
>>> Time:  09:30:15.100000
```

Also to know what time it is right now and today’s date,

```python
dt1 = datetime.datetime.now()

# for utc standard time
dt2 = datetime.datetime.utcnow()

print("Datetime1: {}".format(dt1))
print("Datetime2: {}".format(dt2))
>>> Datetime1: 2017-08-27 21:09:43.908397
>>> Datetime2: 2017-08-27 15:09:43.908513
```

Sometimes we have to work with timezone , so dealing with this there is a library for us which is **“pytz”**. As it is not built-in, we have to install it first using pip. If you don’t know what is pip, read this documentation : https://packaging.python.org/tutorials/installing-packages/

so first install pytz in your machine , 

``` bash
$ pip install pytz
```

then you can import it.

```python
import pytz
```

for using a key is used which is **tzinfo**, and from pytz we can get UTC standard time,

```python
dt_1 = datetime.datetime(2017, 8, 27, 9, 34, 30,tzinfo=pytz.UTC)
print(dt_1)
>>> 2017-08-27 09:34:30+00:00
```

We can also use specific timezone, here I’m using “Asia/Dhaka” as I’m from Bangladesh

```python
dt_mytz = dt_1.astimezone(pytz.timezone("Asia/Dhaka"))
print(dt_mytz)
>>> 2017-08-27 15:34:30+06:00

dt_utcnow = datetime.datetime.now(tz=pytz.timezone("Asia/Dhaka"))
print(dt_utcnow)
>>> 2017-12-08 23:34:19.171335+06:00
```

for more readable format there is **strftime(format)** method, returns a string representing the date. There is list of all format codes that supported by **strftime(format)** method here, https://docs.python.org/3/library/datetime.html

```python
print(dt_utcnow.strftime("%B %d, %Y and %I:%M %p")) 
>>> December 08, 2017 and 11:34 PM
```

Here, "%B %d, %Y and %I:%M %p" are format code for Month, day of the month, Year, Hour(12-hour-clock), Minute and AM/PM respectively.

If we have date and time as string we can convert it into a datetime according to given format by **strptime(format)** method, 

```python
t1 = datetime.datetime.strptime(str(input()), "%a %d %b %Y %H:%M:%S %z")
print(t1)
>>>
Sun 10 May 2015 13:54:36 -0700
>>> 2015-05-10 13:54:36-07:00
```

I hope from this post you’ve got some hints how to use datetime module. To explore more , check out the official documentation: https://docs.python.org/3/library/datetime.html  and also this video tutorial from Corey Schafer : https://www.youtube.com/watch?v=eirjjyP2qcQ&index=15&list=PL-osiE80TeTskrapNbzXhwoFUiLCjGgY7 . Actually , what I’ve written so far in this post is that what I’ve learned from his tutorial.

Any kind of question occurs in your mind regarding this post you can comment that below. Thanks!















