# Method Calls

## Learning Outcomes

In this chapter, you will learn how to write and call methods in Java.
By the end of the chapter, you should be able to:
- Write methods that return values
- Call methods
- Overload methods

## Writing methods

Methods are essentially a way to break down your program into more readable, reusable blocks. In Java the usual form of a method is:

```java
public static int myAddmethod(int firstInput, int secondInput) {
    return firstInput + secondInput;
}
```

The data type that is returned is added before the method name (in thia case, int), while any parameters (or values that are passed to the method) necessary for the method are added in brackets after the method name (in this case, two integers, which are referred to as firstInput and secondInput by this method). If no return value is required, simply use "void" in place of the data type (hence the default `public static void main(String[] args)` returns no value). The use of "static" here is not explained in this chapter; in the chapter on objects we'll cover this in more detail.

## Calling Methods

Calling methods simply requires the programmer to refer to the method by name, and provide any parameters necessary for the method. For the example above:

```java
int firstNum = 6;
int secondNum = 3;
int result = myAddmethod(firstNum, secondNum); // this is the method call
System.out.println(result);
```

Note that the rules for assigning values for numeric data types apply here as well: it is possible to provide an integer value to a parameter that expects a double value (since the double value has a larger range than the integer), but not the other way around:

```java
public static double addDouble(double firstDouble, double secondDouble) {
    return firstDouble + secondDouble;
}

public static int subInt(int firstInt, secondInt) {
    return firstInt - secondInt;
}

public static void main(String[] args) {
    int int1 = 3;
    int int2 = 6;
    double double1 = 3.0;
    double double2 = 6.0;
    System.out.println("Adding integer values: " + addDouble(int1, int2));
    System.out.println("Subtracting integer values: " + subInt(int1, int2));
    System.out.println("Adding double values: " + addDouble(double1, double2));
    //System.out.println("Subtracting double values: " + subInt(double1, double2)); // will cause an error
}
```

Also, note that from the chapter on memory organisation, there is a difference between primitives and objects: as the values of the parameters are copied over to the method (and the values of objects are the memory addresses of the object themselves), passing a primitive will not modify that primitive in the caller method, while passing an object will modify that object in the caller method as well, provided the parameter still points to the same object:

```java
public static void modifyArray(int[] param) {
    param[0] = -5;
}

public static void notModifyingArray(int[] param) {
    param = new int[3]; // no longer points to the same array
    param[0] = 42;
}

public static void main(String[] args) {
    int[] arr = new int[3];
    arr[0] = 2;
    arr[1] = 3;
    arr[2] = 7;
    System.out.println(arr[0]);
    modifyArray(arr);
    System.out.println(arr[0]);
    notModifyingArray(arr);
    System.out.println(arr[0]);
}
```

## Method Overloading

Note that since methods have to declare what parameters they expect, as well as their type, it is in fact possible to have multiple methods with the same name, but different parameters. The easiest form of this is to have a different number of parameters:

```java
public static int multiply(int number) {
    return number * number;
}

public static int multiply(int firstNum, int secondNum) {
    return firstNum * secondNum;
}

public static void main(String[] args) {
    int num1 = 3;
    int num2 = 6;
    System.out.println("One parameter: " + multiply(num1));
    System.out.println("Two parameters: " + multiply(num1, num2));
}
```

It is also possible to have the same number of parameters, but different types:

```java
public static int getQuotientOfDivision(int dividend, int divisor) {
    System.out.println("Dividing using integers");
    return dividend / divisor;
}

// note that you can change the above method body to just "return (int) dividend / divisor;" to avoid this redundant method below,
// but for purposes of illustration we'll use two different methods
public static int getQuotientOfDivision(double dividend, double divisor) {
    System.out.println("Dividing using doubles");
    double result = dividend / divisor;
    return (int) result;
}

public static void main(String[] args) {
    int int1 = 17;
    int int2 = 5;
    double double1 = 32.7;
    double double2 = 4.3;
    System.out.println("Calling using integers: " + getQuotientOfDivision(int1, int2));
    System.out.println("Calling using doubles: " + getQuotientOfDivision(double1, double2));
}
```

Note that since we can still promote numeric data types as mentioned earlier, the following (despite having different parameter types) will result in an error:

```java
public static double add(int i, double d) {
    return i + d;
}

public static double add(double d, int i) {
    return d + i;
}

public static void main(String[] args) {
    int int1 = 3;
    int int2 = 6;
    System.out.println("Result of adding: " + add(int1, int2)); // error
}
```