---
layout: default
title: Keys
nav_order: 5
parent: Workshop Content
has_toc: false
---

# **Keys**

As mentioned in the previous section, combining two data frames requires at least a key variable shared by those data frames.
* If a key variable or set of variables uniquely identifies each observation/row in a data frame, it is called the **primary key** of that data frame.
* If a key variable or set of variables in a data frame uniquely identifies each observation/row in another data frame, it is called a **foreign key** in the current data frame.

For example, in the following relationship diagram,   
![Student Course Enrollment](https://www.databasestar.com/wp-content/uploads/2019/07/Physical.png)  
*Source: Ben Brumm, [A Guide to the Entity Relationship Diagram (ERD)](https://www.databasestar.com/entity-relationship-diagram/)*
* `student_id` is the primary key (PK) in the data frame named `student`, because each `student_id` should be able to identify one and only one student.   
* `course_id` is the PK in the data frame named `course`. Each `course_id` should correspond to one and only one course (not exactly like the system at UBC).  
* The `course_enrollment`data frame can connect to the other two data frames because it has the two variables `student_id` and `course_id`. And that's why those two variables are marked as the foreign key (FK) in the `course_enrollment` data frame.

Such a diagram would be excellent when we come across a new set of data frames, but it is not always available. We can identify the primary key by making sense of the data frame or examining whether a variable can uniquely identify each row.  
If you do not have questions, we will now switch to the R markdown file to walk through an example of identifying primary and keys, and have some exercises.
{: .note}
