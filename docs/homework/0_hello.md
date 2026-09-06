# Homework 0: Hello CS108!

## Due Sunday 9/13/26

## Description:

Welcome to CS 108! This HW will be verifying that you have installed the compiler correctly as well as some questions based off our introduction lessons on history and the basics of hardware/software. For the questions in the second section, you will be answering using your program to print the answers to the screen as your "helloworld" program. 

## How to Hand In

- Follow instructions to produce the following files:
	-  installation.png
	- hello_questions.c
	
- Take all of the above files and put them into a folder, zipping it and naming it:
	-  CS108-HW0-Lastname.zip
	- Replace "LastName" with your last name
- Submit the zip file to Brightspace


# Section 1: Environment Setup

1. Follow the instructions within the [Software Install tab](./gcc_install.md) to install the GCC compiler on your system. 

2. Take a screenshot of the terminal output of you testing the installation by compiling a simple hello world program with your own custom message. Use the below as a starting off point, however your message must be unique and not the same thing as below nor any iteration of "hello world". Make the computer say something you want it to say.
```c
#include<stdio.h>

int main()
{
	printf("Hello CS108!");
	return 0;
}
```

3. Take a screenshot of the terminal after you have compiled and ran your program. Remember compilation is done like this:
```
gcc your_file.c -o your_program
```

## Section 2: Printf Answers

For the questions below, you are to answer them using a program using `printf` statements in the proper order and using the proper format specifiers when applicable. Each format specifier can be found in the `printf` reference page

