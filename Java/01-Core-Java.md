# Java 
- Java is a platform-independent, secure, object-oriented programming language widely used for web, enterprise, Android, and cloud-based applications due to its robustness, performance, and strong ecosystem.

### 🔹 Uses of Java

-   **Web Applications** -- Used in backend development (Spring Boot,
    Hibernate).
-   **Enterprise Applications** -- Banking, ERP, CRM systems.
-   **Android Development** -- Core language for Android apps.
-   **Desktop Applications** -- JavaFX, Swing-based software.
-   **Cloud & Microservices** -- Widely used with Spring Boot in
    cloud-native apps.
-   **Big Data Technologies** -- Hadoop and related tools are
    Java-based.
-   **Embedded Systems** -- Used in smart cards, IoT devices.
-   **Financial Systems** -- High-performance and secure transaction
    systems.

### 🔹 Advantages of Java

-   **Platform Independent** -- Write Once, Run Anywhere (JVM-based).
-   **Object-Oriented** -- Supports OOP concepts (Encapsulation,
    Inheritance, Polymorphism).
-   **Secure** -- No pointers, bytecode verification, sandbox security
    model.
-   **Robust** -- Strong memory management and exception handling.
-   **Multithreaded** -- Built-in support for concurrent programming.
-   **High Performance** -- JIT compiler improves execution speed.
-   **Rich API & Libraries** -- Large standard library and frameworks.
-   **Large Community Support** -- Strong ecosystem and long-term
    stability.

-------------------------------------------

## The latest version of Java (as of 2025) ? - Important Features
- Java SE 25 (JDK 25) — released on September 16, 2025 

__Features :__

- #1  Java 25 (JDK 25) is the latest Long-Term Support (LTS) release in 2025.
- #2  Pattern Matching for primitives enhances instanceof and switch expressions.
- #3 Compact source files and instance main methods reduce boilerplate code.
- #4 Flexible constructor bodies allow statements before super() or this() calls.
- #5 Structured Concurrency simplifies multithreaded task management.
- #6 Scoped Values provide a safer alternative to ThreadLocal for sharing data.
- #7 Compact Object Headers reduce object memory footprint, improving JVM efficiency.
- #8 Ahead-of-Time (AOT) Method Profiling and enhanced Java Flight Recorder (JFR) improve startup performance and profiling capabilities.


## What is an Identifier in Java ?

- An identifier is the name given to a variable, method, class, interface, package, or object in Java.
- It is used to identify something in a program.

## What are reserved words ? How many reserved words in java ?

Reserved words (also called keywords) are words that have a special predefined meaning in Java.
You `cannot use` them as `identifier` like below:

- Variable names
- Class names
- Method names
- Interface names
- Package names

Because the `Java compiler` already understands them `as part of the java language syntax`.

### Java has 52 reserved words (keywords).

```java

abstract     assert       boolean      break        byte
case         catch        char         class        const*
continue     default      do           double       else
enum         extends      final        finally      float
for          goto*        if           implements   import
instanceof   int          interface    long         native
new          package      private      protected    public
return       short        static       strictfp     super
switch       synchronized this         throw        throws
transient    try          void         volatile     while
const        goto
```

## Data Types Supported in Java (With Size)

- Java data types are divided into 2 categories:
    - **Primitive Data Types (8 types)**
    -  **Non-Primitive (Reference) Data Types**

<img width="938" height="493" alt="image" src="https://github.com/user-attachments/assets/c4cb98ca-851c-4655-a65c-513f0d3439e5" />
<img width="989" height="836" alt="image" src="https://github.com/user-attachments/assets/f48ad646-41dc-4779-ac6c-dd9ff529bf91" />

## What are the Short-circuit operators in java
- Short-circuit operators are `logical operators` that stop evaluating the expression as soon as the result is determined.
- Java has two short-circuit operators:
    - __Logical AND__ → `&&`
    - __Logical OR__ → `||`

## What is difference in between == operator and .equal() method in java ?
- `==` compares object references (memory location), while `ob.equals()` compares the actual content of the String. For String comparison, `.equals()` should be used.

```sql
---------------------------------------------------------------------------------------------------
== Operator	                                    | .equals() Method
--------------------------------------------------------------------------------------------------
Compares memory reference (address)	            | Compares actual content (value)
Checks if two references point to same object	| Checks if values inside objects are equal
Works for primitive & objects	                | Mainly used for objects
---------------------------------------------------------------------------------------------------

```

```java
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1 == s2);   // false   // Two different objects are created in heap with diffrent refs memory address

System.out.println(s1.equals(s2));   // true  // Content same
```

## what is instance of operator in Java ?
- The instanceof operator is used to check whether an object is an instance of a specific class, subclass, or interface.
- It returns boolean type:
    - `true` → if the object belongs to that type
    - `false` → otherwise

```java

class Animal { }
class Dog extends Animal { }

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();

        System.out.println(d instanceof Dog);      // true
        System.out.println(d instanceof Animal);   // true
    }
}

// Example 2: Returns False

Animal a = new Animal();
System.out.println(a instanceof Dog);   // false
```
- Used mainly in inheritance and polymorphism
- Works only with objects (not primitives)
- Returns `false` if object is `null`


## What are tpes of type-casting supported in JAVA
- Type casting is the process of converting one data type into another data type.
- In Java, there are two types of type casting:

        - Widening / Implicit automatic Casting
        - Narrowing / Explicit manual Casting

  - Java also supports object casting through `upcasting` and `downcasting` of objects relared through inheritance.
    
<img width="1422" height="279" alt="image" src="https://github.com/user-attachments/assets/2fe3428b-bf34-4f5a-b310-a3193dcb03ac" />

```java

///////////////////// Widening Casting / Implicit casting  /////////////////////////////////////
int num = 10;
double d = num;   // automatic casting
System.out.println(d);   // 10.0

//✅ No data loss
//✅ No need to write cast manually

///////////////////// Narrowing Casting / Explicit casting  /////////////////////////////////////
int x = 130;
byte b = (byte) x;   // Need explicitely casting

System.out.println(b);  // -126

// Converting a larger data type into a smaller data type.  Data loss may occur
// Because byte range is -128 to 127 → overflow happens.
```
## What is object-oriented programming?
Object-Oriented Programming (OOP) is a programming paradigm based on the concept of __objects__, which contain:
```
Data (variables / fields)
Behavior (methods / functions)
```
In OOP, programs are designed by creating __classes__ and __objects__ that model real-world entities.

```Java
class Student {
    String name;     // data
    int age;

    void study() {   // behavior
        System.out.println("Studying...");
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();  // object creation
        s1.name = "Rahul";
        s1.age = 20;
        s1.study();
    }
}
```

- `Student` → Class
- `s1` → Object
- `name, age` → Data
- `study()` → Behavior

- OOP built on four main principles: `Encapsulation`, `Abstraction`, `Inheritance`, and `Polymorphism`.


## `new` vs `newInstance()` in Java

### 1️⃣ `new` Operator

-   `new` is an **operator** used to create objects.
-   Used when we **know the class name at compile time**.
-   Object creation is **direct and type-safe**.
-   Constructor can have parameters.
-   If `.class` file is missing at runtime → `NoClassDefFoundError`
    (Unchecked).

### ✅ Example

``` java
class Test {
    void display() {
        System.out.println("Object created using new");
    }
}

public class Main {
    public static void main(String[] args) {
        Test t = new Test();   // Direct object creation
        t.display();
    }
}
```

------------------------------------------------------------------------

### 2️⃣ `newInstance()` Method

-   `newInstance()` is a **method of `Class` class**.
-   Used to create objects **dynamically at runtime**.
-   Used when **class name is not known at compile time**.
-   Requires **no-argument constructor** (otherwise throws exception).
-   Throws checked exceptions like:
    -   `ClassNotFoundException`
    -   `InstantiationException`
    -   `IllegalAccessException`

⚠ Note: `Class.newInstance()` is deprecated (Java 9+).\
Modern approach uses:

``` java
getDeclaredConstructor().newInstance()
```

### ✅ Example (Dynamic Object Creation)

``` java
class Test {
    public Test() {
        System.out.println("Object created using newInstance()");
    }
}

public class Main {
    public static void main(String[] args) throws Exception {

        Class<?> clazz = Class.forName("Test");
        Object obj = clazz.getDeclaredConstructor().newInstance();

        System.out.println(obj.getClass().getName());
    }
}
```

------------------------------------------------------------------------

<img width="982" height="576" alt="image" src="https://github.com/user-attachments/assets/8b7cf7a9-3304-40f2-b817-d94978b105a4" />

------------------------------------------------------------------------

## 🎯 When to Use What?

### ✅ Use `new` when:

-   You know the class at compile time
-   Normal application development
-   You want better performance and type safety

Example:

``` java
Car car = new Car();
```

### ✅ Use `newInstance()` when:

-   Class name comes from:
    -   Configuration file
    -   Database
    -   User input
    -   Framework (Spring, Hibernate, JDBC drivers)
-   You need dynamic loading

Example:

``` java
String className = "com.example.Car";
Class<?> clazz = Class.forName(className);
Object obj = clazz.getDeclaredConstructor().newInstance();
```

------------------------------------------------------------------------

<img width="1516" height="986" alt="image" src="https://github.com/user-attachments/assets/0b842410-4731-4b39-b2f1-a8ff2895eeb0" />

------------------------------------------------------------------------

## Difference between ClassNotFoundException vs NoClassdefFoundError in java
- `ClassNotFoundException` → Loading problem  - is a checked exception thrown when Java tries to dynamically load a class that is not found in the classpath.
- `NoClassDefFoundError` → Runtime missing problem  - is an unchecked error thrown when a class was present at compile time but missing at runtime.

### 1️⃣ ClassNotFoundException

-   It is a **Checked Exception**.
-   Occurs when Java **tries to load a class dynamically at runtime**.
-   Happens mainly with:
    -   `Class.forName()`
    -   `ClassLoader.loadClass()`
-   Must be handled using **try-catch** or `throws`.

### ✅ Example

``` java
public class Main {
    public static void main(String[] args) {
        try {
            Class.forName("Test");   // Class not found in classpath
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

If `Test.class` is not present in classpath → `ClassNotFoundException`



### 2️⃣ NoClassDefFoundError

-   It is an **Unchecked Error** (subclass of `Error`).
-   Occurs when:
    -   Class was available at compile time
    -   But **missing at runtime**
-   JVM throws it automatically.
-   Usually caused by configuration or deployment issues.

### ✅ Example

``` java
class Test { }

public class Main {
    public static void main(String[] args) {
        Test t = new Test();
    }
}
```

If `Test.class` is deleted after compilation → `NoClassDefFoundError`

```sql

  ClassNotFoundException        |  NoClassDefFoundError
  ------------------------------- --------------------------------------
  Checked Exception             |  Unchecked Error
  Occurs during dynamic loading |  Occurs when class missing at runtime
  Must be handled               |  No need to handle
  Extends `Exception`           |  Extends `Error`
  Example: `Class.forName()`    |  Example: Missing `.class` file

```
<img width="1542" height="610" alt="image" src="https://github.com/user-attachments/assets/6bb0e138-b421-436b-b622-e49262536158" />


## Class vs Object difference

## class:
- A class in Java is a User Defined Composite Data Type that encapsulates multiple data members and related methods into a single unit, acting as a blueprint for creating objects.

```java
// Class definition (blueprint)

class Car {
    // Data members (state)
    String color;
    String model;

    // Method (behavior)
    void drive() {
        System.out.println(model + " is driving");
    }
}
```
- Logical entity	Physical entity
- No memory allocated

## Object:

- An object is an instance of a class. It represents a real-world entity with state (data) and behavior (methods) defined by the class. While the class is the blueprint, the object is the actual thing you can use in your program.

- __State:__ Stored in fields/variables (also called attributes).
- __Behavior:__ Defined by methods of the class.
- __Identity:__ Each object has a unique memory address/reference.

```java
// Creating an object of Car class
Car myCar = new Car();
Car anotherCar = new Car();

myCar.color = "Red";
myCar.model = "Toyota";

anotherCar.color = "Blue";
anotherCar.model = "Honda";

// Accessing object behavior
myCar.drive();        // Output: Toyota is driving
anotherCar.drive();   // Output: Honda is driving
```
- `Class` => blueprint,
- `Object` => real-world entity.
  
- Objects are Physical entity , Memory is allocated only when an object is created.
- You can create multiple objects from a single class.
- Objects hold state and can perform behavior.

##  Local Variables in Java: 
- Local Variables declared inside a method, constructor, or block, They exist only during method execution.
- Their scope is limited to that method/block.
- They do not get default values — you must initialize them before use.

```java
public void greet(String name) {
        // local variable
        String message = "Hello, " + name;   // message in greet() → local variable (only exists while greet() is running)
        System.out.println(message);
    }
```

## Instance Variables in Java:
- Instance Variables(class data member) are declared inside a class but outside methods, constructor, or block.. Each object gets its own copy.
- They store the state of an object
- If not initialized explicitly, they get default values (e.g., 0 for int, null for objects, false for boolean).

- **Student.java**
```java
// This file contains only the Student class
public class Student {
    // Instance variables
    String name;
    int age;

    // Method to display student details
    public void display() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}
```
- **Test.java**
```java
// This file contains the main method
public class Test {
    public static void main(String[] args) {

        // Create objects of Student
        Student s1 = new Student();
        s1.name = "Alice";
        s1.age = 20;

        Student s2 = new Student();
        s2.name = "Bob";
        s2.age = 22;

        s1.display();
        s2.display();
    }
}
```
- `name` and `age` → instance variables
- Each object (s1, s2) has its own copy of these variables.
- Can be accessed using object reference (s1.name, s2.age).
- If you create `100 objects`, there are `100 copies` of `instance variables` in memory (one per object).
- Default values (name = null , age = 0 ) are automatically assigned as not initialized.

## Can a class exist without an object?
- Yes. In Java, a class can exist without creating any objects. Objects are needed only when you want to store instance data or call instance methods.
- But if a class contains `only static members` (variables or methods), you don’t need to create an object to use it.
- You can call these methods directly using the class name, without creating objects.

- __Utility / Helper Classes :__ Many classes are designed only to provide functionality, like `Math` or `Collections` in Java. These classes usually have static methods.
- __Abstract classes and interfaces:__ These exist without objects and are used as templates for other classes. i.e for inherit or implementation.

## 10. What happens when an object is created?
- Constructor called, Memory allocated in heap, each object has its own state/memory.
- Instance variables initialized

## Where are objects stored in memory?
- `Object` → `Heap`
- `Reference` variable → Stack (if local)

<img width="1500" height="620" alt="image" src="https://github.com/user-attachments/assets/fd236ddf-7fb2-4f64-b56e-940c27510d4b" />
