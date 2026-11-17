# Homework 3: Strings

## Due 11/28/26

## Description:

This homework is about strings and will focus on using them in our programs to work with textual data. You will make two different programs, each within their own files.

## How to Hand In

- Follow instructions to produce the following file:
```
/
└── CS108-HW3-Lastname/
	├── date.c
	└── encoder.c
```

- With the file above in a folder, zip it and name it:
	- CS108-HW3-Lastname.zip
	- Replace "Lastname" with your last name
- Submit the zip file to Brightspace

## Section 1: `date.c`

This program will validate whether a date entered by the user is valid or not. This means the formatting must make sense, and the date must be a **real date on the calendar**. You will check these two things separately, and the program must tell the user which one failed.

### Input Format

Prompt the user to enter a date in one of these two formats:

```
MM/DD/YYYY
MM-DD-YYYY
```

- `MM` is a two-digit month, `DD` is a two-digit day, and `YYYY` is a four-digit year.
- The separator is either `/` or `-`.
- The **same separator must be used in both places**. `12/25-2026` is not valid.
- Single digit months and days must have a leading zero. `1/5/2026` is not valid, but `01/05/2026` is.
- There must be no spaces or other characters anywhere in the input.
- Years must be between `0001` and `9999`.

### Check 1: Format

Before you look at any numbers, verify the string is shaped correctly. Your program should check that:

- The string is exactly 10 characters long (not counting the newline).
- Characters at index 2 and 5 are separators, they are either both `/` or both `-`.
- Every other character is a digit.

If any of these fail, print `Invalid format` and do not move on to Check 2.

### Check 2: Calendar

Once the format is confirmed, pull out the month, day, and year as integers and check that:

- The month is between 1 and 12.
- The day is at least 1 and no more than the number of days in that month.
- The year is at least 1.

Use this table for the number of days in each month:

|Month|Days|
|---|---|
|01 January|31|
|02 February|28 (29 in a leap year)|
|03 March|31|
|04 April|30|
|05 May|31|
|06 June|30|
|07 July|31|
|08 August|31|
|09 September|30|
|10 October|31|
|11 November|30|
|12 December|31|

If any of these fail, print `Invalid date`.

#### Leap Years

A year is a leap year if:

1. It is divisible by 4, **and**
2. It is **not** divisible by 100, **unless** it is also divisible by 400.

```c
int is_leap_year(int year)
{
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}
```

Examples: 2024 is a leap year. 1900 is not (divisible by 100 but not 400). 2000 is a leap year (divisible by 400). 2026 is not.

You may copy this function into your program. Write it as its own function and use it in your solution.

### Program Flow

- Your program should keep asking for dates until the user types `quit`.
- If the date is valid, print `Valid date`.
- Print a blank line after each result.
- Use `fgets()` to read the input (not `scanf("%s")`) so that inputs containing spaces are handled correctly. Remember to remove the trailing newline.
- Convert the digit characters into integers yourself, either with `sscanf()`, `atoi()`, or by using the character math you learned in class (`'7' - '0'`).

### Required Functions

Your program must include at least these functions (you may add more):

```c
int is_leap_year(int year);
int days_in_month(int month, int year);
int valid_format(char date[]);
```

### Example Run

```
Enter a date as MM/DD/YYYY or MM-DD-YYYY (or type quit to exit): 02/29/2024
Valid date

Enter a date as MM/DD/YYYY or MM-DD-YYYY (or type quit to exit): 02/29/2026
Invalid date

Enter a date as MM/DD/YYYY or MM-DD-YYYY (or type quit to exit): 12-25-2026
Valid date

Enter a date as MM/DD/YYYY or MM-DD-YYYY (or type quit to exit): 12/25-2026
Invalid format

Enter a date as MM/DD/YYYY or MM-DD-YYYY (or type quit to exit): 4/5/2026
Invalid format

Enter a date as MM/DD/YYYY or MM-DD-YYYY (or type quit to exit): 13/01/2026
Invalid date

Enter a date as MM/DD/YYYY or MM-DD-YYYY (or type quit to exit): quit
Goodbye!
```

### Test Your Program

Test with several different inputs, not just the ones shown above. Think about edge cases. A few to get you started:

|Input|Expected|
|---|---|
|`02/29/1900`|Invalid date|
|`02/29/2000`|Valid date|
|`04/31/2026`|Invalid date|
|`00/10/2026`|Invalid date|
|`10/00/2026`|Invalid date|
|`10/10/0000`|Invalid date|
|`10/10/26`|Invalid format|
|`10/1O/2026`|Invalid format (that's a letter O)|
|`10\|10\|2026`|Invalid format|
|(empty line)|Invalid format|

## Section 2: `encoder.c`

This program will compress a string using run-length encoding (RLE). Run-length encoding replaces each group of consecutive identical characters with that character followed by the number of times it repeats.

```
aaabbcddddee  ->  a3b2c1d4e2
```

Notice that a character that appears only once (like the `c` above) still gets a count of `1`.

### Input Format

Prompt the user to enter a string to encode. The input must follow these rules:

- The string must contain **only lowercase letters** (`a` through `z`).
- The string must be **1 to 50 characters long**.
- There must be no spaces, digits, uppercase letters, or other characters anywhere in the input.

Your prompt must tell the user all of the above. Remember that I will be doing EXACTLY what the prompt tells me to do, so be explicit about what is acceptable.

### How Encoding Works

Walk through the string one character at a time, keeping track of the current character and how many times in a row you have seen it:

1. Start with the first character and a count of 1.
2. Look at the next character. If it matches the current one, add 1 to the count.
3. If it does not match, write the current character and its count to the output, then start counting the new character from 1.
4. When you reach the end of the string, remember to write out the final group. This step is easy to forget.

Only consecutive characters are grouped. The same letter appearing in separate places is encoded separately:

```
aabaa  ->  a2b1a2
```

### Counts Above 9

A run can be longer than 9 characters, so its count can have more than one digit. The count is written out in full as a normal number.

```
aaaaaaaaaaaa  ->  a12
```

(That is the letter `a` repeated 12 times.) Since the input is limited to 50 characters, the largest possible count is 50. Be careful here: you cannot simply add `'0' + count` to build the count character when the count is 10 or more. Think about how you can convert a number into its digit characters, or consider using `sprintf()` to write the count into a string.

### Validation

Before encoding, verify the input. If it fails, print an error message and do not encode it. Your program should print a **different message** for each type of failure:

|Problem|Message|
|---|---|
|The line is empty|`Error: Input is empty`|
|More than 50 characters|`Error: Input is too long`|
|Contains any character that is not a lowercase letter|`Error: Input must contain only lowercase letters`|

Check them in the order listed above, and print only the first error that applies.

### Program Flow

- Your program should keep asking for strings until the user types `quit`.
- If the input is valid, print the encoded string using the format shown in the example run.
- Print a blank line after each result.
- Since `quit` is made of lowercase letters, it would otherwise be a valid string. Check for `quit` **before** validating.
- Your program should handle input longer than the buffer without crashing. Make your buffer large enough to detect that an input is too long (for example, 100 characters), instead of making it exactly 51.

### Required Functions

Your program must include at least these functions (you may add more):

```c
int validate_input(char str[]);
void encode(char str[], char result[]);
```

- `validate_input` returns a value indicating which error occurred (or that the input was valid). You decide on the return values, but use them to decide which message to print.
- `encode` takes the original string and fills `result` with the encoded string. Make sure `result` is large enough for the worst case. When every character is different, each character becomes two characters, so the encoded string can be up to double the length of the input. Make sure there is room for the null terminator.

### Example Run

```
Enter a string of 1 to 50 lowercase letters (a-z only, no spaces) or type quit to exit: aaabbcddddee
Encoded: a3b2c1d4e2

Enter a string of 1 to 50 lowercase letters (a-z only, no spaces) or type quit to exit: abc
Encoded: a1b1c1

Enter a string of 1 to 50 lowercase letters (a-z only, no spaces) or type quit to exit: aabaa
Encoded: a2b1a2

Enter a string of 1 to 50 lowercase letters (a-z only, no spaces) or type quit to exit: zzzzzzzzzzzz
Encoded: z12

Enter a string of 1 to 50 lowercase letters (a-z only, no spaces) or type quit to exit: Hello
Error: Input must contain only lowercase letters

Enter a string of 1 to 50 lowercase letters (a-z only, no spaces) or type quit to exit: aab b
Error: Input must contain only lowercase letters

Enter a string of 1 to 50 lowercase letters (a-z only, no spaces) or type quit to exit: 
Error: Input is empty

Enter a string of 1 to 50 lowercase letters (a-z only, no spaces) or type quit to exit: quit
Goodbye!
```

### Test Your Program

Test with several different inputs, not just the ones shown above. Think about edge cases. A few to get you started:

| Input                                                          | Expected                                           |
| -------------------------------------------------------------- | -------------------------------------------------- |
| `a`                                                            | `Encoded: a1`                                      |
| `aa`                                                           | `Encoded: a2`                                      |
| `ab`                                                           | `Encoded: a1b1`                                    |
| `aaaaaaaaaa` (10 a's)                                          | `Encoded: a10`                                     |
| `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa` (50 a's)  | `Encoded: a50`                                     |
| `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa` (51 a's) | `Error: Input is too long`                         |
| `abababab`                                                     | `Encoded: a1b1a1b1a1b1a1b1`                        |
| `aaabbb`                                                       | `Encoded: a3b3`                                    |
| `abc123`                                                       | `Error: Input must contain only lowercase letters` |
| `aaa bbb`                                                      | `Error: Input must contain only lowercase letters` |
| `Quit`                                                         | `Error: Input must contain only lowercase letters` |
| `quitt`                                                        | `Encoded: q1u1i1t2`                                |
| (empty line)                                                   | `Error: Input is empty`                            |

## Grade Breakdown

| Component                                   | Points  |
| ------------------------------------------- | ------- |
| Section 1: Installation screenshot          | 45      |
| Section 2: Printf Answers (Q1–Q3)           | 45      |
| Correct file/folder naming & zip submission | 10      |
| **Total**                                   | **100** |
