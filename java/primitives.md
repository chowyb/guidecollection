# Primitive Data Types and Basic Statements

## Learning Outcomes

In this chapter, you will learn about the different primitive data types in Java.
By the end of the chapter, you should be able to:
- Know the different primitive data types
- Use basic operators to manipulate these primitive data types

## Primitive Data Types

Primitive data types (or "primitives" for short) are basic data types that are built into Java. These can be broadly broken down into integers and floating point numbers. A few other primitives play a special role not covered in these 2 categories.

### Integer Types

Java provides a few types of primitives for handling integers. They differ in terms of the amount of space they take up in memory, and as a result also affects the range of values they can take. The following primitives fall into this category:

`byte` - takes up 1 byte, holds values from -128 to 127 inclusive
`short` - takes up 2 bytes, holds values from -65,536 to 65,535 inclusive
`char` - takes up 2 bytes, holds values from 0 to 131,071 inclusive
`int` - takes up 4 bytes, holds values from -2,147,483,648 to 2,147,483,647 inclusive
`long` - takes up 8 bytes, holds values from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 inclusive

For most programs, using just the `int` primitive is sufficient.

### Floating Point Types

Floating point primitives are able to support values with decimal places (eg. 1.25), unlike integer types, and also have a much larger range of values they can hold, although they may not hold the exact value of the number (the difference however is usually negligible). The following primitives fall into this category:

`float` - takes up 4 bytes, holds values from -2<sup>149</sup> to (2-2<sup>23</sup>)*2<sup>127</sup>
`double` - takes up 8 bytes, holds values from -2<sup>1074</sup> to (2-2<sup>52</sup>)*2<sup>1023</sup>

For most programs, using `double` is encouraged, as it offers less precision loss over the `float` data type.

### Other Types

The following type does not fit into the above two categories:

`boolean` - takes up 1 byte, holds only the values `true` and `false`

Note that the String data type is conspicuously absent from this list; this is because it's not strictly a primitive, and behaves more like an object instead (more in another chapter).

## Basic Operations

Now that we know the various types of primitives, we can start to manipulate these primitives.

### Declaration and Initialisation

Variables in Java must be declared with the appropriate data type before use. Examples are as follows:

```java
int someInteger;
char character;
float decimal;
```

Variables can also be initialised when declared:

```java
int someInteger = 2;
char character = 'a';
float decimal = 1.25;
```

Note that each statement is followed by a semicolon `;` which indicates the end of that statement. This allows a long statement to span multiples lines of code if necessary.
Also note the usage of `'a'` in the second example; this indicates to return the ASCII value of the character 'a', which is 97.

## Basic Arithmetic

The following operators can be used on the numeric (integer and floating point) primitives:

`+` - adds two numbers
`-` - subtracts two numbers
`*` - multiplies two numbers
`/` - divides the first number by the second number
`=` - assigns the value of the second number to the first number (does not work if the first number is not a variable)

Note the following rules for numeric operations:

When operands of an operation have differing types:
1. If one of the operands is double, convert the other to double
1. Otherwise, if one of them is float, convert the other to float
1. Otherwise, if one of them is long, convert the other to long
1. Otherwise, convert both into int
Essentially, this attempts to convert both operands to the type with the larger range.

It is also possible for the assignment operator to assign two numbers of different types. One of two possible cases will arise:
1. The variable storing the value has a larger range than the value that is being assigned (eg. `float newValue = 3;`). In this case, the value is converted automatically, with no input required on the programmer's part.
2. The variable storing the value has a smaller range than the value that is being assigned (eg. `int newValue = 2.02;`). In this case, the value must be explicitly typecasted. Casting can be done by including the data type it should be casted to in brackets before the value, as follows:

```java
int newValue = (int)2.02;
```

Note that this will result in some loss of data (in the example above, newValue would now contain the number 2).

Also note that for division, if two integer types are used for the division, it will attempt to perform integer division (ie. the remainder is discarded). To avoid this, explicitly cast either number to a float or double eg:

```java
int number = 100;
int quotient = 9;
double result = (double)number / quotient;
```