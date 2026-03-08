## What is super Keyword in Java ?

The `super` keyword in Java is used to refer to the `immediate parent` class object.

It is mainly used in inheritance for..

- ✅ Parent constructor call - from inside child class constructor.
- ✅ Parent variable access  - When parent and child class have the same variable name (same identifier).
- ✅ Parent method call  - When method is overridden in child class.(same identifier).


```java
class Base {

    String message;

    // Parameterized constructor
    Base(String message) {
        this.message = message;
        System.out.println("Base Constructor Called");
    }

    void display() {
        System.out.println("Base display(): " + message);
    }
}
```

```java
class Derived extends Base {

    String message;

    Derived(String baseMessage, String derivedMessage) {

        // 1️⃣ Calling parent parameterized constructor
        super(baseMessage);

        this.message = derivedMessage;

        System.out.println("Derived Constructor Called");
    }

    @Override
    void display() {
        System.out.println("Derived display(): " + message);
    }


    ///////////////////////////////////////////////////////////
    void show() {

        // 2️⃣ Access parent variable
        System.out.println("Parent variable: " + super.message);

        // Child variable
        System.out.println("Child variable: " + this.message);

        // 3️⃣ Call parent method
        super.display();

        // Call child method
        display();
    }
    /////////////////////////////////////////////////////////////
}

```

```java

public class Main {
    public static void main(String[] args) {

        Derived obj = new Derived(
                "Hello from Base",
                "Hello from Derived"
        );

        obj.show();
    }
}

```
