# Data Types

## Background

How often do you think about information? You probably think about it more than you realize. Whatever the answer, as we start to think about programming and databases, we need to start looking at data on a fundamental level, the same way that a computer does. Today’s topic is looking at different types of data. To start with, data types fall into two broad categories: simple and complex. We are going to look at complex data types in a few weeks. Today, we are only looking at simple or “primitive” data types.

## Simple Data Types

You probably know that computers store everything in binary which means that everything gets broken down into 1s and 0s. Each of these is called a bit. Put 8 of them together and you have a byte. Put 1024 bytes together and you have a kilobyte (kb). 1024 kilobytes make a megabyte (MB). 1024 megabytes make a gigabyte (GB). 1024 gigabytes is a terabyte (TB) and so on. For those of you who are lost already, cheer up, this is probably the last time we will ever reference bits and bytes in this course.

We are talking a couple levels up from that and are looking at the data being passed around which, although it consists of bits and bytes, are more “human friendly” than 1s and 0s.

There are 5 simple data types we are going to use in this class:

* Strings
* Integers
* Floats
* Booleans
* Dates

Depending on the level of persnicketiness ([real-ish word](http://www.thefreedictionary.com/persnicketiness)) in the documentation you are reading, this list might change a little bit but not a great deal. Each of these types has a clear conceptual definition. However, because definitions need to visit the real world, each has a few subtypes as well. This is because all of this data is stored on a drive someplace in, whoops, I was wrong about it being the last time, in 1s and 0s. Because databases can become gigantic in size (think of all the data that [Amazon.com](http://amazon.com) or the NSA stores!), sometimes it is important to limit the amount of space that is allocated to storing that data. The “subtypes” typically come from the amount of bytes allocated to store that data.

### Integers

An integer consists of a whole number with no fractions, decimal places, letters or other characters. Seems simple enough. Let’s look at the subtypes

* First a concept - Integers can be signed or unsigned.
  * Unsigned integers only consist of 0 and positive integers.
  * Signed integers can be positive or negative. There needs to be a special sign as part of the datatype since nothing in binary itself indicates that a number is negative. That had to be added later.
* Type: 8bit number
  * Signed Range: -128 to 127
  * Unsigned Range: 0 to 255
* Type: Small Int (16bit)
  * Signed Range: -32,768 – 32,767
  * Unsigned - 0-65,535
* Double Int (32bit)
  * Signed: - 2,147,483,648 to 2,147,483,647
  * Unsigned: 0-4,294,967,295
* Long int (64bit)
* Big Int: unlimited

The point here is not the specific numbers that each type can store, although that does become important in planning a project if your data could potentially get to numbers that big or small. The point is that when you see these data types listed, you recognize them for what they are – whole numbers of various sizes.

Why are there limits put on the size of the numbers you can put into a database? There are a few reasons but the main two are the cost of storing that data and the time it takes for a database to wade through the data needed to find what it is looking for . Originally, hard drives were very expensive which made storing data very expensive. Therefore, it made sense to allow just enough space for the number needed. For example, it’s a waste to tell a database to expect a number 10 digits long when it is meant to store someone’s age which, at most, is a 3 digit positive number. Storage is much much cheaper now, but the databases can get much much much much larger. When they are this large, there are not only storage costs to think about but the cost it takes for a processor to run the applications that are using that data.

### Floats

A float is a number which has a fraction (or decimal) with it. A single float uses 32 bits of storage while a double uses 64 bits. Fairly straightforward

### Booleans

Booleans, also called bits (there they are again) have two values – true or false. This can be represented in a number of ways such as 1 or 0, yes or no, true or false. Often you will see Booleans in programming when your program needs to make a decision. You might say “If the number of apples is equal to 7”….. The program evaluates that statement into a Boolean (either true or false) and then does what it is supposed to accordingly. We’ll talk more about that concept later in the course when we talk about Data Type Conversions but we can leave it there for now.

### Strings

Strings, also called literals, are a collection of any combination of letters, numbers or symbols. It doesn’t matter if they are words, all numbers, all letters, gibberish, HTML, characters which make up HTML, a scripting language or the entire works of Shakespeare. In a programming language, or even HTML, strings are wrapped in quotes, either double (“) or single (‘). For example if you see: name=”Stephen”, that means that the property “name” is a string with the value of “Stephen”.&#x20;

Of course there are subtypes for this as well. In this case, the differences are a combination of size and the format in which the data is stored.

The two main formats are:

* ASCII – one of the first coding systems that has 128 characters including English lowercase and capital letters, numbers and some special characters such as &,\*,@,!,), and #
* Unicode – This format allows over 110,000 characters in many different scripts. A script is a format of writing such as the Latin Script (i.e. the character set in English), Arabic Script and 121 others. (for more information on this see ([http://en.wikipedia.org/wiki/Script\_(Unicode)](http://en.wikipedia.org/wiki/Script_\(Unicode\))))

Some of the subtypes of strings which exist are:



| Name          | Ascii / Unicode | Length                                    |
| ------------- | --------------- | ----------------------------------------- |
| Char(x)       | Ascii           | Fixed at x characters                     |
| Varchar(x)    | Ascii           | From 0 to x characters                    |
| Varchar(max)  | Ascii           | From 0 to the upper limit of the database |
| nChar(x)      | Unicode         | Fixed at x characters                     |
| nVarchar(x)   | Unicode         | From 0 to x characters                    |
| nVarchar(max) | Unicode         | From 0 to the upper limit of the database |

For this class, we’re going to mostly use nvarchar(x). The x is a number that defines how long it is going to be. Therefore, nvarchar(25) is a Unicode string which is of variable length and can be up to 25 characters long.

### Dates

Dates refer to a particular point in time. Depending on the programming language being used, a date might be considered a complex data type since it can be broken down into sub parts. The parts of a date are:

* Year
* Month
* Day
* Hour
* Minute
* Second

Seems reasonable so far. Why are dates so complicated? Several Reasons.

#### Format

Humans write dates so many different ways. For example, Christmas day, 2014 can be written:

* 12/25/2014
* 12/25/14
* 12:25:14
* 25/12/2014 (in Europe)
* December 25, 2014
* December 25th, 2014
* December Twenty-Fifth, Two Thousand Fourteen
* 25 December 14
* Dec 25, 2014 AD
* Dec 25, 2014 CE (Common Era as opposed to BCE – Before Common Era)

And so on. Plus, when you add military time with a 24hour format and you have a number of ways to write the time. It’s tricky to make sure that computer knows which part of the date is what. If the computer thinks that 12/25/2014 is a date, it can compute time spans, add or subtract it with other dates, use that time to make decisions and other functions.

#### Time Zones

I tell you that the time for an appointment is 12pm. Is that Eastern? Central? GMT? What about Daylight Savings? What about those places that don’t observe Daylight Savings? Put in the wrong time zone and you can even be giving someone the wrong day if they are over the dateline.

For some interesting additional insights into time zones, check out this youtube video:

[The Problem with Time & Timezones - Computerphile](https://www.youtube.com/watch?v=-5wpm-gesOY)

#### Important Concepts About Dates

**GMT** – This stands for Greenwich Mean Time. When time zones were being created, there needed to be a starting point. This ended up being the Royal Observatory in Greenwich England. All of the other time zones are then calculated based on that spot. For example, Eastern Time is normally 5 hours behind GMT and is therefore considered -5GMT. During the summer is it -4 because of daylight savings.

**UTC** – It turns out that the way GMT was calculated wasn’t accurate enough for computers and more precise measurements since it allowed for a swing of almost 15 minutes depending on different times of the year (hence the “mean” in mean time. It was an average). On January 1, 1970 a coordinated switch to UTC occurred. UTC or Coordinated Universal Time is the same concept as GMT but more exact with the same time being coordinated with atomic clocks all over the world. UTC does not take into account leap seconds ( watch the video above to learn more about those ).

**Epoch Time** – An Epoch is the moment that something starts. For example, the epoch of UTC was midnight, January 1, 1970. Epoch time is a measurement from that moment until now, whenever NOW is. Usually it’s in seconds but sometimes in milliseconds. Why? Computers like numbers. Therefore, it’s easier to convert to a standard number to compare or add dates than it is to remember a combination of base 24 (hours in a day), base 60 (minutes in an hour or seconds in a minute), base 365 (days in a year), or base 7 (days in a week) numbers.

## Conclusion

Coming back up to the surface after diving into all the complexity, in spite of the detail, what we have are simply numbers, text, yes/no, and dates. The complexities are something we deal with when we need to and try not to think about when we don’t. However, as you will see many of these data types as we dive into the database world, it’s important to have been exposed to them.
