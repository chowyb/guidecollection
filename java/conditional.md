# Conditional Statements

## Learning Outcomes

In this chapter, you will learn how to use conditional statements Java.
By the end of the chapter, you should be able to:
- Understand the usage of booleans
- Understand how to use selection statements (if, else-if, else, switch-case and the ternary operator)
- Understand how to use repetition statements (while, do-while, for)

## Booleans

For Java, conditionals can only be used in conjunction with boolean values, so we'll cover that first. Recall in the chapter on primitives that we have a primitive data type called `boolean` which only holds `true` and `false` values. Apart from these variables, other operators exist that can return a boolean value, the most common being comparison operators. A few examples follow:

`a > b`: returns true if a is greater than b; returns false otherwise.\
`a >= b`: returns true if a is greater to or equals to b; returns false otherwise.\
`a == b`: returns true if a is equals to b; returns false otherwise.\
`a <= b`: returns true if a is equal to or less than b; returns false otherwise.\
`a < b`: returns true if a is less than b; returns false otherwise.\
`a != b`: returns true if a is not equals to b; returns false otherwise.\

```java
int small = 3; // some small number
int large = 100; // some large number
int alsoSmall = 3; // some other small number that's the same value as small

System.out.println(small > large); // should be false
System.out.println(small > alsoSmall); // should be false
System.out.println(small >= alsoSmall); // should be true
System.out.println(small == small); // should be true
System.out.println(small < large); // should be true
```

In addition, we also have logical operators that work on boolean values, which themselves return a boolean value:

`a || b`: (or): returns true if at least one of a and b are true; returns false otherwise.\
`a && b`: (and): returns true if both a and b are true; returns false otherwise.\
`a ^ b`: (xor): returns true if exactly one of a and b are true; returns false otherwise.\
`!a`: (not): returns the opposite value of a (eg. returns true if a is false, and false if a is true).\

Also note the use of || and && above as opposed to | and &; || and && are intended to work on boolean values, while | and & are intended to work on bits. Using | and & on boolean values may produce the same results, but this is not the intended use of these operators.

## Selection Statements

With the knowledge regarding booleans, we can now move on to selection statements. The simplest selection statement would be the if statement, which merely checks if a condition is true or false, and executes the code contained within only if the condition holds true:

```java
int small = 3;
int large = 100;
if (small > large) {
    System.out.println("small is greater than large");
}
if (small < large) {
    System.out.println("small is less than large");
}
```

If we instead have multiple blocks of code, but we only want to execute one of them, we can use else-if statements in conjunction with if statements. Note that every block of selection statements must begin with an if statement, and the program will look through the statements from top to bottom, stopping at the first statement that returns true:

```java
int small = 3;
int large = 100;
if (small > large) {
    System.out.println("small is greater than large");
}
else if (small < large) {
    System.out.println("small is less than large");
}
else if (large > small) {
    System.out.println("large is greater than small, but you won't see this printed out");
}
```

If we wanted to have a block of code that executes if all previous conditions were false, we could use an `else if (true)` statement, but a simpler solution exists: just use an else statement:

```java
int small = 3;
int large = 100;
if (small > large) {
    System.out.println("small is greater than large");
}
else if (small == large) {
    System.out.println("small is equals to large");
}
else {
    System.out.println("small is not greater than or equals to large; ie. small is less than large");
}
```

A different selection statement exists: the switch-case. Unlike the statements above, this does not use a boolean, but instead uses an integer type. This integer is compared against several different possible cases, and executes the code starting from the corresponding case.

```java
int firstNumber = 3;
switch (firstNumber) {
    case 3:
        System.out.println("The number is 3");
    case 2:
        System.out.println("The number is either 3 or 2"); // note that if the value is 3, it executes this line of code as well
        break; // this prevents the program from executing code in later blocks (known as fallthrough)
    case 1:
        System.out.println("The number is 1");
        break;
    default:
        System.our.println("The number is not 3, 2 or 1"); //runs if all previous cases fail
}
```


There also exists a ternary operator which behaves in a different manner:

`(value) = (statement) ? (value if statement is true) : (value if statement is false)`

One possible example (to get the minimum of two values) is as follows:

```java
int firstNumber = 3;
int secondNumber = 100;
int minimumNumber = (firstNumber < secondNumber) ? firstNumber : secondNumber;
System.out.println(minimumNumber);
```

## Repetition Statements

Three different repetition statements are available in Java: while loop, do-while loop, and for loop. The while loop is the simplest loop, as it simply checks for a given condition, and executes the body of the code block if the condition holds true.

```java
int linesPrinted = 0;
while (linesPrinted < 10) {
    System.out.println("This is line " + linesPrinted);
    linesPrinted++;
}
```

The do-while loop is a slightly different variation of the while loop, as it will execute the body of the code block once (regardless of whether the condition of the loop holds true). After the first iteration, it will then check for the condition, and exit if the condition is not true.

```java
do {
    System.out.println("This line only prints once");
} while (false);
```

Note that unlike the while loop, a semicolon is added at the end of the condition.

Finally, we have the for loop, which is likely the most frequently used type of loop. Let us first look at the syntax of the for loop:

```java
for (initialisation; condition; update) {
    body
}
```
This can in fact be converted into a while loop, with the statements being rearranged:

```java
initialisation
while (condition) {
    body
    update
}
```

Also, note that for the while loop, any of the statements (initialisation, condition and update) can be empty. In the event the condition is left empty, the loop simply continues infinitely.

```java
for (int i = 0; i < 10; i++) {
    System.out.println("This is line " + i);
}
int j = 0;
for (; j < 10; j++) {
    System.out.println("This is also line " + j);
}
for (; j >= 0; j--) {
    System.out.println("This is again line " + j);
}
```

Due to this, the initialisation, condition and update statements usually refer exclusively to the variable used in the condition, to more easily see how it changes per iteration.