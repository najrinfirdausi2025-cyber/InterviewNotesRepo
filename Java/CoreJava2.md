##  Abstract Class  vs Interface in Java:

```sql

| Abstract Class                                 | Interface                                                                 |
| ---------------------------------------------- | ------------------------------------------------------------------------- |
| Can have **abstract and non-abstract methods** | Methods are **abstract by default** (Java 8+ allows `default` & `static`) |
| Can have **instance variables**                | Variables are **public, static, final** by default                        |
| Supports **constructors**                      | ❌ No constructors                                                         |
| Supports **single inheritance**                | Supports **multiple inheritance**                                         |
| Can have **access modifiers**                  | Methods are **public by default**                                         |
| Uses `extends` keyword                         | Uses `implements` keyword                                                 |
| Can have method implementation                 | Focuses on **what to do**, not how                                        |

```

````
##  1. What is Java?

Theory:
Java is a high-level, object-oriented, platform-independent programming language.

Code:

class Hello {
    public static void main(String[] args) {
        System.out.println("Hello Java");
    }
}

## 2. Why is Java platform-independent?

Theory:
Java is platform-independent because it compiles code into bytecode, which runs on any system using the JVM,
 enabling write once run anywhere.

Code:

Java Source → Bytecode → JVM → Any OS

## 3. What is JVM?

Theory:
JVM executes bytecode and handles memory, GC, and runtime.

Code:

System.out.println("Executed by JVM");

## 4. Difference between JDK, JRE, JVM?

Theory:

JVM: Runs bytecode

JRE: JVM + libraries

JDK: JRE + dev tools

Code:

javac → JDK
java  → JRE

## 5. What are Java features?

Theory:
OOP, portable, secure, robust, multithreaded.

## 6. What is a class?

Theory:
Blueprint of an object.

Code:

class Car {
    String color;
}

## 7. What is an object?

Theory:
Instance of a class.

Code:

Car c = new Car();

## 8. What is Encapsulation?

Theory:
Wrapping data and methods, hiding data using private access.

Code:

class User {
    private String name;
    public String getName() {
        return name;
    }
}

## 9. What is Inheritance?

Theory:
One class acquires properties of another.

Code:

class Animal {
    void eat() {}
}
class Dog extends Animal {}

## 10. What is Polymorphism?

Theory:
Same method name, different behavior.

Code:

class A {
    void show() { System.out.println("A"); }
}
class B extends A {
    void show() { System.out.println("B"); }
}

## 11. Compile-time vs Runtime polymorphism?

Theory:

Compile-time: Method overloading

Runtime: Method overriding

Code:

int add(int a, int b) {}
double add(double a, double b) {}

## 12. What is Abstraction?

Theory:
Hiding implementation details.

Code:

abstract class Shape {
    abstract void draw();
}

## 13. Abstract class vs Interface?

Theory:
Interface supports multiple inheritance; abstract class does not.

Code:

interface A { void show(); }
abstract class B { abstract void display(); }

## 14. What is a constructor?

## What is a Constructor?

**Answer:**
A **constructor** is a special method in a class that is automatically called when an object is created.
It is used to **initialize object data members (variables)**.

---

### Key Features

* Same name as the class
* No return type (not even `void`)
* Called automatically during object creation
* Used for initializing values

---

### Example

```java
class Student {
    String name;

    // Constructor
    Student(String n) {
        name = n;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student("Rahul"); // constructor called
        System.out.println(s.name);
    }
}
```

---

### Types of Constructors

1. **Default Constructor** – no parameters
2. **Parameterized Constructor** – accepts values

--
```
## constructor-
> A constructor is a special method that runs automatically when an object is
created and is used to initialize the object's data members.
It is mainly used to initialize the instance variables of the class.

## Key Points to Mention in Interview

Constructor name must be same as class name

It does not have a return type

It is called automatically when using the new keyword

Used for object initialization

## Example
class Employee {
    String name;

    // Constructor
    Employee(String name) {
        this.name = name;
    }
}

public class Main {
    public static void main(String[] args) {
        Employee e = new Employee("John");
    }
}
```


Code:

class Test {
    Test() {
        System.out.println("Constructor");
    }
}

## 15. Can constructors be overloaded?

Theory:
Yes, multiple constructors with different parameters.

Code:

Test() {}
Test(int a) {}

## 16. What is this keyword?

Theory:
Refers to current object.

Code:

this.name = name;
```
## Constructors & Types
* A **constructor** is a special method used to **initialize an object**.
* It is **automatically invoked** when an object is created.
* The constructor name is **same as the class name**.
* Constructors **do not have a return type**.
* They are used to **assign initial values** to data members.
``
## class Test {
    Test() {
        System.out.println("Constructor");
    }
}
```


Yes ✅ — **constructors can be overloaded**.

### **Constructor Overloading (Interview Answer)**

* Constructor overloading means **having multiple constructors** in the same class with **different parameter lists**.
* It allows creating objects in **different ways**.
* Overloading is based on **number, type, or order of parameters**.
* All constructors have the **same class name**.
* It improves **flexibility and usability** of the class.

### **One-line Answer**

Yes, constructors can be overloaded by using different parameter lists in the same class.

If you want, I can also share a **short example**.


