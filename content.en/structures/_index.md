---
title: 'Structures'
weight: 8
---

# Structures

## Y you need structure

Store in variable like 
 - int a = 5;

What if we need to store value of 60 students ?? Arrays...

- int a[60] --> stores 60 int values.
 - Colection of homogenous data item.

What if we need to store Info of a student or 60 students ... 
- rollno - int    
- name - string
- marks - float

for st1 == we need 3 variables, for st2 == we need 3 variables.
Not feasible

Primitive Datatypes - int char float double
Derived == array

USER DEFINED DATATYPE == Structure -- that holds or uses primitive datatypes.

## Declare a struct

### struct Student { ... };

## Assigning Variable 

### struct Student s1; 
- s1 object of the structure.. (calculate the mem allocated) 

### Initializtion & Accessing of Structure

- struct Student s = {1, "Hari", 75.00}
OR
- s = {1}
OR
- In struct definition itself

- printf("%d", s.rollno);

- s1 = s2, possible

- s1 > s2  - not possible

## What if for 60 students.....

## Array of Structure

- struct Student s[60]; eg : s[3]

- s[0].rollno;
- s[1].name;

## Add values in array

- for loop

## Structure Pointer

- holds addr of the memory block that stores the structure.

ptr -> rollno;

## Union

## struct using typedef




