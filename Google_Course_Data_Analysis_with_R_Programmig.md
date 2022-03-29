A Quick Intro for R Beginners
================
true
2/28/2022

## Hi everyone,

This notebook is a summarization of the
<a href="https://www.coursera.org/learn/data-analysis-r/home/welcome"
style="(color: blue)" title="Google">Google Introductory Course to R
Programming</a> the seventh course of the Google Data Analytics
Certificate. Personally I highly recommend to take that course if you
wanna start learning R.

It covers its contents and as you go through the notebook you’ll find
more resources attached in the markdown. During my enrollment, I’ve made
this notebook as a learn-by-practice approach and to spread the
knowledge as much as I can with my fellow aspiring data analysts.

Hope this notebook is useful for you and if you have anything you wanna
modify, I’m looking forward for the feed backs.

Before we write our first code, kindly read the following quotes by
[Yihui Xie](https://bookdown.org/yihui/rmarkdown-cookbook/cache.html).
You’ll know why this is a very important tip as you proceed.

> “When a code chunk is time-consuming to run, you may consider caching
> it via the chunk option `cache = TRUE`. When the cache is turned on,
> knitr will skip the execution of this code chunk if it has been
> executed before and nothing in the code chunk has changed since then.
> When you modify the code chunk.”

> “We do not recommend that you set the chunk option `cache = TRUE`
> globally in a document. Caching can be fairly tricky. Instead, we
> recommend that you enable caching only on individual code chunks that
> are surely time-consuming and do not have side effects.”

*Speaking of code chunks, the easiest way to add code chunks is to press
(ctrl + alt + I). Also you may wanna rename your code chunks
`{r chunk_name}` to easily find that code chunk from the toggle menu
above the console pane.*

``` r
# Run the following code to specify the options for all code chunks in the
# markdown without having to specify the options for each single chunk
knitr::opts_chunk$set(
  echo = TRUE, # Show the input code chunks in your document
  message = FALSE, 
  warning = FALSE, 
  cache =TRUE
) 
```

*Remember you can change the settings of any code chunk from the gear
symbol at the top right of the chunk*

> *“If your script uses add-on packages, load them all at once at the
> very beginning of the file. This is more transparent than sprinkling
> library() calls throughout your code*” Hadley Wickham

``` r
# First load the required packages and the datasets
library(tidyverse)
library(palmerpenguins)
library(lubridate)
library(readxl)
library(here)
library(skimr)
library(janitor)
library(directlabels)
```

Now let’s explore the [Tidyverse package](https://www.tidyverse.org/)

*In short the tidyverse core consists of eight
[packages](https://www.tidyverse.org/packages/). But there’re four
packages that are an essential part of the workflow for data analysts
(ggplot2, dplyr, tidyr and readr). You’ll most likely use these more
often than the others.*

\\newpage

``` r
# Load the dataset
data("penguins")
```

To view the entire dataset in a new window use *`View(penguins)`.*

``` r
# To output the first n rows 
head(penguins,5)
```

    ## # A tibble: 5 × 8
    ##   species island bill_length_mm bill_depth_mm flipper_length_… body_mass_g sex  
    ##   <fct>   <fct>           <dbl>         <dbl>            <int>       <int> <fct>
    ## 1 Adelie  Torge…           39.1          18.7              181        3750 male 
    ## 2 Adelie  Torge…           39.5          17.4              186        3800 fema…
    ## 3 Adelie  Torge…           40.3          18                195        3250 fema…
    ## 4 Adelie  Torge…           NA            NA                 NA          NA <NA> 
    ## 5 Adelie  Torge…           36.7          19.3              193        3450 fema…
    ## # … with 1 more variable: year <int>

``` r
# To output the last n rows
tail(penguins,12)
```

    ## # A tibble: 12 × 8
    ##    species   island bill_length_mm bill_depth_mm flipper_length_mm body_mass_g
    ##    <fct>     <fct>           <dbl>         <dbl>             <int>       <int>
    ##  1 Chinstrap Dream            45.2          16.6               191        3250
    ##  2 Chinstrap Dream            49.3          19.9               203        4050
    ##  3 Chinstrap Dream            50.2          18.8               202        3800
    ##  4 Chinstrap Dream            45.6          19.4               194        3525
    ##  5 Chinstrap Dream            51.9          19.5               206        3950
    ##  6 Chinstrap Dream            46.8          16.5               189        3650
    ##  7 Chinstrap Dream            45.7          17                 195        3650
    ##  8 Chinstrap Dream            55.8          19.8               207        4000
    ##  9 Chinstrap Dream            43.5          18.1               202        3400
    ## 10 Chinstrap Dream            49.6          18.2               193        3775
    ## 11 Chinstrap Dream            50.8          19                 210        4100
    ## 12 Chinstrap Dream            50.2          18.7               198        3775
    ## # … with 2 more variables: sex <fct>, year <int>

``` r
# To output a specific row(s) 
# syntax: dataset[row number(s),column number(s)]
# For a range
penguins[1:5,] 
```

    ## # A tibble: 5 × 8
    ##   species island bill_length_mm bill_depth_mm flipper_length_… body_mass_g sex  
    ##   <fct>   <fct>           <dbl>         <dbl>            <int>       <int> <fct>
    ## 1 Adelie  Torge…           39.1          18.7              181        3750 male 
    ## 2 Adelie  Torge…           39.5          17.4              186        3800 fema…
    ## 3 Adelie  Torge…           40.3          18                195        3250 fema…
    ## 4 Adelie  Torge…           NA            NA                 NA          NA <NA> 
    ## 5 Adelie  Torge…           36.7          19.3              193        3450 fema…
    ## # … with 1 more variable: year <int>

``` r
# For a specified no of rows
penguins[c(2,5),]
```

    ## # A tibble: 2 × 8
    ##   species island bill_length_mm bill_depth_mm flipper_length_… body_mass_g sex  
    ##   <fct>   <fct>           <dbl>         <dbl>            <int>       <int> <fct>
    ## 1 Adelie  Torge…           39.5          17.4              186        3800 fema…
    ## 2 Adelie  Torge…           36.7          19.3              193        3450 fema…
    ## # … with 1 more variable: year <int>

``` r
# To output the entire row for a specific column(s)
penguins[1:3]
```

    ## # A tibble: 344 × 3
    ##    species island    bill_length_mm
    ##    <fct>   <fct>              <dbl>
    ##  1 Adelie  Torgersen           39.1
    ##  2 Adelie  Torgersen           39.5
    ##  3 Adelie  Torgersen           40.3
    ##  4 Adelie  Torgersen           NA  
    ##  5 Adelie  Torgersen           36.7
    ##  6 Adelie  Torgersen           39.3
    ##  7 Adelie  Torgersen           38.9
    ##  8 Adelie  Torgersen           39.2
    ##  9 Adelie  Torgersen           34.1
    ## 10 Adelie  Torgersen           42  
    ## # … with 334 more rows

``` r
# To output specific columns by name for a specific range
# Note the (levels) that appear in the code output. 
# They're basically the unique values of the selected column
penguins$island[2:8]
```

    ## [1] Torgersen Torgersen Torgersen Torgersen Torgersen Torgersen Torgersen
    ## Levels: Biscoe Dream Torgersen

``` r
# for a specific list of rows
penguins$island[c(2,8)]
```

    ## [1] Torgersen Torgersen
    ## Levels: Biscoe Dream Torgersen

*Kindly refer to this [brief introduction to
vectors](https://drive.google.com/file/d/1V_6Ssp2FcEvs6JXhPEBlEwoe3kGvb7oj/view?usp=sharing)
as you proceed.*

``` r
# For atomic vectors, we can't input more than one data type 
# (character, double, integer, logical) in the same vector 
vec = c("ok", "this", "is_a_trial")

# To know the type of data in a specific vector
typeof(vec)
```

    ## [1] "character"

``` r
# To assign names for vector elements (optional)
names(vec) = c("a", "b", "c")

# To output specifc element of a vector either by using the element name
vec["c"]
```

    ##            c 
    ## "is_a_trial"

``` r
# Or by the element number(s) 
vec[2]
```

    ##      b 
    ## "this"

``` r
vec[c(2, 3)]
```

    ##            b            c 
    ##       "this" "is_a_trial"

``` r
# To output the length of a vector
length(vec)
```

    ## [1] 3

``` r
# Unlike atomic vectors, When using lists we may include more than one data type
# as follows
new_list = list(1L, 5.2, "Ok", TRUE, NULL)

# Similarly, we could also assign a name to each element
names(new_list) = c("a", "b", "c", "d", "e")

# To know the datatype of each element
str(new_list)
```

    ## List of 5
    ##  $ a: int 1
    ##  $ b: num 5.2
    ##  $ c: chr "Ok"
    ##  $ d: logi TRUE
    ##  $ e: NULL

``` r
# Alternatively you can assign name while you're creating the list as follows
another_list = list("a" = 1L, "b" = 5.3, "c" = "OK", "d" = FALSE)
names(another_list)
```

    ## [1] "a" "b" "c" "d"

*For more information about vectors, you may refer to this
[chapter](https://r4ds.had.co.nz/vectors.html#vectors).*

``` r
# To compare two floating numbers using a specified tolerance. 
# Obviously, this is more useful than just using (==)
dplyr::near(4.56161, 4.56, tol = 0.01)
```

    ## [1] TRUE

*Kindly refer to this*
[Introduction](https://www.coursera.org/learn/data-analysis-r/supplement/g0l4l/dates-and-times-in-r)
*and [Cheat
Sheet](https://drive.google.com/file/d/16iP4ZMl3KnD6OThP0QoOKOyqASKDkkDu/view?usp=sharing)
as you follow along*

``` r
# After loading the lubridate libray, let's make some codes to learn more 
# about it. 
# For the date in Calgary, Canada
today(tzone = 'MST') 
```

    ## [1] "2022-03-28"

``` r
# The time difference in hours between Cairo & Calgary
calgary = now(tzone = "MST")
cairo = now(tzone = "EET")  
cat((hour(cairo) - hour(calgary)),"hrs")
```

    ## -14 hrs

``` r
# Some examples to convert strings into datetime format. 
# Note how we should use the right function that matches the string order
# All datetimes will be shown in the default format 
# (yyyy-mm-dd hh:mm:ss UTC)
dmy("6th of October 2021")
```

    ## [1] "2021-10-06"

``` r
dmy_hms("13 of January 1993 10:59:12 PM")
```

    ## [1] "1993-01-13 22:59:12 UTC"

``` r
mdy_hm("November 13th 2014 10:13") 
```

    ## [1] "2014-11-13 10:13:00 UTC"

``` r
# To extract specific part of the datetime 
minute(dmy_hms("13 of January 1993 10:59:12 PM"))
```

    ## [1] 59

``` r
second(dmy_hms("13 of January 1993 10:59:12 PM"))
```

    ## [1] 12

``` r
year(dmy_hms("13 of January 1993 10:59:12 PM"))
```

    ## [1] 1993

``` r
week(calgary)
```

    ## [1] 13

*As usual refer to this
[reading](https://www.coursera.org/learn/data-analysis-r/supplement/xEM9d/other-common-data-structures)
and this
[site](http://statseducation.com/Introduction-to-R/modules/getting%20data/data-wrangling/)
for more info about the following subject.*

``` r
# First let's start with this creating a simple dataframe
new_df = data.frame(
                name = c("mohamed", "aly", "farid"), 
                salary = c(15000, 12000, 16500)
              )
new_df
```

    ##      name salary
    ## 1 mohamed  15000
    ## 2     aly  12000
    ## 3   farid  16500

``` r
# Or by using the tribble funciton
new_tibble = tribble(
               ~name, ~salary,
               "mohamed", 15000,
               "aly", 12000,
               "farid", 16500
             )
new_tibble
```

    ## # A tibble: 3 × 2
    ##   name    salary
    ##   <chr>    <dbl>
    ## 1 mohamed  15000
    ## 2 aly      12000
    ## 3 farid    16500

``` r
# To separate a column
x_df = tribble(
          ~name, ~age, ~email,
          "aly_kamal", 25, "aly_kamal@gmail",
       )

x_df %>%
  separate(name, c("first", "last"), sep = "_")
```

    ## # A tibble: 1 × 4
    ##   first last    age email          
    ##   <chr> <chr> <dbl> <chr>          
    ## 1 aly   kamal    25 aly_kamal@gmail

``` r
# To see all available built in datasets in R and their installed packages
data()
```

*The list of available datasets will appear in a new window. That’s why
you can’t see the output of the above code anyway here’s a glimpse of
what will appear.*

<img src="data().JPG" style="width:6in;height:3in" />

``` r
# To load a built in dataset,specify its name and package 
who_data = read_builtin("who", "tidyr")
```

``` r
# To show columns names, datatype in each column and the values you can use
str(who_data)
```

    ## tibble [7,240 × 60] (S3: tbl_df/tbl/data.frame)
    ##  $ country     : chr [1:7240] "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
    ##  $ iso2        : chr [1:7240] "AF" "AF" "AF" "AF" ...
    ##  $ iso3        : chr [1:7240] "AFG" "AFG" "AFG" "AFG" ...
    ##  $ year        : int [1:7240] 1980 1981 1982 1983 1984 1985 1986 1987 1988 1989 ...
    ##  $ new_sp_m014 : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_m1524: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_m2534: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_m3544: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_m4554: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_m5564: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_m65  : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_f014 : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_f1524: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_f2534: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_f3544: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_f4554: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_f5564: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sp_f65  : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_m014 : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_m1524: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_m2534: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_m3544: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_m4554: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_m5564: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_m65  : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_f014 : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_f1524: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_f2534: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_f3544: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_f4554: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_f5564: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_sn_f65  : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_m014 : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_m1524: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_m2534: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_m3544: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_m4554: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_m5564: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_m65  : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_f014 : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_f1524: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_f2534: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_f3544: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_f4554: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_f5564: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ new_ep_f65  : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_m014 : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_m1524: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_m2534: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_m3544: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_m4554: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_m5564: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_m65  : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_f014 : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_f1524: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_f2534: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_f3544: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_f4554: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_f5564: int [1:7240] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ newrel_f65  : int [1:7240] NA NA NA NA NA NA NA NA NA NA ...

``` r
# Or
glimpse(who_data)
```

    ## Rows: 7,240
    ## Columns: 60
    ## $ country      <chr> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan…
    ## $ iso2         <chr> "AF", "AF", "AF", "AF", "AF", "AF", "AF", "AF", "AF", "AF…
    ## $ iso3         <chr> "AFG", "AFG", "AFG", "AFG", "AFG", "AFG", "AFG", "AFG", "…
    ## $ year         <int> 1980, 1981, 1982, 1983, 1984, 1985, 1986, 1987, 1988, 198…
    ## $ new_sp_m014  <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_m1524 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_m2534 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_m3544 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_m4554 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_m5564 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_m65   <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_f014  <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_f1524 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_f2534 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_f3544 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_f4554 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_f5564 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sp_f65   <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_m014  <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_m1524 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_m2534 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_m3544 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_m4554 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_m5564 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_m65   <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_f014  <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_f1524 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_f2534 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_f3544 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_f4554 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_f5564 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_sn_f65   <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_m014  <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_m1524 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_m2534 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_m3544 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_m4554 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_m5564 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_m65   <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_f014  <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_f1524 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_f2534 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_f3544 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_f4554 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_f5564 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ new_ep_f65   <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_m014  <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_m1524 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_m2534 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_m3544 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_m4554 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_m5564 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_m65   <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_f014  <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_f1524 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_f2534 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_f3544 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_f4554 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_f5564 <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ newrel_f65   <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…

``` r
# To show only the number and names of the datasets columns
print(colnames(who_data))
```

    ##  [1] "country"      "iso2"         "iso3"         "year"         "new_sp_m014" 
    ##  [6] "new_sp_m1524" "new_sp_m2534" "new_sp_m3544" "new_sp_m4554" "new_sp_m5564"
    ## [11] "new_sp_m65"   "new_sp_f014"  "new_sp_f1524" "new_sp_f2534" "new_sp_f3544"
    ## [16] "new_sp_f4554" "new_sp_f5564" "new_sp_f65"   "new_sn_m014"  "new_sn_m1524"
    ## [21] "new_sn_m2534" "new_sn_m3544" "new_sn_m4554" "new_sn_m5564" "new_sn_m65"  
    ## [26] "new_sn_f014"  "new_sn_f1524" "new_sn_f2534" "new_sn_f3544" "new_sn_f4554"
    ## [31] "new_sn_f5564" "new_sn_f65"   "new_ep_m014"  "new_ep_m1524" "new_ep_m2534"
    ## [36] "new_ep_m3544" "new_ep_m4554" "new_ep_m5564" "new_ep_m65"   "new_ep_f014" 
    ## [41] "new_ep_f1524" "new_ep_f2534" "new_ep_f3544" "new_ep_f4554" "new_ep_f5564"
    ## [46] "new_ep_f65"   "newrel_m014"  "newrel_m1524" "newrel_m2534" "newrel_m3544"
    ## [51] "newrel_m4554" "newrel_m5564" "newrel_m65"   "newrel_f014"  "newrel_f1524"
    ## [56] "newrel_f2534" "newrel_f3544" "newrel_f4554" "newrel_f5564" "newrel_f65"

``` r
# To rename a column(s)
# Either temporarily
rename(who_data, sp_m1524 = new_sp_m1524)
```

    ## # A tibble: 7,240 × 60
    ##    country     iso2  iso3   year new_sp_m014 sp_m1524 new_sp_m2534 new_sp_m3544
    ##    <chr>       <chr> <chr> <int>       <int>    <int>        <int>        <int>
    ##  1 Afghanistan AF    AFG    1980          NA       NA           NA           NA
    ##  2 Afghanistan AF    AFG    1981          NA       NA           NA           NA
    ##  3 Afghanistan AF    AFG    1982          NA       NA           NA           NA
    ##  4 Afghanistan AF    AFG    1983          NA       NA           NA           NA
    ##  5 Afghanistan AF    AFG    1984          NA       NA           NA           NA
    ##  6 Afghanistan AF    AFG    1985          NA       NA           NA           NA
    ##  7 Afghanistan AF    AFG    1986          NA       NA           NA           NA
    ##  8 Afghanistan AF    AFG    1987          NA       NA           NA           NA
    ##  9 Afghanistan AF    AFG    1988          NA       NA           NA           NA
    ## 10 Afghanistan AF    AFG    1989          NA       NA           NA           NA
    ## # … with 7,230 more rows, and 52 more variables: new_sp_m4554 <int>,
    ## #   new_sp_m5564 <int>, new_sp_m65 <int>, new_sp_f014 <int>,
    ## #   new_sp_f1524 <int>, new_sp_f2534 <int>, new_sp_f3544 <int>,
    ## #   new_sp_f4554 <int>, new_sp_f5564 <int>, new_sp_f65 <int>,
    ## #   new_sn_m014 <int>, new_sn_m1524 <int>, new_sn_m2534 <int>,
    ## #   new_sn_m3544 <int>, new_sn_m4554 <int>, new_sn_m5564 <int>,
    ## #   new_sn_m65 <int>, new_sn_f014 <int>, new_sn_f1524 <int>, …

``` r
# Or permanently 
who_data = rename(who_data, sp_m1524 = new_sp_m1524, iso = iso2)
```

``` r
# We may also use summarize() to show summary statistics
# You'll learn more about pipes (%>%) later in this notebook
who_data %>% 
  summarise(
    latest_year = max(year, na.rm = TRUE),
    average_sp = mean(c(new_sp_f5564, new_sp_f65, new_sn_m014), na.rm = TRUE)
  )
```

    ## # A tibble: 1 × 2
    ##   latest_year average_sp
    ##         <int>      <dbl>
    ## 1        2013       300.

*Always set `na.rm = TRUE` to remove the null values during calculation
and avoid getting NA in the results.*

``` r
# To load a dataset either from the web or by uploading it
# Note that each file may contain only one sheet and be in the CSV format
world_happiness = read_csv(
                    "World_Happiness_data.csv",
                    show_col_types = FALSE
                  )
world_happiness
```

    ## # A tibble: 470 × 14
    ##    Country   `Year of Year` Region Year  `Dystopia Resi…` `Economy (GDP …` F4   
    ##    <chr>              <dbl> <chr>  <chr>            <dbl>            <dbl> <lgl>
    ##  1 Switzerl…           2015 Weste… 1/1/…             2.52              1.4 NA   
    ##  2 Iceland             2015 Weste… 1/1/…             2.70              1.3 NA   
    ##  3 Denmark             2015 Weste… 1/1/…             2.49              1.3 NA   
    ##  4 Norway              2015 Weste… 1/1/…             2.47              1.5 NA   
    ##  5 Canada              2015 North… 1/1/…             2.45              1.3 NA   
    ##  6 Finland             2015 Weste… 1/1/…             2.62              1.3 NA   
    ##  7 Netherla…           2015 Weste… 1/1/…             2.47              1.3 NA   
    ##  8 Sweden              2015 Weste… 1/1/…             2.37              1.3 NA   
    ##  9 New Zeal…           2015 Austr… 1/1/…             2.26              1.3 NA   
    ## 10 Australia           2015 Austr… 1/1/…             2.27              1.3 NA   
    ## # … with 460 more rows, and 7 more variables: Family <dbl>, Freedom <dbl>,
    ## #   Generosity <dbl>, `Happiness Rank` <dbl>, `Happiness Score` <dbl>,
    ## #   `Health (Life Expectancy)` <dbl>, `Trust (Government Corruption)` <dbl>

``` r
# To view the list of sheets for an excel file
excel_sheets("CO2 Dataset.xlsx")
```

    ## [1] "About"                    "CO2 (kt) Pivoted"        
    ## [3] "CO2 (kt) RAW DATA"        "CO2 Data Cleaned"        
    ## [5] "CO2 (kt) for Split"       "CO2 for World to Union"  
    ## [7] "CO2 Per Capita RAW DATA"  "CO2 Per Capita (Pivoted)"
    ## [9] "Metadata - Countries"

``` r
# Paste the file path and the sheet name
co2_df = read_excel(
           "CO2 Dataset.xlsx", 
           sheet = "CO2 Data Cleaned"
         )
```

``` r
# We may create new directories and new files as follows
# If they're created successfully, TRUE will appear in the code output
dir.create("trial_dir")
dir.create("new_dir")
file.create("new_file.csv")
```

    ## [1] TRUE

``` r
# We may create matrices using the matrix() function provided the elements and 
# the number of rows or the number of cols
matrix_a = matrix(c(3:14), nrow = 4)
matrix_b = matrix(c(20:31), nrow = 3)
```

``` r
# For matrices multiplication, use the (%*%) operator
# The number of columns of the first one must equal the number of rows of the 
# second
matrix_c = matrix_b %*% matrix_a
```

*Check out this link to know more about [operators and
conditions](https://drive.google.com/file/d/1b7ZeDWQJ0IU9WhOMRmTpcDc6LCqX5Qr7/view?usp=sharing)*

``` r
# First check the simple examples below
x = 5 
x > 3 & x < 8
```

    ## [1] TRUE

``` r
x > 7 & x == 5  # TRUE & FALSE = FALSE
```

    ## [1] FALSE

``` r
x > 5 | x == 3  # | is the same as ||
```

    ## [1] FALSE

``` r
x != 8
```

    ## [1] TRUE

``` r
y = 0
!y # As y equals zero, not zero is TRUE
```

    ## [1] TRUE

``` r
# Now if we have a multiple values/elements
price <- c(100, 20, 5, 200, 60, 88, 190, 33, 290, 64)
price > 50
```

    ##  [1]  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE

``` r
x = c(12, 15, 20)
y = c(13, 16, 34)

# In case of element-wise logical operators, each single element will be checked
x & y < 15
```

    ## [1]  TRUE FALSE FALSE

``` r
# In the other case, the first element only will be checked
x && y < 15
```

    ## [1] TRUE

``` r
# A quick note regarding arithmatic operators (%%) and (%/%)
7 %% 3
```

    ## [1] 1

``` r
7 %/% 3
```

    ## [1] 2

``` r
# If we wanna choose a variable name that's a reserved word (TRUE, in, etc.) or
# starts with an (_), we must use backticks (` `) to avoid getting errors.
`TRUE` = 18
`_x01` = 21
`TRUE`
```

    ## [1] 18

``` r
`_x01`
```

    ## [1] 21

``` r
# (<<-) is an assigment operator that's mainly used in functions. 
# For instance if we wanna change change the global value of a variable inside a
# function as follows.
x <- 1
y <- 3
fun_3 <- function() {
          x <- 2
          y <<- 5
          print(paste(x, y))
}

fun_3() 
```

    ## [1] "2 5"

``` r
x # (the value hasn't changed)
```

    ## [1] 1

``` r
y # (the value has changed)
```

    ## [1] 5

``` r
# To access functions of a pacakge use the (::) operators
# Enter the package name then (::) and press tab to view the list of functions
lubridate::.__C__Interval 
```

    ## Class "Interval" [package "lubridate"]
    ## 
    ## Slots:
    ##                                     
    ## Name:      .Data     start     tzone
    ## Class:   numeric   POSIXct character
    ## 
    ## Extends: 
    ## Class "Timespan", directly
    ## Class "numeric", from data part
    ## Class "vector", by class "numeric", distance 2

``` r
# We may filter a dataframe based on logical condtion(s) using the filter() function
filter(who_data, country == c("Afghanistan",'Albania') & year > 1990)
```

    ## # A tibble: 23 × 60
    ##    country     iso   iso3   year new_sp_m014 sp_m1524 new_sp_m2534 new_sp_m3544
    ##    <chr>       <chr> <chr> <int>       <int>    <int>        <int>        <int>
    ##  1 Afghanistan AF    AFG    1992          NA       NA           NA           NA
    ##  2 Afghanistan AF    AFG    1994          NA       NA           NA           NA
    ##  3 Afghanistan AF    AFG    1996          NA       NA           NA           NA
    ##  4 Afghanistan AF    AFG    1998          30      129          128           90
    ##  5 Afghanistan AF    AFG    2000          52      228          183          149
    ##  6 Afghanistan AF    AFG    2002          90      476          481          368
    ##  7 Afghanistan AF    AFG    2004         139      537          568          360
    ##  8 Afghanistan AF    AFG    2006         193      837          791          574
    ##  9 Afghanistan AF    AFG    2008         187      941          773          545
    ## 10 Afghanistan AF    AFG    2010         197      986          819          491
    ## # … with 13 more rows, and 52 more variables: new_sp_m4554 <int>,
    ## #   new_sp_m5564 <int>, new_sp_m65 <int>, new_sp_f014 <int>,
    ## #   new_sp_f1524 <int>, new_sp_f2534 <int>, new_sp_f3544 <int>,
    ## #   new_sp_f4554 <int>, new_sp_f5564 <int>, new_sp_f65 <int>,
    ## #   new_sn_m014 <int>, new_sn_m1524 <int>, new_sn_m2534 <int>,
    ## #   new_sn_m3544 <int>, new_sn_m4554 <int>, new_sn_m5564 <int>,
    ## #   new_sn_m65 <int>, new_sn_f014 <int>, new_sn_f1524 <int>, …

``` r
# Let's see an example of how the if,else and else if can be used in R
# Note the code syntax. To make sure you fully get it try to apply some changes
# and see the results
# & and | should never be used inside of an if clause because they can return 
# vectors. Always use && and || instead.
if (who_data[100,]['country'] %in% 
  c('China','Afghanistan','SaudiArabia')) {
  print("Asian Country")
} else if (who_data[100,]['country'] == 'Algeria') {
  print("African Country")
} else {
  print("European Country")
}
```

    ## [1] "African Country"

``` r
# To show the unique values of a column
print(unique(who_data['country']))
```

    ## # A tibble: 219 × 1
    ##    country            
    ##    <chr>              
    ##  1 Afghanistan        
    ##  2 Albania            
    ##  3 Algeria            
    ##  4 American Samoa     
    ##  5 Andorra            
    ##  6 Angola             
    ##  7 Anguilla           
    ##  8 Antigua and Barbuda
    ##  9 Argentina          
    ## 10 Armenia            
    ## # … with 209 more rows

### Note for using if

when you run the above code you can see that Egypt, Algeria and Senegal
are in the countries list. However when you run the code below, you’ll
get “not exist” and that’s because when using if for more than one
element, it’ll look through the first element/row only and in our
dataframe the country in the first row is ‘Afghanistan’ hence we got the
‘not exist’ result.

``` r
if (who_data['country'] %in% c("Egypt", 'Algeria', 'Senegal')) {
  print("ok")
} else {
  print("not exist")
}
```

    ## [1] "not exist"

*Additional notes by Google on* [Keeping your code
readable](https://drive.google.com/file/d/1p0njnrFYsLpMcKcNojmiW_eqL4FyJvv3/view?usp=sharing)

*Check out this chapter on [Pipes](https://r4ds.had.co.nz/pipes.html) as
you proceed through the following*

``` r
# We shall use the (ToothGrowth) dataset to explore the pipes tool
tg_df = read_builtin("ToothGrowth","datasets")
tg_df
```

    ##     len supp dose
    ## 1   4.2   VC  0.5
    ## 2  11.5   VC  0.5
    ## 3   7.3   VC  0.5
    ## 4   5.8   VC  0.5
    ## 5   6.4   VC  0.5
    ## 6  10.0   VC  0.5
    ## 7  11.2   VC  0.5
    ## 8  11.2   VC  0.5
    ## 9   5.2   VC  0.5
    ## 10  7.0   VC  0.5
    ## 11 16.5   VC  1.0
    ## 12 16.5   VC  1.0
    ## 13 15.2   VC  1.0
    ## 14 17.3   VC  1.0
    ## 15 22.5   VC  1.0
    ## 16 17.3   VC  1.0
    ## 17 13.6   VC  1.0
    ## 18 14.5   VC  1.0
    ## 19 18.8   VC  1.0
    ## 20 15.5   VC  1.0
    ## 21 23.6   VC  2.0
    ## 22 18.5   VC  2.0
    ## 23 33.9   VC  2.0
    ## 24 25.5   VC  2.0
    ## 25 26.4   VC  2.0
    ## 26 32.5   VC  2.0
    ## 27 26.7   VC  2.0
    ## 28 21.5   VC  2.0
    ## 29 23.3   VC  2.0
    ## 30 29.5   VC  2.0
    ## 31 15.2   OJ  0.5
    ## 32 21.5   OJ  0.5
    ## 33 17.6   OJ  0.5
    ## 34  9.7   OJ  0.5
    ## 35 14.5   OJ  0.5
    ## 36 10.0   OJ  0.5
    ## 37  8.2   OJ  0.5
    ## 38  9.4   OJ  0.5
    ## 39 16.5   OJ  0.5
    ## 40  9.7   OJ  0.5
    ## 41 19.7   OJ  1.0
    ## 42 23.3   OJ  1.0
    ## 43 23.6   OJ  1.0
    ## 44 26.4   OJ  1.0
    ## 45 20.0   OJ  1.0
    ## 46 25.2   OJ  1.0
    ## 47 25.8   OJ  1.0
    ## 48 21.2   OJ  1.0
    ## 49 14.5   OJ  1.0
    ## 50 27.3   OJ  1.0
    ## 51 25.5   OJ  2.0
    ## 52 26.4   OJ  2.0
    ## 53 22.4   OJ  2.0
    ## 54 24.5   OJ  2.0
    ## 55 24.8   OJ  2.0
    ## 56 30.9   OJ  2.0
    ## 57 26.4   OJ  2.0
    ## 58 27.3   OJ  2.0
    ## 59 29.4   OJ  2.0
    ## 60 23.0   OJ  2.0

``` r
# Let's say we want to the effectiveness of each supplement on teeth
# Always remeber to indent every new line of code in the pipe
supp_effect <- tg_df %>%
  group_by(supp) %>%
  summarise(
    average_length = mean(len, na.rm = TRUE),
    average_dose = mean(dose, na.rm = TRUE),
  )
supp_effect
```

    ## # A tibble: 2 × 3
    ##   supp  average_length average_dose
    ##   <fct>          <dbl>        <dbl>
    ## 1 OJ              20.7         1.17
    ## 2 VC              17.0         1.17

``` r
# Now let's try a new dataframe from the ggplot2 package
diamond_df = read_builtin("diamonds", "ggplot2")

# We may create new column(s) and specify their locations and values either by
# add_column() or mutate()
diamond_df = add_column(
               diamond_df, 
               category = "low_price",
              .before = "cut"
             )
diamond_df$category[
             diamond_df$price > 1000 & 
             diamond_df$price < 10000 
           ] = 'Meduim Price'
diamond_df$category[diamond_df$price > 10000] = "High Price"
```

``` r
# Let's say for easier interpretation we wanna create a dataframe that has only
# selected columns of the original dataframe.
cut_to_price = select(diamond_df, colnames(diamond_df)[3:8])
cut_to_price
```

    ## # A tibble: 53,940 × 6
    ##    cut       color clarity depth table price
    ##    <ord>     <ord> <ord>   <dbl> <dbl> <int>
    ##  1 Ideal     E     SI2      61.5    55   326
    ##  2 Premium   E     SI1      59.8    61   326
    ##  3 Good      E     VS1      56.9    65   327
    ##  4 Premium   I     VS2      62.4    58   334
    ##  5 Good      J     SI2      63.3    58   335
    ##  6 Very Good J     VVS2     62.8    57   336
    ##  7 Very Good I     VVS1     62.3    57   336
    ##  8 Very Good H     SI1      61.9    55   337
    ##  9 Fair      E     VS2      65.1    61   337
    ## 10 Very Good H     VS1      59.4    61   338
    ## # … with 53,930 more rows

``` r
# On the other hand, if we wanna exclude specific columns
select(diamond_df, -colnames(diamond_df)[c(3,8)])
```

    ## # A tibble: 53,940 × 9
    ##    carat category  color clarity depth table     x     y     z
    ##    <dbl> <chr>     <ord> <ord>   <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1  0.23 low_price E     SI2      61.5    55  3.95  3.98  2.43
    ##  2  0.21 low_price E     SI1      59.8    61  3.89  3.84  2.31
    ##  3  0.23 low_price E     VS1      56.9    65  4.05  4.07  2.31
    ##  4  0.29 low_price I     VS2      62.4    58  4.2   4.23  2.63
    ##  5  0.31 low_price J     SI2      63.3    58  4.34  4.35  2.75
    ##  6  0.24 low_price J     VVS2     62.8    57  3.94  3.96  2.48
    ##  7  0.24 low_price I     VVS1     62.3    57  3.95  3.98  2.47
    ##  8  0.26 low_price H     SI1      61.9    55  4.07  4.11  2.53
    ##  9  0.22 low_price E     VS2      65.1    61  3.87  3.78  2.49
    ## 10  0.23 low_price H     VS1      59.4    61  4     4.05  2.39
    ## # … with 53,930 more rows

``` r
# The readr package has 8 buitlin datasets of different formats 
# (csv, txt, zip, etc.)
readr_example()
```

    ##  [1] "challenge.csv"         "chickens.csv"          "epa78.txt"            
    ##  [4] "example.log"           "fwf-sample.txt"        "massey-rating.txt"    
    ##  [7] "mtcars.csv"            "mtcars.csv.bz2"        "mtcars.csv.zip"       
    ## [10] "whitespace-sample.txt"

``` r
# To load anyone of those datasets
read_csv(readr_example('mtcars.csv'), show_col_types = FALSE)
```

    ## # A tibble: 32 × 11
    ##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
    ##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
    ##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
    ##  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
    ##  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
    ##  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
    ##  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
    ##  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
    ##  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
    ##  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
    ## 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
    ## # … with 22 more rows

``` r
# we may even read a compressed file and the read_csv function will decompress
# it.
mt_cars = read_csv(readr_example('mtcars.csv.zip'), show_col_types = FALSE)
mt_cars
```

    ## # A tibble: 32 × 11
    ##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
    ##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
    ##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
    ##  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
    ##  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
    ##  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
    ##  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
    ##  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
    ##  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
    ##  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
    ## 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
    ## # … with 22 more rows

``` r
# We may create a new file in the directory and put/write data in it 
file.create("massey_rating")
```

    ## [1] TRUE

``` r
mr = read_file(readr_example('massey-rating.txt'))
write_file(mr, file = "massey_rating")
```

``` r
# To get summarized statistics about the dataframe
skim_without_charts(co2_df)
```

|                                                  |        |
|:-------------------------------------------------|:-------|
| Name                                             | co2_df |
| Number of rows                                   | 11127  |
| Number of columns                                | 6      |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |        |
| Column type frequency:                           |        |
| character                                        | 3      |
| numeric                                          | 3      |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |        |
| Group variables                                  | None   |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| Country Code  |         0 |             1 |   3 |   3 |     0 |      214 |          0 |
| Country Name  |         0 |             1 |   4 |  30 |     0 |      214 |          0 |
| Region        |         0 |             1 |  10 |  26 |     0 |        7 |          0 |

**Variable type: numeric**

| skim_variable                | n_missing | complete_rate |     mean |        sd |      p0 |     p25 |     p50 |      p75 |       p100 |
|:-----------------------------|----------:|--------------:|---------:|----------:|--------:|--------:|--------:|---------:|-----------:|
| Year                         |         0 |          1.00 |  1985.50 |     15.01 | 1960.00 | 1973.00 | 1986.00 |  1998.50 |    2011.00 |
| CO2 (kt)                     |      2095 |          0.81 | 98607.44 | 466399.81 |    3.67 |  594.05 | 4327.06 | 39924.46 | 9019518.21 |
| CO2 Per Capita (metric tons) |      2098 |          0.81 |     4.34 |      7.56 |    0.00 |    0.35 |    1.45 |     5.95 |      99.84 |

``` r
# We may also use the summary() function
summary(co2_df)
```

    ##  Country Code       Country Name          Region               Year     
    ##  Length:11127       Length:11127       Length:11127       Min.   :1960  
    ##  Class :character   Class :character   Class :character   1st Qu.:1973  
    ##  Mode  :character   Mode  :character   Mode  :character   Median :1986  
    ##                                                           Mean   :1986  
    ##                                                           3rd Qu.:1998  
    ##                                                           Max.   :2011  
    ##                                                                         
    ##     CO2 (kt)       CO2 Per Capita (metric tons)
    ##  Min.   :      4   Min.   : 0.0006             
    ##  1st Qu.:    594   1st Qu.: 0.3490             
    ##  Median :   4327   Median : 1.4506             
    ##  Mean   :  98607   Mean   : 4.3408             
    ##  3rd Qu.:  39924   3rd Qu.: 5.9532             
    ##  Max.   :9019518   Max.   :99.8404             
    ##  NA's   :2095      NA's   :2098

``` r
# Now if we wanna make our columns names lower case and consists only of letters
# numbers and underscores
co2_df = clean_names(co2_df)

co2_df %>% 
  group_by(country_name) %>%
  summarize(average_emissions = mean(co2_per_capita_metric_tons, na.rm = TRUE))
```

    ## # A tibble: 214 × 2
    ##    country_name        average_emissions
    ##    <chr>                           <dbl>
    ##  1 Afghanistan                     0.139
    ##  2 Albania                         1.66 
    ##  3 Algeria                         2.39 
    ##  4 American Samoa                NaN    
    ##  5 Andorra                         6.93 
    ##  6 Angola                          0.610
    ##  7 Antigua and Barbuda             5.11 
    ##  8 Argentina                       3.56 
    ##  9 Armenia                         1.23 
    ## 10 Aruba                          21.8  
    ## # … with 204 more rows

``` r
# We can create a new column that's the sum of multiple columns as follows
co2_df = co2_df %>%
  mutate(
    'total' = rowSums(
                co2_df[,c('co2_per_capita_metric_tons', 'co2_kt')],
                na.rm = TRUE
              )
  ) 
head(co2_df)
```

    ## # A tibble: 6 × 7
    ##   country_code country_name region            year co2_kt co2_per_capita_… total
    ##   <chr>        <chr>        <chr>            <dbl>  <dbl>            <dbl> <dbl>
    ## 1 ABW          Aruba        Latin America &…  1960     NA               NA     0
    ## 2 ABW          Aruba        Latin America &…  1961     NA               NA     0
    ## 3 ABW          Aruba        Latin America &…  1962     NA               NA     0
    ## 4 ABW          Aruba        Latin America &…  1963     NA               NA     0
    ## 5 ABW          Aruba        Latin America &…  1964     NA               NA     0
    ## 6 ABW          Aruba        Latin America &…  1965     NA               NA     0

``` r
# If we want to get the sum of each column separately
colSums(co2_df[,c('co2_per_capita_metric_tons', 'co2_kt')], na.rm = TRUE)
```

    ## co2_per_capita_metric_tons                     co2_kt 
    ##                   39193.28               890622393.98

``` r
# If we wanna merge multiple column into a single one
# Set remove to FALSE if you also wanna keep the original columns
co2_df = co2_df %>%
  unite(
    combined, 
    c("country_name", "co2_per_capita_metric_tons", "year"),
    sep = "/"
  )
co2_df
```

    ## # A tibble: 11,127 × 5
    ##    country_code combined      region                    co2_kt total
    ##    <chr>        <chr>         <chr>                      <dbl> <dbl>
    ##  1 ABW          Aruba/NA/1960 Latin America & Caribbean     NA     0
    ##  2 ABW          Aruba/NA/1961 Latin America & Caribbean     NA     0
    ##  3 ABW          Aruba/NA/1962 Latin America & Caribbean     NA     0
    ##  4 ABW          Aruba/NA/1963 Latin America & Caribbean     NA     0
    ##  5 ABW          Aruba/NA/1964 Latin America & Caribbean     NA     0
    ##  6 ABW          Aruba/NA/1965 Latin America & Caribbean     NA     0
    ##  7 ABW          Aruba/NA/1966 Latin America & Caribbean     NA     0
    ##  8 ABW          Aruba/NA/1967 Latin America & Caribbean     NA     0
    ##  9 ABW          Aruba/NA/1968 Latin America & Caribbean     NA     0
    ## 10 ABW          Aruba/NA/1969 Latin America & Caribbean     NA     0
    ## # … with 11,117 more rows

``` r
# Now let's do the reverse process
co2_df = co2_df %>%
  separate(
    combined, 
    c("country_name", "co2_per_capita_metric_tons", "year"),
    sep = "/"
  )
co2_df
```

    ## # A tibble: 11,127 × 7
    ##    country_code country_name co2_per_capita_metric_to… year  region co2_kt total
    ##    <chr>        <chr>        <chr>                     <chr> <chr>   <dbl> <dbl>
    ##  1 ABW          Aruba        NA                        1960  Latin…     NA     0
    ##  2 ABW          Aruba        NA                        1961  Latin…     NA     0
    ##  3 ABW          Aruba        NA                        1962  Latin…     NA     0
    ##  4 ABW          Aruba        NA                        1963  Latin…     NA     0
    ##  5 ABW          Aruba        NA                        1964  Latin…     NA     0
    ##  6 ABW          Aruba        NA                        1965  Latin…     NA     0
    ##  7 ABW          Aruba        NA                        1966  Latin…     NA     0
    ##  8 ABW          Aruba        NA                        1967  Latin…     NA     0
    ##  9 ABW          Aruba        NA                        1968  Latin…     NA     0
    ## 10 ABW          Aruba        NA                        1969  Latin…     NA     0
    ## # … with 11,117 more rows

*To learn more about
[Pivoting](https://tidyr.tidyverse.org/articles/pivot.html)*

``` r
beachbugs_wide = read_csv('beachbugs_wide.csv')
head(beachbugs_wide)
```

    ## # A tibble: 6 × 12
    ##    year `Bondi Beach` `Bronte Beach` `Clovelly Beach` `Coogee Beach`
    ##   <dbl>         <dbl>          <dbl>            <dbl>          <dbl>
    ## 1  2013          32.2           26.8             9.28           39.7
    ## 2  2014          11.1           17.5            13.8            52.6
    ## 3  2015          14.3           23.6             8.82           40.3
    ## 4  2016          19.4           61.3            11.3            59.5
    ## 5  2017          13.2           16.8             7.93           20.7
    ## 6  2018          22.9           43.4            10.6            21.6
    ## # … with 7 more variables: `Gordons Bay (East)` <dbl>,
    ## #   `Little Bay Beach` <dbl>, `Malabar Beach` <dbl>, `Maroubra Beach` <dbl>,
    ## #   `South Maroubra Beach` <dbl>, `South Maroubra Rockpool` <dbl>,
    ## #   `Tamarama Beach` <dbl>

``` r
bb_long = beachbugs_wide %>%
  pivot_longer(
    cols = colnames(beachbugs_wide)[2:12],
    names_to = 'beach',
    values_to = 'bugs'
  )
head(bb_long)
```

    ## # A tibble: 6 × 3
    ##    year beach                bugs
    ##   <dbl> <chr>               <dbl>
    ## 1  2013 Bondi Beach         32.2 
    ## 2  2013 Bronte Beach        26.8 
    ## 3  2013 Clovelly Beach       9.28
    ## 4  2013 Coogee Beach        39.7 
    ## 5  2013 Gordons Bay (East)  24.8 
    ## 6  2013 Little Bay Beach   122.

``` r
beachbugs_long = read_csv("beachbugs_long.csv")
head(beachbugs_long)
```

    ## # A tibble: 6 × 3
    ##    year site               buglevels
    ##   <dbl> <chr>                  <dbl>
    ## 1  2013 Bondi Beach            32.2 
    ## 2  2013 Bronte Beach           26.8 
    ## 3  2013 Clovelly Beach          9.28
    ## 4  2013 Coogee Beach           39.7 
    ## 5  2013 Gordons Bay (East)     24.8 
    ## 6  2013 Little Bay Beach      122.

``` r
bb_wide = beachbugs_long %>%
  pivot_wider(
    names_from = 'site',
    values_from = 'buglevels'
  )
head(bb_wide)
```

    ## # A tibble: 6 × 12
    ##    year `Bondi Beach` `Bronte Beach` `Clovelly Beach` `Coogee Beach`
    ##   <dbl>         <dbl>          <dbl>            <dbl>          <dbl>
    ## 1  2013          32.2           26.8             9.28           39.7
    ## 2  2014          11.1           17.5            13.8            52.6
    ## 3  2015          14.3           23.6             8.82           40.3
    ## 4  2016          19.4           61.3            11.3            59.5
    ## 5  2017          13.2           16.8             7.93           20.7
    ## 6  2018          22.9           43.4            10.6            21.6
    ## # … with 7 more variables: `Gordons Bay (East)` <dbl>,
    ## #   `Little Bay Beach` <dbl>, `Malabar Beach` <dbl>, `Maroubra Beach` <dbl>,
    ## #   `South Maroubra Beach` <dbl>, `South Maroubra Rockpool` <dbl>,
    ## #   `Tamarama Beach` <dbl>

### Note that every plot in the gglpot package must start with the ggplot()

### function where you specify the dataset.

Bar plots can be used to show the count of each categorical value in one
variable only. If we want to used the bar plot for two variables, we use
the column chart. However it’s better to use scatter plots and heat
maps. Let’s try this simple column & scatter plots to see the
difference.

``` r
ggplot(drop_na(penguins)) + 
  geom_col(mapping = aes(flipper_length_mm, body_mass_g, fill = sex))
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

``` r
ggplot(
  drop_na(penguins),
  # We may change the opaquity of the points using the alpha aesthetic to     
  # be able to see whether if there're points plotted on top of each other
  # For instance, setting the alpha = 0.25 means that four points staked      
  # on top of each other will create a solid point.
  aes(flipper_length_mm, body_mass_g, color = sex, alpha = 0.25)
) +
  # When plotting large number of points, it's quite useful to use geom_smooth
  # to clearly see the overall relationship between the variables.
  geom_smooth(se = FALSE) +
  geom_point(show.legend = FALSE) +
  # To apply labels inside the chart
  geom_dl(aes(label = sex, fontface = "italic"), method = "smart.grid") +
  # To add titles, subtitles, captions, y and x labels
  labs(
    title = "Flipper length vs Body mass",
    # Subtitles are usually used to highlight important information
    subtitle = "The relation between body mass and the flipper length",
    # Caption let us show the source of our data
    caption = "Data collected by Dr. Kristen Gorman",
    x = "Flipper length (mm)",
    y = "Body mass (g)"
  ) +
  # Another way to (manually) add the labels or create shapes
  annotate(
    geom = "segment",
    x = c(204, 200),
    xend = c(204, 200),
    y = c(3200, 4800),
    yend = c(4000, 4150),
    color = c("lightcoral", "lightblue"),
    size = c(0.45, 0.45),
    angle = c(90, 90),
    arrow = arrow()
  )
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-47-1.png)<!-- -->

``` r
# We may also use the geom_count to visualize the relationship between 
# the flipper_length and the body_mass in addition to the frequency of 
# value.

count_table = drop_na(penguins) %>%
  count(flipper_length_mm, body_mass_g) 
count_table
```

    ## # A tibble: 298 × 3
    ##    flipper_length_mm body_mass_g     n
    ##                <int>       <int> <int>
    ##  1               172        3150     1
    ##  2               174        3400     1
    ##  3               176        3450     1
    ##  4               178        2900     1
    ##  5               178        3250     2
    ##  6               178        3900     1
    ##  7               180        3550     1
    ##  8               180        3600     1
    ##  9               180        3800     1
    ## 10               180        3950     1
    ## # … with 288 more rows

``` r
ggplot(
  drop_na(penguins), 
  aes(flipper_length_mm, body_mass_g, shape = sex)
) + 
  geom_count() 
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-48-1.png)<!-- -->

``` r
drop_na(penguins) %>%
  count(island, species) %>%
  ggplot() +
  geom_tile(mapping = aes(island,species,fill = n))
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-49-1.png)<!-- -->

Now let’s say we wanna create a bar plot that shows the number of each
species per island and apply customized color to each species. Note that
the default position is the stack one. There’s also the dodge so fill
feel free to try each of them. We could create multiple plots using
facet_grid as follows.

``` r
ggplot(drop_na(penguins), aes(island, fill = species)) +
  geom_bar(show.legend = FALSE, width = 0.3, position = "stack") +
  # Select desired colors either by name or code
  scale_fill_manual(values = c("#00AFBB", "#E7B300", "#FC4E07")) +
  facet_wrap(sex ~ ., ncol = 1, strip.position = "top") +
  scale_y_continuous(limits = c(0, 90), n.breaks = 10) +
  theme(
    axis.text = element_text(size = 15, angle = 45),
    axis.text.x = element_text(vjust = 0.65),
    axis.title = element_text(size = 25, color = "steelblue"),
    strip.text = element_text(size = 20, color = "steelblue"),
    strip.background = element_blank()
  ) +
  # If we wanna to show label(s) on each bar
  stat_count(
    geom = "text",
    colour = "black",
    size = 5,
    aes(label = species),
    position = position_stack(vjust = 0.5)
  ) +
  stat_count(
    geom = "text",
    color = "black",
    size = 4,
    position = position_stack(vjust = 0.28),
    aes(label = ..count..)
  )
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-50-1.png)<!-- -->

We may define Histograms as similar of barplots except they’re used for
quantitative variables.

``` r
ggplot(penguins, aes(bill_length_mm, fill = species)) + 
  geom_histogram(show.legend = FALSE, col = 'grey') + 
  scale_fill_manual(values = c("ForestGreen", "#E7B300", "#FC4E07")) + 
  facet_wrap(species ~ ., strip.position = 'top', ncol = 1) + 
  theme(
   axis.title = element_text(size = 20),
   strip.text = element_text(size = 20),
   axis.text = element_text(size = 15)
  ) +  
  scale_y_continuous(limits = c(0,25))
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-51-1.png)<!-- -->

``` r
# To save the plot separately in a specific format
ggsave("penguins_2.png")
```

``` r
# Another example
ggplot(data = diamonds) +
  geom_bar(mapping = aes(x = color, fill = cut)) +
  facet_wrap(.~cut)
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-52-1.png)<!-- -->

There are three alternatives to the histogram as well

``` r
# Density plot
ggplot(penguins, aes(bill_length_mm, fill = species)) + 
  geom_density(show.legend = FALSE) + 
  scale_fill_manual(values = c("ForestGreen", "#E7B300", "#FC4E07")) + 
  facet_wrap(species ~ ., ncol = 1, strip.position = 'top') + 
  scale_x_continuous(limits = c(20,60), n.breaks = 5) + 
  theme(
   axis.text = element_text(size = 15, angle = 45),
   axis.title = element_text(size = 20),
   strip.text = element_text(size = 20)              
  )
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-53-1.png)<!-- -->

``` r
# Frequency plot
ggplot(penguins, aes(bill_length_mm, color = species)) + 
  geom_freqpoly(show.legend = FALSE) + 
  scale_color_manual(values = c("ForestGreen", "#E7B300", "#FC4E07")) + 
  facet_grid(species ~ .) + 
  scale_x_continuous(limits = c(20,60), n.breaks = 5) + 
  scale_y_continuous(limits = c(0,30), n.breaks = 6) + 
  theme(
    axis.text = element_text(size = 15, angle = 45),
    axis.title = element_text(size = 20),
    strip.text = element_text(size = 20)
  )
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-54-1.png)<!-- -->

``` r
# Dot plot
ggplot(penguins, aes(bill_length_mm, fill = species)) + 
  geom_dotplot(show.legend = FALSE) +
  scale_fill_manual(values = c("ForestGreen", "#E7B300", "#FC4E07")) + 
  facet_wrap(species ~ ., ncol = 1, strip.position = 'top') + 
  scale_x_continuous(limits = c(20,60), n.breaks = 5) + 
  theme(
    axis.title = element_text(size = 20),
    axis.text = element_text(size = 15),
    strip.text = element_text(size = 20)
  )
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-55-1.png)<!-- -->

\\newpage

Now when working with Box plots, always keep in mind these two main
notes: a) Box plots are usually used to plot qualitative
vs. quantitative variables b) Any value \> 1.5\*IQR will be plotted as
an outlier

``` r
ggplot(drop_na(penguins), aes(species, body_mass_g, fill = species)) + 
  geom_boxplot(
      show.legend = FALSE,
      outlier.shape = 21, # A number 0:25 , NA will hide the outliers
      outlier.size = 3,
      outlier.fill = 'red'
  ) + 
  facet_wrap(sex ~ ., scales = 'free_x', ncol = 1, strip.position = 'top') + 
  scale_y_continuous(limits = c(2500,6500), n.breaks = 10)  + 
  theme(
    axis.text = element_text(angle = 45, size = 15),
    axis.text.x = element_text(vjust = 0.65),
    axis.title = element_text(size = 20, color = 'steelblue'),
    strip.text = element_text(size = 20, color = 'steelblue')
  ) +
  ylim(3000, 6000) # To zoom in a specified portion of the plot (with clipping)
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-56-1.png)<!-- -->

*Note that zoom with clipping removes the excluded point and recreate
the plot*

Another similar plot is the violin plot. note how each violin shape gets
thicker and thinner corresponding to the frequency of each value.

``` r
ggplot(drop_na(penguins),aes(species, body_mass_g, fill = species)) + 
  geom_violin(
      show.legend = FALSE,
      outlier.shape = 21, # A number 0:25 , NA will hide the outliers
      outlier.size = 3,
      outlier.fill = 'red',
      draw_quantiles = c(0.25, 0.5, 0.75)
  ) + 
  facet_wrap(sex ~ ., scales = 'free_x', ncol = 1) + 
  scale_y_continuous(limits = c(2000,7000), n.breaks = 10) + 
  theme(
    axis.text = element_text(angle = 45, size = 15),
    axis.text.x = element_text(vjust = 0.65),
    axis.title = element_text(size = 20, color = 'steelblue'),
    strip.text = element_text(size = 20, color = 'steelblue')
  ) +
  # To zoom without clipping use coord_cartesian() as follows.
  coord_cartesian(ylim = c(2500, 6500)) 
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-57-1.png)<!-- -->

If we want to plot two continuous variables using box plots. we may use
cut_interval/cut_number/cut_width. Those cut functions basically group
the values into a specified number of categories as shown below.

*Note: If we don’t wanna the source code to appear highlighted in the
final rendered file, we set highlight = FALSE as shown below.*

``` text
penguins %>%
  ggplot(
    aes(
      flipper_length_mm, 
      body_mass_g, 
      group = cut_interval(flipper_length_mm, n = 4),
      fill = cut_interval(flipper_length_mm, n = 4),
    )
  ) + 
  geom_boxplot(show.legend = FALSE) +
  scale_y_continuous(limits = c(2500, 6500), n.breaks = 20)
```

![](Google_Course_Data_Analysis_with_R_Programmig_files/figure-gfm/unnamed-chunk-58-1.png)<!-- -->

### Introduction to Rmarkdown

You may refer to the following
[Link](https://www.coursera.org/learn/data-analysis-r/supplement/NSC0c/r-markdown-resources)
for further resources.

``` r
add a code block inside the text like this one using insert->code block
```

\\newpage

We may create the table like the one below using table shown in the top
right.

| First Name | Last Name |         Email          |
|:----------:|:---------:|:----------------------:|
|    Aly     |   Kamel   |  aly.kamel@gmail.com   |
|  Mohamed   |  Mustafa  | mo.mustafa@outlook.com |

This is a trial table

-   We may choose different \\textcolor{green}{colors} for our text. by
    writing the \\textcolor{red}{desired color names}.

-   To add a superscript add ^ before and after the super scripted text
    (x<sup>2</sup>)

-   To create an equation:
    *C**i**r**c**l**e**A**r**e**a* = *π* \* *r*<sup>2</sup>

-   Another method to create an equation is to choose display math from
    insert drop down list.
    *A* = *π* \* *r*<sup>2</sup>

------------------------------------------------------------------------

To add a horizontal ruler before or after a text just type (\*\*\*)

------------------------------------------------------------------------

> You may add a quote inside the text also by selecting the block quote
> symbol above.

\\newpage

An image can simply be inserted using the image symbol above

<figure>
<img src="penguins_2.png" title="image_1" style="width:6in;height:8in"
alt="you may also add a caption to the image here" />
<figcaption aria-hidden="true">you may also add a caption to the image
here</figcaption>
</figure>

\\newpage

*You may create the below dashed line using (—) multiple times*

------------------------------------------------------------------------

below are the main six types of fonts in the markdown files. you can
choose any one of them either from the drop down list at the top right
or using (ctrl + alt + (0:6))

# Heading_1

## Heading_2

### Heading_3

#### Heading_4

Normal Text

##### Heading_5

###### Heading_6

------------------------------------------------------------------------

We may add definitions in our rmd files from the insert drop down list
above

RMD file  
R Markdown is a file format for making dynamic documents with R. An R
Markdown document is written in markdown (an easy-to-write plain text
format) and contains chunks of embedded R code.

-   Place code inline with a single back ticks. The first back tick must
    be followed by an R, like this This is an inline code outlet . Note
    that in this case, only the code outlet will be displayed.

-   To write sub_items just enter the plus sign and space.

1.  Item_1

    -   sub_item

        -   sub_sub_item
