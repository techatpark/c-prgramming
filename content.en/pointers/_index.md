---
title: 'Pointers'
weight: 9
---

# Pointers

## Call by Value

Pass 'values' to variables to the called function.

Eg : 
- sum = calcum(a, b, c);
- f = factr (a);


!["How"](how.png)

## Call by Reference

- Variables are stored in memory. 
- Instead of passing the value of variable, **why not** pass the location number or address of that variable.
- That is called call by reference

### Pointer Notation

**int i = 3;**

This declaration tells the C-compiler to :

  - Reserve
  - Associate
  - Store

fig 1.

Here .. 
- the memory location 65524 is the selected location to store the value 3.
- This number cannot be relied on.
- i's address in memory is a number.

```C
#include <studio.h>
int main()
{
    int i = 3;
    printf("Address of i = %u\n", &i);
    printf("Value of i = %d\n", i);
    return 0;
}
```

### Points to note:

- & -> 'address of' operator
- &i -> returns address of variable i
- %u -> format identifier == unsigned integer
- '*' -> 'value at address' operator

```C
#include <studio.h>
int main()
{
    int i = 3;
    printf("Address of i = %u\n", &i);
    printf("Value of i = %d\n", i);
    printf("Value of i = %d\n", *(&i));

    return 0;
}
```
### Points to note:

- *(&i) is same as printing value of i
- &i represents addr of variable i
- j = &i ;
    -  here j is another variable located somewhere in memory
    fig 2

- declaration of j -> int *j; (* stands for value of address)

```C
#include <studio.h>
int main()
{
    int i = 3;
    int *j;

    j = &i;
    printf("Address of i = %u\n", &i); //location of variable i.
    printf("Address of i = %u\n", j); //stored the location of i in variable j.
    printf("Address of j = %u\n", &j); //location of variable j.
    printf("Value of j = %u\n", j); //its holding the addr of i.
    printf("Value of i = %d\n", i);
    printf("Value of i = %d\n", *(&i)); //returns value of some variable stored in that particular location 
    printf("Value of i = %d\n", j); //returns value of some variable stored in that particular location

    return 0;
}
```

### More Declarations

- char *ch; //ch - variable holding addr of a char variable
- float *s; // s - variable holding addr of a float variable

### *j & **k

fig 3

### In general ***Actual arguements cannot be altered***. But it can the achieved through ***Call By Reference***

```C
#include <studio.h>

void areaperi(int, float *, float *);

int main()
{
    int radius;
    float area, perimeter;

    printf("Enter radius");
    scanf("%d", &radius);

    areaperi(radius, &area, &perimeter);

    printf("Area = %f\n", area);
    printf("Perimeter = %f\n", perimeter);
    return 0;
}

void areaperi( int r, float *a, float *p)
{
     *a = 3.14 * r * r;
     *p = 2 * 3.14 * r;

}
```






