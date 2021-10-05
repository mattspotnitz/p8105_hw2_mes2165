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
sb_alt = df_three %>% pull("sports_balls")
sum(sb_alt)
```

    ## [1] 4064.6
