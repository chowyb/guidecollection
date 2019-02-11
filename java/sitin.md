# Sit-In Labs

## Learning Outcomes

In this chapter, you will learn about handling sit-in labs in Java.
By the end of the chapter, you should be able to:
- Run basic commands from the Unix interface
- Debug using compilation error messages/stack traces
- Apply certain strategies to fully utilise the time provided during the lab

## Basic Commands

The following commands will be useful in almost all sit-in labs. Note that any terms in square brackets `[]` should be replaced with the appropriate term.
For [classname], this is the name of the Java class, while for [filename], this is the name of the test case (usually a number).

Running the text editor to edit your file:
```sh
vim [classname].java
```

Compiling:
```sh
javac [classname].java
```

Running your program (with manual input):
```sh
java [classname]
```

Running your program (with file input):
```sh
java [classname] < [filename].in
```

Running your program (with file input/output):
```sh
java [classname] < [filename].in > [filename].o
```

Comparing your output (in a file) with expected output:
```sh
cmp [filename].o [filename].out
```

Printing the contents of a file (three cases are presented below, but the general idea is the same):
```sh
cat [filename].in
cat [filename].o
cat [filename].out
```

Removing an old output file (usually needed if the shell refuses to overwrite an existing file):
```sh
rm [filename].o
```
A prompt will likely appear asking you if you wish to delete this file. Answer with "y" or "yes" to confirm.

Removing a swap file (likely due to vim exiting unexpectedly, and prompting you to retrieve a swap file):
```sh
ls -a
rm [swapfile]
```
Look through the results of `ls -a` to find which files end with a ".swp", and enter the name in the [swapfile] field. Unix will not delete this file if you use "*.swp".
Alternatively, if you already know which Java file is causing it, you can do the following:
```sh
rm .[classname].java.swp
```

Changing directory:
```sh
cd [directoryname]
```
Use ".." as the directory name to go up one level (ie. similar to a "back").

Running a previously issued command:
Press the "up arrow" key to view previous commands.

## Debugging

Bugs can be broadly broken down into three sections: compile time errors, runtime errors, and logical errors. We'll cover each of them in turn:

### Compile Time Errors

Compile time errors occur when a program fails to compile. We'll begin with a simple program that fails to compile:

```java
public class Test {
    public static void main(String[] args) {
        int a, b;
        System.out.println(a + b)
}
```

The following errors occur:
```
Test.java:4: error: ';' expected
                System.out.println(a + b)
                                         ^
Test.java:5: error: reached end of file while parsing
}
 ^
```

Note the line numbers (4, and 5, shown after "Test.java" above). These show the lines that need to be fixed. The caret sign "^" also serves as a guide as to where in the line you should look at. In this case, it seems that we need a semicolon on line 4, and line 5 seems to be incorrect due to a mismatch in braces. Fixing them should give us the following:

```java
public class Test {
    public static void main(String[] args) {
        int a, b;
        System.out.println(a + b);
    }
}
```

Now your program should be able to compile.

### Runtime Errors

Runtime errors occur when something unexpected happens while the program is running. Consider the following program:

```java
import java.util.*;

public class Test {
    public static void main(String[] args) {
        ArrayList<Integer> arr = new ArrayList<Integer>();
        arr.add(7);
        arr.add(4);
        arr.add(3);
        System.out.println(sum(arr));
    }

    public static int sum(ArrayList<Integer> arr) {
        int ans = 0;
        for (int i = 0; i <= arr.size(); i++) {
            ans += arr.get(i);
        }
        return ans;
    }
}
```

This program compiles fine, but crashes upon running with the following stack trace:
```
Exception in thread "main" java.lang.IndexOutOfBoundsException: Index 3 out-of-bounds for length 3
        at java.base/jdk.internal.util.Preconditions.outOfBounds(Preconditions.java:64)
        at java.base/jdk.internal.util.Preconditions.outOfBoundsCheckIndex(Preconditions.java:70)
        at java.base/jdk.internal.util.Preconditions.checkIndex(Preconditions.java:248)
        at java.base/java.util.Objects.checkIndex(Objects.java:372)
        at java.base/java.util.ArrayList.get(ArrayList.java:440)
        at Test.sum(Test.java:15)
        at Test.main(Test.java:9)
```

When viewing stack traces, for starters, ignore the lines starting with "java", since these are usually part of the Java library, and therefore contains code that you cannot modify. Instead, focus on the code that belongs to you:
```
        at Test.sum(Test.java:15)
        at Test.main(Test.java:9)
```

Note that the first line contains the line of code which caused the crash (line 15 in the sum() method, in this case). Any subsequent lines in the stack trace simply indicate which methods called this method (the main() method called sum() in line 9, in this case).

Now that we know which line we should look at, let us consider what error occurred:
```
Exception in thread "main" java.lang.IndexOutOfBoundsException: Index 3 out-of-bounds for length 3
```

From this, it appears that we accessed an element that was out of bounds in our ArrayList. We could fix this by simply changing "<= arr.size()" to "< arr.size()".

### Logical Errors

Sometimes your program may compile and run just fine, but give a result that is not what you expected. This is likely caused by a logical error (or basically, you didn't code the program correctly). In most cases it's difficult to determine the issue by staring at your code, so it's usually easier to use print statements to figure out what happens in the program at a certain point in time (note that most IDEs for Java have debugging tools, but as these are not allowed in a sit-in lab there's not much point in covering them). Consider the following program:

```java
import java.util.*;

public class Test {
    public static void main(String[] args) {
        System.out.println(process(42));
    }

    // checks how many iterations are necessary for the number to hit 1
    public static int process(int num) {
        int ans = 0;
        while (num != 1) {
            if (num % 2 == 0) {
                num /= 2;
            }
            else {
                num *= 3 + 1;
            }
            ans++;
        }
        return ans;
    }
}
```

The above program attempts to process a number according to the Collatz conjecture (ie. for any positive integer n, if n is even, then n = n / 2; otherwise, n = 3n + 1. Given enough iterations, n will become 1). Running this for 42, the expected answer would be 8 (42 -> 21 -> 64 -> 32 -> 16 -> 8 -> 4 -> 2 -> 1). Instead, the program appears to run infinitely.

Suppose that we were unable to figure the reason out by staring at the code (although the error is relatively obvious). The next best way to figure out the error is to try printing the value of num for each iteration:

```java
import java.util.*;

public class Test {
    public static void main(String[] args) {
        System.out.println(process(42));
    }

    // checks how many iterations are necessary for the number to hit 1
    public static int process(int num) {
        int ans = 0;
        while (num != 1) {
            System.out.println(num);
            if (num % 2 == 0) {
                num /= 2;
            }
            else {
                num *= 3 + 1;
            }
            ans++;
        }
        return ans;
    }
}
```

From this, we see a pattern of 84 -> 42 -> 21 -> 84, which seems to suggest that perhaps the calculation for an odd number isn't working. Due to this, we can possibly fix it.
However, one possible issue with doing this is that the extra print statements will show up as part of the results, which will result in a difference when comparing the output. One would have to comment out all the extra print statements after the bug has been fixed as a result (which may take awhile).

To resolve this, it could help to use a separate method for printing debug statements instead:

```java
import java.util.*;

public class Test {
    public static boolean debug = true;

    // separate method for no arguments
    public static void debugPrint() {
        if (debug) System.out.println();
    }

    // encompasses most cases, except where no arguments are provided
    public static void debugPrint(Object obj) {
        if (debug) System.out.println(obj);
    }

    public static void main(String[] args) {
        System.out.println(process(42));
    }

    // checks how many iterations are necessary for the number to hit 1
    public static int process(int num) {
        int ans = 0;
        while (num != 1) {
            debugPrint(num);
            if (num % 2 == 0) {
                num /= 2;
            }
            else {
                num *= 3 + 1;
            }
            ans++;
        }
        return ans;
    }
}
```

Simply change `debug` to false before submission.

## Strategies

For sit-in labs, it is usually encouraged for students to have two terminals open: one for coding only (ie. it only has vim open for the entire duration of the lab), and one for compiling/execution (ie. it executes bash commands). This helps reduce the time needed to toggle between coding and compiling.

Also note that for sit-in labs, a certain amount of time is provided strictly for designing algorithms (no coding on the computer is allowed). However, it is still possible to view the Java API on your computer to plan in advance as to what API you'll be using once you're allowed to start coding.