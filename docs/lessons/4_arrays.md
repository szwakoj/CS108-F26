# Arrays

Up until now, we have been dealing with singular value variables. This meant that if we wanted to represent a collection of numbers we had to make a variable for each, leading to some boring programs. Arrays are lists of numbers/datatypes that can store multiple values under a single variable. 
## Basic Array

```c
int int_array[5] = {0, 10, 20, 30, 40};
char char_array[3] = {'A', 'B', 'C'};
float float_array[4] = {3.141, 2.718, 1.618, 1.414};
```

Arrays are collections of numbers that allow us to store multiple values under a single variable. They are declared as indicated above, with the general form looking like this:

```c
array_element_type array_name[array_size] = {array, initial, elements};
```

Like the primary datatypes, arrays can be initialized as empty, if one were to omit the "= {}". If you do initialize it with values or fill it later with values, **elements of the array must be of the same datatype.** 

You access elements of the array using square brackets; array\[index\]. Array indexes start at 0, meaning an array with 5 elements has elements 0-4:

```c
int int_array[5] = {0, 10, 20, 30, 40};

printf("%d", int_array[0]);
// Prints 0
printf("%d", int_array[1]);
// Prints 1
printf("%d", int_array[2]);
// Prints 2
printf("%d", int_array[3]);
// Prints 3
printf("%d", int_array[4]);
// Prints 4
```

You can also modify the array elements in the same way:

```c
int int_array[5] = {0, 10, 20, 30, 40};

printf("%d", int_array[0]);
// Prints 0

int_array[0] = 100;

printf("%d", int_array[0]);
// Prints 100
```

 And do user input the same as well:
 
```c
int int_array[5] = {0, 10, 20, 30, 40};

scanf("%d", &int_array[0]);

printf("%d", int_array[0]);
// Prints user input number
```

You may be seeing the natural connection between arrays and loops already. Loops are the only way to do repeated operations on all elements of an array.

```c
int high_scores[3] = {23500, 22990, 22000};

for(int i = 0; i < 3; i ++){
	printf("%d", high_scores[i]);
}
```

You must access each element at some point in order to apply the operation. You cannot do something like:

```c
// ILLEGAL! CANNOT DO!
int array_a[3] = {1, 2, 3};
int array_b[3] = {4, 5, 6};
int array_c[3];

array_c = array_a + array_b;
printf("%d", array_c);
//ILLEGAL! CANNOT DO!
```

Instead you must do the operation on each element manually:

```c
int array_size = 3;
int array_a[array_size] = {1, 2, 3};
int array_b[array_size] = {4, 5, 6};
int array_c[array_size];

for(int i = 0; i < array_size; i++){
	array_c[i] = array_a[i] + array_b[i];
	printf("%d", array_c[i]);
}
```

### Arrays and Functions

Arrays and functions work a little differently than normal variables. For reasons we will cover in another lesson, when arrays are passed-by-value they are not passed element-wise, rather when an array is given as an argument a reference to that array is passed. This means that the argument used in the function is acting on the same memory that an input variable uses, making changes to arrays used as argument persist outside of the function scope.

```c
#include <stdio.h>
// Changes made to an input array within a function
// effect the array outside of the function
void array_func(int size, int in_array[size]){
	in_array[0] = 21;
}
// Not the case for normal variable inputs
void var_func(int input){
	input = 21;
}

void main(void){
	int array_a[3] = {1, 2, 3};
	int var = 10;

	for(int i = 0; i < 3; i++)
		printf("%d, ", array_a[i]);
	//prints 1, 2, 3,

	printf("\n%d\n", var);
	//prints 10

	array_func(3, array_a);
	var_func(var);

	for(int i = 0; i < 3; i++)
		printf("%d, ", array_a[i]);
	//prints 21, 2, 3,

	printf("\n%d\n", var);
	//prints 10
}
```
Here, array_func() is able to change the input array from 1,2,3 to 21, 2, 3. However, when we tried to to it with the normal variable it didn't work. 

The reason arrays behave like this, is that the array identifier, when used without square brackets in order to access a specific index, acts like a location to where the elements are in the computer. When we use the brackets, we use the identifer to say where we want to access that data and use an index to say how far in we want to grab from. We will cover this in more depth later, just know that passing array variables as arguments changes the variable outside of the function. 
## Array Sizes

Array sizes can be declared by the programmer or the compiler:

```c
int student_ids[3] = {1001, 1002, 1003};
float student_grades[] = {97.4, 89.7, 78.3};
```

Both of these are valid because I am giving initial values for each entry. However, if I wanted an array with a few starting entries that I could add on to later in the program, or wanted an empty one to fill, I would need to define the size of the array. Usually we set some max size and keep it constant in the program, making it bigger if needed. 

```c
// A const variable cannot be changed
// Because it cannot be changed, it is fine to make global
cont int MAX_SIZE = 500;

int main(){
	int student_ids[MAX_SIZE] = {1001, 1002, 1003};
	float student_grades[MAX_SIZE] = {97.4, 89.7, 78.3};
	int failing_ids[MAX_SIZE];

	int cur_entries = 3;

	...
}
```

Here I can expand into MAX_SIZE number of entries if I need to. The compiler cannot make your arrays bigger out of the box, so you have to plan around some maximum size number for now. You will need to keep track of the number of current entries you are working with, since the array will allow you to go beyond the entries you set. 


!!! note Out-of-bounds
	See what happens when you try and access array elements that do not exist yet. For example, in the above code,  try to access student_ids[10] and then try to access student_ids[501]. See what kind of errors you get when you try and read a number from those spots or what error occur when you try to change those entries. Experiment!


Much like recursion, where you can have functions that call themselves, you can have arrays of arrays. Yet another mind-blow, I know.

```c
#include <stdio.h>

void main(void){
	int matrix[5][5];
	int sum = 0;

	// Fill array with its overall count starting from 0,0
	for(int i = 0; i < 5; i++){
		for(int j = 0; j < 5; j++){
			matrix[i][j] = sum;
			sum++;
		}
	}

	// Print the final array
	for(int i = 0; i < 5; i++){
		for(int j = 0; j < 5; j++){
			printf("%d\t", matrix[i][j]);
		}
		printf("\n");
	}
}
```

Output:

```
(base) szwakoj@dkl-coe-f749:~$ gcc array.c && ./a.out
0	1	2	3	4	
5	6	7	8	9	
10	11	12	13	14	
15	16	17	18	19	
20	21	22	23	24	
(base) szwakoj@dkl-coe-f749:~$
```

As you can see, we need a loop for each dimension of array. These 2-D arrays are called matrices, and they will become important as your programming skills increase. Essentially, they are set up in the following way:

- `int matrix\[2\]\[3\] = {{1, 2, 3}, {4, 5, 6}};`
	- We are saying we have a size 2 array of size 3 arrays of ints
	- Another way to look at it is to look at it like a table:

|       | col 0 | col 1 | col 2 |
| ----- | ----- | ----- | ----- |
| row 0 | 1     | 2     | 3     |
| row 1 | 4     | 5     | 6     |
- A more concrete example of a array that stores the acronyms for local air ports:
	- char airports \[5\]\[3\] = {{'S', 'Y', 'R'},  {'R', 'O', 'C'}, {'Y', 'O', 'W'}, {'B','U','F'}, {'B','D','L'}};

|                  | airport[][0] | airport[][1] | airport[][2] |
| ---------------- | ------------ | ------------ | ------------ |
| airport[0][]     | S            | Y            | R            |
| airport[1][]<br> | R            | O            | C            |
| airport[2][]<br> | Y            | O            | W            |
| airport[3][]<br> | B            | U            | F            |
| airport[4][]<br> | B            | D            | L            |

So the first size refers to the number of rows and the second the number of columns. This further goes into the 3rd and 4th dimensions as well :
- int tensor\[2\]\[3\]\[3\];

| tensor[0]      | tensor[0][][0] | tensor[0][][1] | tensor[0][][2] |
| -------------- | -------------- | -------------- | -------------- |
| tensor[0][0][] | 0              | 1              | 2              |
| tensor[0][1][] | 3              | 4              | 5              |
| tensor[0][2][] | 6              | 7              | 8              |

| tensor[1]      | tensor[1][][0] | tensor[1][][1] | tensor[1][][2] |
| -------------- | -------------- | -------------- | -------------- |
| tensor[1][0][] | 0              | 1              | 2              |
| tensor[1][1][] | 3              | 4              | 5              |
| tensor[1][2][] | 6              | 7              | 8              |
Note: Tensor refers to a 3-D list of numbers, same way a vector is a 1-D list and a matrix is a 2-D list.

Multi-dimensional arrays are very important, they are our main means of storing tabular information and doing things like rendering on a grid. Remember, graphing as you have learned it from high school requires 2 dimensions, an x and y.

