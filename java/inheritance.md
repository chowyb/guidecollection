# Inheritance

## Learning Outcomes

In this chapter, you will learn about classes objects in Java.
By the end of the chapter, you should be able to:
- Know what interfaces and abstract classes are
- Understand inheritance, and overriding

## Interfaces

Where classes contain attributes and methods that already have a method body, interfaces are different in that they only provide a method signature (ie. the first line of a method, containing the name, parameters and return type, among other things) for all methods in the interface. Usually, a specificiation is provided as to what these methods are expected to do, but not as to how it is actually done. As a short example:

```java
// note the "interface" instead of "class"
interface TriangleHelper {
    /* gets the length of two sides of a right angled triangle and returns the hypotenuse
     */
    public double getHypotenuse(double side1, double side2);
}
```

This interface provides only one method, but currently there is no way to run it. Instead, we will need to create a class that implements (ie. provides a method body for) the interface.

```java
// note the "implements" here
class TriangleHelperImpl implements TriangleHelper {
    public double getHypotenuse(double side1, double side2) {
        return Math.sqrt(side1 * side1 + side2 * side2);
    }
}
```

Now that we have a class which implements this interface, we can finally use it (code below is for one Java file):

```java
public class Program {
    public static void main(String[] args) {
        TriangleHelper th = new TriangleHelperImpl(); // note that you cannot create a new instance of an interface; you will need to use a class that implements the interface
        System.out.println(th.getHypotenuse(3, 4));
    }
}

interface TriangleHelper {
    public double getHypotenuse(double side1, double side2);
    // interface methods don't need comments, strictly speaking, but it's always good practice to mention what it should do, especially since an interface has no method body
}

class TriangleHelperImpl implements TriangleHelper {
    public double getHypotenuse(double side1, double side2) {
        return Math.sqrt(side1 * side1 + side2 * side2);
    }
}
```

The main use of an interface (why not just use a class and skip the interface directly?) is that with an interface, you are able to use different implementations of the methods, without having to worry about making too many changes to code that calls this interface. Some implementations are better than others at certain areas (eg. works faster or uses less memory), which may affect a programmer's decision as to which one to use. Suppose we have a different implementation of TriangleHelper as follows:

```java
class BadTriangleHelperImpl implements TriangleHelper {
    public double getHypotenuse(double side1, double side2) {
        double angle = Math.atan(side1 / side2);
        return side1 / sin(angle);
    }
}
```

If we were to use this implementation initially (instead of TriangleHelperImpl), it'd likely be worse due to redundant calculations, but were we to find a better implementation (TriangleHelperImpl) later on, we'd only need to worry about changing the implementation class (change what class we instantiate). We wouldn't need to worry about whether the method names are the same (if they both implement the same interface, they should be the same)


## Abstract Classes

Abstract classes are sort of a middle ground between interfaces and normal classes, in that you can provide method bodies and attributes in an abstract class (similar to classes), but still allowing for some methods to not be implemented (similar to interfaces). An example follows:

```java
abstract class Pet {
    protected int numLegs = 4; // we assume most pets are 4-legged; note that in some cases it may be best not to have a default case in the abstract class itself
    protected String name; // note the use of "protected"; we want subclasses to be able to access this, but not other classes

    public String toString() {
        return name + " has " + numLegs + " legs";
    }

    public int getNumLegs() {
        return numLegs;
    }

    public String getName() {
        return name;
    }

    abstract public String makeSound();
}
```

Now, since it is an abstract class, we still need a non-abstract class to inherit from it, and include a method body for any abstract methods it may have:

```java
// note the "extends"
class Cat extends Pet {
    public Cat() {
        name = "Cat";
    }

    public String makeSound() {
        return "Meow";
    }
}

// a pet cow?
class Cow extends Pet {
    public Cow() {
        name = "Cow";
    }

    public String makeSound() {
        return "Moo";
    }
}
```

Now, let's put them all together into one program:

```java
public class Program {
    public static void main(String[] args) {
        Pet a = new Cat(); // keep the variable names short, just so that we can't tell from the variable name what kind of pet it is for this example
        Pet b = new Cow();
        System.out.println(a); // again, calls toString() implicitly
        System.out.println(a.makeSound());
        System.out.println(b);
        System.out.println(b.makeSound());
    }
}

abstract class Pet {
    protected int numLegs = 4; // we assume most pets are 4-legged; note that in some cases it may be best not to have a default case in the abstract class itself
    protected String name; // note the use of "protected"; we want subclasses to be able to access this, but not other classes

    public String toString() {
        return name + " has " + numLegs + " legs";
    }

    public int getNumLegs() {
        return numLegs;
    }

    public String getName() {
        return name;
    }

    abstract public String makeSound();
}

class Cat extends Pet {
    public Cat() {
        name = "Cat";
    }

    public String makeSound() {
        return "Meow";
    }
}

class Cow extends Pet {
    public Cow() {
        name = "Cow";
    }

    public String makeSound() {
        return "Moo";
    }
}
```

Note how we are able to access method bodies from both the abstract class and its subclasses. Also note that, as in the chapter on objects, we call toString() implicitly when printing. This occurs because every class we create implicitly extends the Object class in Java, which has a toString() method of its own. Since every class extends Object, it is therefore assumed that every class would have a toString() method, which allows the implementation of println() (strictly speaking, actually a different method called from println()) to use the toString() method for printing. In all the classes where we write a toString() method, we are actually overriding the original implementation provided by the Object class with our own.
This idea can be applied to custom classes as well (suppose we override getName):

```java
public class Program {
    public static void main(String[] args) {
        Pet a = new Cat(); // keep the variable names short, just so that we can't tell from the variable name what kind of pet it is for this example
        Pet b = new Cow();
        System.out.println(a); // again, calls toString() implicitly
        System.out.println(a.getName());
        System.out.println(b);
        System.out.println(b.getName());
    }
}

abstract class Pet {
    protected int numLegs = 4; // we assume most pets are 4-legged; note that in some cases it may be best not to have a default case in the abstract class itself
    protected String name; // note the use of "protected"; we want subclasses to be able to access this, but not other classes

    public String toString() {
        return name + " has " + numLegs + " legs";
    }

    public int getNumLegs() {
        return numLegs;
    }

    public String getName() {
        return name;
    }

    abstract public String makeSound();
}

class Cat extends Pet {
    public Cat() {
        name = "Cat";
    }

    public String getName() {
        return name + ", and hoomans serve us";
    }

    public String makeSound() {
        return "Meow";
    }
}

class Cow extends Pet {
    public Cow() {
        name = "Cow";
    }

    public String makeSound() {
        return "Moo";
    }
}
```