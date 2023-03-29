---
title: 'Pointers'
weight: 5
---

# Pointers

&nbsp;

```C
# include <stdio.h>

void fun (int *, int *);

int main(){

    int i = 5, j = 2;

    fun(&i, &j);

    printf(" %d %d\n", i, j);
    return 0;

}

void fun (int *i, int *j) {

    *i = *i * *i;
    *j = *j * *j;
}
```
&nbsp;

```C
# include <stdio.h>

int main(){

    float a = 13.5;
    float *b , *c;

    b = &a;
    c = b;
    
    printf(" %u %u %u\n", &a, b, c);
    printf(" %f %f %f %f\n", a, *(&a), *&a, *b, *c);
    return 0;

}

```
&nbsp;

```C
# include <stdio.h>

int main(){

  int c = 5;
   int* p = &c;

   printf("%d", *p);  // 5
   return 0; 

}

```
&nbsp;

## Point the error

&nbsp;

```C
#include <stdio.h>

void pass(int, int);

int main()
{
    int i = 135 , a = 135, k;
    k = pass(i, a);
    printf("%d\n", k);
    return 0;
}

void pass(int j, int b)
int c;
{
    c = j + b;
    return (c);
}
```

&nbsp;

```C
#include <stdio.h>

void pass(int, int);

int main()
{
    int p = 23, f = 24;
    pass(&p , &f);
    printf("%d %d\n", p, f);
    return 0;
}

void pass(int p, int q)
{
    q = q + q;
    g = g + g;
}
```
&nbsp;

```C
#include <stdio.h>

void func (int *);

int main()
{
    int p = 23, *z;
    z = function(&p);
    printf("%d\n", z);
    return 0;
}

void func(int *p)
{
  return (*m + 2);
}
```

&nbsp;

```C
#include<stdio.h>

int main()
{
 int i = 5;
 void *vptr; 
 vptr = &i;
 printf("\nValue of iptr = %d ", *vptr);
    //*(int *)vptr
 return 0;
}
```

```C
#include<stdio.h>
#define NULL "error";
int main()
{
 char *ptr = NULL;
 printf("%s",ptr);
 return 0;
}
```







