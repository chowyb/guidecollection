# Handling Input/Output

## Learning Outcomes

In this chapter, you will learn how to handle basic input and output in Java.
By the end of the chapter, you should be able to:
- Reading input from screen
- Printing output to screen

## Reading Input

For reading input, the Scanner class provided by the Java library is the simplest way to do so. Make sure you include the package the Scanner class is contained in by putting the following line at the top of your program:

```java
import java.util.*;
```

Then, within your program (inside the main method), use the following line to initialise the Scanner:

```java
Scanner sc = new Scanner(System.in);
```

This declares a new variable called "sc" which points to a Scanner that reads in input from the screen for us. With this, we can now start to read input.

### Scanner Methods

For Scanner methods, a method call will return a value of a certain data type (depending on the method which is called), which must be stored in the appropriate data type. Some possible uses:

```java
int integer = sc.nextInt(); // reads in the first value encountered as an integer
double decimal = sc.nextDouble() // reads in the first value encountered as a double
String word = sc.next(); // reads in the first value encountered as a string, and stops upon encountering a whitespace.
String line = sc.nextLine(); // keeps reading until it reaches a line separator
```

The value stored can then be manipulated in the same manner as any other variable.

## Printing Output

For printing output, we do not have to explicitly declare another class to do so; we can simply use the special `System.out` stream directly, such as the one seen in the Hello World program:

```java
System.out.println("Hello World!");
```

It is also possible to call other methods to perform the printing, such as:
```java
System.out.print("This does not add a newline character");
int numberToPrint = 3;
System.out.printf("This emulates scanf from C: %d %d\n", numberToPrint, 8);
```
