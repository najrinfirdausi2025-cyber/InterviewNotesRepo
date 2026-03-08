## Generics in Java:
- Generics were introduced in Java 5.
- This provides a way of writing code and algorithms that work with any primitive wrapper or user-defined type—independent of a particular data type.
- Generics data-Types are duduced in compile time by java compiler, provide type safety, ensuring errors are caught at compile-time, avoiding ClassCastException at runtime.
- They can be used to define classes, interfaces, and methods, making code reusable and type-independent.
- Promotes code reusability: the same class or method can operate on multiple data types.
- Eliminates the need for explicit casting of objects.

✅ In short: Generics make Java code safer, cleaner, and more flexible.

```java
// Generic class with one data member of type T

class Test<T> {
    private T data;  // single generic data member

    // Constructor
    public Test(T newdata) { this.data = newdata; }

    // Getter
    public T get() { return data; }
}

```
- `<T>` means this is a generic class/type.
-  Since `T` is a generic `type` parameter, `T data` can store any type depending on how the object is created.
- `<T>`type` parameter, will be replaced with a specific type, such as `Integer`, `String`, or even a custom class.
 when you create an object of this class.
- This shows the flexibility of generics: the same class can work with any type.

```java
Test<Integer> intTest = new Test<>(123);
System.out.println(intTest.get()); // Output: 123

Test<String> stringTest = new Test<>("Hello");
System.out.println(stringTest.get()); // Output: Hello

```

- `Test<Integer>` creates a Test object that stores an `Integer`.
- `Test<String>` creates a Test object that stores a `String`.
- This class is a generic wrapper around a single data member. It allows you to store and retrieve values of any type safely, without casting.

--------------------------------------------------------------------------------------------------------------------------------------------------
## SWAP 

```java
    // Wrapper class
    static class Ref<T> {
        public T value;
        public Ref(T value) { this.value = value; }
    }
```

```java
    // Generic swap method
    public static <T> void swap(Ref<T> a, Ref<T> b) {
        T tmp = a.value;
        a.value = b.value;
        b.value = tmp;
    }

```
```java
// --- Swap integers ---
Ref<Integer> intA = new Ref<>(3);
Ref<Integer> intB = new Ref<>(7);

System.out.println("Before swap: " + intA.value + ", " + intB.value);  // Before swap: 3, 7
swap(intA, intB);
System.out.println("After swap: " + intA.value + ", " + intB.value); // After swap: 7, 3

// --- Swap characters ---
Ref<Character> charA = new Ref<>('g');
Ref<Character> charB = new Ref<>('e');

System.out.println("Before swap: " + charA.value + ", " + charB.value); // Before swap: g, e
swap(charA, charB);
System.out.println("After swap: " + charA.value + ", " + charB.value);  // After swap: e, g

// --- Swap strings ---
Ref<String> strA = new Ref<>("Hello");
Ref<String> strB = new Ref<>("World");

System.out.println("Before swap: " + strA.value + ", " + strB.value);  // Before swap: Hello, World
swap(strA, strB);
System.out.println("After swap: " + strA.value + ", " + strB.value);  // After swap: World, Hello

```
----------------------------------------------------------------------------------------------------------------------------------------------------------------
## Generic + Varargs in Java :
- `varargs:`- which lets a method accept a variable number of arguments of the same type `<T>`

```java
public static <T> void printAllGeneric(T... args) {
    for (T arg : args) {
        System.out.print(arg + " ");
    }
    System.out.println();
}

public static void main(String[] args) {
    printAllGeneric(1, 2, 3);           // Integer
    printAllGeneric("A", "B", "C");     // String
    printAllGeneric(1.1, 2.2, 3.3);     // Double
}
```
- Here, all arguments must be of the same type T, but you can instantiate with different types at different calls.

```java
public static <T> void printAllGeneric(T... args) {
    for (T arg : args) {
        System.out.print(arg + " ");
    }
    System.out.println("\nInferred Type: " + args.getClass().getComponentType().getSimpleName());
}

public static void main(String[] args) {
    printAllGeneric(1, "Hello", 3.5);  // 1 Hello 3.5 Inferred Type: Object
}
```

------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Understand Inheritance and Polymorphism with Java Generics using your Test<T> class.

## Generics Inheritance:
```java
class Base<T> {}
class Derived<T> extends Base<T> {}
```
✅`Generic base class:` 
```java
class Test<T> {
    private T data;

    public Test(T newdata) {
        this.data = newdata;
    }

    public T get() {
        return data;
    }

    public void showType() {
        System.out.println("Type: " + data.getClass().getSimpleName());
    }
}
```
✅ `Subclass keeps Generic Type`

```java
class Child<T> extends Test<T> {

    public Child(T data) {
        super(data);
    }

    public void display() {
        System.out.println("Value: " + get());
    }
}
```
```java
Child<Integer> obj1 = new Child<>(10);
obj1.display();        // Value: 10
obj1.showType();       // Type: Integer

Child<String> obj2 = new Child<>("Hello");
obj2.display();      // Value: Hello
obj2.showType();     // Type: String
```

### Runtime polymorphism (method overriding) with Generics:

```java
class AdvancedTest<T> extends Test<T> {

    public AdvancedTest(T data) {
        super(data);
    }

    @Override
    public T get() {
        System.out.println("Overridden get() called");
        return super.get();
    }
}
```
```java
Test<Integer> obj = new AdvancedTest<>(100);  
System.out.println(obj.get());  // Overridden get() called 100
```

-------------------------------------------------------------------------------------------
##  Interface using Generics
 
✅ 1️⃣ Generic Interface:

```java
// Generic Interface
interface Container<T> {
    T get();
}

```
- `<T>` makes the interface generic.
- Any class implementing this interface must specify the type.

✅ 2️⃣ Implementing the Generic Interface (Keep it Generic)
```java
class Box<T> implements Container<T> {

    private T value;

    // Constructor to initialize value
    public Box(T value) {
        this.value = value;
    }

    @Override
    public T get() {
        return value;
    }
}

```
✅ 3️⃣ Using It
```java
Box<Integer> intBox = new Box<>(100);
System.out.println("Integer: " + intBox.get());

Box<String> strBox = new Box<>("Hello");
System.out.println("String: " + strBox.get());
```

## Collection vs Collections :



- `Collection` → Interface (root for List, Set, Queue)
- `Collections` → Utility class with static methods (sort, reverse, shuffle)

## Why Collections Use Generics?

```java

interface Collection<E> { }

public interface List<E> extends Collection<E> { }
public interface Set<E> extends Collection<E> { }
public interface Queue<E> extends Collection<E> { }


public class ArrayList<E> extends AbstractList<E> implements List<E> {}
public class Vector<E> extends AbstractList<E> implements List<E>, RandomAccess, Cloneable, Serializable { }
public class LinkedList<E> extends AbstractSequentialList<E> implements List<E>, Deque<E>, Cloneable, Serializable { }


public interface Deque<E> extends Queue<E>
public class Stack<E> extends Vector<E>

public class HashSet<E> extends AbstractSet<E> implements Set<E>, Cloneable, Serializable {}

```
- __Because of using Generics below All are valid__

```java
// Used Generics Data type E
LinkedList<int>
LinkedList<char>
LinkedList<string>
```

## Java Collection Hierarchy

```swift
                           Iterable<E>
                                ↑
                        ----------------
                        |              |
                 Collection<E>        (Map - separate hierarchy)
                        ↑
        -----------------------------------------
        |                |                     |
     List<E>           Set<E>               Queue<E>
        |                |                     |
        |                |                  Deque<E>
        |                |                     ↑
        |                |                 LinkedList<E>
        |                |
   ----------------      |
   |              |      |
AbstractList<E>  AbstractSet<E>
   |              |
   |              |
-----------       |
|         |       |
ArrayList Vector  HashSet<E>
            ↑
          Stack<E>

```

## Map Collection

```java
public class Hashtable<K, V> extends Dictionary<K, V> implements Map<K, V>, Cloneable, Serializable { }
public class HashMap<K, V> extends AbstractMap<K, V> implements Map<K, V>, Cloneable, Serializable { }

```

```swift
                           Map<K, V>   (Interface)
                                ↑
                ------------------------------------
                |                                  |
        AbstractMap<K, V>                 Dictionary<K, V>
                |                                  |
             HashMap<K, V>                  Hashtable<K, V>
```
