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
### practise 1
>Write a program that uses one printf() call to print your first name and last name on one line uses a second printf() call to print your first and last names on two separate lines,and uses a pair of printf() calls tos print your first and last names on one line.The output should look like this (but using your name):
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

### practise 2
>Write a program to print your name and address.

```
#include<stdio.h>

int main(void){
        printf("My name is %s，and my address is %s\n","pythonbug","luduo");
        return 0;
}
```

### practise 3
>Write a program that converts your age in years to days and displays both values.At this point ,don't worry about fractional years and leap years.

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

### practise 4
>Write a program that produces the following output:
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

### practise 5
>Write a program that produces the following output:
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

### practise 6
>Write a program that creates an integer variable called toes.Have the program set toes to 10.Also have the program calculate what twice toes is and what toes squared is.The program should print all three values.identifying them.

```
#include<stdio.h>

int main(void){
        int toes,toes_twice,toes_squared;

        toes = 10;
        toes_twice = toes*2;
        toes_squared = toes*toes;

        printf("toes: %d\n",toes);
        printf("toes_twice: %d\n",toes_twice);
        printf("toes_squared: %d\n",toes_squared);

        return 0;
}
```

### practise 7
>Many studies suggest that smiling has benefits,Write a program that produces the following output:
Smile!Smile!Smile!
Smile!Smile!
Smile!
Have the program define a function that displays the string Smile! once,and have the program use the function as often as needed.

```
#include<stdio.h>

void smile(void);

int main(void){
        smile();
        smile();
        smile();
        printf("\n");
        smile();
        smile();
        printf("\n");
        smile();
        printf("\n");

        return 0;
}

void smile(void){
        printf("Smile!");
}
```

### practise 8
>In C,one function can call another.Write a program that calls a function named one_three().This function should display the word one on one line,call a second function named two(),and then display the word three on one line.The function two() should display the word two on one line.The main() function should display the phrase starting now: nefore calling one_three() and display done!after calling it.Thus,the output should look like the following:
starting now:
one
two
three
done!

```
#include<stdio.h>

void one_three(void);
void two(void);

int main(void){
        printf("starting now:\n");
        one_three();
        printf("done!\n");
        return 0;
}

void one_three(void){
        printf("one\n");
        two();
        printf("three\n");
}

void two(void){
        printf("two\n");

}
```