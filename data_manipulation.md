data_manipulation
================

importa datasets

``` r
litters_df <-
  read_csv("data/FAS_litters.csv", na = c("NA", ".", ""))
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df <-
  janitor::clean_names(litters_df)

pups_df <-
  read_csv("data/FAS_pups.csv", skip = 3, na = c("NA", ".", ""))
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_df <-
  janitor::clean_names(pups_df)
```

## ‘select’

‘select’ selects variables from dataframe

``` r
select(litters_df, group, litter_number, gd0_weight)
```

    ## # A tibble: 49 × 3
    ##    group litter_number   gd0_weight
    ##    <chr> <chr>                <dbl>
    ##  1 Con7  #85                   19.7
    ##  2 Con7  #1/2/95/2             27  
    ##  3 Con7  #5/5/3/83/3-3         26  
    ##  4 Con7  #5/4/2/95/2           28.5
    ##  5 Con7  #4/2/95/3-3           NA  
    ##  6 Con7  #2/2/95/3-2           NA  
    ##  7 Con7  #1/5/3/83/3-3/2       NA  
    ##  8 Con8  #3/83/3-3             NA  
    ##  9 Con8  #2/95/3               NA  
    ## 10 Con8  #3/5/2/2/95           28.5
    ## # ℹ 39 more rows

select a range

``` r
select(litters_df, group:gd_of_birth)
```

    ## # A tibble: 49 × 5
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>
    ##  1 Con7  #85                   19.7        34.7          20
    ##  2 Con7  #1/2/95/2             27          42            19
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19
    ##  5 Con7  #4/2/95/3-3           NA          NA            20
    ##  6 Con7  #2/2/95/3-2           NA          NA            20
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20
    ##  8 Con8  #3/83/3-3             NA          NA            20
    ##  9 Con8  #2/95/3               NA          NA            20
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20
    ## # ℹ 39 more rows

select by removal

``` r
select(litters_df, -group)
```

    ## # A tibble: 49 × 7
    ##    litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85                   19.7        34.7          20               3
    ##  2 #1/2/95/2             27          42            19               8
    ##  3 #5/5/3/83/3-3         26          41.4          19               6
    ##  4 #5/4/2/95/2           28.5        44.1          19               5
    ##  5 #4/2/95/3-3           NA          NA            20               6
    ##  6 #2/2/95/3-2           NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 #3/83/3-3             NA          NA            20               9
    ##  9 #2/95/3               NA          NA            20               8
    ## 10 #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
select(litters_df, -group:gd_of_birth)
```

    ## Warning in x:y: numerical expression has 7 elements: only the first used

    ## # A tibble: 49 × 4
    ##    litter_number   gd0_weight gd18_weight gd_of_birth
    ##    <chr>                <dbl>       <dbl>       <dbl>
    ##  1 #85                   19.7        34.7          20
    ##  2 #1/2/95/2             27          42            19
    ##  3 #5/5/3/83/3-3         26          41.4          19
    ##  4 #5/4/2/95/2           28.5        44.1          19
    ##  5 #4/2/95/3-3           NA          NA            20
    ##  6 #2/2/95/3-2           NA          NA            20
    ##  7 #1/5/3/83/3-3/2       NA          NA            20
    ##  8 #3/83/3-3             NA          NA            20
    ##  9 #2/95/3               NA          NA            20
    ## 10 #3/5/2/2/95           28.5        NA            20
    ## # ℹ 39 more rows

select by prefix

``` r
select(litters_df, group, starts_with("gd"))
```

    ## # A tibble: 49 × 4
    ##    group gd0_weight gd18_weight gd_of_birth
    ##    <chr>      <dbl>       <dbl>       <dbl>
    ##  1 Con7        19.7        34.7          20
    ##  2 Con7        27          42            19
    ##  3 Con7        26          41.4          19
    ##  4 Con7        28.5        44.1          19
    ##  5 Con7        NA          NA            20
    ##  6 Con7        NA          NA            20
    ##  7 Con7        NA          NA            20
    ##  8 Con8        NA          NA            20
    ##  9 Con8        NA          NA            20
    ## 10 Con8        28.5        NA            20
    ## # ℹ 39 more rows

rearrange by selecting

``` r
select(litters_df, starts_with("gd"), group)
```

    ## # A tibble: 49 × 4
    ##    gd0_weight gd18_weight gd_of_birth group
    ##         <dbl>       <dbl>       <dbl> <chr>
    ##  1       19.7        34.7          20 Con7 
    ##  2       27          42            19 Con7 
    ##  3       26          41.4          19 Con7 
    ##  4       28.5        44.1          19 Con7 
    ##  5       NA          NA            20 Con7 
    ##  6       NA          NA            20 Con7 
    ##  7       NA          NA            20 Con7 
    ##  8       NA          NA            20 Con8 
    ##  9       NA          NA            20 Con8 
    ## 10       28.5        NA            20 Con8 
    ## # ℹ 39 more rows

``` r
select(litters_df, litter_number, everything()) #gives litter number first and then everything in dataset
```

    ## # A tibble: 49 × 8
    ##    litter_number   group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>           <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85             Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2       Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3   Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2     Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3     Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2     Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2 Con7        NA          NA            20               9
    ##  8 #3/83/3-3       Con8        NA          NA            20               9
    ##  9 #2/95/3         Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95     Con8        28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
relocate(litters_df, litter_number)
```

    ## # A tibble: 49 × 8
    ##    litter_number   group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>           <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85             Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2       Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3   Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2     Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3     Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2     Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2 Con7        NA          NA            20               9
    ##  8 #3/83/3-3       Con8        NA          NA            20               9
    ##  9 #2/95/3         Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95     Con8        28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

rename by selecting

``` r
select(litters_df, GROUP = group, everything()) #renaming variable group to GROUP and then keeping everything else
```

    ## # A tibble: 49 × 8
    ##    GROUP litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
rename(litters_df, GROUP = group) #renaming variable group to GROUP
```

    ## # A tibble: 49 × 8
    ##    GROUP litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

what if I only select one variable?

``` r
select(litters_df, group) #selecting one variable, give df with just that variable
```

    ## # A tibble: 49 × 1
    ##    group
    ##    <chr>
    ##  1 Con7 
    ##  2 Con7 
    ##  3 Con7 
    ##  4 Con7 
    ##  5 Con7 
    ##  6 Con7 
    ##  7 Con7 
    ##  8 Con8 
    ##  9 Con8 
    ## 10 Con8 
    ## # ℹ 39 more rows

``` r
pull(litters_df, group) #gives vector, NEVER USE THIS, don't pull variable out of df to manipulate
```

    ##  [1] "Con7" "Con7" "Con7" "Con7" "Con7" "Con7" "Con7" "Con8" "Con8" "Con8"
    ## [11] "Con8" "Con8" "Con8" "Con8" "Con8" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7"
    ## [21] "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Low7" "Low7" "Low7"
    ## [31] "Low7" "Low7" "Low7" "Low7" "Low7" "Mod8" "Mod8" "Mod8" "Mod8" "Mod8"
    ## [41] "Mod8" "Mod8" "Low8" "Low8" "Low8" "Low8" "Low8" "Low8" "Low8"

``` r
litters_df$group #same as pull above
```

    ##  [1] "Con7" "Con7" "Con7" "Con7" "Con7" "Con7" "Con7" "Con8" "Con8" "Con8"
    ## [11] "Con8" "Con8" "Con8" "Con8" "Con8" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7"
    ## [21] "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Low7" "Low7" "Low7"
    ## [31] "Low7" "Low7" "Low7" "Low7" "Low7" "Mod8" "Mod8" "Mod8" "Mod8" "Mod8"
    ## [41] "Mod8" "Mod8" "Low8" "Low8" "Low8" "Low8" "Low8" "Low8" "Low8"
