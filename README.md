# Today-I-Leared (TIL)

Documenting software-things I learn almost everyday.
Inspired by 
[jbranchaud/til](https://github.com/jbranchaud/til).

##### How This Will Be Organized

Start simple–one `README.md` (this one) for all entries.
There will be no categorization yet
because I am just getting started
and want to mitigate the friction and frills.
So, I'll start by simply keying each entry 
by time, fully knowing that as the entry list 
grows (hopefully)–I'll eventually index them differently.

---

# Entries

##### 2020-05-27

I was browsing the [Scala 2.13.0 release notes](https://github.com/scala/scala/releases/v2.13.0)
and came across the change "Partial unification on by default".
[djspiewak's gist](https://gist.github.com/djspiewak/7a81a395c461fd3a09a6941d4cd040f2)
explained the motivation nicely–I've actually read it multiple times but
today's pass-through led me to internalize the take away:

> ...if your type constructor takes multiple parameters, 
you should order them such that the parameters you expect users to 
vary (i.e. write a map function over, change frequently between 
functions, etc) should be right-most, while the parameters you expect 
to be consistent (i.e. the same at multiple unrelated places in the 
code) should be left-most.

Doing so will allow the compiler to help you in the
edge cases. To me, this also rhymes with `Either[Error, A]`.

##### 2020-05-28

Timestamp timezone handling with Scala/Java and PostgreSQL
can get tricky. There are layers of conversions
and data types between application, driver, and the database itself.
Today I was reminded of these nuances for both read and writes.
UTC for storage is preferred, of course, but when rubber meets the road
here are some nice resources I came across today to color this in practice:

1. PostgreSQL, [All timezone-aware dates and times are stored internally in UTC.](https://www.postgresql.org/docs/11/datatype-datetime.html#DATATYPE-TIMEZONES)
1. Using a joda-time/JDBC app layer, avoid a `LocalDateTime` hop
and jump to `java.sql.Timestamp` from joda `DateTime` (with timezone)
via `getMillis`.	
1. [Great Stack Overflow answer](https://stackoverflow.com/a/6627999) that outlines the above and
when one may want to deviate as well.