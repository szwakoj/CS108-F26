# Homework 0: Hello CS108!

## Due Sunday 9/18/26

## Description:

Welcome to CS 108! This HW will be verifying that you have installed the compiler correctly as well as some questions based off our introduction lessons on history and the basics of hardware/software. For the questions in the second section, you will be answering using your program to print the answers to the screen as your "helloworld" program. 

## How to Hand In

- Follow instructions to produce the following files:
```
/
└── CS108-HW0-Lastname/
    ├── install_proof.png
    ├── hello_questions.c
    └── gpa_calculator.c
```
	
- With all of the above files in a folder, zip it and name it:
	-  CS108-HW0-Lastname.zip
	- Replace "LastName" with your last name
- Submit the zip file to Brightspace

# Section 1: Environment Setup

1. Follow the instructions within the [Software Install tab](./gcc_install.md) to install the GCC compiler on your system. 

2. After installing, test your environment by compiling a simple "hello world" program with your own custom message. Use the below as a starting off point, however your message must be unique and not the same thing as below nor any iteration of "hello world". Make the computer say something you want it to say.
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
and running:
```
For windows:
your_program.exe

For Linux/MacOS:
./your_program
```

## Section 2: Printf Answers

For the questions below, you are to answer them using a program using `printf` statements in the proper order and using the proper format specifiers when applicable. Each format specifier can be found in the `printf` reference page ([link](https://cplusplus.com/reference/cstdio/printf/)) or the W3 schools reference page on `stdio.h` ([link](https://www.w3schools.com/c/c_ref_stdio.php)). For example, if the answer to a question is a year, do something like this: `printf("Answer to Q3: %d", 1990);`. If the answer is just text, you do not need to use a format specifier, unless otherwise stated. 

The answers are based off of the lessons in class, as well as your ability to find answers. For any questions with mathematical equations, you must translate them into mathematical statements in C and print the answers using format specifiers. 

1. What is the earliest definition of a computer and about what year was it recorded?
2. Explain Moore's law, but in reverse, explaining the general trend of the number of transistors on microchips going backwards in time. Express the rate as a floating point number.
3. $${{(3 + 4)}\over{17 \times 9}} - 57$$
## Section 3: GPA Calculator

Using the basic I/O functions, arithmetic operators, and variables you are to make GPA calculator that will convert the percentage grades of four classes into a 0.0-4.0 scaled grade point average. This program will require you to use `scanf()` in order to input numbers into your program. 

Write a C program that:

1. Greets the user and prompts them to enter in their class grades.
2. Allows the user to input four classes' grades on a 0.0-100.0 scale and stores them within the program.
	- Store values as `double`
3. Converts each grade into a 0.0-4.0 scale using arithmetic operators.
	- Use a simple conversion method, like dividing by `25.0`.
4. Calculates the average grade from the converted values.
5. Displays each classes converted grade and the overall average of all the class grades in the terminal.
	- The displayed grades should only have two decimal places, utilizing the `%.2lf` format specifier.

Note:
You do not need to check user inputs are valid, assume an ideal user, ie one that listens to your program's instructions exactly. So, make good instructions.


## Grade Breakdown

|Component|Points|
|---|---|
|Section 1: Installation screenshot|20|
|Section 2: Printf Answers (Q1–Q3)|30|
|Section 3: GPA Calculator|40|
|Correct file/folder naming & zip submission|10|
|**Total**|**100**|

