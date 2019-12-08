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