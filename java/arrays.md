# Arrays

## Learning Outcomes

In this chapter, you will learn how to use arrays in Java.
By the end of the chapter, you should be able to:
- Know what an array is
- Be able to use multidimensional arrays

## Array Basics

Arrays are used as a way to group data of the same type together. The advantage of doing this over using individual variables is that it allows for easier coding should there be a need to repeat the same few lines of code over some data. You will need to first declare/initialise the array as follows:

```java
int[] firstArray; // declares that firstArray is used to hold integers, but has not been initialised yet
double[] secondArray = new double[10]; // declares and initialises secondArray to be an array that holds 10 double values, all initially set to 0
long[] thirdArray = {3, 7, 4}; // declares and initialises thirdArray to be an array that holds 3 longs values, which are 3, 7 and 4 respectively
```

With arrays, we can then refer to individual elements with the following syntax:

```java
int[] array = {3, 7, 4};
System.out.println("This value is 7: " + array[1]); // refers to index 1 in the array, or the second element in the array (since Java uses 0-based indices).
array[2] = array[2] + 5; // adds 5 to index 2 (third element)
System.out.println("This value is 9 : " + array[2]);
```

## Multidimensional arrays

It is also possible to have an array containing arrays, which is what we call a multidimensional array. Note that unlike languages such as C, arrays in each level of a multidimensional array may vary in size:

```java
int[][] array = new int[3][]; // initialises a 2D array, with the topmost level having 3 elements
array[0] = new int[2]; // sets the first element of the topmost element to be an array holding two integers
//array[1] = {3, 7, 4}; // doesn't work
int[][] array2 = new int[3][4] //initialies a 2D array, with the topmost level having 3 elements, and each subarray holds 4 elements, all initialised to 0
int[][] array3 = new int[][] {
    {3, 4},
    {1},
    {4, 6}
}; // initialises a 2D array of 3 elements, with the first element containing [1, 4], the second containing [1], and the third containing [4, 6]
```


