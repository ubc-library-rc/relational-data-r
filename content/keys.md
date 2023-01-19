---
layout: default
title: Keys
nav_order: 5
parent: Workshop Content
has_toc: false
---

# **Keys**

## Primary keys and foreign keys

As mentioned in the previous section, combining two data frames requires at least a key variable shared by those data frames.
* If a key variable or set of variables uniquely identifies each observation/row in a data frame, it is called the **primary key** of that data frame.
* If a key variable or set of variables in a data frame uniquely identifies each observation/row in another data frame, it is called a **foreign key** in the current data frame.

For example, in the following relationship diagram,   
<p align="center">
<img src="https://www.databasestar.com/wp-content/uploads/2019/07/Physical.png" width="1500" />
</p>
*Source: Ben Brumm, [A Guide to the Entity Relationship Diagram (ERD)](https://www.databasestar.com/entity-relationship-diagram/)*
* `student_id` is the primary key (PK) in the data frame named `student`, because each `student_id` should be able to identify one and only one student.   
* `course_id` is the PK in the data frame named `course`. Each `course_id` should correspond to one and only one course (not exactly like the system at UBC).  
* The `course_enrollment`data frame can connect to the other two data frames because it has the two variables `student_id` and `course_id`. And that's why those two variables are marked as the foreign key (FK) in the `course_enrollment` data frame.

Such a diagram would be excellent when we come across a new set of data frames, but it is not always available. We can identify the primary key by making sense of the data frame or examining whether a variable can uniquely identify each row.

## Examining primary keys in R

One way to examine whether a variable can uniquely identify each row is to `count()` by the primary key(s) and look for entries where `n`, i.e., the number of cases associated with each value of the primary key(s), is greater than one. For example, let's say we make a guess that `tailnum` is the primary key for the `planes` data frame, then we can check if any `tailnum` shows up more than once in `planes` by the following code.

Input
{: .label .label-green }
```r
planes %>%
  count(tailnum) %>%
  filter(n > 1)
```

The output shows zero rows, which indicates that each value of `tailnum` only shows up once in the `planes` table. In other words, `tailnum` can serve as the primary key for the `planes` table.

Output
{: .label .label-yellow}
```r
# A tibble: 0 × 2
# … with 2 variables: tailnum <chr>, n <int>
# ℹ Use `colnames()` to see all variable names
```

### Practice
1. Could you identify and examine the primary keys for the other four data frames in the `nycflights13` packages?  
2. Could you find an example of foreign key from those five data frames?

Once you are comfortable identifying keys, the next step is to see how they can help us join multiple data frames.
{: .note}
