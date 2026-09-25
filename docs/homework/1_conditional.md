# Homework 1: Boolean Expressions and Conditional Statements

## Due Sunday 10/3/26

## Description: 

This homework is centered on understanding boolean expressions + operators and using them in conditional statements. The first section is meant to test your ability to convert real life situations into relational and logical operators into boolean expressions. The second will have you create programs that require you to create programs utilizing boolean expressions within if-else statements. 


## How to Hand In

- Follow instructions to produce the following files:
```
/
└── CS108-HW1-Lastname/
    ├── answers.txt/.png/.pdf/any file type that you can store text on
    ├── gpa_calculator_v2.c
    ├── triangle_valid.c
    └── atm_machine.c
```
	
- With all of the above files in a folder, zip it and name it:
	-  CS108-HW0-Lastname.zip
	- Replace "LastName" with your last name
- Submit the zip file to Brightspace

## Section 1: Conditional Statements

Convert each of the following real-world scenarios into a boolean expression that could be used in an `if` statement. You can answer on paper, type them out, take a picture, whatever works for you.

**Example:** "Someone can vote if they are 18 or older"  
**Answer:** `age >= 18`

1. A student gets to leave class early if they have finished all their assignments AND their grade is above a 90.
2. You can go to an R-rated movie only if you are 17 or older, or if you have a parent with you.
3. A bank account is in overdraft if the balance goes below zero.
4. An online purchase can be processed if the credit card is valid AND the billing address matches the shipping address.
5. A password is strong if it has at least 8 characters AND contains both letters and numbers.
6. You're eligible for a scholarship if your GPA is 3.5 or higher AND your family income is below $75,000.
7. A temperature is comfortable if it's between 68°F and 75°F (inclusive on both ends).
8. A student passes the class if they score 60 or higher on the final exam OR they have an average of 70 or higher on all assignments.
9. A video game is age-appropriate for your little cousin if it's rated E for Everyone OR if it's rated T for Teen and they're at least 13 years old.
10. A person can withdraw money from an ATM if they have enough balance to cover the withdrawal AND their daily withdrawal limit hasn't been exceeded.

## Section 2: Conditional Programs

For each of the programs below store each as an individual file with the named indicated in the "How to Hand in" section of this page. 

**IMPORTANT**

I will be doing EXACTLY what the user prompts will ask of my at every step. This means the format of user input must be explicitly stated by the program before taking the input in. Any ambiguity will result in me possibly breaking the program and getting some points off. ENSURE YOU ARE TELLING THE USER THE EXACT THINGS THAT ARE ACCEPTABLE AS INPUT.

### Program 1: GPA Calculator 2.0

Take your `gpa_calculator.c` from HW0 and improve it. Your program should now include a letter grade output using the grading scale from the syllabus.

**Your program should:**

- Calculate the average of four grade inputs (0-100 scale)
- Convert each grade to the 0.0-4.0 scale
- Convert the average to a letter grade (A, B, C, D, F - no +/- signs)
- Display all three formats of the final grade:
    - 0-100 scale average
    - 0.0-4.0 scale average
    - Letter grade

**Grading criteria:** Does it correctly convert grades, calculate averages, and display all three output formats?

### Program 2: Triangle Validation 

Create a program that determines if three given side lengths can form a valid triangle using the triangle inequality theorem (the sum of any two sides must be greater than the third side).

**Your program should:**

- Ask the user for three side lengths
- Check if those sides form a valid triangle
- If valid, ask if they want to:
    - `A` - Calculate the area (using Heron's formula)
    - `P` - Calculate the perimeter
    - End program if it is not one of the above
- If invalid, let the user know and exit

**Grading criteria:** Does it correctly validate triangles? Do the area and perimeter calculations work? Does the menu system work as intended?

### Program 3: ATM Program

Create a simple ATM program that simulates basic banking transactions.

**Your program should:**

- Prompt the user for a PIN and compare it to a correct PIN (hardcode a PIN like 1234)
- If the PIN is wrong, reject access
- If correct, show a menu:
    - `B` - Check balance
    - `D` - Deposit money
    - `W` - Withdraw money
- **Balance check:** Display the current balance and exit
- **Deposit:** Ask for an amount, add it to the starting balance (start with $1000), and display the new balance
- **Withdrawal:** Ask for an amount, check if there's enough money, reject if not, or show the new balance if there is

**Grading criteria:** Does PIN verification work? Do all three transactions function correctly? Does the withdrawal properly check for sufficient funds?


## Grade Breakdown

| Component                                               | Points  |
| ------------------------------------------------------- | ------- |
| Section 1: Boolean Expression Conversions (10 problems) | 25      |
| Program 1: GPA Calculator v2                            | 20      |
| Program 2: Triangle Validator                           | 20      |
| Program 3: ATM Machine                                  | 20      |
| Correct file/folder naming & zip submission             | 15      |
| **Total**                                               | **100** |
