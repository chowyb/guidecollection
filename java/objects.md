# Classes and Objects

## Learning Outcomes

In this chapter, you will learn about classes objects in Java.
By the end of the chapter, you should be able to:
- Know what classes and objects are
- Know the different access levels of attributes/methods
- Write your own classes (attributes, methods)

## Classes

Classes are basically a custom data type, which contains a collection of different attributes and methods. These are usually grouped together to make the code tidier and more cohesive. A very basic class could simply contain only attributes, though this would not be the best application of classes:

```java
public class Program {
    public static void main(String[] args) {
        MyObject myobj = new MyObject(); // calls the default constructor and creates an instance (object) of this class
        myobj.index = 3; // accesses myobj, and changes the value of the index attribute
        myobj.name = "Ball"; // accesses myobj, and changes the value of the name attribute
        System.out.println("Object index: " + myobj.index + ", object name: " + myobj.name);
    }
}

class MyObject {
    public int index;
    public String name;
}
```

Note that when writing attributes or methods that apply to an instance, we do not require the use of "static".

Already, an issue can be seen from the code above: the main method of Program has to define a way to display the object as a string. An improvement could be made to group the code necessary for translating the object into text within the object itself:

```java
public class Program {
    public static void main(String[] args) {
        MyObject myobj = new MyObject();
        myobj.index = 3;
        myobj.name = "Ball";
        System.out.println(myobj); // calls myobj.toString() implicitly
    }
}

class MyObject {
    public int index;
    public String name;

    public String toString() {
        return "Object index: " + index + ", object name: " + name;
    }
}
```

Note that the toString() method above is implicitly called when printing out the object; you can make it explicit by using `myobj.toString()` instead of just `myobj`.

Also, note that this can still be improved further: what if we could simply initialise the attributes of the class when we construct it for the first time? For this, we write our own constructor in class MyObject:

```java
public class Program {
    public static void main(String[] args) {
        MyObject myobj = new MyObject(3, "Ball"); // cals the custom constructor
        System.out.println(myobj); // calls myobj.toString() implicitly
    }
}

class MyObject {
    public int index;
    public String name;

    public MyObject(int index, String name) { // note the syntax: this uses the same name as the class itself
        this.index = index; // note the use of this.: since the variable index refers to the parameter, we use this. to explicitly reference the attribute of this object
        this.name = name;
    }

    public String toString() {
        return "Object index: " + index + ", object name: " + name;
    }
}
```

We can also modify the default constructor to initialise the attributes for us:

```java
public class Program {
    public static void main(String[] args) {
        MyObject myobj = new MyObject(); // cals the default constructor
        System.out.println(myobj); // calls myobj.toString() implicitly
    }
}

class MyObject {
    public int index;
    public String name;

    public MyObject() { // overrides default constructor
        index = 0;
        name = "void";
    }

    public MyObject(int index, String name) { // note the syntax: this uses the same name as the class itself
        this.index = index;
        this.name = name;
    }

    public String toString() {
        return "Object index: " + index + ", object name: " + name;
    }
}
```

Finally, we can write our own methods to read and modify the attributes instead. Such methods are usually refered to as accessors and mutators:

```java
public class Program {
    public static void main(String[] args) {
        MyObject myobj = new MyObject(); // cals the default constructor
        myobj.setIndex(7);
        System.out.println(myobj.getIndex()); // calls myobj.toString() implicitly
    }
}

class MyObject {
    public int index;
    public String name;

    public MyObject() { // overrides default constructor
        index = 0;
        name = "void";
    }

    public MyObject(int index, String name) { // note the syntax: this uses the same name as the class itself
        this.index = index;
        this.name = name;
    }

    // accessors
    public int getIndex() {
        return index;
    }

    publi String getName() {
        return name;
    }

    // mutators
    public void setIndex(int index) {
        this.index = index;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String toString() {
        return "Object index: " + index + ", object name: " + name;
    }
}
```

Of course, this appears redundant since you could always modify the attributes directly, instead of using methods, so let's now move on to something more grounded in reality: Suppose you want to create a class representing a vehicle. It can carry a certain non-negative number of passengers. Suppose we use the following program:

```java
public class Program {
    public static void main(String[] args) {
        Vehicle car = new Vehicle(-3, "car");
        System.out.println("A car can carry " + car.capacity + " person(s)");
    }
}

class Vehicle {
    public int capacity; // should not be negative
    public String name;

    public Vehicle(int capacity, String name) {
        this.capacity = capacity;
        this.name = name;
    }
}
```

Suddenly this stops making sense, because a vehicle is now able to carry a negative number of passengers (how?). As such, sometimes we want to restrict direct access to the attributes, which is where access levels come in:

## Access Levels

There are several different access levels for attributes and methods. These are, from most restrictive to least restrictive:

| Access Level | Own Class | Package* | Subclasses | Other Classes |
| --- | --- | --- | --- | --- |
| private | Can access | ~~Cannot access~~ | ~~Cannot access~~ | ~~Cannot access~~ |
| (none) | Can access | Can access | ~~Cannot access~~ | ~~Cannot access~~ |
| protected | Can access | Can access | Can access | ~~Cannot access~~ |
| public | Can access | Can access | Can access | Can access |

*Packages are presently not covered in this guide

Now, using this, we can avoid the situation from earlier:

```java
public class Program {
    public static void main(String[] args) {
        Vehicle car = new Vehicle(-3, "car");
        System.out.println("A car can carry " + car.getCapacity() + " person(s)");
    }
}

class Vehicle {
    private int capacity; // should not be negative
    public String name; // can still be public, but bad practice in most cases

    public Vehicle(int capacity, String name) {
        setCapacity(capacity);
        this.name = name;
    }

    // sets capacity if it is non-negative, doesn't do anything otherwise
    public void setCapacity(int capacity) {
        if (capacity >= 0) {
            this.capacity = capacity;
        }
    }

    public int getCapacity() {
        return capacity;
    }
}
```

This helps us prevent unintended changes to the attributes. However, note this possible issue when using objects as attributes themselves:

```java
public class Program {
    public static void main(String[] args) {
        Vehicle car = new Vehicle(3, "car");
        car.setSeat(0, true);
        car.setSeat(1, true);
        System.out.println("Seat 2 is " + (car.getSeat(2) ? "occupied" : "unoccupied"));
        boolean[] seats = car.getSeats();
        seats[2] = true;
        System.out.println("Seat 2 is " + (car.getSeat(2) ? "occupied" : "unoccupied")); // unexpected output?
    }
}

class Vehicle {
    private boolean[] seatOccupied; // keeps track of individual seats
    public String name; // can still be public, but bad practice in most cases

    public Vehicle(int capacity, String name) {
        setCapacity(capacity);
        this.name = name;
    }

    // sets boolean array if capacity is non-negative; does nothing otherwise
    public void setCapacity(int capacity) {
        if (capacity >= 0) {
            seatOccupied = new boolean[capacity];
        }
    }

    public void setSeat(int index, boolean status) {
        if (index >= 0 && index < seatOccupied.length) {
            seatOccupied[index] = status;
        }
    }

    public boolean getSeat(int index) {
        if (index >= 0 && index < seatOccupied.length) {
            return seatOccupied[index];
        }
        return false;
    }

    public boolean[] getSeats() {
        return seatOccupied;
    }
}
```