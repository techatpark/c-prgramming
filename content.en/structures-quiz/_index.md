---
title: 'Structures Quiz'
weight: 9
---

# Structures Quiz

&nbsp;

```C
#include<stdio.h>
int main()
{
	struct simp 
	{
		int i = 6;
		char city[] = "chennai";
	};
	struct simp s1;
	printf("%d",s1.city);
	printf("%d", s1.i);
	return 0;
}
```
&nbsp;

```C
#include<stdio.h>
int main()
{
	struct leader
	{
	char *lead;
	int born;
	};
	struct leader l1 = {"AbdulKalam", 1931};
	struct leader l2 = l1;
	printf("%s %d", l2.lead, l1.born);
}

```
&nbsp;

```C
//assume int as 2 bytes.
#include<stdio.h>
int main()
{
	struct employee 
	{
		int empid[5];
		int salary;
		employee *s;
	}emp;
printf("%d %d", sizeof(employee), sizeof(emp.empid));
return 0;
}

```
&nbsp;


&nbsp;

```C
#include<stdio.h>
struct TeamScore
{
	int wickets;
	int score;
}ts = {2, 325};
struct country
{
	char *name;
}coun = {"India"};
int main()
{
	struct TeamScore tcon = ts;
	printf("%d %s %d", tcon.score, ts.wickets, coun.name);
	return 0;
}
```

&nbsp;

```C
#include<stdio.h>
int main()
{
	struct zoho
	{
		int employees;
		char comp[5];

		struct founder
		{
			char ceo[10];
		}p;
	};
	struct zoho zs = {4000, "zoho", "sridhar"};
	printf("%d %s %s", zs.comp, zs.employees, zs.p.ceo);
	return 0;
}
```
&nbsp;

```C
 #include<stdio.h>
int main()
{
	struct play
	{
		char name[10];
		int playnum;
	};
	struct play p1 = {"virat", 18};
	struct play p2 = p1;
	if(p1 == p2)
	printf("Two structure members are equal");
	return 0;
}
```

&nbsp;

```C
#include<stdio.h>
int main()
{
	enum week{sun = -1, mon, tue, wed, thu = 5, fri, sat};
	printf("%d %d %d %d %d %d %d", sun, mon, tue, wed, thu, fri, sat);
	return 0;
}
```
&nbsp;

```C
#include<stdio.h>
int main()
{
	struct check
	{
	}ck;
	printf("%d", sizeof(ck));
}
```
&nbsp;

```C
#include<stdio.h>
int main()
{
	struct num 
	{
	int i, j, k, l;
	};
	struct num n = {1, 2, 3};
	printf("%d %d %d %d", n.i, n.j, n.k, n.l);
}
```

&nbsp;

```C
#include<stdio.h>
#include<string.h>
struct player 
{
	char pname[20];
}pl;
char* play(struct player *temp_pl)
{
	strcpy(temp_pl->pname, "kohli");
	return temp_pl->pname;
}
int main()
{
	strcpy(pl.pname, "dhoni");
	printf("%s %s", pl.pname, play(&pl));
	return 0;
}
```







