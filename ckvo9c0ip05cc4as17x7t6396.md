---
title: "Programmers Guide to Solving Computational Problems"
seoTitle: "Programmers guide to solving computational problems"
seoDescription: "A systematic way of approaching and breaking down programming problems with python"
datePublished: Sat Nov 06 2021 20:26:39 GMT+0000 (Coordinated Universal Time)
cuid: ckvo9c0ip05cc4as17x7t6396
slug: programmers-guide-to-solving-computational-problems
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1636227978922/E9sAOrxPQ.png
tags: data-structures, python3, competitive-programming, programming-tips, problem-solving-skills

---


## Introduction
Hello everyone, welcome back! today I want to talk about a very important topic: how to solve problems?. Learning how to solve problems is one of the most important skills you can learn, and improving as a problem solver is a lifelong challenge that cannot be learned through this short lesson, however, I want to show you important tips on how to tackle more complex programming problems, and hopefully, this post will teach you the essentials to problem-solving.

## What Problems?
In this post, we will tackle a specific problem, and talk about how I would go about solving it, and the goal of this exercise is not just to solve the problem but to draw general ideas on how to solve any type of programming problem.

### Days Between Dates
> 
Given your birthday and the current date, calculate your age in days. Compensate for leap years. Assume that the birthday and current date are correct (no time travel).

## Understanding a Problem
It's often tempting to start writing code early, the problem with this is that we are likely to write the wrong code and get frustrated, it's also likely that you think that you "solved the problem" but in reality, you might end up doing something completely different to what it was asked.

### So what does it mean to understand a problem?.
We need to emphasize that we are working on a `computational problem`, and what all computational problems have in common is that they have inputs and desired outputs, so, a problem is defined by the set of possible inputs (this is usually an infinite set) and the relationships between those inputs and the desired outputs. And a solution is a procedure that can take any input in that set and produces the desired output that satisfies the relationship, in this case, the relationship we want is that the output is the number of days between the birthday and the current date.

So, the first step to understanding a problem is to understand what the possible inputs are.

![understand input.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635880990506/u4Cn-HP3U.png)

## Step - 1 What are the inputs?
If we take another look at the problem we realized that it's clearly stated that we're given two dates as inputs.

> 
<mark>Given your birthday and the current date</mark>, calculate your age in days. Compensate for leap years. Assume that the birthday and current date are correct (no time travel).

### What is the set of valid inputs?
We always need to ask ourselves this question, for the moment we know the type of the inputs, but if we take another look at our problem we can find a good clue on what to expect.
> 
Given your birthday and the current date, calculate your age in days. Compensate for leap years. <mark>Assume that the birthday and current date are correct (no time travel).</mark>

Thanks to that statement we know that the second date needs to be after the first one. Assumptions like this one make life easier for programmers since our code has to work for fewer possible inputs, however, we are going to be good defensive programmers and check if the second date is after the first date in our code. Checking if the requirement is correct is a good practice since other people or even ourselves can make mistakes.

The other assumption we might need to think about is the range of dates. Calendars are very complicated and they've changed over history, so, we are going to require that the dates are valid dates in the Gregorian calendar, which started in October 1582.


![what are the inputs.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635886958157/PDyAljbAt.png)

### How are inputs represented?
For most real-world problems, it's up to you to figure out how to encode the inputs and this is one of the most important decisions that you can make in solving a problem. In this case, the problem template below indicates how the inputs are represented
```python
# function that returns the dates difference in days
def daysBetweenDates( year1, month1, day1, year2, month2, day2 ):
    # You're code goes here

```
As we can see there are six parameters to the daysBetweenDates procedure, which means we're going to be passing in six different values to represent those two dates. Some of you might see that there are better ways to pass the date, as an object for example but for the sake of clarity we're going to be passing those six values.

## Step - 2 What are the outputs?
The statement of the question gives us some idea of what the output should be in the calculate your age part.
> 
Given your birthday and the current date, <mark>calculate your age in days.</mark> Compensate for leap years. Assume that the birthday and current date are correct (no time travel).

But it doesn't specify really explicitly what we want the output to be

### How should we specify the output?
In this case, after reading the problem, it's clear that the output should be a **number ** representing the days of the difference between date1 and date2 assuming date1 is before date2.

## Step - 3 Understanding the relationship
Now that we know what the inputs are and what the outputs are it's time to understand the relationship between the two by working out some examples.

Take a good look at the problems below and try to figure out what the output for each call should be.

```python
daysBetweenDates(2020,11,7, 2020,11,7)

daysBetweenDates(2015,12,7, 2015,12,8)

daysBetweenDates(2010,12,8, 2010,12,7)

daysBetweenDates(2019,5,15, 2021,5,15)

daysBetweenDates(2012,6,29,2013,6,31)
```
For problem one, the output should be 0 since both dates are the same. For problem two the output should be 1 since there is only a one-day difference. Output for problem three should be an error since the second date is before the first date. Problem four was hard since, there was a two-year difference and 2020 is a leap year, so, the output should be 731. The last one was tricky since there is no day 31 in June!, so we would like to have an error indicating the invalid input.

At this point, you might be ready to start coding, but if the problem is challenging one you're probably not.

## Step - 4 Solving the problem as a human
The first step to solving a problem as a human is to look at an example and in this case let's say we wanted to find the difference between the dates (2013,01,24) and (2013,06,29), as a human the first thing that we might do is to look at a calendar and find the first date, then see how many days are left for that month, in this case, that is 7 days, we would probably grab a piece of paper and write that number down. Then we would count how many days has every month until we reach the second date.
`7+28+31+30+31+29 = 156`

![calendar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635968662441/-b5vj4Y1q.png)

We now have a starting point and it's time to write down an algorithm that systematizes how we solve it, in this case, we're going to write this as `Pseudocode` meaning we aren't focusing on coding real python code but the ideas instead. 
```python
# find the days between the dates (2013,01,24) and (2013,06,29)
#(year1,month1,day1,year2,month2,day2)

days = # days in month1(31) - starting day(24) = 7
while month1 < month2:
    days += # days in current month1
    month1 += 1 # moving to the next month
days += day2 # add the remaining days from the second date month(29)
# add the years days
while year1 < year2:
    days += # days in year1
```
### Should we implement this algorithm?
In this case, I don't think we should, there are several cases that this code does not consider, like:

-  input dates in same month `(2013,06,24 and 2013,06,29) # valid input`
-  month2 < month1 `(2012,07,24 and 2013,06,29) # valid input`
-  year2 < year1 `(2013,01,24 and 2012,06,29) # invalid input`
-  accounting for leap years.

### Different approach
Let's think of a more simple mechanical algorithm. As humans, it's very inefficient to manually count day by day, but not for computers, and I want to emphasize optimization, don't optimize prematurely! focus on solving the problem first.

```python
days = 0
while date1 < date2:
    date1 += # advance to next day
    days += 1
return days
```
This is the most simple approach possible, it's adding 1 day until we reach the second date.

## Step - 5 Coding nextDay procedure
I want to take a look at line three.
```
date1 += # advance to next day
``` 

This is clearly the most important part, and because of it, we should start by coding a `nextDay(year,month,day)` procedure. The function should receive a year, month, and day and return the year, month, and day of the next day.

```python
def nextDay(year, month, day):
    """
    For simplicity, assume every month has 30 days.
    """
    if day < 30:
        return year, month, day + 1
    elif month < 12:
        return year, month + 1, 1
    else:
        return year + 1, 1 ,1

print(nextDay(2021,3,11)) # expected output: 2021,3,12
print(nextDay(2021,3,29)) # expected output: 2021,3,30
print(nextDay(2021,3,30)) # expected output: 2021,4,1
print(nextDay(2021,11,30)) # expected output: 2021,12,1
print(nextDay(2021,12,30)) # expected output: 2022,1,1
```
As we can see, the code above accounts for the case that it's the end of the month and for the end of the year, the only problem with it it's that it's assuming all months have 30 days, so, what should we do next?

## Step - 6 Coding daysBetweenDates procedure
In this case, we can make the `nextDay` procedure to work with real months but we can actually do that later and start coding the `daysBetweenDates` procedure first, the advantage is that we'll be more confident if we're on the right track and most importantly, we'll be closer to having an answer, then we can correct the `nextDay` procedure since that will be a significantly smaller detail that shouldn't affect our `daysBetweenDates` procedure.

### Step - 1 look at the pseudocode
```python
days = 0
while date1 < date2:
    date1 += # advance to next day
    days += 1
return days
```
with our new `nextDay` procedure we can now code this right? well, not quite, if you have already tried you realized what the problem is. The comparison between dates.
```python
while date1 < date2:
```
### Step - 2 Helper Function
Let's understand exactly what the helper function shall do, in this case, we only need to return a boolean, True if the first date is before the second, and False if it is not. Let's code it!. 
```python
def date1BeforeDate2(year1,month1,day1,year2,month2,day2):
    """
    returns True if the first date is before the second date
    """
    if year1 < year2:
        return True
    if month1 < month2:
        return True
    if day1 < day2:
        return True
    return False

```
The solution for this helper function was really easy, we only needed to compare if the year1 was before year2, if that condition it's True, simply return True, then repeat the condition with the months and days, if none of the conditions were True simply return False.

### Step - 3 daysBetweenDates 
Now that we have our helper function, it's time to try to code the pseudocode again with our newly created function.

Pseudocode:
```python
days = 0
while date1 < date2:
    date1 += # advance to next day
    days += 1
return days
```

DaysBetweenDates procedure:
```python
def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """
    returns the difference of two dates in days
    """
    days = 0
    while date1BeforeDate2(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days

print(daysBetweenDates(2019, 5, 15, 2021, 5, 15)) # output should have been 731
print(daysBetweenDates(2023, 5, 15, 2020, 5, 15))  # invalid inputs
```
So much progress! however, if you run the code above you will realize that the output is 720 when it should have been 731, why?. Let's not forget that the `nextDay` procedure is incorrectly assuming all months have 30 days!!. However, it's very clear that we're on the right track. For the second print, we purposely passed invalid inputs to see what happens, in this case, the code output 0, but that is not really what we want.

### Step - 4 Test for invalid inputs
Like we talked about before, we are going to follow a good defensive programming practice and check for invalid inputs inside our `daysBetweenDates` procedure.

Python `assert()` is perfect for what we want. `assert()` allows us to perform comparisons. If the expression contained within it is False, an exception will be thrown, specifically an `AssertionError`.

Example:
```python
assert(5 < 3) # False, an AssertionError will be shown
assert(2 < 4) # True, nothing will happen
```

This fits perfectly for what we want, that is, checking if the first date is before the second date. Here is my implementation:

```python
def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """
    returns the difference of two dates in days
    """
    assert(date1BeforeDate2(year1, month1, day1, year2, month2, day2))

    days = 0
    while date1BeforeDate2(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days

```

Now if we test an invalid case where the second date is before the first date we should see an `AssertionError` pop up in the terminal like the image below:

![AssertionError.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636074389545/ZqHxCjbrI.png)

## Step - 7 Finishing daysBetweenDates procedure
Right now, we're 70% of the way, some of the things left to do are to make sure that the `daysBetweenDates` procedure accounts for leap years and months with the correct amount of days.

### Step - 1 Coding daysInMonths procedure

The way I'm going to approach this is that I'm going to write a `daysInMonth(year,month)` procedure that returns the correct number of days of the specified month. 
```python
def daysInMonth(year, month):
    return  # the number of days of the specified month
```
First things first, I'm going to do some googling to figure out what months have 31 days.

![months with days.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636080194957/XEZz_qWEu.png)

After a quick search, I found that the months with 31 days are months: 01, 03, 05, 07, 08, 10, and 12. With this information we can now add a condition in our code, like this:

```python
if month in (1, 3, 5, 7, 8, 10, 12):
        return 31
``` 
Let's repeat the process with the month of February, normally it has 28 days except on leap years where February has 29. For this first stage, we are going to check if the month is the number two and return 28 without accounting for leap years yet.

```python
def daysInMonth(year, month):
    """
    Function that receives a month and a year
    and based on that, it will return the number
    of days the specific month has.

    WARNING: This code does not account for leap years yet
    """
    if month in (1, 3, 5, 7, 8, 10, 12):
        return 31
    elif month == 2:
        return 28
    else:
        return 30
``` 

As you can see from the code above, in the case that none of the conditions are true, it will return the normal 30 days.

### Step - 2 Integrating daysInMonth procedure
Let's go back to our `nextDay` procedure and change it so that it now uses the correct number of days.

Before:
```python
if day < 30:
```
After:
```python
if day < daysInMonth(year, month):
```

### Step - 3 Coding isLeapYear procedure
Just as we coded our `daysInMonth` helper procedure, we should also create a procedure to check if a specified year is a leap year, but before we code, we should understand what a leap year is.

> <h3>Leap year</h3>
a year, occurring once every four years, that has 366 days including February 29 as an intercalary day. - https://en.wikipedia.org/wiki/Leap_year

If you scroll below the Wikipedia article, you will find an algorithm section that is incredibly useful for programmers. 

![algorithm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636143194735/550b9yIGg.png)

Here is my implementation of the algorithm:

```python
def isLeapYear(year):
    """
    Function that receives a year and returns
    a boolean, True if the year is a leap year
    and False if it's not
    """
    if not (year % 4 == 0):
        return False
    elif not (year % 100 == 0):
        return True
    elif not (year % 400 == 0):
        return False
    else:
        return True
```
After we are done writing our function it's important to test it to make sure it works, in this case, the code is giving the expected output so now it's time to integrate it in our `daysInMonth` procedure.

### Step - 4 Finishing daysInMonth procedure
For the moment, the `daysInMonth` procedure does not account for leap years and it's returning 28 days if the month is February, let's change that with our newly created `isLeapYear` procedure.


```python
def daysInMonth(year, month):
    """
    Function that receives a month and a year
    and based on that, it will return the number
    of days the specific month has, accounting for
    leap years.
    """
    if month in (1, 3, 5, 7, 8, 10, 12):
        return 31
    elif month == 2:
        if isLeapYear(year):
            return 29
        else:
            return 28
    else:
        return 30
``` 
Now, if the month is February, the code will check if the year is a leap year, if that it's true it will return 29 days, and if it's not it will return the normal 28 days. 
At this point, it looks like we are done, now it's time to test the full code with several examples.

After testing we realized that everything looks to be working except for the case where the dates are the same.
`print(daysBetweenDates(2021, 8, 24, 2021, 8, 24))` 
If you run this test case you will see an AssertionError when the output should be 0, to fix this I'm going to simply change the assertion line in the `daysBetweenDates` procedure.

Before:
```python
assert(date1BeforeDate2(year1, month1, day1, year2, month2, day2))
```

After:
```python
assert not (date1BeforeDate2(year2, month2, day2, year1, month1, day1))
```

Now everything looks to be finished, it's time to do final testing to be confident our code it's working as expected, and in this case, it looks like we can consider our code done!.

## Finished Result

Full python code:
```python
def isLeapYear(year):
    """
    Function that receives a year and returns
    a boolean, True if the year is a leap year
    and False if it's not
    """
    if not (year % 4 == 0):
        return False
    elif not (year % 100 == 0):
        return True
    elif not (year % 400 == 0):
        return False
    else:
        return True


def daysInMonth(year, month):
    """
    Function that receives a month and a year
    and based on that, it will return the number
    of days the specific month has, accounting for
    leap years.
    """
    if month in (1, 3, 5, 7, 8, 10, 12):
        return 31
    elif month == 2:
        if isLeapYear(year):
            return 29
        else:
            return 28
    else:
        return 30


def nextDay(year, month, day):
    """
    The function receives a year, month, and day and returns
    the year, month, and day of the next day.
    """
    if day < daysInMonth(year, month):
        return year, month, day + 1
    elif month < 12:
        return year, month + 1, 1
    else:
        return year + 1, 1, 1


def date1BeforeDate2(year1, month1, day1, year2, month2, day2):
    """
    The function receives two dates and returns a boolean, True
    if the first date is before the second, and False if it is not.
    """
    if year1 < year2:
        return True
    if month1 < month2:
        return True
    if day1 < day2:
        return True
    return False


def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """
    returns the difference between two dates in days accounting for 
    leap years and no time travel.
    """
    assert not (date1BeforeDate2(year2, month2, day2, year1, month1, day1))

    days = 0
    while date1BeforeDate2(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days


print(daysBetweenDates(2019, 5, 24, 2020, 5, 24))

```

## Conclusion - Farewell
You've reached the end of this lesson on problem-solving for programmers, remember that this is a skill that takes a lifetime to master so don't feel frustrated if you don't get it right away because this isn't easy, but I hope that some of the guidelines I've shared today can help you with any problem you might encounter in the future.


![how to solve problems.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636230302008/OtrX4zc5p.png)

That's all for today guys, I really hope this was helpful, and let me know in the comments any thoughts, suggestions and I will see you in the next post, stay tuned!.
