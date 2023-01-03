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
![](https://www.r4epi.com/img/05_part_data_management/08_multiple_data_frames/goal.png)
![](https://www.r4epi.com/img/05_part_data_management/08_multiple_data_frames/two_data_sets2.png)
*Source: Brad Cannell, [R for Epidemiology](https://www.r4epi.com/working-with-multiple-data-frames.html#combining-data-frames-horizontally-adding-columns)*
![](https://r4ds.hadley.nz/diagrams/relational.png)
*Source: Garrett Grolemund & Hadley Wickham, [R for Data Science (2e)](https://r4ds.hadley.nz/)*

## Common scenarios
* Combining **data from multiple agencies**  
  *Case 1:* binding GDP data from the World Bank and gender inequality index from the United Nations Development Program to examine the relationship between gender equality and economic development across countries  
* Combining **data from multiple units**  
  *Case 2:* binding student performance data from different classes and schools to examine the relationship between individual performance and class level and school level factors such as class size and school funding  
* Combining **data from multiple time points**  
  *Case 3:* matching several waves of survey data pre, during and post a six-month group psychotherapy intervention to track the change of depression levels of each individual to evaluate the effectiveness of the intervention  
* Working with **data from relational databases[^1]**  
  *Case 4:* matching flights delay information and airports weather information to identify weather conditions that associated with the severest flight delays  

Up to now, you are assumed to get a sense of why would there be a need to work with multiple data frames.  
Reasons include 1) data being collected separately, 2) data being kept/stored separately because a huge combined data frame takes up more memory, slows analysis speed, is less secure and harder to manage.
{: .note}

* The data frames must have at least one variable in common so that they can be combined. Check if this rule applies to the scenarios you come up with and the cases listed above.  
* The variable(s) two tables have in common that helps them relate to each other is known as keys. If you do not have questions, we will now move on to the next section of identifying keys.
{: .note}

[^1]: Relational_Database: If this term means nothing to you, you probably don't need to know it. For this workshop, you can think of it as a place where someone has put together multiple data frames that can be related for you. If you are highly interested, you may check the [Wikipedia page](https://en.wikipedia.org/wiki/Relational_database).
