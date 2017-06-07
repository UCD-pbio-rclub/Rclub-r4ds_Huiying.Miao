# week9
huiyingmiao  
June 5, 2017  



# 11 DATA IMPORT

```r
library(tidyverse)
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

```r
read_csv("The first line of metadata
  The second line of metadata
  x,y,z
  1,2,3",skip=2)
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```

```r
read_csv("#the comment i want to skip
         x,y,z
         1,2,3",comment="#")
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```

```r
read_csv("1,2,3\n 4,5,6",col_names = FALSE)
```

```
## # A tibble: 2 × 3
##      X1    X2    X3
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

```r
read_csv("1,2,3\n 4,5,6",col_names =c( "X","Y","Z"))# a vector as name--c()
```

```
## # A tibble: 2 × 3
##       X     Y     Z
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```


```r
read_csv("a,b,c\n n1,n2,.", na =".") #na should be low case~
```

```
## # A tibble: 1 × 3
##       a     b     c
##   <chr> <chr> <chr>
## 1    n1    n2  <NA>
```

## 11.2.2 Exercises
### 1 What function would you use to read a file where fields were separated with
“|”?

```r
read_delim("a|b\n1.0|2.0", delim = "|")
```

```
## # A tibble: 1 × 2
##       a     b
##   <dbl> <dbl>
## 1     1     2
```
## 2 Apart from file, skip, and comment, what other arguments do read_csv() and read_tsv() have in common?

read_csv(file, **col_names = TRUE**, **col_types = NULL**,
  **locale = default_locale()**, **na = c("", "NA")**, **quoted_na = TRUE**,
  **quote = "\""**, comment = "", **trim_ws = TRUE**, skip = 0, **n_max = Inf**,
  **guess_max = min(1000, n_max)**, **progress = show_progress()**)
  
read_tsv(file, col_names = TRUE, col_types = NULL,
  locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
  quote = "\"", comment = "", trim_ws = TRUE, skip = 0, n_max = Inf,
  guess_max = min(1000, n_max), progress = show_progress())

## 3 What are the most important arguments to read_fwf()?

read_fwf(file, **col_positions**, col_types = NULL, locale = default_locale(),
  na = c("", "NA"), comment = "", skip = 0, n_max = Inf,
  guess_max = min(n_max, 1000), progress = show_progress())
  
## 4 Sometimes strings in a CSV file contain commas. To prevent them from causing problems they need to be surrounded by a quoting character, like " or '. By convention, read_csv() assumes that the quoting character will be ", and if you want to change it you’ll need to use read_delim() instead. What arguments do you need to specify to read the following text into a data frame?

"x,y\n1,'a,b'"


```r
read_csv("x,y\n1,'a,b'",quote="'")
```

```
## # A tibble: 1 × 2
##       x     y
##   <int> <chr>
## 1     1   a,b
```
## 5 Identify what is wrong with each of the following inline CSV files. What happens when you run the code?


```r
read_csv("a,b\n1,2,3\n4,5,6")#one colume is dropped.
```

```
## Warning: 2 parsing failures.
## row col  expected    actual         file
##   1  -- 2 columns 3 columns literal data
##   2  -- 2 columns 3 columns literal data
```

```
## # A tibble: 2 × 2
##       a     b
##   <int> <int>
## 1     1     2
## 2     4     5
```


```r
read_csv("a,b,c\n1,2\n1,2,3,4")#numbers of columes and that in the header don't match.
```

```
## Warning: 2 parsing failures.
## row col  expected    actual         file
##   1  -- 3 columns 2 columns literal data
##   2  -- 3 columns 4 columns literal data
```

```
## # A tibble: 2 × 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2    NA
## 2     1     2     3
```


```r
read_csv("a,b\n\"1")# quote? I dont know...
```

```
## Warning: 2 parsing failures.
## row col                     expected    actual         file
##   1  a  closing quote at end of file           literal data
##   1  -- 2 columns                    1 columns literal data
```

```
## # A tibble: 1 × 2
##       a     b
##   <int> <chr>
## 1     1  <NA>
```



```r
read_csv("a,b\n1,2\na,b")# what do you want to say?
```

```
## # A tibble: 2 × 2
##       a     b
##   <chr> <chr>
## 1     1     2
## 2     a     b
```

```r
read_csv("a;b\n1;3")# delim=";"
```

```
## # A tibble: 1 × 1
##   `a;b`
##   <chr>
## 1   1;3
```


```r
read_delim("a;b\n1;3",delim  = ";")
```

```
## # A tibble: 1 × 2
##       a     b
##   <int> <int>
## 1     1     3
```

============================

```r
str(parse_integer(c("1", "2", "3")))
```

```
##  int [1:3] 1 2 3
```

```r
str(parse_logical(c("TRUE", "FALSE", "NA")))
```

```
##  logi [1:3] TRUE FALSE NA
```

```r
str(parse_date(c("2010-01-01", "1979-10-14")))
```

```
##  Date[1:2], format: "2010-01-01" "1979-10-14"
```


```r
parse_integer(c("1", "231", ".", "456"),na=".")
```

```
## [1]   1 231  NA 456
```


```r
x<-parse_integer(c("123", "345", "abc", "123.45"))
```

```
## Warning: 2 parsing failures.
## row col               expected actual
##   3  -- an integer                abc
##   4  -- no trailing characters    .45
```

```r
x
```

```
## [1] 123 345  NA  NA
## attr(,"problems")
## # A tibble: 2 × 4
##     row   col               expected actual
##   <int> <int>                  <chr>  <chr>
## 1     3    NA             an integer    abc
## 2     4    NA no trailing characters    .45
```

```r
problems(x)
```

```
## # A tibble: 2 × 4
##     row   col               expected actual
##   <int> <int>                  <chr>  <chr>
## 1     3    NA             an integer    abc
## 2     4    NA no trailing characters    .45
```

**11.3.1 Numbers**

```r
parse_double("1,23",locale = locale(decimal_mark = ","))#You can override the default value of . by creating a new locale and setting the decimal_mark argument.
```

```
## [1] 1.23
```


```r
parse_number("$100")#it ignores non-numeric characters before and after the number. 
```

```
## [1] 100
```

```r
parse_number("123,456,789")
```

```
## [1] 123456789
```

```r
parse_number("123.456.789")
```

```
## [1] 123.456
```

```r
parse_number("123.456.789",locale = locale(grouping_mark = "."))#combination of parse_number() and the locale
```

```
## [1] 123456789
```

**11.3.2 Strings**

we can get at the underlying representation of a string using charToRaw():

```r
charToRaw("hadley")
```

```
## [1] 68 61 64 6c 65 79
```


```r
x2 <- "\x82\xb1\x82\xf1\x82\xc9\x82\xbf\x82\xcd"#The first argument to guess_encoding() can either be a path to a file, or, as in this case, a raw vector (useful if the strings are already in R).
guess_encoding(charToRaw(x2))
```

```
## # A tibble: 1 × 2
##   encoding confidence
##      <chr>      <dbl>
## 1   KOI8-R       0.42
```
**11.3.4 Dates, date-times, and times**

```r
parse_datetime("2010-10-10T2009")#there's a Capital T.
```

```
## [1] "2010-10-10 20:09:00 UTC"
```

```r
parse_datetime("2010-10-10")#If time is omitted, it will be set to midnight
```

```
## [1] "2010-10-10 UTC"
```

```r
parse_datetime("20101010")
```

```
## [1] "2010-10-10 UTC"
```

```r
parse_date("2010/10/10")#expects a four digit year, a - or /, the month, a - or /, then the day.
```

```
## [1] "2010-10-10"
```


```r
library(hms)
parse_time("10:10 am")
```

```
## 10:10:00
```

```r
parse_time("10:10 pm")
```

```
## 22:10:00
```

## 11.3.5 Exercises

### 1. What are the most important arguments to locale()?

locale(date_names = "en", date_format = "%AD", time_format = "%AT",
  decimal_mark = ".", grouping_mark = ",", tz = "UTC",
  encoding = "UTF-8", asciify = FALSE)

### 2. What happens if you try and set decimal_mark and grouping_mark to the same character? What happens to the default value of grouping_mark when you set decimal_mark to “,”? What happens to the default value of decimal_mark when you set the grouping_mark to “.”?

if set decimal_mark and grouping_mark to the same character, it will return Error: `decimal_mark` and `grouping_mark` must be different.

parse_number("123,456.789", locale = locale(decimal_mark = ".",grouping_mark = "."))
```
when you set decimal_mark to “,”, grouping_mark is set to a period.

```r
parse_number("12.34,56", locale = locale(decimal_mark = ","))
```

```
## [1] 1234.56
```
when you set the grouping_mark to “.”,decimal_mark is set to a comma.

```r
parse_number("12.34,56", locale = locale(grouping_mark = "."))
```

```
## [1] 1234.56
```


```r
locale(decimal_mark = ",")
```

```
## <locale>
## Numbers:  123.456,78
## Formats:  %AD / %AT
## Timezone: UTC
## Encoding: UTF-8
## <date_names>
## Days:   Sunday (Sun), Monday (Mon), Tuesday (Tue), Wednesday (Wed),
##         Thursday (Thu), Friday (Fri), Saturday (Sat)
## Months: January (Jan), February (Feb), March (Mar), April (Apr), May
##         (May), June (Jun), July (Jul), August (Aug), September
##         (Sep), October (Oct), November (Nov), December (Dec)
## AM/PM:  AM/PM
```

```r
 locale(grouping_mark = ".")
```

```
## <locale>
## Numbers:  123.456,78
## Formats:  %AD / %AT
## Timezone: UTC
## Encoding: UTF-8
## <date_names>
## Days:   Sunday (Sun), Monday (Mon), Tuesday (Tue), Wednesday (Wed),
##         Thursday (Thu), Friday (Fri), Saturday (Sat)
## Months: January (Jan), February (Feb), March (Mar), April (Apr), May
##         (May), June (Jun), July (Jul), August (Aug), September
##         (Sep), October (Oct), November (Nov), December (Dec)
## AM/PM:  AM/PM
```

### 3. I didn’t discuss the date_format and time_format options to locale(). What do they do? Construct an example that shows when they might be useful.



```r
parse_date("1 janvier 2015", "%d %B %Y", locale = locale("fr"))
```

```
## [1] "2015-01-01"
```

### 4. If you live outside the US, create a new locale object that encapsulates the settings for the types of file you read most commonly.

???

### 5. What’s the difference between read_csv() and read_csv2()?

read_csv, comma delimited files;   
read_csv2, semicolon seperated files.


### 6.What are the most common encodings used in Europe? What are the most common encodings used in Asia? Do some googling to find out.

see in wikipedia...

### 7. Generate the correct format string to parse each of the following dates and times:

d1 <- "January 1, 2010"
d2 <- "2015-Mar-07"
d3 <- "06-Jun-2017"
d4 <- c("August 19 (2015)", "July 1 (2015)")
d5 <- "12/30/14" # Dec 30, 2014
t1 <- "1705"
t2 <- "11:15:10.12 PM"

```r
d1 <- "January 1, 2010"
d2 <- "2015-Mar-07"
d3 <- "06-Jun-2017"
d4 <- c("August 19 (2015)", "July 1 (2015)")
d5 <- "12/30/14" # Dec 30, 2014
t1 <- "1705"
t2 <- "11:15:10.12 PM"
parse_date(d1, "%B %d, %Y")
```

```
## [1] "2010-01-01"
```

```r
parse_date(d2,"%Y-%b-%d")
```

```
## [1] "2015-03-07"
```

```r
parse_date(d3,"%d-%b-%Y")
```

```
## [1] "2017-06-06"
```

```r
parse_date(d4,"%B %d (%Y)")
```

```
## [1] "2015-08-19" "2015-07-01"
```

```r
parse_date(d5,"%m/%d/%y")
```

```
## [1] "2014-12-30"
```

```r
parse_time(t1,"%H%M")
```

```
## 17:05:00
```

```r
parse_time(t2,"%I:%M:%OS %p")
```

```
## 23:15:10.12
```

