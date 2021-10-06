Homework2
================

\#\#Problem 1 \#Import and view \#I will import the Mr. Trash Wheel
sheet, clean its column names, and examine the structure, head, and tail
of the data set. \#Then, I will view the data set

``` r
df_one = read_excel("Trash-Wheel-Collection-Totals-8-6-19.xlsx", sheet = "Mr. Trash Wheel")
```

    ## New names:
    ## * `` -> ...15
    ## * `` -> ...16
    ## * `` -> ...17

``` r
df_one = janitor::clean_names(df_one)
str(df_one)
```

    ## tibble [406 × 17] (S3: tbl_df/tbl/data.frame)
    ##  $ dumpster          : num [1:406] 1 2 3 4 5 6 7 8 NA 9 ...
    ##  $ month             : chr [1:406] "May" "May" "May" "May" ...
    ##  $ year              : num [1:406] 2014 2014 2014 2014 2014 ...
    ##  $ date              : POSIXct[1:406], format: "2014-05-16" "2014-05-16" ...
    ##  $ weight_tons       : num [1:406] 4.31 2.74 3.45 3.1 4.06 ...
    ##  $ volume_cubic_yards: num [1:406] 18 13 15 15 18 13 8 16 116 14 ...
    ##  $ plastic_bottles   : num [1:406] 1450 1120 2450 2380 980 1430 910 3580 14300 2400 ...
    ##  $ polystyrene       : num [1:406] 1820 1030 3100 2730 870 ...
    ##  $ cigarette_butts   : num [1:406] 126000 91000 105000 100000 120000 90000 56000 112000 800000 98000 ...
    ##  $ glass_bottles     : num [1:406] 72 42 50 52 72 46 32 58 424 49 ...
    ##  $ grocery_bags      : num [1:406] 584 496 1080 896 368 ...
    ##  $ chip_bags         : num [1:406] 1162 874 2032 1971 753 ...
    ##  $ sports_balls      : num [1:406] 7.2 5.2 6 6 7.2 5.2 3.2 6.4 46.4 5.6 ...
    ##  $ homes_powered     : num [1:406] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ x15               : chr [1:406] NA NA NA NA ...
    ##  $ x16               : logi [1:406] NA NA NA NA NA NA ...
    ##  $ x17               : logi [1:406] NA NA NA NA NA NA ...

``` r
head(df_one)
```

    ## # A tibble: 6 × 17
    ##   dumpster month  year date                weight_tons volume_cubic_yards
    ##      <dbl> <chr> <dbl> <dttm>                    <dbl>              <dbl>
    ## 1        1 May    2014 2014-05-16 00:00:00        4.31                 18
    ## 2        2 May    2014 2014-05-16 00:00:00        2.74                 13
    ## 3        3 May    2014 2014-05-16 00:00:00        3.45                 15
    ## 4        4 May    2014 2014-05-17 00:00:00        3.1                  15
    ## 5        5 May    2014 2014-05-17 00:00:00        4.06                 18
    ## 6        6 May    2014 2014-05-20 00:00:00        2.71                 13
    ## # … with 11 more variables: plastic_bottles <dbl>, polystyrene <dbl>,
    ## #   cigarette_butts <dbl>, glass_bottles <dbl>, grocery_bags <dbl>,
    ## #   chip_bags <dbl>, sports_balls <dbl>, homes_powered <dbl>, x15 <chr>,
    ## #   x16 <lgl>, x17 <lgl>

``` r
tail(df_one)
```

    ## # A tibble: 6 × 17
    ##   dumpster month        year date                weight_tons volume_cubic_yards
    ##      <dbl> <chr>       <dbl> <dttm>                    <dbl>              <dbl>
    ## 1       NA May Total      NA NA                        33.4                 165
    ## 2      342 June         2019 2019-06-12 00:00:00        3.23                 15
    ## 3      343 June         2019 2019-06-12 00:00:00        3.08                 15
    ## 4      344 June         2019 2019-06-17 00:00:00        3.02                 15
    ## 5       NA June Total     NA NA                         9.33                 45
    ## 6       NA Grand Total    NA NA                      1122.                 5347
    ## # … with 11 more variables: plastic_bottles <dbl>, polystyrene <dbl>,
    ## #   cigarette_butts <dbl>, glass_bottles <dbl>, grocery_bags <dbl>,
    ## #   chip_bags <dbl>, sports_balls <dbl>, homes_powered <dbl>, x15 <chr>,
    ## #   x16 <lgl>, x17 <lgl>

``` r
view(df_one)
```

\#Clean dataset \#I will omit the last columns ‘x15’, ‘x16’, and ‘x17’,
which do not contain data \#Then I will drop other ‘NA’ values

``` r
df_two = select(df_one, -c("x15", "x16", "x17"))
view(df_two)
df_three = drop_na(df_two)
view(df_three)
```

\#Calculate the number of sports balls

``` r
sb = select(df_three, "sports_balls")
sum(sb)
```

    ## [1] 4064.6

\#\#\#4065 is the closest integer value of sports balls

\#\#This calculation could also be achieved by the “pull” function,
which I will show below

``` r
df_three %>% pull("sports_balls") %>% sum()
```

    ## [1] 4064.6

\#Import and view \#I will import the 2019 precipitation sheet, clean
its column names, and examine the structure, head, and tail of the data
set. \#Then, I will view the data set

``` r
df_four = read_excel("Trash-Wheel-Collection-Totals-8-6-19.xlsx", sheet = "2019 Precipitation")
```

    ## New names:
    ## * `` -> ...2

``` r
df_four = janitor::clean_names(df_four)
str(df_four)
```

    ## tibble [14 × 2] (S3: tbl_df/tbl/data.frame)
    ##  $ precipitation_in: chr [1:14] "Month" "1" "2" "3" ...
    ##  $ x2              : chr [1:14] "Total" "3.1" "3.64" "4.47" ...

``` r
head(df_four)
```

    ## # A tibble: 6 × 2
    ##   precipitation_in x2   
    ##   <chr>            <chr>
    ## 1 Month            Total
    ## 2 1                3.1  
    ## 3 2                3.64 
    ## 4 3                4.47 
    ## 5 4                1.46 
    ## 6 5                3.58

``` r
tail(df_four)
```

    ## # A tibble: 6 × 2
    ##   precipitation_in x2                
    ##   <chr>            <chr>             
    ## 1 8                <NA>              
    ## 2 9                <NA>              
    ## 3 10               <NA>              
    ## 4 11               <NA>              
    ## 5 12               <NA>              
    ## 6 <NA>             16.670000000000002

``` r
view(df_four)
```

\#The first row contains column names. \#I will clean the column names.

``` r
df_five = read_excel("Trash-Wheel-Collection-Totals-8-6-19.xlsx", sheet = "2019 Precipitation", skip = 1, col_names = TRUE)
df_five = janitor::clean_names(df_five)
str(df_five)
```

    ## tibble [13 × 2] (S3: tbl_df/tbl/data.frame)
    ##  $ month: num [1:13] 1 2 3 4 5 6 7 8 9 10 ...
    ##  $ total: num [1:13] 3.1 3.64 4.47 1.46 3.58 0.42 NA NA NA NA ...

``` r
head(df_five)
```

    ## # A tibble: 6 × 2
    ##   month total
    ##   <dbl> <dbl>
    ## 1     1  3.1 
    ## 2     2  3.64
    ## 3     3  4.47
    ## 4     4  1.46
    ## 5     5  3.58
    ## 6     6  0.42

``` r
tail(df_five)
```

    ## # A tibble: 6 × 2
    ##   month total
    ##   <dbl> <dbl>
    ## 1     8  NA  
    ## 2     9  NA  
    ## 3    10  NA  
    ## 4    11  NA  
    ## 5    12  NA  
    ## 6    NA  16.7

``` r
view(df_five)
```

\#Now I will omit rows with missing data

``` r
df_six = drop_na(df_five)
view(df_six)
```

# I will add a year column to this data set

``` r
df_2019 = df_six %>% mutate(year = 2019)
view(df_2019)
```

\#\#\#Now I will move on to the 2018 precipitation sheet

``` r
df_seven = read_excel("Trash-Wheel-Collection-Totals-8-6-19.xlsx", sheet = "2018 Precipitation")
```

    ## New names:
    ## * `` -> ...2

``` r
df_seven = janitor::clean_names(df_seven)
str(df_seven)
```

    ## tibble [14 × 2] (S3: tbl_df/tbl/data.frame)
    ##  $ precipitation_in: chr [1:14] "Month" "1" "2" "3" ...
    ##  $ x2              : chr [1:14] "Total" "0.94" "4.8" "2.69" ...

``` r
head(df_seven)
```

    ## # A tibble: 6 × 2
    ##   precipitation_in x2                
    ##   <chr>            <chr>             
    ## 1 Month            Total             
    ## 2 1                0.94              
    ## 3 2                4.8               
    ## 4 3                2.69              
    ## 5 4                4.6900000000000004
    ## 6 5                9.27

``` r
tail(df_seven)
```

    ## # A tibble: 6 × 2
    ##   precipitation_in x2   
    ##   <chr>            <chr>
    ## 1 8                6.45 
    ## 2 9                10.47
    ## 3 10               2.12 
    ## 4 11               7.82 
    ## 5 12               6.11 
    ## 6 <NA>             70.33

``` r
view(df_seven)
```

\#The first row contains column names. \#I will clean the column names
and drop the NA values

``` r
df_eight = read_excel("Trash-Wheel-Collection-Totals-8-6-19.xlsx", sheet = "2018 Precipitation", skip = 1, col_names = TRUE)
df_eight = janitor::clean_names(df_eight)
str(df_eight)
```

    ## tibble [13 × 2] (S3: tbl_df/tbl/data.frame)
    ##  $ month: num [1:13] 1 2 3 4 5 6 7 8 9 10 ...
    ##  $ total: num [1:13] 0.94 4.8 2.69 4.69 9.27 ...

``` r
head(df_eight)
```

    ## # A tibble: 6 × 2
    ##   month total
    ##   <dbl> <dbl>
    ## 1     1  0.94
    ## 2     2  4.8 
    ## 3     3  2.69
    ## 4     4  4.69
    ## 5     5  9.27
    ## 6     6  4.77

``` r
tail(df_eight)
```

    ## # A tibble: 6 × 2
    ##   month total
    ##   <dbl> <dbl>
    ## 1     8  6.45
    ## 2     9 10.5 
    ## 3    10  2.12
    ## 4    11  7.82
    ## 5    12  6.11
    ## 6    NA 70.3

``` r
view(df_eight)
df_nine = drop_na(df_eight)
view(df_nine)
```

# I will add a year column to this data set

``` r
df_2018 = df_nine %>% mutate(year = 2018)
view(df_2018)
```

\#I will convert from numeric value to month name for 2018

``` r
df_2018_m = df_2018 %>% mutate(month_name = month.name[month])
view(df_2018_m)
```

\#I will convert from numeric value to month name for 2019

``` r
df_2019_m = df_2019 %>% mutate(month_name = month.name[month])
view(df_2019_m)
```

\#I merge precipitation datasets

``` r
precipitation = merge(df_2018_m, df_2019_m, by = c("year", "month", "month_name", "total"), all=TRUE)
view(precipitation)
```

\#I will remove then numeric month column from the dataset. \#Then, I
will rename the month\_name column as month to merge with the Mr. Trash
Wheel dataset better.

``` r
precipitation_m = precipitation %>% select("year", "month_name", "total") %>% rename("month" = "month_name", "total_precipitation" = "total")
view(precipitation_m)
```

\#I will characterize the precipitation data sets by viewing the
structure, head and tail

``` r
str(precipitation)
```

    ## 'data.frame':    18 obs. of  4 variables:
    ##  $ year      : num  2018 2018 2018 2018 2018 ...
    ##  $ month     : num  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ month_name: chr  "January" "February" "March" "April" ...
    ##  $ total     : num  0.94 4.8 2.69 4.69 9.27 ...

``` r
head(precipitation)
```

    ##   year month month_name total
    ## 1 2018     1    January  0.94
    ## 2 2018     2   February  4.80
    ## 3 2018     3      March  2.69
    ## 4 2018     4      April  4.69
    ## 5 2018     5        May  9.27
    ## 6 2018     6       June  4.77

``` r
tail(precipitation)
```

    ##    year month month_name total
    ## 13 2019     1    January  3.10
    ## 14 2019     2   February  3.64
    ## 15 2019     3      March  4.47
    ## 16 2019     4      April  1.46
    ## 17 2019     5        May  3.58
    ## 18 2019     6       June  0.42

\#This data set has 18 observations and 4 variables. There are 4
columns. Of those, 3 columns are in numerical format and month\_name is
in a character format.

\#I will merge Mr. Trash Wheel with precipitation data

``` r
data_set_full = merge(df_three, precipitation_m, by = c("year", "month"), all=TRUE)
view(data_set_full)
```

\#I will characterize the merged data sets by viewing the structure,
head and tail

``` r
str(data_set_full)
```

    ## 'data.frame':    344 obs. of  15 variables:
    ##  $ year               : num  2014 2014 2014 2014 2014 ...
    ##  $ month              : chr  "August" "August" "August" "August" ...
    ##  $ dumpster           : num  25 26 27 28 29 42 43 44 18 19 ...
    ##  $ date               : POSIXct, format: "2014-08-04" "2014-08-04" ...
    ##  $ weight_tons        : num  4.39 5.33 3.58 3.1 1.77 1.81 3.48 3.18 2.54 2.41 ...
    ##  $ volume_cubic_yards : num  16 17 20 17 10 17 15 15 15 15 ...
    ##  $ plastic_bottles    : num  2140 1630 3640 1430 570 1370 550 640 1640 1730 ...
    ##  $ polystyrene        : num  2050 1950 4360 1870 780 3140 1450 1670 1960 2100 ...
    ##  $ cigarette_butts    : num  118000 123000 141000 121000 32000 38000 22000 26000 108000 107000 ...
    ##  $ glass_bottles      : num  68 75 82 63 21 28 34 42 65 63 ...
    ##  $ grocery_bags       : num  904 512 1560 552 310 950 740 880 744 896 ...
    ##  $ chip_bags          : num  1762 1318 3067 1144 1440 ...
    ##  $ sports_balls       : num  6.4 6.8 8 6.8 4 6.8 6 6 6 6 ...
    ##  $ homes_powered      : num  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ total_precipitation: num  NA NA NA NA NA NA NA NA NA NA ...

``` r
head(data_set_full)
```

    ##   year    month dumpster       date weight_tons volume_cubic_yards
    ## 1 2014   August       25 2014-08-04        4.39                 16
    ## 2 2014   August       26 2014-08-04        5.33                 17
    ## 3 2014   August       27 2014-08-13        3.58                 20
    ## 4 2014   August       28 2014-08-13        3.10                 17
    ## 5 2014   August       29 2014-08-19        1.77                 10
    ## 6 2014 December       42 2014-12-01        1.81                 17
    ##   plastic_bottles polystyrene cigarette_butts glass_bottles grocery_bags
    ## 1            2140        2050          118000            68          904
    ## 2            1630        1950          123000            75          512
    ## 3            3640        4360          141000            82         1560
    ## 4            1430        1870          121000            63          552
    ## 5             570         780           32000            21          310
    ## 6            1370        3140           38000            28          950
    ##   chip_bags sports_balls homes_powered total_precipitation
    ## 1      1762          6.4             0                  NA
    ## 2      1318          6.8             0                  NA
    ## 3      3067          8.0             0                  NA
    ## 4      1144          6.8             0                  NA
    ## 5      1440          4.0             0                  NA
    ## 6      1620          6.8             0                  NA

``` r
tail(data_set_full)
```

    ##     year month dumpster       date weight_tons volume_cubic_yards
    ## 339 2019   May      336 2019-05-13        2.92                 15
    ## 340 2019   May      337 2019-05-15        2.83                 15
    ## 341 2019   May      338 2019-05-15        2.76                 15
    ## 342 2019   May      339 2019-05-28        2.51                 15
    ## 343 2019   May      340 2019-05-28        2.72                 15
    ## 344 2019   May      341 2019-05-31        3.19                 15
    ##     plastic_bottles polystyrene cigarette_butts glass_bottles grocery_bags
    ## 339             980        1200            2400            18          640
    ## 340            1880        2440            4200            10          990
    ## 341             900        1300            3800             4          480
    ## 342            1740        2000            6400            13          600
    ## 343            1140        1080            5400            16          900
    ## 344            2040        1250            6600            17          860
    ##     chip_bags sports_balls homes_powered total_precipitation
    ## 339       800           14      48.66667                3.58
    ## 340       460           22      47.16667                3.58
    ## 341       660            6      46.00000                3.58
    ## 342       780            9      41.83333                3.58
    ## 343      1080           10      45.33333                3.58
    ## 344      1480            8      53.16667                3.58

\#The data set has 344 observations and is 344 x 15 in size. There are
15 columns. Of those, 13 are in nmerical format. 1 column is a character
format and the date column is in time stamp format.

\#\#I will drop missing values from the dataset, which will remove all
values before 2018\#\#\#

``` r
data_set_edit = drop_na(data_set_full)
view(data_set_edit)
```

\#I will characterize the new data set by viewing the structure, head
and tail

``` r
str(data_set_edit)
```

    ## 'data.frame':    123 obs. of  15 variables:
    ##  $ year               : num  2018 2018 2018 2018 2018 ...
    ##  $ month              : chr  "April" "April" "April" "April" ...
    ##  $ dumpster           : num  235 236 237 238 239 240 241 242 243 244 ...
    ##  $ date               : POSIXct, format: "2018-04-16" "2018-04-16" ...
    ##  $ weight_tons        : num  4.3 2.91 3.62 2.4 3.19 3.03 3.26 3.04 3.09 2.72 ...
    ##  $ volume_cubic_yards : num  15 15 15 12 15 15 15 15 15 15 ...
    ##  $ plastic_bottles    : num  2150 970 840 790 750 810 790 670 710 730 ...
    ##  $ polystyrene        : num  2300 1100 920 910 830 890 1020 840 910 840 ...
    ##  $ cigarette_butts    : num  23000 8000 7000 8000 6000 5000 6000 7000 7000 6000 ...
    ##  $ glass_bottles      : num  16 2 3 4 3 4 3 2 4 6 ...
    ##  $ grocery_bags       : num  1320 300 290 260 190 200 150 230 310 280 ...
    ##  $ chip_bags          : num  2070 800 650 590 400 450 500 620 780 640 ...
    ##  $ sports_balls       : num  12 1 4 2 4 3 4 3 4 2 ...
    ##  $ homes_powered      : num  71.7 48.5 60.3 40 53.2 ...
    ##  $ total_precipitation: num  4.69 4.69 4.69 4.69 4.69 4.69 4.69 4.69 4.69 4.69 ...

``` r
head(data_set_edit)
```

    ##   year month dumpster       date weight_tons volume_cubic_yards plastic_bottles
    ## 1 2018 April      235 2018-04-16        4.30                 15            2150
    ## 2 2018 April      236 2018-04-16        2.91                 15             970
    ## 3 2018 April      237 2018-04-16        3.62                 15             840
    ## 4 2018 April      238 2018-04-16        2.40                 12             790
    ## 5 2018 April      239 2018-04-17        3.19                 15             750
    ## 6 2018 April      240 2018-04-17        3.03                 15             810
    ##   polystyrene cigarette_butts glass_bottles grocery_bags chip_bags sports_balls
    ## 1        2300           23000            16         1320      2070           12
    ## 2        1100            8000             2          300       800            1
    ## 3         920            7000             3          290       650            4
    ## 4         910            8000             4          260       590            2
    ## 5         830            6000             3          190       400            4
    ## 6         890            5000             4          200       450            3
    ##   homes_powered total_precipitation
    ## 1      71.66667                4.69
    ## 2      48.50000                4.69
    ## 3      60.33333                4.69
    ## 4      40.00000                4.69
    ## 5      53.16667                4.69
    ## 6      50.50000                4.69

``` r
tail(data_set_edit)
```

    ##     year month dumpster       date weight_tons volume_cubic_yards
    ## 118 2019   May      336 2019-05-13        2.92                 15
    ## 119 2019   May      337 2019-05-15        2.83                 15
    ## 120 2019   May      338 2019-05-15        2.76                 15
    ## 121 2019   May      339 2019-05-28        2.51                 15
    ## 122 2019   May      340 2019-05-28        2.72                 15
    ## 123 2019   May      341 2019-05-31        3.19                 15
    ##     plastic_bottles polystyrene cigarette_butts glass_bottles grocery_bags
    ## 118             980        1200            2400            18          640
    ## 119            1880        2440            4200            10          990
    ## 120             900        1300            3800             4          480
    ## 121            1740        2000            6400            13          600
    ## 122            1140        1080            5400            16          900
    ## 123            2040        1250            6600            17          860
    ##     chip_bags sports_balls homes_powered total_precipitation
    ## 118       800           14      48.66667                3.58
    ## 119       460           22      47.16667                3.58
    ## 120       660            6      46.00000                3.58
    ## 121       780            9      41.83333                3.58
    ## 122      1080           10      45.33333                3.58
    ## 123      1480            8      53.16667                3.58

\#The data set has 123 observations and is 344 x 15 in size. There are
15 columns. Of those, 13 are in nmerical format. 1 column is a character
format and the date column is in time stamp format.

\#I will view the data set

``` r
view(data_set_edit)
```

\#\#I will calculate the median precipitation in 2018

``` r
 data_set_edit %>% filter (year == 2018) %>% pull (total_precipitation) %>% median()
```

    ## [1] 6.11

\#\#The median precipitation in 2018 was 6.11

\#\#I will calculate the median sports balls in 2019

``` r
 data_set_edit %>% filter (year == 2019) %>% pull (sports_balls) %>% median()
```

    ## [1] 8.5

\#\#\#The median number of sports balls was 8.5 in 2019

\#\#I will calculate the median weight in tons, volume in cubic volume,
number of plastic bottles, amount of polystyrene, and homes powered in
2018

``` r
 data_set_edit %>% filter (year == 2018) %>% pull (weight_tons) %>% median() ##weight
```

    ## [1] 3.31

``` r
data_set_edit %>% filter (year == 2018) %>% pull (volume_cubic_yards) %>% median() #cubic volume
```

    ## [1] 15

``` r
data_set_edit %>% filter (year == 2018) %>% pull (plastic_bottles) %>% median() #plastic bottles
```

    ## [1] 1200

``` r
data_set_edit %>% filter (year == 2018) %>% pull (polystyrene) %>% median() #ploystyrene
```

    ## [1] 1020

``` r
data_set_edit %>% filter (year == 2018) %>% pull (homes_powered) %>% median() #homes powered
```

    ## [1] 55.16667

\#The median weight is 3 tons, median volume is 15 cubic yards, number
of plastic botles is 1200, amount of polystyrene is 1020, and number of
homes powered is 55.

\#\#I will calculate the median weight in tons, volume in cubic volume,
number of plastic bottles, amount of polystyrene, and homes powered in
2019

``` r
 data_set_edit %>% filter (year == 2019) %>% pull (weight_tons) %>% median() ##weight
```

    ## [1] 3.065

``` r
data_set_edit %>% filter (year == 2019) %>% pull (volume_cubic_yards) %>% median() #cubic volume
```

    ## [1] 15

``` r
data_set_edit %>% filter (year == 2019) %>% pull (plastic_bottles) %>% median() #plastic bottles
```

    ## [1] 1075

``` r
data_set_edit %>% filter (year == 2019) %>% pull (polystyrene) %>% median() #ploystyrene
```

    ## [1] 1350

``` r
data_set_edit %>% filter (year == 2019) %>% pull (homes_powered) %>% median() #homes powered
```

    ## [1] 51.08333

\#The median weight is 3 tons, median volume is 15 cubic yards, number
of plastic botles is 1075, amount of polystyrene is 1350, and number of
homes powered is 51.

\#Problem 2 \#Clean data in pols-months and characterize the data frame

``` r
df_pols = read_csv("pols-month.csv")
```

    ## Rows: 822 Columns: 9

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl  (8): prez_gop, gov_gop, sen_gop, rep_gop, prez_dem, gov_dem, sen_dem, r...
    ## date (1): mon

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
df_pols = janitor::clean_names(df_pols)
str(df_pols)
```

    ## spec_tbl_df [822 × 9] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ mon     : Date[1:822], format: "1947-01-15" "1947-02-15" ...
    ##  $ prez_gop: num [1:822] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ gov_gop : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop : num [1:822] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop : num [1:822] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ prez_dem: num [1:822] 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gov_dem : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem : num [1:822] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem : num [1:822] 198 198 198 198 198 198 198 198 198 198 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   mon = col_date(format = ""),
    ##   ..   prez_gop = col_double(),
    ##   ..   gov_gop = col_double(),
    ##   ..   sen_gop = col_double(),
    ##   ..   rep_gop = col_double(),
    ##   ..   prez_dem = col_double(),
    ##   ..   gov_dem = col_double(),
    ##   ..   sen_dem = col_double(),
    ##   ..   rep_dem = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
head(df_pols)
```

    ## # A tibble: 6 × 9
    ##   mon        prez_gop gov_gop sen_gop rep_gop prez_dem gov_dem sen_dem rep_dem
    ##   <date>        <dbl>   <dbl>   <dbl>   <dbl>    <dbl>   <dbl>   <dbl>   <dbl>
    ## 1 1947-01-15        0      23      51     253        1      23      45     198
    ## 2 1947-02-15        0      23      51     253        1      23      45     198
    ## 3 1947-03-15        0      23      51     253        1      23      45     198
    ## 4 1947-04-15        0      23      51     253        1      23      45     198
    ## 5 1947-05-15        0      23      51     253        1      23      45     198
    ## 6 1947-06-15        0      23      51     253        1      23      45     198

``` r
tail(df_pols)
```

    ## # A tibble: 6 × 9
    ##   mon        prez_gop gov_gop sen_gop rep_gop prez_dem gov_dem sen_dem rep_dem
    ##   <date>        <dbl>   <dbl>   <dbl>   <dbl>    <dbl>   <dbl>   <dbl>   <dbl>
    ## 1 2015-01-15        0      31      54     245        1      18      44     188
    ## 2 2015-02-15        0      31      54     245        1      18      44     188
    ## 3 2015-03-15        0      31      54     245        1      18      44     188
    ## 4 2015-04-15        0      31      54     244        1      18      44     188
    ## 5 2015-05-15        0      31      54     245        1      18      44     188
    ## 6 2015-06-15        0      31      54     246        1      18      44     188

``` r
view(df_pols)
```

\#Now I will drop any missing values and reassess the data frame

``` r
df_pols %>% drop_na()
```

    ## # A tibble: 822 × 9
    ##    mon        prez_gop gov_gop sen_gop rep_gop prez_dem gov_dem sen_dem rep_dem
    ##    <date>        <dbl>   <dbl>   <dbl>   <dbl>    <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 1947-01-15        0      23      51     253        1      23      45     198
    ##  2 1947-02-15        0      23      51     253        1      23      45     198
    ##  3 1947-03-15        0      23      51     253        1      23      45     198
    ##  4 1947-04-15        0      23      51     253        1      23      45     198
    ##  5 1947-05-15        0      23      51     253        1      23      45     198
    ##  6 1947-06-15        0      23      51     253        1      23      45     198
    ##  7 1947-07-15        0      23      51     253        1      23      45     198
    ##  8 1947-08-15        0      23      51     253        1      23      45     198
    ##  9 1947-09-15        0      23      51     253        1      23      45     198
    ## 10 1947-10-15        0      23      51     253        1      23      45     198
    ## # … with 812 more rows

``` r
str(df_pols)
```

    ## spec_tbl_df [822 × 9] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ mon     : Date[1:822], format: "1947-01-15" "1947-02-15" ...
    ##  $ prez_gop: num [1:822] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ gov_gop : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop : num [1:822] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop : num [1:822] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ prez_dem: num [1:822] 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gov_dem : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem : num [1:822] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem : num [1:822] 198 198 198 198 198 198 198 198 198 198 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   mon = col_date(format = ""),
    ##   ..   prez_gop = col_double(),
    ##   ..   gov_gop = col_double(),
    ##   ..   sen_gop = col_double(),
    ##   ..   rep_gop = col_double(),
    ##   ..   prez_dem = col_double(),
    ##   ..   gov_dem = col_double(),
    ##   ..   sen_dem = col_double(),
    ##   ..   rep_dem = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
head(df_pols)
```

    ## # A tibble: 6 × 9
    ##   mon        prez_gop gov_gop sen_gop rep_gop prez_dem gov_dem sen_dem rep_dem
    ##   <date>        <dbl>   <dbl>   <dbl>   <dbl>    <dbl>   <dbl>   <dbl>   <dbl>
    ## 1 1947-01-15        0      23      51     253        1      23      45     198
    ## 2 1947-02-15        0      23      51     253        1      23      45     198
    ## 3 1947-03-15        0      23      51     253        1      23      45     198
    ## 4 1947-04-15        0      23      51     253        1      23      45     198
    ## 5 1947-05-15        0      23      51     253        1      23      45     198
    ## 6 1947-06-15        0      23      51     253        1      23      45     198

``` r
tail(df_pols)
```

    ## # A tibble: 6 × 9
    ##   mon        prez_gop gov_gop sen_gop rep_gop prez_dem gov_dem sen_dem rep_dem
    ##   <date>        <dbl>   <dbl>   <dbl>   <dbl>    <dbl>   <dbl>   <dbl>   <dbl>
    ## 1 2015-01-15        0      31      54     245        1      18      44     188
    ## 2 2015-02-15        0      31      54     245        1      18      44     188
    ## 3 2015-03-15        0      31      54     245        1      18      44     188
    ## 4 2015-04-15        0      31      54     244        1      18      44     188
    ## 5 2015-05-15        0      31      54     245        1      18      44     188
    ## 6 2015-06-15        0      31      54     246        1      18      44     188

\#There were no missing values \#Now I will separate the month value

``` r
df_pols_two = separate(df_pols, mon, c("year", "month", "day"), "-")
head(df_pols_two)
```

    ## # A tibble: 6 × 11
    ##   year  month day   prez_gop gov_gop sen_gop rep_gop prez_dem gov_dem sen_dem
    ##   <chr> <chr> <chr>    <dbl>   <dbl>   <dbl>   <dbl>    <dbl>   <dbl>   <dbl>
    ## 1 1947  01    15           0      23      51     253        1      23      45
    ## 2 1947  02    15           0      23      51     253        1      23      45
    ## 3 1947  03    15           0      23      51     253        1      23      45
    ## 4 1947  04    15           0      23      51     253        1      23      45
    ## 5 1947  05    15           0      23      51     253        1      23      45
    ## 6 1947  06    15           0      23      51     253        1      23      45
    ## # … with 1 more variable: rep_dem <dbl>

\#\#Now I will replace the month number with the month name. \#\#First,
I will convert the month into a numeric type.

``` r
month_numeric = df_pols_two %>% pull(month) %>% as.numeric()
df_pols_three = df_pols_two %>% mutate(month = month_numeric)
str(df_pols_three)
```

    ## tibble [822 × 11] (S3: tbl_df/tbl/data.frame)
    ##  $ year    : chr [1:822] "1947" "1947" "1947" "1947" ...
    ##  $ month   : num [1:822] 1 2 3 4 5 6 7 8 9 10 ...
    ##  $ day     : chr [1:822] "15" "15" "15" "15" ...
    ##  $ prez_gop: num [1:822] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ gov_gop : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop : num [1:822] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop : num [1:822] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ prez_dem: num [1:822] 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gov_dem : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem : num [1:822] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem : num [1:822] 198 198 198 198 198 198 198 198 198 198 ...

\#\#Now I will convert the numeric values to month names

``` r
df_pols_four = df_pols_three %>% mutate(month = month.name[month])
str(df_pols_four)
```

    ## tibble [822 × 11] (S3: tbl_df/tbl/data.frame)
    ##  $ year    : chr [1:822] "1947" "1947" "1947" "1947" ...
    ##  $ month   : chr [1:822] "January" "February" "March" "April" ...
    ##  $ day     : chr [1:822] "15" "15" "15" "15" ...
    ##  $ prez_gop: num [1:822] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ gov_gop : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop : num [1:822] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop : num [1:822] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ prez_dem: num [1:822] 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gov_dem : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem : num [1:822] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem : num [1:822] 198 198 198 198 198 198 198 198 198 198 ...

\#\#Now, I will convert the year and day into a numeric types.

``` r
year_numeric = df_pols_four %>% pull(year) %>% as.numeric()
df_pols_four = df_pols_four %>% mutate(year = year_numeric)
day_numeric = df_pols_four %>% pull(day) %>% as.numeric()
df_pols_four = df_pols_four %>% mutate(day = day_numeric)

str(df_pols_four)
```

    ## tibble [822 × 11] (S3: tbl_df/tbl/data.frame)
    ##  $ year    : num [1:822] 1947 1947 1947 1947 1947 ...
    ##  $ month   : chr [1:822] "January" "February" "March" "April" ...
    ##  $ day     : num [1:822] 15 15 15 15 15 15 15 15 15 15 ...
    ##  $ prez_gop: num [1:822] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ gov_gop : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop : num [1:822] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop : num [1:822] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ prez_dem: num [1:822] 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gov_dem : num [1:822] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem : num [1:822] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem : num [1:822] 198 198 198 198 198 198 198 198 198 198 ...

\#\#\#Now I will create a president variable

``` r
df_pols_five = pivot_longer(
  df_pols_four, c(prez_dem, prez_gop), names_to = "president", values_to = c("prez_values")
)
str(df_pols_five)
```

    ## tibble [1,644 × 11] (S3: tbl_df/tbl/data.frame)
    ##  $ year       : num [1:1644] 1947 1947 1947 1947 1947 ...
    ##  $ month      : chr [1:1644] "January" "January" "February" "February" ...
    ##  $ day        : num [1:1644] 15 15 15 15 15 15 15 15 15 15 ...
    ##  $ gov_gop    : num [1:1644] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop    : num [1:1644] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop    : num [1:1644] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ gov_dem    : num [1:1644] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem    : num [1:1644] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem    : num [1:1644] 198 198 198 198 198 198 198 198 198 198 ...
    ##  $ president  : chr [1:1644] "prez_dem" "prez_gop" "prez_dem" "prez_gop" ...
    ##  $ prez_values: num [1:1644] 1 0 1 0 1 0 1 0 1 0 ...

\#\#\#Now I will replace the president value names

``` r
president_edit = df_pols_five %>% pull(president) %>% str_replace_all("prez_dem", "dem") %>% str_replace_all("prez_gop", "gop")
```

\#\#\#Now I will replace the old president vector with the edited
president vector

``` r
df_pols_five = df_pols_five %>% mutate (president = president_edit)
str (df_pols_five)
```

    ## tibble [1,644 × 11] (S3: tbl_df/tbl/data.frame)
    ##  $ year       : num [1:1644] 1947 1947 1947 1947 1947 ...
    ##  $ month      : chr [1:1644] "January" "January" "February" "February" ...
    ##  $ day        : num [1:1644] 15 15 15 15 15 15 15 15 15 15 ...
    ##  $ gov_gop    : num [1:1644] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop    : num [1:1644] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop    : num [1:1644] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ gov_dem    : num [1:1644] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem    : num [1:1644] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem    : num [1:1644] 198 198 198 198 198 198 198 198 198 198 ...
    ##  $ president  : chr [1:1644] "dem" "gop" "dem" "gop" ...
    ##  $ prez_values: num [1:1644] 1 0 1 0 1 0 1 0 1 0 ...

\#\#\#Now I will omit the day and president values columns

``` r
df_pols_six = select(df_pols_five, -c("day", "prez_values"))
str(df_pols_six)
```

    ## tibble [1,644 × 9] (S3: tbl_df/tbl/data.frame)
    ##  $ year     : num [1:1644] 1947 1947 1947 1947 1947 ...
    ##  $ month    : chr [1:1644] "January" "January" "February" "February" ...
    ##  $ gov_gop  : num [1:1644] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop  : num [1:1644] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop  : num [1:1644] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ gov_dem  : num [1:1644] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem  : num [1:1644] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem  : num [1:1644] 198 198 198 198 198 198 198 198 198 198 ...
    ##  $ president: chr [1:1644] "dem" "gop" "dem" "gop" ...

\#\#I will import and characterize snip.csv

``` r
df_snip_one = read_csv("snp.csv")
```

    ## Rows: 787 Columns: 2

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): date
    ## dbl (1): close

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
df_snip_one = janitor::clean_names(df_snip_one)
str(df_snip_one)
```

    ## spec_tbl_df [787 × 2] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ date : chr [1:787] "7/1/15" "6/1/15" "5/1/15" "4/1/15" ...
    ##  $ close: num [1:787] 2080 2063 2107 2086 2068 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   date = col_character(),
    ##   ..   close = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
head(df_snip_one)
```

    ## # A tibble: 6 × 2
    ##   date   close
    ##   <chr>  <dbl>
    ## 1 7/1/15 2080.
    ## 2 6/1/15 2063.
    ## 3 5/1/15 2107.
    ## 4 4/1/15 2086.
    ## 5 3/2/15 2068.
    ## 6 2/2/15 2104.

``` r
tail(df_snip_one)
```

    ## # A tibble: 6 × 2
    ##   date   close
    ##   <chr>  <dbl>
    ## 1 6/1/50  17.7
    ## 2 5/1/50  18.8
    ## 3 4/3/50  18.0
    ## 4 3/1/50  17.3
    ## 5 2/1/50  17.2
    ## 6 1/3/50  17.0

``` r
view(df_snip_one)
```

\#Now I will drop any missing values and reassess the data frame

``` r
df_snip_one %>% drop_na()
```

    ## # A tibble: 787 × 2
    ##    date    close
    ##    <chr>   <dbl>
    ##  1 7/1/15  2080.
    ##  2 6/1/15  2063.
    ##  3 5/1/15  2107.
    ##  4 4/1/15  2086.
    ##  5 3/2/15  2068.
    ##  6 2/2/15  2104.
    ##  7 1/2/15  1995.
    ##  8 12/1/14 2059.
    ##  9 11/3/14 2068.
    ## 10 10/1/14 2018.
    ## # … with 777 more rows

``` r
str(df_snip_one)
```

    ## spec_tbl_df [787 × 2] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ date : chr [1:787] "7/1/15" "6/1/15" "5/1/15" "4/1/15" ...
    ##  $ close: num [1:787] 2080 2063 2107 2086 2068 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   date = col_character(),
    ##   ..   close = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
head(df_snip_one)
```

    ## # A tibble: 6 × 2
    ##   date   close
    ##   <chr>  <dbl>
    ## 1 7/1/15 2080.
    ## 2 6/1/15 2063.
    ## 3 5/1/15 2107.
    ## 4 4/1/15 2086.
    ## 5 3/2/15 2068.
    ## 6 2/2/15 2104.

``` r
tail(df_snip_one)
```

    ## # A tibble: 6 × 2
    ##   date   close
    ##   <chr>  <dbl>
    ## 1 6/1/50  17.7
    ## 2 5/1/50  18.8
    ## 3 4/3/50  18.0
    ## 4 3/1/50  17.3
    ## 5 2/1/50  17.2
    ## 6 1/3/50  17.0

\#There were no missing values

\#I will convert the 2 digit year date into a 4 digit year date

``` r
date_vector = df_snip_one %>% pull(date) %>% lubridate::mdy()
df_snip_two = mutate(df_snip_one, date = date_vector)
df_snip_two
```

    ## # A tibble: 787 × 2
    ##    date       close
    ##    <date>     <dbl>
    ##  1 2015-07-01 2080.
    ##  2 2015-06-01 2063.
    ##  3 2015-05-01 2107.
    ##  4 2015-04-01 2086.
    ##  5 2015-03-02 2068.
    ##  6 2015-02-02 2104.
    ##  7 2015-01-02 1995.
    ##  8 2014-12-01 2059.
    ##  9 2014-11-03 2068.
    ## 10 2014-10-01 2018.
    ## # … with 777 more rows

\#\#Some of the dates are impossible, as they have occurred after the
year 2050. I will separate the values and then fix the year column.
\#Now I will separate the month value

``` r
df_snip_two = separate(df_snip_two, date, c("year", "month", "day"), "-")
head(df_snip_two)
```

    ## # A tibble: 6 × 4
    ##   year  month day   close
    ##   <chr> <chr> <chr> <dbl>
    ## 1 2015  07    01    2080.
    ## 2 2015  06    01    2063.
    ## 3 2015  05    01    2107.
    ## 4 2015  04    01    2086.
    ## 5 2015  03    02    2068.
    ## 6 2015  02    02    2104.

\#\#Now, I will convert the year and day into a numeric types.

``` r
year_numeric = df_snip_two %>% pull(year) %>% as.numeric()
df_snip_two = df_snip_two %>% mutate(year = year_numeric)
month_numeric = df_snip_two %>% pull(month) %>% as.numeric()
df_snip_two = df_snip_two %>% mutate(month = month_numeric)

day_numeric = df_snip_two %>% pull(day) %>% as.numeric()
df_snip_two = df_snip_two %>% mutate(day = day_numeric)

str(df_snip_two)
```

    ## tibble [787 × 4] (S3: tbl_df/tbl/data.frame)
    ##  $ year : num [1:787] 2015 2015 2015 2015 2015 ...
    ##  $ month: num [1:787] 7 6 5 4 3 2 1 12 11 10 ...
    ##  $ day  : num [1:787] 1 1 1 1 2 2 2 1 3 1 ...
    ##  $ close: num [1:787] 2080 2063 2107 2086 2068 ...

\#I will rearrange so that year and month are the leading columns

``` r
close = df_snip_two %>% pull(close)
df_snip_two = select(df_snip_two, -"close")
df_snip_two = mutate(df_snip_two, close)
df_snip_two = df_snip_two %>% arrange (year)
view (df_snip_two)
```

\#now I will convert the year column into plausible values

``` r
df_snip_three = df_snip_two %>% mutate (year = ifelse(test = (year > 2020), yes = year - 100, no = year)) %>% arrange(year)

  
view(df_snip_three)
```

\#\#I will convert the month from numbers to names

``` r
df_snip_three = df_snip_three %>% mutate(month = month.name[month])
str(df_snip_three)
```

    ## tibble [787 × 4] (S3: tbl_df/tbl/data.frame)
    ##  $ year : num [1:787] 1950 1950 1950 1950 1950 1950 1950 1950 1950 1950 ...
    ##  $ month: chr [1:787] "December" "November" "October" "September" ...
    ##  $ day  : num [1:787] 1 1 2 1 1 3 1 1 3 1 ...
    ##  $ close: num [1:787] 20.4 19.5 19.5 19.5 18.4 ...

\#\#I will import and characterize unemployment.csv

``` r
df_un_one = read_csv("unemployment.csv")
```

    ## Rows: 68 Columns: 13

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (13): Year, Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
df_un_one = janitor::clean_names(df_un_one)
str(df_un_one)
```

    ## spec_tbl_df [68 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ year: num [1:68] 1948 1949 1950 1951 1952 ...
    ##  $ jan : num [1:68] 3.4 4.3 6.5 3.7 3.2 2.9 4.9 4.9 4 4.2 ...
    ##  $ feb : num [1:68] 3.8 4.7 6.4 3.4 3.1 2.6 5.2 4.7 3.9 3.9 ...
    ##  $ mar : num [1:68] 4 5 6.3 3.4 2.9 2.6 5.7 4.6 4.2 3.7 ...
    ##  $ apr : num [1:68] 3.9 5.3 5.8 3.1 2.9 2.7 5.9 4.7 4 3.9 ...
    ##  $ may : num [1:68] 3.5 6.1 5.5 3 3 2.5 5.9 4.3 4.3 4.1 ...
    ##  $ jun : num [1:68] 3.6 6.2 5.4 3.2 3 2.5 5.6 4.2 4.3 4.3 ...
    ##  $ jul : num [1:68] 3.6 6.7 5 3.1 3.2 2.6 5.8 4 4.4 4.2 ...
    ##  $ aug : num [1:68] 3.9 6.8 4.5 3.1 3.4 2.7 6 4.2 4.1 4.1 ...
    ##  $ sep : num [1:68] 3.8 6.6 4.4 3.3 3.1 2.9 6.1 4.1 3.9 4.4 ...
    ##  $ oct : num [1:68] 3.7 7.9 4.2 3.5 3 3.1 5.7 4.3 3.9 4.5 ...
    ##  $ nov : num [1:68] 3.8 6.4 4.2 3.5 2.8 3.5 5.3 4.2 4.3 5.1 ...
    ##  $ dec : num [1:68] 4 6.6 4.3 3.1 2.7 4.5 5 4.2 4.2 5.2 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   Year = col_double(),
    ##   ..   Jan = col_double(),
    ##   ..   Feb = col_double(),
    ##   ..   Mar = col_double(),
    ##   ..   Apr = col_double(),
    ##   ..   May = col_double(),
    ##   ..   Jun = col_double(),
    ##   ..   Jul = col_double(),
    ##   ..   Aug = col_double(),
    ##   ..   Sep = col_double(),
    ##   ..   Oct = col_double(),
    ##   ..   Nov = col_double(),
    ##   ..   Dec = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
head(df_un_one)
```

    ## # A tibble: 6 × 13
    ##    year   jan   feb   mar   apr   may   jun   jul   aug   sep   oct   nov   dec
    ##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1  1948   3.4   3.8   4     3.9   3.5   3.6   3.6   3.9   3.8   3.7   3.8   4  
    ## 2  1949   4.3   4.7   5     5.3   6.1   6.2   6.7   6.8   6.6   7.9   6.4   6.6
    ## 3  1950   6.5   6.4   6.3   5.8   5.5   5.4   5     4.5   4.4   4.2   4.2   4.3
    ## 4  1951   3.7   3.4   3.4   3.1   3     3.2   3.1   3.1   3.3   3.5   3.5   3.1
    ## 5  1952   3.2   3.1   2.9   2.9   3     3     3.2   3.4   3.1   3     2.8   2.7
    ## 6  1953   2.9   2.6   2.6   2.7   2.5   2.5   2.6   2.7   2.9   3.1   3.5   4.5

``` r
tail(df_un_one)
```

    ## # A tibble: 6 × 13
    ##    year   jan   feb   mar   apr   may   jun   jul   aug   sep   oct   nov   dec
    ##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1  2010   9.8   9.8   9.9   9.9   9.6   9.4   9.4   9.5   9.5   9.4   9.8   9.3
    ## 2  2011   9.2   9     9     9.1   9     9.1   9     9     9     8.8   8.6   8.5
    ## 3  2012   8.3   8.3   8.2   8.2   8.2   8.2   8.2   8     7.8   7.8   7.7   7.9
    ## 4  2013   8     7.7   7.5   7.6   7.5   7.5   7.3   7.2   7.2   7.2   7     6.7
    ## 5  2014   6.6   6.7   6.6   6.2   6.3   6.1   6.2   6.1   5.9   5.7   5.8   5.6
    ## 6  2015   5.7   5.5   5.5   5.4   5.5   5.3  NA    NA    NA    NA    NA    NA

``` r
view(df_un_one)
```

\#I will do a long pivot on the month names

``` r
df_un_two = pivot_longer(
  df_un_one, c(jan:dec), names_to = "month", values_to = c("counts")
)
str(df_un_two)
```

    ## tibble [816 × 3] (S3: tbl_df/tbl/data.frame)
    ##  $ year  : num [1:816] 1948 1948 1948 1948 1948 ...
    ##  $ month : chr [1:816] "jan" "feb" "mar" "apr" ...
    ##  $ counts: num [1:816] 3.4 3.8 4 3.9 3.5 3.6 3.6 3.9 3.8 3.7 ...

``` r
view(df_un_two)
```

I will replace the month names in the unemployment data set to
standardize them with other data sets

``` r
un_month_edit = df_un_two %>% pull(month) %>% str_replace_all("jan", "January") %>% str_replace_all("feb", "February") %>% str_replace_all("mar", "March") %>% str_replace_all("apr", "April")%>% str_replace_all("may", "May") %>% str_replace_all("jun", "June") %>% str_replace_all("jul", "July") %>% str_replace_all("aug", "August") %>% str_replace_all("sep", "September") %>% str_replace_all("oct", "October") %>% str_replace_all("nov", "November") %>% str_replace_all("dec", "December")

un_month_edit
```

    ##   [1] "January"   "February"  "March"     "April"     "May"       "June"     
    ##   [7] "July"      "August"    "September" "October"   "November"  "December" 
    ##  [13] "January"   "February"  "March"     "April"     "May"       "June"     
    ##  [19] "July"      "August"    "September" "October"   "November"  "December" 
    ##  [25] "January"   "February"  "March"     "April"     "May"       "June"     
    ##  [31] "July"      "August"    "September" "October"   "November"  "December" 
    ##  [37] "January"   "February"  "March"     "April"     "May"       "June"     
    ##  [43] "July"      "August"    "September" "October"   "November"  "December" 
    ##  [49] "January"   "February"  "March"     "April"     "May"       "June"     
    ##  [55] "July"      "August"    "September" "October"   "November"  "December" 
    ##  [61] "January"   "February"  "March"     "April"     "May"       "June"     
    ##  [67] "July"      "August"    "September" "October"   "November"  "December" 
    ##  [73] "January"   "February"  "March"     "April"     "May"       "June"     
    ##  [79] "July"      "August"    "September" "October"   "November"  "December" 
    ##  [85] "January"   "February"  "March"     "April"     "May"       "June"     
    ##  [91] "July"      "August"    "September" "October"   "November"  "December" 
    ##  [97] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [103] "July"      "August"    "September" "October"   "November"  "December" 
    ## [109] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [115] "July"      "August"    "September" "October"   "November"  "December" 
    ## [121] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [127] "July"      "August"    "September" "October"   "November"  "December" 
    ## [133] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [139] "July"      "August"    "September" "October"   "November"  "December" 
    ## [145] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [151] "July"      "August"    "September" "October"   "November"  "December" 
    ## [157] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [163] "July"      "August"    "September" "October"   "November"  "December" 
    ## [169] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [175] "July"      "August"    "September" "October"   "November"  "December" 
    ## [181] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [187] "July"      "August"    "September" "October"   "November"  "December" 
    ## [193] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [199] "July"      "August"    "September" "October"   "November"  "December" 
    ## [205] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [211] "July"      "August"    "September" "October"   "November"  "December" 
    ## [217] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [223] "July"      "August"    "September" "October"   "November"  "December" 
    ## [229] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [235] "July"      "August"    "September" "October"   "November"  "December" 
    ## [241] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [247] "July"      "August"    "September" "October"   "November"  "December" 
    ## [253] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [259] "July"      "August"    "September" "October"   "November"  "December" 
    ## [265] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [271] "July"      "August"    "September" "October"   "November"  "December" 
    ## [277] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [283] "July"      "August"    "September" "October"   "November"  "December" 
    ## [289] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [295] "July"      "August"    "September" "October"   "November"  "December" 
    ## [301] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [307] "July"      "August"    "September" "October"   "November"  "December" 
    ## [313] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [319] "July"      "August"    "September" "October"   "November"  "December" 
    ## [325] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [331] "July"      "August"    "September" "October"   "November"  "December" 
    ## [337] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [343] "July"      "August"    "September" "October"   "November"  "December" 
    ## [349] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [355] "July"      "August"    "September" "October"   "November"  "December" 
    ## [361] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [367] "July"      "August"    "September" "October"   "November"  "December" 
    ## [373] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [379] "July"      "August"    "September" "October"   "November"  "December" 
    ## [385] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [391] "July"      "August"    "September" "October"   "November"  "December" 
    ## [397] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [403] "July"      "August"    "September" "October"   "November"  "December" 
    ## [409] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [415] "July"      "August"    "September" "October"   "November"  "December" 
    ## [421] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [427] "July"      "August"    "September" "October"   "November"  "December" 
    ## [433] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [439] "July"      "August"    "September" "October"   "November"  "December" 
    ## [445] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [451] "July"      "August"    "September" "October"   "November"  "December" 
    ## [457] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [463] "July"      "August"    "September" "October"   "November"  "December" 
    ## [469] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [475] "July"      "August"    "September" "October"   "November"  "December" 
    ## [481] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [487] "July"      "August"    "September" "October"   "November"  "December" 
    ## [493] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [499] "July"      "August"    "September" "October"   "November"  "December" 
    ## [505] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [511] "July"      "August"    "September" "October"   "November"  "December" 
    ## [517] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [523] "July"      "August"    "September" "October"   "November"  "December" 
    ## [529] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [535] "July"      "August"    "September" "October"   "November"  "December" 
    ## [541] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [547] "July"      "August"    "September" "October"   "November"  "December" 
    ## [553] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [559] "July"      "August"    "September" "October"   "November"  "December" 
    ## [565] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [571] "July"      "August"    "September" "October"   "November"  "December" 
    ## [577] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [583] "July"      "August"    "September" "October"   "November"  "December" 
    ## [589] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [595] "July"      "August"    "September" "October"   "November"  "December" 
    ## [601] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [607] "July"      "August"    "September" "October"   "November"  "December" 
    ## [613] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [619] "July"      "August"    "September" "October"   "November"  "December" 
    ## [625] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [631] "July"      "August"    "September" "October"   "November"  "December" 
    ## [637] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [643] "July"      "August"    "September" "October"   "November"  "December" 
    ## [649] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [655] "July"      "August"    "September" "October"   "November"  "December" 
    ## [661] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [667] "July"      "August"    "September" "October"   "November"  "December" 
    ## [673] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [679] "July"      "August"    "September" "October"   "November"  "December" 
    ## [685] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [691] "July"      "August"    "September" "October"   "November"  "December" 
    ## [697] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [703] "July"      "August"    "September" "October"   "November"  "December" 
    ## [709] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [715] "July"      "August"    "September" "October"   "November"  "December" 
    ## [721] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [727] "July"      "August"    "September" "October"   "November"  "December" 
    ## [733] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [739] "July"      "August"    "September" "October"   "November"  "December" 
    ## [745] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [751] "July"      "August"    "September" "October"   "November"  "December" 
    ## [757] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [763] "July"      "August"    "September" "October"   "November"  "December" 
    ## [769] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [775] "July"      "August"    "September" "October"   "November"  "December" 
    ## [781] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [787] "July"      "August"    "September" "October"   "November"  "December" 
    ## [793] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [799] "July"      "August"    "September" "October"   "November"  "December" 
    ## [805] "January"   "February"  "March"     "April"     "May"       "June"     
    ## [811] "July"      "August"    "September" "October"   "November"  "December"

\#\#\#Now I will replace the old month vector with the new month vector

``` r
df_un_three = df_un_two %>% mutate (month = un_month_edit)
str (df_un_three)
```

    ## tibble [816 × 3] (S3: tbl_df/tbl/data.frame)
    ##  $ year  : num [1:816] 1948 1948 1948 1948 1948 ...
    ##  $ month : chr [1:816] "January" "February" "March" "April" ...
    ##  $ counts: num [1:816] 3.4 3.8 4 3.9 3.5 3.6 3.6 3.9 3.8 3.7 ...

\#\#I will make the snp year into a 4 digit number from a 2 digit number

\#\#\#Now I will merge snp and pols

``` r
view(df_snip_one)
str(df_pols_six)
```

    ## tibble [1,644 × 9] (S3: tbl_df/tbl/data.frame)
    ##  $ year     : num [1:1644] 1947 1947 1947 1947 1947 ...
    ##  $ month    : chr [1:1644] "January" "January" "February" "February" ...
    ##  $ gov_gop  : num [1:1644] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_gop  : num [1:1644] 51 51 51 51 51 51 51 51 51 51 ...
    ##  $ rep_gop  : num [1:1644] 253 253 253 253 253 253 253 253 253 253 ...
    ##  $ gov_dem  : num [1:1644] 23 23 23 23 23 23 23 23 23 23 ...
    ##  $ sen_dem  : num [1:1644] 45 45 45 45 45 45 45 45 45 45 ...
    ##  $ rep_dem  : num [1:1644] 198 198 198 198 198 198 198 198 198 198 ...
    ##  $ president: chr [1:1644] "dem" "gop" "dem" "gop" ...
