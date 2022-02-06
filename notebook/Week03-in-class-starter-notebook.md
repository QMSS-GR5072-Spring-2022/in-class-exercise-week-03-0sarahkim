</br>

### Instructions

This is a notebook with starter code for you to follow the examples that
we’ll review in class. This is a place for you to add your class notes.
*REMEMBER:* `push`ing back this annotated-by-you notebook and the
associated GitHub-flavored markdown file to your **GitHub Classroom**
repo counts towards you class participation grade.

</br>

### Loading packages

Let’s begin by loading all the packages that we’ll need today

\[INSERT YOUR NOTES HERE\]

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.3     v dplyr   1.0.7
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   2.0.0     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(nycflights13)
```

    ## Warning: package 'nycflights13' was built under R version 4.1.2

### Creating Tibbles

\[INSERT YOUR NOTES HERE\] Tibbles: modern ver on data frames -
dataframes w/o all the prior issues(keep strings as string, not factors,
etc) –created by tibble()

``` r
tibble(x = letters)  #create a tibble where x is all the alphabet that I have
```

    ## # A tibble: 26 x 1
    ##    x    
    ##    <chr>
    ##  1 a    
    ##  2 b    
    ##  3 c    
    ##  4 d    
    ##  5 e    
    ##  6 f    
    ##  7 g    
    ##  8 h    
    ##  9 i    
    ## 10 j    
    ## # ... with 16 more rows

## Printing

\[INSERT YOUR NOTES HERE\]
options(tibble.print_max=n,tibble.print_min=m) :^ makes you print n rows
instead of the default option of 10

``` r
tibble(x = -5:1000)
```

    ## # A tibble: 1,006 x 1
    ##        x
    ##    <int>
    ##  1    -5
    ##  2    -4
    ##  3    -3
    ##  4    -2
    ##  5    -1
    ##  6     0
    ##  7     1
    ##  8     2
    ##  9     3
    ## 10     4
    ## # ... with 996 more rows

## Subsetting

\[INSERT YOUR NOTES HERE\] Tibbles are strict about subsetting - it
always returns another tibble

``` r
df1 <- data.frame(x = 1:3, y = 3:1)
class(df1[, 1:2])
```

    ## [1] "data.frame"

``` r
class(df1[, 1])
```

    ## [1] "integer"

``` r
df2 <- tibble(x = 1:3, y = 3:1)
class(df2[, 1:2])
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

``` r
class(df2[, 1])
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

## To extract a single column use `[[` or `$`:

\[\[\]\]- are more Python-like $ - is more R

``` r
class(df2[[1]])
```

    ## [1] "integer"

``` r
class(df2$x)
```

    ## [1] "integer"

## Intro to `dplyr` package

\[INSERT YOUR NOTES HERE\]

``` r
## using data contained in the nycflights13 package that we loaded at the beginning of this notebook
dim(flights)
```

    ## [1] 336776     19

``` r
flights
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

## Single table verbs

\[INSERT YOUR NOTES HERE\]

## Filter rows with `filter()`

Very useful function- both filter() and arrange()

``` r
filter(flights, month == 1, day == 1)
```

    ## # A tibble: 842 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 832 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

## Filter rows with `filter()`

``` r
flights[flights$month == 1 & flights$day == 1, ]
```

    ## # A tibble: 842 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 832 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

## Arrange rows with `arrange()`

Useful when indexing dataframes in the order of columns

``` r
arrange(flights, year, month, day)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

\[INSERT YOUR NOTES HERE\]

``` r
arrange(flights, desc(arr_delay))
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     9      641            900      1301     1242           1530
    ##  2  2013     6    15     1432           1935      1137     1607           2120
    ##  3  2013     1    10     1121           1635      1126     1239           1810
    ##  4  2013     9    20     1139           1845      1014     1457           2210
    ##  5  2013     7    22      845           1600      1005     1044           1815
    ##  6  2013     4    10     1100           1900       960     1342           2211
    ##  7  2013     3    17     2321            810       911      135           1020
    ##  8  2013     7    22     2257            759       898      121           1026
    ##  9  2013    12     5      756           1700       896     1058           2020
    ## 10  2013     5     3     1133           2055       878     1250           2215
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

## Select columns with `select()`

\[INSERT YOUR NOTES HERE\]

## Select columns by name

\[INSERT YOUR NOTES HERE\]

``` r
select(flights, year, month, day)
```

    ## # A tibble: 336,776 x 3
    ##     year month   day
    ##    <int> <int> <int>
    ##  1  2013     1     1
    ##  2  2013     1     1
    ##  3  2013     1     1
    ##  4  2013     1     1
    ##  5  2013     1     1
    ##  6  2013     1     1
    ##  7  2013     1     1
    ##  8  2013     1     1
    ##  9  2013     1     1
    ## 10  2013     1     1
    ## # ... with 336,766 more rows

## Select all columns between year and day (inclusive)

not really recommended bc the order may change

``` r
select(flights, year:day)
```

    ## # A tibble: 336,776 x 3
    ##     year month   day
    ##    <int> <int> <int>
    ##  1  2013     1     1
    ##  2  2013     1     1
    ##  3  2013     1     1
    ##  4  2013     1     1
    ##  5  2013     1     1
    ##  6  2013     1     1
    ##  7  2013     1     1
    ##  8  2013     1     1
    ##  9  2013     1     1
    ## 10  2013     1     1
    ## # ... with 336,766 more rows

## Select all columns except those from year to day (inclusive)

\[INSERT YOUR NOTES HERE\]

``` r
select(flights, -(year:day))
```

    ## # A tibble: 336,776 x 16
    ##    dep_time sched_dep_time dep_delay arr_time sched_arr_time arr_delay carrier
    ##       <int>          <int>     <dbl>    <int>          <int>     <dbl> <chr>  
    ##  1      517            515         2      830            819        11 UA     
    ##  2      533            529         4      850            830        20 UA     
    ##  3      542            540         2      923            850        33 AA     
    ##  4      544            545        -1     1004           1022       -18 B6     
    ##  5      554            600        -6      812            837       -25 DL     
    ##  6      554            558        -4      740            728        12 UA     
    ##  7      555            600        -5      913            854        19 B6     
    ##  8      557            600        -3      709            723       -14 EV     
    ##  9      557            600        -3      838            846        -8 B6     
    ## 10      558            600        -2      753            745         8 AA     
    ## # ... with 336,766 more rows, and 9 more variables: flight <int>,
    ## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
    ## #   hour <dbl>, minute <dbl>, time_hour <dttm>

## Helper functions

## Use `rename()` to change variable names

\[INSERT YOUR NOTES HERE\]

``` r
rename(flights, tail_num = tailnum)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tail_num <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
colnames(flights)
```

    ##  [1] "year"           "month"          "day"            "dep_time"      
    ##  [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
    ##  [9] "arr_delay"      "carrier"        "flight"         "tailnum"       
    ## [13] "origin"         "dest"           "air_time"       "distance"      
    ## [17] "hour"           "minute"         "time_hour"

## Add new columns with `mutate()`

Columns to be transformed in a particular way

``` r
mutate(flights,
  gain = arr_delay - dep_delay,
  speed = distance / air_time * 60
)
```

    ## # A tibble: 336,776 x 21
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 13 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>,
    ## #   gain <dbl>, speed <dbl>

Other ways of using mutate

``` r
starwars %>%
  select(name:mass, gender, species) %>%
  mutate(
    type = case_when(
      height > 200 | mass > 200 ~ "large",
      species == "Droid"        ~ "robot",
      TRUE                      ~ "other"  
      # this "TRUE" code defines what to define everything                                              # else
    )
  )
```

    ## # A tibble: 87 x 6
    ##    name               height  mass gender    species type 
    ##    <chr>               <int> <dbl> <chr>     <chr>   <chr>
    ##  1 Luke Skywalker        172    77 masculine Human   other
    ##  2 C-3PO                 167    75 masculine Droid   robot
    ##  3 R2-D2                  96    32 masculine Droid   robot
    ##  4 Darth Vader           202   136 masculine Human   large
    ##  5 Leia Organa           150    49 feminine  Human   other
    ##  6 Owen Lars             178   120 masculine Human   other
    ##  7 Beru Whitesun lars    165    75 feminine  Human   other
    ##  8 R5-D4                  97    32 masculine Droid   robot
    ##  9 Biggs Darklighter     183    84 masculine Human   other
    ## 10 Obi-Wan Kenobi        182    77 masculine Human   other
    ## # ... with 77 more rows

## Summarise values with `summarise()`

``` r
summarise(flights,
  delay = mean(dep_delay, na.rm = TRUE)
)
```

    ## # A tibble: 1 x 1
    ##   delay
    ##   <dbl>
    ## 1  12.6

## Calculate stats by variable category

\[INSERT YOUR NOTES HERE\]

## `group_by()` examples:

Often used together with the summarise function

``` r
destinations <- group_by(flights, dest)
summarise(destinations,
  planes = n_distinct(tailnum),
  flights = n()
)
```

    ## # A tibble: 105 x 3
    ##    dest  planes flights
    ##    <chr>  <int>   <int>
    ##  1 ABQ      108     254
    ##  2 ACK       58     265
    ##  3 ALB      172     439
    ##  4 ANC        6       8
    ##  5 ATL     1180   17215
    ##  6 AUS      993    2439
    ##  7 AVL      159     275
    ##  8 BDL      186     443
    ##  9 BGR       46     375
    ## 10 BHM       45     297
    ## # ... with 95 more rows

## Pipe Operators and the `tidyverse`

\[INSERT YOUR NOTES HERE\]

## Different ways to organize code

\[INSERT YOUR NOTES HERE\]

``` r
a <- filter(mtcars, carb > 1)
b <- group_by(a, cyl)
c <- summarise(b, Avg_mpg = mean(mpg))
d <- arrange(c, desc(Avg_mpg))
print(d)
```

    ## # A tibble: 3 x 2
    ##     cyl Avg_mpg
    ##   <dbl>   <dbl>
    ## 1     4    25.9
    ## 2     6    19.7
    ## 3     8    15.1

\[INSERT YOUR NOTES HERE\]

``` r
arrange(
   summarize(
       group_by(
           filter(mtcars, carb > 1),
           cyl
          ),
       Avg_mpg = mean(mpg)
      ),
   desc(Avg_mpg)
 )
```

    ## # A tibble: 3 x 2
    ##     cyl Avg_mpg
    ##   <dbl>   <dbl>
    ## 1     4    25.9
    ## 2     6    19.7
    ## 3     8    15.1

\[INSERT YOUR NOTES HERE\]

``` r
mtcars %>%
        filter(carb > 1) %>%
        group_by(cyl) %>%
        summarise(Avg_mpg = mean(mpg)) %>%
        arrange(desc(Avg_mpg))
```

    ## # A tibble: 3 x 2
    ##     cyl Avg_mpg
    ##   <dbl>   <dbl>
    ## 1     4    25.9
    ## 2     6    19.7
    ## 3     8    15.1

## Separating

\[INSERT YOUR NOTES HERE\]

``` r
table3 %>% 
  separate(rate, into = c("cases", "population"), sep = "/")
```

    ## # A tibble: 6 x 4
    ##   country      year cases  population
    ##   <chr>       <int> <chr>  <chr>     
    ## 1 Afghanistan  1999 745    19987071  
    ## 2 Afghanistan  2000 2666   20595360  
    ## 3 Brazil       1999 37737  172006362 
    ## 4 Brazil       2000 80488  174504898 
    ## 5 China        1999 212258 1272915272
    ## 6 China        2000 213766 1280428583

\[INSERT YOUR NOTES HERE\]

``` r
#Separate year values after second element of value

table3 %>% 
  separate(year, into = c("century", "year"), sep = 2)
```

    ## # A tibble: 6 x 4
    ##   country     century year  rate             
    ##   <chr>       <chr>   <chr> <chr>            
    ## 1 Afghanistan 19      99    745/19987071     
    ## 2 Afghanistan 20      00    2666/20595360    
    ## 3 Brazil      19      99    37737/172006362  
    ## 4 Brazil      20      00    80488/174504898  
    ## 5 China       19      99    212258/1272915272
    ## 6 China       20      00    213766/1280428583

## Uniting

\[INSERT YOUR NOTES HERE\]

``` r
table5[1:2,]
```

    ## # A tibble: 2 x 4
    ##   country     century year  rate         
    ##   <chr>       <chr>   <chr> <chr>        
    ## 1 Afghanistan 19      99    745/19987071 
    ## 2 Afghanistan 20      00    2666/20595360

``` r
table5 %>% 
  unite(new, century, year, sep = "")
```

    ## # A tibble: 6 x 3
    ##   country     new   rate             
    ##   <chr>       <chr> <chr>            
    ## 1 Afghanistan 1999  745/19987071     
    ## 2 Afghanistan 2000  2666/20595360    
    ## 3 Brazil      1999  37737/172006362  
    ## 4 Brazil      2000  80488/174504898  
    ## 5 China       1999  212258/1272915272
    ## 6 China       2000  213766/1280428583

## Joining (merging) data in the Tidyverse

\[INSERT YOUR NOTES HERE\]

## Keys

\[INSERT YOUR NOTES HERE\]

``` r
planes %>% 
  count(tailnum) %>% 
  filter(n > 1)
```

    ## # A tibble: 0 x 2
    ## # ... with 2 variables: tailnum <chr>, n <int>

## Mutating Joins

\[INSERT YOUR NOTES HERE\]

``` r
flights2 <- flights %>% 
  select(year:day, hour, origin, dest, tailnum, carrier)
flights2
```

    ## # A tibble: 336,776 x 8
    ##     year month   day  hour origin dest  tailnum carrier
    ##    <int> <int> <int> <dbl> <chr>  <chr> <chr>   <chr>  
    ##  1  2013     1     1     5 EWR    IAH   N14228  UA     
    ##  2  2013     1     1     5 LGA    IAH   N24211  UA     
    ##  3  2013     1     1     5 JFK    MIA   N619AA  AA     
    ##  4  2013     1     1     5 JFK    BQN   N804JB  B6     
    ##  5  2013     1     1     6 LGA    ATL   N668DN  DL     
    ##  6  2013     1     1     5 EWR    ORD   N39463  UA     
    ##  7  2013     1     1     6 EWR    FLL   N516JB  B6     
    ##  8  2013     1     1     6 LGA    IAD   N829AS  EV     
    ##  9  2013     1     1     6 JFK    MCO   N593JB  B6     
    ## 10  2013     1     1     6 LGA    ORD   N3ALAA  AA     
    ## # ... with 336,766 more rows

\[INSERT YOUR NOTES HERE\]

``` r
# the airlines dataset looks like:
head(airlines)
```

    ## # A tibble: 6 x 2
    ##   carrier name                    
    ##   <chr>   <chr>                   
    ## 1 9E      Endeavor Air Inc.       
    ## 2 AA      American Airlines Inc.  
    ## 3 AS      Alaska Airlines Inc.    
    ## 4 B6      JetBlue Airways         
    ## 5 DL      Delta Air Lines Inc.    
    ## 6 EV      ExpressJet Airlines Inc.

\[INSERT YOUR NOTES HERE\]

``` r
flights2 %>%
  select(-origin, -dest) %>% 
  left_join(airlines, by = "carrier")
```

    ## # A tibble: 336,776 x 7
    ##     year month   day  hour tailnum carrier name                    
    ##    <int> <int> <int> <dbl> <chr>   <chr>   <chr>                   
    ##  1  2013     1     1     5 N14228  UA      United Air Lines Inc.   
    ##  2  2013     1     1     5 N24211  UA      United Air Lines Inc.   
    ##  3  2013     1     1     5 N619AA  AA      American Airlines Inc.  
    ##  4  2013     1     1     5 N804JB  B6      JetBlue Airways         
    ##  5  2013     1     1     6 N668DN  DL      Delta Air Lines Inc.    
    ##  6  2013     1     1     5 N39463  UA      United Air Lines Inc.   
    ##  7  2013     1     1     6 N516JB  B6      JetBlue Airways         
    ##  8  2013     1     1     6 N829AS  EV      ExpressJet Airlines Inc.
    ##  9  2013     1     1     6 N593JB  B6      JetBlue Airways         
    ## 10  2013     1     1     6 N3ALAA  AA      American Airlines Inc.  
    ## # ... with 336,766 more rows

\[INSERT YOUR NOTES HERE\]

``` r
flights2 %>%
  select(-origin, -dest) %>% 
  left_join(airlines, by = "carrier")
```

    ## # A tibble: 336,776 x 7
    ##     year month   day  hour tailnum carrier name                    
    ##    <int> <int> <int> <dbl> <chr>   <chr>   <chr>                   
    ##  1  2013     1     1     5 N14228  UA      United Air Lines Inc.   
    ##  2  2013     1     1     5 N24211  UA      United Air Lines Inc.   
    ##  3  2013     1     1     5 N619AA  AA      American Airlines Inc.  
    ##  4  2013     1     1     5 N804JB  B6      JetBlue Airways         
    ##  5  2013     1     1     6 N668DN  DL      Delta Air Lines Inc.    
    ##  6  2013     1     1     5 N39463  UA      United Air Lines Inc.   
    ##  7  2013     1     1     6 N516JB  B6      JetBlue Airways         
    ##  8  2013     1     1     6 N829AS  EV      ExpressJet Airlines Inc.
    ##  9  2013     1     1     6 N593JB  B6      JetBlue Airways         
    ## 10  2013     1     1     6 N3ALAA  AA      American Airlines Inc.  
    ## # ... with 336,766 more rows

## Inner Join

\[INSERT YOUR NOTES HERE\]

``` r
x <- tribble(
  ~key, ~val_x,
     1, "x1",
     2, "x2",
     3, "x3"
)
y <- tribble(
  ~key, ~val_y,
     1, "y1",
     2, "y2",
     4, "y3"
)
```

\[INSERT YOUR NOTES HERE\]

``` r
x %>% 
  inner_join(y, by = "key")
```

    ## # A tibble: 2 x 3
    ##     key val_x val_y
    ##   <dbl> <chr> <chr>
    ## 1     1 x1    y1   
    ## 2     2 x2    y2

## Outer joins

\[INSERT YOUR NOTES HERE\]

``` r
#leftjoin() with same variable name in two datasets
flights2 %>% 
  left_join(planes, by = "tailnum")
```

    ## # A tibble: 336,776 x 16
    ##    year.x month   day  hour origin dest  tailnum carrier year.y type            
    ##     <int> <int> <int> <dbl> <chr>  <chr> <chr>   <chr>    <int> <chr>           
    ##  1   2013     1     1     5 EWR    IAH   N14228  UA        1999 Fixed wing mult~
    ##  2   2013     1     1     5 LGA    IAH   N24211  UA        1998 Fixed wing mult~
    ##  3   2013     1     1     5 JFK    MIA   N619AA  AA        1990 Fixed wing mult~
    ##  4   2013     1     1     5 JFK    BQN   N804JB  B6        2012 Fixed wing mult~
    ##  5   2013     1     1     6 LGA    ATL   N668DN  DL        1991 Fixed wing mult~
    ##  6   2013     1     1     5 EWR    ORD   N39463  UA        2012 Fixed wing mult~
    ##  7   2013     1     1     6 EWR    FLL   N516JB  B6        2000 Fixed wing mult~
    ##  8   2013     1     1     6 LGA    IAD   N829AS  EV        1998 Fixed wing mult~
    ##  9   2013     1     1     6 JFK    MCO   N593JB  B6        2004 Fixed wing mult~
    ## 10   2013     1     1     6 LGA    ORD   N3ALAA  AA          NA <NA>            
    ## # ... with 336,766 more rows, and 6 more variables: manufacturer <chr>,
    ## #   model <chr>, engines <int>, seats <int>, speed <int>, engine <chr>

\[INSERT YOUR NOTES HERE\]

``` r
#leftjoin() with diff't variable name in two datasets
flights2 %>% 
  left_join(airports, c("dest" = "faa"))
```

    ## # A tibble: 336,776 x 15
    ##     year month   day  hour origin dest  tailnum carrier name     lat   lon   alt
    ##    <int> <int> <int> <dbl> <chr>  <chr> <chr>   <chr>   <chr>  <dbl> <dbl> <dbl>
    ##  1  2013     1     1     5 EWR    IAH   N14228  UA      Georg~  30.0 -95.3    97
    ##  2  2013     1     1     5 LGA    IAH   N24211  UA      Georg~  30.0 -95.3    97
    ##  3  2013     1     1     5 JFK    MIA   N619AA  AA      Miami~  25.8 -80.3     8
    ##  4  2013     1     1     5 JFK    BQN   N804JB  B6      <NA>    NA    NA      NA
    ##  5  2013     1     1     6 LGA    ATL   N668DN  DL      Harts~  33.6 -84.4  1026
    ##  6  2013     1     1     5 EWR    ORD   N39463  UA      Chica~  42.0 -87.9   668
    ##  7  2013     1     1     6 EWR    FLL   N516JB  B6      Fort ~  26.1 -80.2     9
    ##  8  2013     1     1     6 LGA    IAD   N829AS  EV      Washi~  38.9 -77.5   313
    ##  9  2013     1     1     6 JFK    MCO   N593JB  B6      Orlan~  28.4 -81.3    96
    ## 10  2013     1     1     6 LGA    ORD   N3ALAA  AA      Chica~  42.0 -87.9   668
    ## # ... with 336,766 more rows, and 3 more variables: tz <dbl>, dst <chr>,
    ## #   tzone <chr>

## Gathering

\[INSERT YOUR NOTES HERE\]

``` r
table4a
```

    ## # A tibble: 3 x 3
    ##   country     `1999` `2000`
    ## * <chr>        <int>  <int>
    ## 1 Afghanistan    745   2666
    ## 2 Brazil       37737  80488
    ## 3 China       212258 213766

\[INSERT YOUR NOTES HERE\]

``` r
# Note that columns are numeric, so we use backticks
# More typically we can just refer to column names.
table4a %>% 
  gather(`1999`, `2000`, key = "year", value = "cases")
```

    ## # A tibble: 6 x 3
    ##   country     year   cases
    ##   <chr>       <chr>  <int>
    ## 1 Afghanistan 1999     745
    ## 2 Brazil      1999   37737
    ## 3 China       1999  212258
    ## 4 Afghanistan 2000    2666
    ## 5 Brazil      2000   80488
    ## 6 China       2000  213766

## Spreading

\[INSERT YOUR NOTES HERE\]

``` r
table2 %>%
    spread(key = type, value = count)
```

    ## # A tibble: 6 x 4
    ##   country      year  cases population
    ##   <chr>       <int>  <int>      <int>
    ## 1 Afghanistan  1999    745   19987071
    ## 2 Afghanistan  2000   2666   20595360
    ## 3 Brazil       1999  37737  172006362
    ## 4 Brazil       2000  80488  174504898
    ## 5 China        1999 212258 1272915272
    ## 6 China        2000 213766 1280428583
