---
layout: post
title:  "C Primer plus课后编程题"
date:   2019-12-08 23:33
categories: C
tags: C 课后练习
excerpt: 知识点记录
author: Pythonbug
mathjax: true
---
>1. Write a program that uses one printf() call to print your first name and last name on one line uses a second printf() call to print your first and last names on two separate lines,and uses a pair of printf() calls tos print your first and last names on one line.The output should look like this (but using your name):
Gustav Mahler <-- First print statement
Gustav        <-- Second print statement
Mahler        <-- Still the second print statement
Gustav Mahler <-- Third and fourth print statement

```
#include<stdio.h>

int main(void){
        printf("python bug\n");
        printf("python\nbug\n");
        printf("python");
        printf(" bug\n");
        return 0;

}

```

>2. Write a program to print your name and address.

```
#include<stdio.h>

int main(void){
        printf("My name is %s，and my address is %s\n","pythonbug","luduo");
        return 0;
}
```

>3. Write a program that converts your age in years to days and displays both values.At this point ,don't worry about fractional years and leap years.

```
#include<stdio.h>

int main(void){
        int age_years,age_days;

        age_years = 28;
        age_days = age_years * 365;

        printf("years: %d,days: %d\n",age_years,age_days);

        return 0;
}
```

>4. Write a program that produces the following output:
For he's a jolly good fellow:
For he's a jolly good fellow:
For he's a jolly good fellow:
Which nobody can deny:
Have the program use two user-defined functions in addition to mian():one named jolly() that prints the "jolly good" message once,and one named deny() that prints the final once.

```
#include<stdio.h>

void jolly(void);
void deny(void);

int main(void){
        jolly();
        jolly();
        jolly();
        deny();

        return 0;
}

void jolly(void){
        printf("For he's a jolly good fellow\n");
}

void deny(void){
        printf("Which nobody can deny\n");
}

```

>5. Write a program that produces the following output:
Brazil,Russia,India,China
India,China
Brazil,Russia
Have the program use two user-defined functions in addition to main(): one named br() that prints "Brazil,Russia" once,abd one named ic() that prints "India,China" once,Let main() take care of any additional printing tasks.
```
#include<stdio.h>

void br(void);
void ic(void);

int main(void){
        br();
        ic();
        br();
        printf("\n");
        ic();
        return 0;
}

void br(void){
        printf("Brazil,Russia");
}

void ic(void){
        printf("India,China\n");
}

```