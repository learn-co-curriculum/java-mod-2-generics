# Generics

## Learning Goals

- Explain generics
- Use generics with static methods

## Generics in Java

As we have seen in the previous sections, classes have hierarchies and classes
that are in the same branch of a hierarchy have common properties and behaviors.

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

1. The type of the array parameter that is passed in
2. The type of the variable used in the `for` loop

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
   type: `<E>`
2. The generic type definition is before the return type for the method
3. Once defined as `E`, the generic type can be used inside the method like any
   other type
4. `E` is the name of the generic type in a method definition by "convention" -
   it can actually be anything you would like but using the conventions for
   generics makes your code easier to read and maintain
5. Here are the conventions for generics, which are based on where they are
   used:
   1. T - Type
   2. E - Element
   3. K - Key
   4. N - Number
   5. V - Value

Another use case for generics is the ability to create classes that can hold and
operate on values that are of any type. A great example of this in Java is
`List` implementations, such as `ArrayList`, which we will study in detail in a
later section.
