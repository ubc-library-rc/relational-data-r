---
layout: default
title: Workshop Content
nav_order: 4
has_children: true
has_toc: false
---

# **Warm-up**

## Coming up with a scenario in which you need to work with multiple datasets
Hints:
<p align="center">
<img src="https://www.r4epi.com/img/05_part_data_management/08_multiple_data_frames/goal.png" width="600" />  
<img src="https://www.r4epi.com/img/05_part_data_management/08_multiple_data_frames/two_data_sets2.png" width="600" />  
</p>
*Source: Brad Cannell, [R for Epidemiology](https://www.r4epi.com/working-with-multiple-data-frames.html#combining-data-frames-horizontally-adding-columns)*

<p align="center">
<img src="https://r4ds.hadley.nz/diagrams/relational.png" width="600" />
</p>
Note. The bolded texts are names of data frames, and the cells below are the variables within the data frame.  
*Source: Garrett Grolemund & Hadley Wickham, [R for Data Science (2e)](https://r4ds.hadley.nz/)*

## Common scenarios
* Combining **data from multiple agencies**  
  *Case 1:* binding World Bank GDP data and the United Nations Development Program gender inequality index (GII) to examine the relationship between gender equality and economic development across countries.   
* Combining **data from multiple units**  
  *Case 2:* binding student performance data from different classes and schools to examine the relationships among individual performance, class, and school level factors such as class size and school funding
* Combining **data from multiple time points**  
  *Case 3:* matching several waves of survey data pre, during and post a six-month group psychotherapy intervention to track the change of depression levels of each individual to evaluate the effectiveness of the intervention  
* Working with **data from relational databases[^1]**  
  *Case 4:* matching flights delay information and airports weather information to identify weather conditions that associated with the severest flight delays  

## A closer look at case 4
Step 1
{: .label .label-step}
Read [R Document](https://rdocumentation.org/packages/nycflights13/versions/1.0.1)
{: .step}

Step 2
{: .label .label-step}
Check each dataset in R Studio
{: .step}

Input
{: .label .label-green }
```r
# Install the required packages if not yet installed
if (!require(tidyverse)) install.packages('tidyverse')
if (!require(nycflights13)) install.packages('nycflights13')
# Load the packages to the current session
library(tidyverse)
library(nycflights13)
# Check the flights data set
?flights
glimpse(flights)
View(flights)
```

Output
{: .label .label-yellow }
```r
> glimpse(flights)
Rows: 336,776
Columns: 19
$ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 201…
$ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
$ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
$ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, 558, 558, 558,…
$ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, 600, 600, 600,…
$ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1, 0, -1, 0, 0,…
$ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849, 853, 924, 923…
$ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851, 856, 917, 937…
$ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -14, 31, -4, -8,…
$ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "AA", "B6", "B6…
$ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 49, 71, 194, 11…
$ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N39463", "N516JB",…
$ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA", "JFK", "LGA",…
$ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD", "MCO", "ORD",…
$ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 158, 345, 361, …
$ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, 1028, 1005, 24…
$ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6, 6, 6, 6, 6, …
$ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0, 0, 0, 0, 10,…
$ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-…
```

### Practice
1. Check the other four data sets: `weather`, `airplanes`, `airports`, `airlines`.
2. Why don't we put all the information in a data frame? What are the benefits of creating multiple data frames? Could you imagine what an overall combined data frame would look like?

Hint
{: .label .label-green }
```r
# You can get the combined data frame by running this chunk of code.  
# No worries if it looks unfamiliar. You will know them well by the end of this workshop.
OverallCombinedDat <- flights |>
  full_join(weather, by = c('time_hour', 'origin')) |>
  full_join(airports, by = c("origin" = "faa")) |>
  full_join(airports, by = c("dest" = "faa"), suffix = c(".origin", ".dest")) |>
  full_join(planes, by = "tailnum") |>
  full_join(airlines, by = "carrier")
View(OverallCombinedDat)
```

Up to now, you are assumed to get a sense of the need to work with multiple data frames.  
Reasons include   
1) data being collected separately from multiple agencies, units and time points,   
2) data being kept/stored separately because a huge combined data frame creates redundancy, takes up more memory, slows analysis speed, is less secure and harder to manage.
{: .note}

The data frames must have at least one variable in common so that they can be combined. Check if this rule applies to the scenarios you come up with.  
The variable(s) two tables have in common that helps them relate to each other is known as keys. Now that we have developed an intuitive sense of keys, we will move on to the next section of identifying keys.
{: .note}

[^1]: Relational_Database: If this term means nothing to you, you probably don't need to know it. For this workshop, you can think of it as a place where someone has put together multiple data frames that can be related for you. If you are highly interested, you may check the [Wikipedia page](https://en.wikipedia.org/wiki/Relational_database).
