# Memory Organisation

## Learning Outcomes

In this chapter, you will learn how memory is organised in Java.
By the end of the chapter, you should be able to:
- Understand how memory of variables are organised

## Memory - Primitives

For primitive data types, memory organisation is simple; when a variable is declared using a primitive data type, that variable simply stores the value itself. As such:

```java
int firstNumber = 2; // firstNumber stores the value 2
int secondNumber = firstNumber; // secondNumber stores a copy of the value of firstNumber, which is 2
secondNumber = 1; // secondNumber now stores the value 1
System.out.println(firstNumber + " " + secondNumber); // should output "2 1"
```

## Memory - Objects

For objects (which is basically anything that's not a primitive, including arrays - this will be covered in more details in a later chapter), when a variable is declared, that variable does not store the value itself; instead, it stores a reference to an instance of an object. Multiple variables can refer to the same object, and modifying this object will cause the changes to be reflected across all other variables referencing this same object.

```java
int[] firstArray = new int[2]; // firstArray contains a reference to an array with 2 integers
int[] secondArray = new int[2]; // secondArray contains a reference to a different array with 2 integers

firstArray[0] = 3;
firstArray[1] = 4;
secondArray[0] = 2;
secondArray[1] = 1;
System.out.println(firstArray[0] + " " + firstArray[1]);
System.out.println(secondArray[0] + " " + secondArray[1]); // note that these two are different

secondArray = firstArray;
System.out.println(firstArray[0] + " " + firstArray[1]);
System.out.println(secondArray[0] + " " + secondArray[1]); // note that these two are the same, which is to be expected

secondArray[0] = 5;
System.out.println(firstArray[0] + " " + firstArray[1]);
System.out.println(secondArray[0] + " " + secondArray[1]); // note that these two are the same, which may not be expected
```