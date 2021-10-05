Homework2
================

\#\#Problem 1 \#I will import the excel file, examine its structure,
head, and tail.

``` r
df_one = read_excel("Trash-Wheel-Collection-Totals-8-6-19.xlsx")
```

    ## New names:
    ## * `` -> ...15
    ## * `` -> ...16
    ## * `` -> ...17

``` r
str(df_one)
```

    ## tibble [406 × 17] (S3: tbl_df/tbl/data.frame)
    ##  $ Dumpster            : num [1:406] 1 2 3 4 5 6 7 8 NA 9 ...
    ##  $ Month               : chr [1:406] "May" "May" "May" "May" ...
    ##  $ Year                : num [1:406] 2014 2014 2014 2014 2014 ...
    ##  $ Date                : POSIXct[1:406], format: "2014-05-16" "2014-05-16" ...
    ##  $ Weight (tons)       : num [1:406] 4.31 2.74 3.45 3.1 4.06 ...
    ##  $ Volume (cubic yards): num [1:406] 18 13 15 15 18 13 8 16 116 14 ...
    ##  $ Plastic Bottles     : num [1:406] 1450 1120 2450 2380 980 1430 910 3580 14300 2400 ...
    ##  $ Polystyrene         : num [1:406] 1820 1030 3100 2730 870 ...
    ##  $ Cigarette Butts     : num [1:406] 126000 91000 105000 100000 120000 90000 56000 112000 800000 98000 ...
    ##  $ Glass Bottles       : num [1:406] 72 42 50 52 72 46 32 58 424 49 ...
    ##  $ Grocery Bags        : num [1:406] 584 496 1080 896 368 ...
    ##  $ Chip Bags           : num [1:406] 1162 874 2032 1971 753 ...
    ##  $ Sports Balls        : num [1:406] 7.2 5.2 6 6 7.2 5.2 3.2 6.4 46.4 5.6 ...
    ##  $ Homes Powered*      : num [1:406] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ ...15               : chr [1:406] NA NA NA NA ...
    ##  $ ...16               : logi [1:406] NA NA NA NA NA NA ...
    ##  $ ...17               : logi [1:406] NA NA NA NA NA NA ...

``` r
head(df_one)
```

    ## # A tibble: 6 × 17
    ##   Dumpster Month  Year Date                `Weight (tons)` `Volume (cubic yards…
    ##      <dbl> <chr> <dbl> <dttm>                        <dbl>                 <dbl>
    ## 1        1 May    2014 2014-05-16 00:00:00            4.31                    18
    ## 2        2 May    2014 2014-05-16 00:00:00            2.74                    13
    ## 3        3 May    2014 2014-05-16 00:00:00            3.45                    15
    ## 4        4 May    2014 2014-05-17 00:00:00            3.1                     15
    ## 5        5 May    2014 2014-05-17 00:00:00            4.06                    18
    ## 6        6 May    2014 2014-05-20 00:00:00            2.71                    13
    ## # … with 11 more variables: Plastic Bottles <dbl>, Polystyrene <dbl>,
    ## #   Cigarette Butts <dbl>, Glass Bottles <dbl>, Grocery Bags <dbl>,
    ## #   Chip Bags <dbl>, Sports Balls <dbl>, Homes Powered* <dbl>, ...15 <chr>,
    ## #   ...16 <lgl>, ...17 <lgl>

``` r
tail(df_one)
```

    ## # A tibble: 6 × 17
    ##   Dumpster Month        Year Date                `Weight (tons)` `Volume (cubic …
    ##      <dbl> <chr>       <dbl> <dttm>                        <dbl>            <dbl>
    ## 1       NA May Total      NA NA                            33.4               165
    ## 2      342 June         2019 2019-06-12 00:00:00            3.23               15
    ## 3      343 June         2019 2019-06-12 00:00:00            3.08               15
    ## 4      344 June         2019 2019-06-17 00:00:00            3.02               15
    ## 5       NA June Total     NA NA                             9.33               45
    ## 6       NA Grand Total    NA NA                          1122.               5347
    ## # … with 11 more variables: Plastic Bottles <dbl>, Polystyrene <dbl>,
    ## #   Cigarette Butts <dbl>, Glass Bottles <dbl>, Grocery Bags <dbl>,
    ## #   Chip Bags <dbl>, Sports Balls <dbl>, Homes Powered* <dbl>, ...15 <chr>,
    ## #   ...16 <lgl>, ...17 <lgl>
