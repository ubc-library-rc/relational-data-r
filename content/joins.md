---
layout: default
title: Joins
nav_order: 6
parent: Workshop Content
has_toc: false
---

# **Joins**
Combining two data frames seems easy if the rows are perfectly aligned, as shown in the first figure. However, the order of the rows in two data frames is usually messy in reality, as shown in the second figure. That's where keys come into place. This section introduces how to join two data frames based on the identified keys.
![](https://www.r4epi.com/img/05_part_data_management/08_multiple_data_frames/one_to_one_emr.png)
<p align="center">
<img src="https://www.r4epi.com/img/05_part_data_management/08_multiple_data_frames/one_to_one.png" width="600" />
</p>
*Source: Brad Cannell, [R for Epidemiology](https://www.r4epi.com/working-with-multiple-data-frames.html#relationship-types)*


## Mutating join
A mutating join allows you to combine variables from two tables. It first matches observations by their keys, then copies across variables from one table to the other. There are four basic types of mutating joins.
* **Inner join** keeps only observations that appear in both data frames..
* Outer join
  * **full join** keeps all observations from either of the two data frames.  
  * **left join** keeps all observations from the left data frame.
  * **right join** keeps all observations from the right data frame.

<p align="center">
<img src="https://r4ds.hadley.nz/diagrams/join/venn.png" width="400" />  
</p>  

<img src="https://r4ds.hadley.nz/diagrams/join/inner.png" width="350" />    <img src="https://r4ds.hadley.nz/diagrams/join/left.png" width="350" />  

<img src="https://r4ds.hadley.nz/diagrams/join/full.png" width="350" />    <img src="https://r4ds.hadley.nz/diagrams/join/right.png" width="350" />   
*Source: Hadley Wickham & Garrett Grolemund, [R for Data Science (2e)](https://r4ds.hadley.nz/joins.html#how-do-joins-work)*

### R execution

Input
{: .label .label-green}
```r
x <- tribble(
  ~key, ~val_x,
     1, "x1",
     2, "x2",
     3, "x3")
y <- tribble(
  ~key, ~val_y,
     1, "y1",
     2, "y2",
     4, "y3")
# A tribble is used for creating a row-wise, readable tibble in R, which is useful for creating small tables of data. A tibble is a new modern data frame, which keeps important features of a data frame and removes outdated features.

x
y

x %>%
  inner_join(y, by = "key")

x %>%
  full_join(y, by = "key")

x %>%
  left_join(y, by = "key")

x %>%
  right_join(y, by = "key")
```

Output
{: .label .label-yellow}
```r
> x %>%
+     inner_join(y, by = "key")
# A tibble: 2 × 3
    key val_x val_y
  <dbl> <chr> <chr>
1     1 x1    y1   
2     2 x2    y2   
>
> x %>%
+     full_join(y, by = "key")
# A tibble: 4 × 3
    key val_x val_y
  <dbl> <chr> <chr>
1     1 x1    y1   
2     2 x2    y2   
3     3 x3    NA   
4     4 NA    y3   
>
> x %>%
+     left_join(y, by = "key")
# A tibble: 3 × 3
    key val_x val_y
  <dbl> <chr> <chr>
1     1 x1    y1   
2     2 x2    y2   
3     3 x3    NA   
>
> x %>%
+     right_join(y, by = "key")
# A tibble: 3 × 3
    key val_x val_y
  <dbl> <chr> <chr>
1     1 x1    y1   
2     2 x2    y2   
3     4 NA    y3   
```

### [Practice](https://r4ds.had.co.nz/relational-data.html#exercises-30)
What weather conditions make it more likely to see a delay?

Step 1
{: .label .label-step}
Join the `weather` and `flights` data frames. What type of join to use? What is the key?

Input
{: .label .label-green}
```r
weather_flights <- weather %>%
  ?_join(flights, by = "")
```

Step 2
{: .label .label-step}
Select the necessary variables, weather conditions from `temp` to `visib` and `dep_delay`.

Input
{: .label .label-green}
```r
use_weather_flights <- weather_flights %>%
  select()
```

Step 3
{: .label .label-step}
Visualize the relationship between each weather condition and departure delay.

Input
{: .label .label-green}
```r
use_weather_flights %>%
  group_by() %>%
  summarise(delay = mean(dep_delay, na.rm = TRUE)) %>%
  ggplot(aes(x = ?, y = delay)) +
  geom_line() + geom_point()
```


## Filtering join
A filtering join filters observations from one data frame based on whether or not they match an observation in another. There are two basic types of filtering joins.
* **Semi join** keeps all rows from a data frame that have a match in the other.
* **Anti join** drops all rows from a data frame that have a match in the other.
<img src="https://r4ds.hadley.nz/diagrams/join/semi.png" width="350" />    <img src="https://r4ds.hadley.nz/diagrams/join/anti.png" width="350" />  
*Source: Hadley Wickham & Garrett Grolemund, [R for Data Science (2e)](https://r4ds.hadley.nz/joins.html#sec-non-equi-joins)*

### [Practice](https://r4ds.had.co.nz/relational-data.html#exercises-31)
Find the 48 hours (over the course of the whole year) that have the worst departure delays. Cross-reference it with the weather data. Can you see any patterns?

Step 1
{: .label .label-step}
To find the 48 hours with the worst departure delays, group flights by hour of scheduled departure time and calculate the average delay, arrange by delay, and select the 48 observations (hours) with the highest average delay.

Input
{: .label .label-green}
```r
worst_hours <- flights %>%
  mutate(hour = sched_dep_time %/% 100) %>%
  group_by(origin, year, month, day, hour) %>%
  summarise(dep_delay = mean(dep_delay, na.rm = TRUE)) %>%
  ungroup() %>%
  arrange(desc(dep_delay)) %>%
  slice(1:48)
```

Step 2
{: .label .label-step}
To get the weather for these hours, choose a type of filtering joins.

Input
{: .label .label-green}
```r
weather_most_delayed <- ?_join(weather, worst_hours,
                               by = c("origin", "year", "month", "day", "hour"))
```

Step 3
{: .label .label-step}
To get the weather for hours except for those hours, choose a type of filtering joins.

Input
{: .label .label-green}
```r
weather_most_delayed <- ?_join(weather, worst_hours,
                               by = c("origin", "year", "month", "day", "hour"))
```

Step 4
{: .label .label-step}
Compare the average weather conditions in the most and less delayed hours.

Input
{: .label .label-green}
```r
weather_less_delayed <- weather_less_delayed %>%
  mutate(most_delayed = 'no')

weather_most_delayed %>%
  mutate(most_delayed = 'yes') %>%
  rows_append(weather_less_delayed) %>%
  group_by(most_delayed) %>%
  summarise(temp = mean(temp, na.rm = TRUE),
            dewp = mean(dewp, na.rm = TRUE),
            humid = mean(humid, na.rm = TRUE),
            wind_speed = mean(wind_speed, na.rm = TRUE),
            precip = mean(precip, na.rm = TRUE),
            visib = mean(visib, na.rm = TRUE))
```
