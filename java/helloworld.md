# Hello World Program

## Learning Outcomes

In this chapter, you will learn how to write, compile and execute a Hello World program in Java.
By the end of the chapter, you should be able to:
- Write a basic Java program
- Compile and execute a Java program
- Identify the basic parts of a Java program

## Writing Your Program

For writing a program, you will first need to use a text editor to do so. In CS2040 this would be Sublime Text.
Alternatively, you can use an Integrated Development Environment (IDE) such as DrJava. 

```java
import java.util.*;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

Do not worry if the code here is confusing to you, as we'll cover what the code means later in this chapter.

## Compiling and Executing Your Program

If using a text editor, you will need to switch to a command line interface to compile and run your program.
This can be done via a terminal (for Unix-based OSes), or via the Windows command prompt.
In your command line, you will first need to navigate to the folder you saved your Java code in.
On both Unix and Windows, this can be done via the `cd` command.
Once there, you can type the following command: `javac HelloWorld.java` and run it.
This will cause the Java compiler to attempt to compile the source code found in "HelloWorld.java". If it is successful, no output will be written to the terminal, but you should find a new file called "HelloWorld.class" in your current directory (use the command `ls` on Unix, or `dir` on Windows to check).

Now, we can execute the program by using the following command: `java HelloWorld` (note that we do not include the ".class" extension in this command).
If everything goes well, you should see a "Hello World!" show up in your terminal. Success!

## Understanding the Program

Now that we know the program works, let us look at the different parts of the program. We begin with the first line:

```java
import java.util.*;
```

This line of code tells the compiler to include the `java.util` package when compiling the code. Think of a package as part of a library of ready-to-use code; you'll have to specify which parts of the library you intend to use in your program.
For this particular program, this package is not actually used by any code in the program (ie. there are no calls to this package), but we'll use it more extensively in later programs.

Then, we move on to the next line:

```java
public class HelloWorld {
    //extra code inside
}
```

This line indicates that we are writing a class called "HelloWorld". Note that the name of the class should match the filename of the .java file (in this case, the "HelloWorld" class corresponds to the file we write it in, which is "HelloWorld.java"). It is possible to have multiple classes in the same file, but for simplicity we'll stick with one class per .java file.

The word `public` in this line indicates that this class can be accessed by any other class (more on this in another chapter).

For the next line:

```java
    public static void main(String[] args) {
        //extra code inside, actually just one line but still
    }
```

This is an example of a "method", as it is called in Java. Conceptually, this is similar to (but not the same as) a function in other programming languages.

To break down the first line:\
`public` means that this method can be accessed by any other class.\
`static` means that this method is static (tied to a class instead of an object).\
`void` means that this method does not return any value (as opposed to say, returning a String).\
The part in the brackets `()` are the parameters passed to this method.

The `main` method is also the method that will be run initially upon executing the program.\
The `String[] args` parameter is used to take in command line arguments.
In the context of CS2040, this will almost never be used, but will still be covered in a later chapter for completion's sake.

Finally, the last line:
```java
        System.out.println("Hello World!");
```

This indicates that we should write the string "Hello World!" to `System.out` (an output stream that usually refers to your screen), by use of a method called `println`. Using `println` causes us to write an additional newline character `\n` after the string. To avoid adding the additional newline character, use `print` instead of `println`.

