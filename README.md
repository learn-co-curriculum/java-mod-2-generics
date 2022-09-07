# Generics

## Learning Goals

- Define generics.
- Explain why we use generics.
- Review the conventions of generics.

## Introduction

Looking back on the data structures we just learned about, we saw we could have
a collection of reference type variables; such as a `List` of `Book` objects,
or a `Queue` of `String` variables. All of these data structures worked
logically the same despite the different type of object we defined the data
structure to hold. That is because Java heavily uses the concept of generics.
**Generics** are _parameterized types_ which enable us to create classes,
interfaces, and methods with a generic type as the parameter (like `String` or
even our `Book` class) in a "type safe" manner. Type safe means the compiler
will know what type is expected to be in the list, but still be generic enough
to avoid explicit casting, which could cause type mismatches.

## Why Use Generics?

We will run into situations where we might want to apply the same logic to
objects regardless of their type. For example, imagine that we want to create a
method that prints a list of the elements in an array. I could have the
following code:

```java
static void printStringArray(String[] arrayToPrint) {
    System.out.println("-------------------------------");
    for (String itemToPrint: arrayToPrint) {
        System.out.println(itemToPrint);
    }
    System.out.println("-------------------------------");
}
```

This code would work for printing an array of String objects, but would not work
for an array of Integers. For that, it would have to be modified as follows:

```java
static void printIntegerArray(Integer[] arrayToPrint) {
    System.out.println("-------------------------------");
    for (Integer itemToPrint: arrayToPrint) {
        System.out.println(itemToPrint);
    }
    System.out.println("-------------------------------");
}
```

The only differences between the `printStringArray()` and `printIntegerArray()`
methods are:

1. The type of the array parameter that is passed in.
2. The type of the variable used in the `for` loop.

We would have to make a similarly different version of the `printArray()` method
for every single type of array we want to be able to handle, even though the
actual logic of the method is exactly the same.

Generics allow us to avoid that code duplication by letting us defined a version
of the `printArray()` method that takes a "generic" type and applies the same
logic as each variation of our methods above:

```java
static <E> void printArray(E[] arrayToPrint) {
    System.out.println("-------------------------------");
    for (E itemToPrint: arrayToPrint) {
        System.out.println(itemToPrint);
    }
    System.out.println("-------------------------------");
}
```

This code will now work with arrays of any type.

Let's break down the syntax:

1. A new syntax is introduced to signify that this method deals with a generic
   type: `<E>`.
2. The generic type definition is before the return type for the method.
3. Once defined as `E`, the generic type can be used inside the method like any
   other type.
4. `E` is the name of the generic type in a method definition by "convention" -
   it can actually be anything we would like, but using the conventions for
   generics makes our code easier to read and maintain. These conventions are
   also used in the Oracle Java documentation that we will look at in a few
   lessons. In the meantime, let's look more at these naming conventions.

## Generic Naming Conventions

By convention, we define a generic type using a single uppercase letter. We
typically do this on purpose to show a sharp contrast between the naming
conventions we are already familiar with (like having variable names be spelled
out and use camel case or classes being spelled out and using pascal case).

Here are the conventions for generics, which are based on where they are
used:

   1. T - Type
   2. E - Element
   3. K - Key
   4. V - Value
   5. N - Number

## Generic Use Cases

Let's look back at our `ArrayList` class from the `List` interface. Remember how
we said this is a valid way of defining a `List` but is not recommended?

```java
List myList = new ArrayList();
```

In the above line of code, we could add any object we wanted to this list. But
by doing so is not recommended as we discussed. This is where generics come into
play: we can change the list definition to specify what type of items we want in
the list by using the **diamond operator**, `<>`. By definition, the `ArrayList`
is a generic class since it is defined as such:

```java
public class ArrayList<E> extends AbstractList<E> implements List<E> {}
```

A generic class is just like a normal class, except it contains the type
parameter section after the class name: `ArrayList<E>`.

So when we do `new ArrayList<String>();` we are replacing the generic type `E`
with the concrete value, `String`. This is called **generic type invocation**.

Let's look at another use case of generics:

```java
import java.util.Map;
import java.util.HashMap;

public class MapExample {
   public static void main(String[] args) {
      Map<String, Character> studentGrades = new HashMap<String, Character>();
      studentGrades.put("Dustin", 'B');
   }
}
```

Our `Map` interface take in a key/value pair of generic types too! Let's look
at the definition of a `HashMap` a little closer.

```java
public class HashMap<K,V> extends AbstractMap<K,V> implements Map<K,V> {}
```

Notice that in the definition for the `HashMap`, it takes in two parameterized
types, `K` and `V`. When we specify two parameters, we can place both generic
types inside the diamond operator and separate them by a comma.

With a `Map`, we are specifically looking for a key/value pair - so it would
make sense to use the generic name conventions of `K` and `V` for key and value
respectively.

So when we do `new HashMap<String, Character>();` we are performing a generic
type invocation to replace the generic type `K` with the concrete value
`String`, and the generic `V` with the concrete value of `Character`. We will
actually do another generic type invocation too when we execute the
`put(K key, V value)` too.
