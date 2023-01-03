---
layout: default
title: Joins
nav_order: 5
parent: Workshop Content
has_toc: false
---

# **Joins**
Combining two data frames seems easy if the rows are perfectly aligned, as shown in the first figure. However, the order of the rows in two data frames is usually messy in reality, as shown in the second figure. That's where keys come into place. This section introduces how to join two data frames based on the identified keys.
![](https://www.r4epi.com/img/05_part_data_management/08_multiple_data_frames/one_to_one_emr.png)
![](https://www.r4epi.com/img/05_part_data_management/08_multiple_data_frames/one_to_one.png)
*Source: Brad Cannell, [R for Epidemiology](https://www.r4epi.com/working-with-multiple-data-frames.html#relationship-types)*


## Mutating join
A mutating join allows you to combine variables from two tables. It first matches observations by their keys, then copies across variables from one table to the other. There are four basic types of mutating joins.
* **Inner join** keeps only observations that appear in both data frames..
* Outer join
  * **left join** keeps all observations from the left data frame.
  * **right join** keeps all observations from the right data frame.
  * **full join** keeps all observations from either of the two data frames.

![venn](https://r4ds.hadley.nz/diagrams/join/venn.png)

![inner join](https://r4ds.hadley.nz/diagrams/join/inner.png)
![left join](https://r4ds.hadley.nz/diagrams/join/left.png)  
![right join](https://r4ds.hadley.nz/diagrams/join/right.png)  
![full join](https://r4ds.hadley.nz/diagrams/join/full.png)  
*Source: Hadley Wickham & Garrett Grolemund, [R for Data Science (2e)](https://r4ds.hadley.nz/joins.html#how-do-joins-work)*

## Filtering join
A filtering join filters observations from one data frame based on whether or not they match an observation in another. There are two basic types of filtering joins.
* **Semi join** keeps all rows from a data frame that have a match in the other.
* **Anti join** drops all rows from a data frame that have a match in the other.
![semi join](https://r4ds.hadley.nz/diagrams/join/semi.png)
![anti join](https://r4ds.hadley.nz/diagrams/join/anti.png)
*Source: Hadley Wickham & Garrett Grolemund, [R for Data Science (2e)](https://r4ds.hadley.nz/joins.html#sec-non-equi-joins)*

Up to now, you are expected to know how joins work conceptually. If that's true, we will move on to the R markdown file to work on some examples.
{: .note}
