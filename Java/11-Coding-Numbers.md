# Odd Even
```java
import java.util.Scanner;

public class OddEven {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        
        System.out.print("Enter a number: ");
        int num = sc.nextInt();

        if (num % 2 == 0)
            System.out.println("Even");
        else
            System.out.println("Odd");

        sc.close();
    }
}

```

#  CountDigits

```java
public class CountDigits {
    public static void main(String[] args) {

        int num = 375879;
        int n = num;
        int count = 0;

        while (n > 0) {
           
            n = n / 10;
            count++;
        }

        
        System.out.println(count);  //6
            
        
    }
}
```

# sum of all digits in a number code in java
```java
public class SumOfDigits {
    public static void main(String[] args) {

        int n = -37942;
        int sum = 0;
        int remainder;

        // Handle negative number
        if (n < 0) {
            n = -n;
        }

        // Extract digits and sum
        while (n > 0) {
            remainder = n % 10;
            sum = sum + remainder;
            n = n / 10;
        }

        System.out.println(sum);
    }
}

// (3 + 7 + 9 + 4 + 2 = 25)

```

# First Last Digit Sum
```java
public class FirstLastDigitSum {
    public static void main(String[] args) {

        int n = -37942;

        // If number is negative, make it positive
        if (n < 0) {
            n = -n;
        }

        // Last digit
        int ldigit = n % 10;
        System.out.println(ldigit);

        // Extract first digit
        while (n > 9) {
            n = n / 10;
        }

        int fdigit = n;
        System.out.println(fdigit);

        // Sum of first and last digit
        int sum = fdigit + ldigit;
        System.out.println(sum);
    }
}


```
```
ldigit = 2
fdigit = 3
sum = 5
```

# Max & Min Digit using long

```java
public class MaxMinDigitLong {
    public static void main(String[] args) {

        long num = 907654321045678L;
        long n = num;

        // Handle negative number
        if (n < 0) {
            n = -n;
        }

        int maxDigit = 0;
        int minDigit = 9;

        while (n > 0) {
            int r = n % 10;

            if (r > maxDigit)
                maxDigit = r;

            if (r < minDigit)
                minDigit = r;

            n = n / 10;
        }

        System.out.println("Max digit = " + maxDigit);
        System.out.println("Min digit = " + minDigit);
    }
}
```
# ArmstrongNumber
```java

public class ArmstrongNumber {
    public static void main(String[] args) {

        int num = 153;
        int n = num;
        int sum = 0;

        while (n > 0) {
            int r = n % 10;
            sum = sum + (r * r * r);
            n = n / 10;
        }

        if (sum == num) {   
            System.out.println("Armstrong number");
        } else {
            System.out.println("Not an Armstrong number");
        }
    }
}

// num == sum = 153 = (1x1x1) + (5x5x5) + (3x3x3)

```

# Palindrome number (121 → true)

```java
public class PalindromeNumber {
    public static void main(String[] args) {

        int num = 121;
        int n = num;
        int sum = 0;

        while (n > 0) {
            int r = n % 10;
            sum = (sum * 10) + r;
            n = n / 10;
        }

        System.out.println("Reverse = " + sum);

        if (sum == num) {
            System.out.println("Palindrome number");
        } else {
            System.out.println("Not a Palindrome");
        }
    }
}
```


# Factorial 
- 5 ! = 5x4x3x2x1
- 1 ! = 1
- 0 ! = 1 


```java
public class FactorialNumber {
    public static void main(String[] args) {

        int num = 5;
        int fact = num;
        int n = num;

        if (num == 0 || num == 1) {
            System.out.println("Factorial = 1");
        }

        while (n > 1) {
            n--;
            fact = fact * n;
        }

        System.out.println("Factorial = " + fact);  // Factorial = 120
    }
}

```
```
fact = 5, n = 5
n-- → 4 → fact = 5 * 4 = 20
n-- → 3 → fact = 20 * 3 = 60
n-- → 2 → fact = 60 * 2 = 120
```

# Recursive Factorial

```java

public class FactorialRecursive {
    public static void main(String[] args) {

        int num = 5;
        int result = factorial(num);

        System.out.println("Factorial = " + result);
    }

    static int factorial(int n) {
        // Base case
        if (n == 0 || n == 1) {
            return 1;
        }
        // Recursive case
        return n * factorial(n - 1);
    }
}

```

```
factorial(5)
= 5 * factorial(4)
= 5 * 4 * factorial(3)
= 5 * 4 * 3 * 2 * 1 = 120
```
