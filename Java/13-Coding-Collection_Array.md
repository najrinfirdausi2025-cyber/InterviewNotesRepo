## Table of Contents

- [Which Collection When](#Which-Collection-Whene)
- [Convert User Input Integers into ArrayList](#convert-User-Input-Integers-into-ArrayList)
- [Convert User Input Strings into ArrayList](#convert-User-Input-Strings-into-ArrayList)
- [Iterate a list one by one element](#Iterate-a-list-one-by-one-element)
- [Check Empty collection or not ?](#Check-Empty-collection-or-not)
- 
## Which Collection When
```sql
- ✅ 1️⃣ Fast Searching :                     HashSet/HashMap     set.contains(5);  // Very fast  O(1)
- ✅ 2️⃣ Fast Random Access (get by index):   ArrayList           numbers.get(3);  // Very fast O(1)
- ✅ 3️⃣ Fast Insert / Remove in Middle :     LinkedList          list.add("A") / list.add(2, "B");  // Practical performance not always better than ArrayList.  O(n)
- ✅ 4️⃣ Remove by Value Fastest:             HashSet/HashMap     set.remove("Banana"); // Very fast ,Because lookup is O(1).
- ✅ 5️⃣ Automatic Sorting Needed:            TreeSet/TreeMap     tree.add(5)  // maintain sorted order automatically during insertion. O(log n)
- ✅ 5️⃣ QUeue FIFO (First In → First Out) :  ArrayDeque          queue.offer(10) & queue.poll() // offer() / poll() /peek() → Very fast O(1) 
```

## convert User Input Integers into ArrayList:
- `Inegers`: 5 , 3, 7, 1, 9   ==Convert==>   ArrayList: [ 5 , 3, 7, 1, 9]

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {
        
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter numbers separated by comma:");
        String input = scanner.nextLine();

        String[] items = input.split(",");

        List<Integer> numbers = new ArrayList<>();

        for (String item : items) {
            numbers.add(Integer.parseInt(item.trim()));
        }

        System.out.println("Final Numbers List: " + numbers);
    }
}
```

---------------------------------------------------
## Iterate a list<int> one by one element

```java
List<Integer> numbers = new ArrayList<>(Arrays.asList(5, 3, 7, 1, 9));
for (Integer num : numbers) {
    System.out.println(num);
}
```
```java
// even shorter way:
numbers.forEach(System.out::println);
```

```java
// OLD style
for (int i = 0; i < numbers.size(); i++) {
    System.out.println(numbers.get(i));
}
```

------------------------------------------------------------
## Check Empty collection or not
- Almost all collections and map interface  has `isEmpty()` to check collection empty or not ? It return `True` or `False`
- supported in all these class `ArrayList, List, LinkedList, Vector, HashSet, TreeSet, Queue, ArrayDeque, LinkedList, PriorityQueue, HashMap, TreeMap, Hashtable, Stack class`
```java
List<Integer> list = new ArrayList<>();
if (list.isEmpty()) {
    System.out.println("List is empty");
}
```
```java
Set<String> set = new HashSet<>();
if (set.isEmpty()) {
    System.out.println("Set is empty");
}
```
```java
Map<String, Integer> map = new HashMap<>();
if (map.isEmpty()) {
    System.out.println("Map is empty");
}
```
```java
Queue<Integer> queue = new ArrayDeque<>();
if (queue.isEmpty()) {
    System.out.println("Queue is empty");
}
```

## Add by value , by index , remove by value, by index

```java
ArrayList<String> list = new ArrayList<>();

list.add("Banana");
list.remove("Banana");   // removes first occurrence

int index = 1 
list.add(index, "Orange");   // add @[index=1] shifts elements right 
list.remove(index);          // removes "Orange"
```

```java
import java.util.*;

public class ArrayListOperations {
    public static void main(String[] args) {

        ArrayList<String> list = new ArrayList<>();

        // ADD BY VALUE (append at end)
        list.add("Apple");
        list.add("Banana");
        list.add("Mango");

        // ADD BY INDEX (insert at position)
        list.add(1, "Orange");   // shifts elements right

        System.out.println("After Adding : " + list);
        // [Apple, Orange, Banana, Mango]


        // REMOVE BY VALUE
        list.remove("Banana");   // removes first occurrence

        System.out.println("After Remove Value : " + list);
        // [Apple, Orange, Mango]


        // REMOVE BY INDEX
        list.remove(0);          // removes "Apple"

        System.out.println("After Remove Index : " + list);
        // [Orange, Mango]
    }
}

```
<img width="1085" height="360" alt="image" src="https://github.com/user-attachments/assets/910a3a90-9b63-4b7d-a853-dc76bf9a8e09" />

------------------------------
## Find key Element present or not
```java
List<Integer> numbers = new ArrayList<>(Arrays.asList(5, 3, 7, 1, 9));
boolean found = numbers.contains(key);   // key = 7 check if number exists  , return True or False
```

## Find postion of Key

```java
 List<Integer> numbers = new ArrayList<>(Arrays.asList(5, 3, 7, 1, 9));
 boolean found = numbers.contains(key);
 if (found) { int position = numbers.indexOf(key); }
```
- Full examples
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        List<Integer> numbers = new ArrayList<>(Arrays.asList(5, 3, 7, 1, 9));

        int key = 7;
        boolean found = numbers.contains(key);
        if (found) {
            int position = numbers.indexOf(key);
            System.out.println("Found at index: " + position); // Found at index: 2
        } else {
            System.out.println("Not found");
        }
    }
}
```

---------------------------------
## Count ElementOccurenceFrequency in array java collection 
```java
List<Integer> numbers = Arrays.asList(5, 3, 7, 1, 9, 3, 5, 3);
int freqCount = Collections.frequency(numbers, key); // key =3

// System.out.println("3 occurs " + freqCount + " times");
```


## Find Max Repeating Element in a List of numbers

```java
public static int findMaxRepeatingElement(List<Integer> numbers) {
        int maxCount = 0;
        int maxRepeatingElement = numbers.get(0);

        for (int key : numbers) {
            int count = Collections.frequency(numbers, key);
            if (count > maxCount) {
                maxCount = count;
                maxRepeatingElement = key;
            }
        }

        return maxRepeatingElement;
    }

List<Integer> numbers = Arrays.asList(5, 3, 7, 3, 1, 3, 5, 9);
int result = findMaxRepeatingElement(numbers);

// System.out.println("Max repeating element: " + result);
```
----
## Find if array/list Has any Duplicates.

```java
// Method to check if a list has duplicates
public static boolean hasDuplicates(List<Integer> numbers) {

    // HashSet stores only unique elements
    Set<Integer> unique = new HashSet<>(numbers);

    // If size is same, no duplicates
    if (unique.size() == numbers.size())
        return false;
     else
        return true;
}

List<Integer> numbers = Arrays.asList(5, 3, 7, 1, 9, 3);
boolean hasDulicateX = hasDuplicates(numbers);
```

-----------------------------------------------------------------
## Find Duplicates in array

```java
 public static Set<Integer> findDuplicates(List<Integer> numbers) {
        Set<Integer> seen = new HashSet<>();
        Set<Integer> duplicates = new HashSet<>();

        for (int num : numbers) {
            if (!seen.add(num)) { // add() returns false if element already exists
                duplicates.add(num);
            }
        }

        return duplicates;
    }

List<Integer> numbers = Arrays.asList(5, 3, 7, 3, 1, 3, 5, 9);
Set<Integer> duplicates = findDuplicates(numbers);
// System.out.println("Duplicates in array: " + duplicates);
```
---------------------------------------------------------------
## Remove duplicate elements from `List` or `ArrayList`

- `List`
```java
List<Integer> numbersList = UserInput.getNumbersFromUser();
List<Integer> numbersList = Arrays.asList(1, 2, 3, 2, 4, 1, 5);

// HashSet does NOT allow duplicate elements, converting time, it Remove all duplicates And insertion Order is preserved 
Set<Integer> uniqueSet = new LinkedHashSet<>(numbersList); //  // [1, 3, 5, 7, 9] 

// HashSet does NOT allow duplicate elements, converting time, it Remove all duplicates But Order is NOT preserved 
Set<Integer> uniqueSet = new HashSet<>(numbersList);  //[5, 3, 7, 1, 9]

System.out.println("Unique elements: " + uniqueSet);
```
`ArrayList`
```java
ArrayList<Integer> numbersList = UserInput.getNumbersFromUser();
ArrayList<Integer> numbersList = new ArrayList<>(Arrays.asList(5, 3, 7, 1, 9, 3, 5, 7));

// HashSet does NOT allow duplicate elements, converting time, it Remove all duplicates And insertion Order is preserved 
Set<Integer> uniqueSet = new LinkedHashSet<>(numbersList); //  [1, 3, 5, 7, 9] 

// HashSet does NOT allow duplicate elements, converting time, it Remove all duplicates But Order is NOT preserved 
Set<Integer> uniqueSet = new HashSet<>(numbersList);  //[5, 3, 7, 1, 9]

System.out.println("Unique elements: " + uniqueSet);
```

----------------------------------

## check if Array (Unsorted) is Subset of another array (Unsorted) 

```java
public static boolean isSubset(List<Integer> subset, List<Integer> superset) {
        // Create a HashSet from superset for fast lookup
        Set<Integer> supersetSet = new HashSet<>(superset);

        // Check if each element of subset exists in superset
        for (int elem : subset) {
            if (!supersetSet.contains(elem)) {
                return false;
            }
        }
        return true;
    }

List<Integer> subset = Arrays.asList(3, 7, 1);
List<Integer> superset = Arrays.asList(5, 3, 7, 1, 9);

if (isSubset(subset, superset)) {  // True
} else { // Flase  }
```

---------------------------------

## Find below for List Numbers
- `Inegers`: 5 , 3, 7, 1, 9   ==Convert==>   ArrayList: [ 5 , 3, 7, 1, 9]
- ✅ Sum
- ✅ Average
- ✅ Maximum
- ✅ Minimum

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {
        
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter numbers separated by comma:");
        String input = scanner.nextLine();

        String[] items = input.split(",");

        List<Integer> numbers = new ArrayList<>();

        for (String item : items) {
            numbers.add(Integer.parseInt(item.trim()));
        }

        System.out.println("Final Numbers List: " + numbers);

        if (numbers.isEmpty()) {
            System.out.println("List is empty.");
            return;
        }

        // ✅ Sum
        int sum = 0;
        for (int num : numbers) {
            sum += num;
        }

        // ✅ Average
        double average = (double) (sum / numbers.size());

        // ✅ Max and Min
        int max = Collections.max(numbers);
        int min = Collections.min(numbers);

        // Output
        System.out.println("Sum: " + sum);
        System.out.println("Average: " + average);
        System.out.println("Maximum: " + max);
        System.out.println("Minimum: " + min);
    }
}
```

## Remove elements of set2 from set1

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        Set<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));
        Set<Integer> set2 = new HashSet<>(Arrays.asList(3, 4));

        // Remove elements of set2 from set1
        set1.removeAll(set2);

        System.out.println("After removing set2 from set1:");
        System.out.println(set1); // Output: [1, 2, 5]
    }
}

```
------------------------------------------------------

## Sorting  Application:
### numbers sorting

```java
import java.util.*;

public class Test {
    public static void main(String[] args) {

        List<Integer> numbers = new ArrayList<>(Arrays.asList(5, 3, 7, 1, 9));

        Collections.sort(numbers);  // Ascending order
        System.out.println("Sorted List (Ascending): " + numbers); // Modifies original list 'numbers' 
        // OutPut: Sorted List (Ascending): [1, 3, 5, 7, 9]

        Collections.sort(numbers, Collections.reverseOrder());
        System.out.println("Sorted List (Descending): " + numbers); // Modifies original list 'numbers' 
        // OutPut: Sorted List (Descending): [9, 7, 5, 3, 1]
    }
}
```

------------------------------------------------------

## 🇳🇱  sorting of an array of 0s, 1s, and 2s ( Dutch National Flag)
- [2, 0, 2, 1, 1, 0] ==sorting==> [0, 0, 1, 1, 2, 2]

```java
List<Integer> nums = new ArrayList<>(Arrays.asList(2, 0, 2, 1, 1, 0));

// Sort using collections
Collections.sort(nums);

System.out.println(nums);  // [0, 0, 1, 1, 2, 2]
```
------------------------------------------------------

## Sort Application: Two List of numbers contain the same elements i.e. one is a permutation of another?

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> v1 = new ArrayList<>(Arrays.asList(3, 1, 2, 4));
        List<Integer> v2 = new ArrayList<>(Arrays.asList(4, 2, 1, 3));

        if (v1.size() != v2.size()) {
            System.out.println(false);
            return;
        }

        // Sort both lists
        Collections.sort(v1);
        Collections.sort(v2);

        // Compare lists
        boolean result = v1.equals(v2);

        System.out.println("Are both lists permutations of each other? " + result);
        // Output: Are both lists permutations of each other? true
    }
}

```
------------------------------------------------------

## Sort Application: Find 3rd Smallest elm using sorting

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> nums = new ArrayList<>(Arrays.asList(7, 2, 9, 4, 1, 5));

        if (nums.size() < 3) {
            System.out.println("List has less than 3 elements.");
            return;
        }

        // Make a copy to preserve original list
        List<Integer> sortedNums = new ArrayList<>(nums);

        // Sort the copied list
        Collections.sort(sortedNums);

        System.out.println("Smallest: " + sortedNums.get(0));         // Smallest: 1
        System.out.println("Second Smallest: " + sortedNums.get(1));  // Second Smallest: 2
        System.out.println("Third Smallest: " + sortedNums.get(2));   // Third Smallest: 4
    }
}
```
------------------------------------------------------

## Sort Application: Find 3rd largest elm using sorting

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> nums = new ArrayList<>(Arrays.asList(7, 2, 9, 4, 1, 5));

        if (nums.size() < 3) {
            System.out.println("List has less than 3 elements.");
            return;
        }

        // Make a copy to preserve original list
        List<Integer> sortedNums = new ArrayList<>(nums);

        // Reverse sorting (Descending order)
        Collections.sort(sortedNums, Collections.reverseOrder());

        System.out.println("Largest: " + sortedNums.get(0));         // Largest: 9
        System.out.println("Second Largest: " + sortedNums.get(1));  // Second Largest: 7
        System.out.println("Third Largest: " + sortedNums.get(2));   // Third Largest: 5
    }
}
```
------------------------------------------------------
## Sort Application: Find Kth Largest elm in array

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> nums = new ArrayList<>(
                Arrays.asList(7, 2, 9, 4, 1, 5));

        int k = 2; // Change this value for different K

        if (nums.size() < k) {
            System.out.println("List has less than " + k + " elements.");
            return;
        }

        // Make a copy to preserve original list
        List<Integer> sortedNums = new ArrayList<>(nums);

        // Reverse sort (Descending order)
        Collections.sort(sortedNums, Collections.reverseOrder());

        System.out.println("Sorted (Descending): " + sortedNums);
        // Sorted (Descending): [9, 7, 5, 4, 2, 1]

        System.out.println(k + "th Largest Element: " + sortedNums.get(k - 1));
        // If k = 2 → 2th Largest Element: 7
    }
}
```

------------------------------------------

## Min Sum Pair + Max Sum Pair ==>  Two element with minimum sum and maximum sum in a List

- `Input:` [7, 2, 9, 4, 1, 5]
- Output:  MinSum = 1 + 2 = 3  AND Maxsum = 9+7 = 15
- Steps:
```java
  //  At First sort array:  [1, 2, 4, 5, 7, 9] 
 
 // 🔹 Minimum Sum Pair (first two elements)
    int minFirst = sortedNums.get(0);  //1
    int minSecond = sortedNums.get(1); //2
    
    int MinSum = minFirst + minSecond;

// 🔹 Maximum Sum Pair (last two elements)
    int n = sortedNums.size();
    int maxFirst = sortedNums.get(n - 1); // 9
    int maxSecond = sortedNums.get(n - 2); // 7
    
    int Maxsum = maxFirst + maxSecond
```

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> nums = new ArrayList<>(
                Arrays.asList(7, 2, 9, 4, 1, 5));

        if (nums.size() < 2) {
            System.out.println("Error: Array must have at least two elements.");
            return;
        }

        // Make a copy to preserve original list
        List<Integer> sortedNums = new ArrayList<>(nums);

        // Sort ascending
        Collections.sort(sortedNums);

        System.out.println("Sorted List: " + sortedNums);
        // Sorted List: [1, 2, 4, 5, 7, 9]

        // 🔹 Minimum Sum Pair (first two elements)
        int minFirst = sortedNums.get(0);
        int minSecond = sortedNums.get(1);

        System.out.println("Two elements with minimum sum: " 
                + minFirst + " and " + minSecond);
        // Two elements with minimum sum: 1 and 2

        System.out.println("Min Sum: " + (minFirst + minSecond));
        // Min Sum: 3


        // 🔹 Maximum Sum Pair (last two elements)
        int n = sortedNums.size();
        int maxFirst = sortedNums.get(n - 1);
        int maxSecond = sortedNums.get(n - 2);

        System.out.println("Two elements with maximum sum: " 
                + maxFirst + " and " + maxSecond);
        // Two elements with maximum sum: 9 and 7

        System.out.println("Max Sum: " + (maxFirst + maxSecond));
        // Max Sum: 16
    }
}

````
-------------------------------------------------------

## 2-SUM : Given a sorted array, find two numbers that sum up to a target value.

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> nums = Arrays.asList(1, 2, 4, 5, 7, 9);
        int target = 11;

        Set<Integer> seen = new HashSet<>();
        boolean found = false;

        for (int num : nums) {

            int complement = target - num;
            if (seen.contains(complement)) {
                System.out.println("Pair found: " + complement + " and " + num);
                // Pair found: 2 and 9
                found = true;
                break;
            }

            seen.add(num);
        }

        if (!found) {
            System.out.println("No pair found.");
        }
    }
}
```

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        int[] nums = {1, 2, 4, 5, 7, 9};  // Sorted array
        int target = 11;

        int left = 0;
        int right = nums.length - 1;

        boolean found = false;

        while (left < right) {
            int sum = nums[left] + nums[right];

            if (sum == target) {
                System.out.println("Pair found: "  + nums[left] + " and " + nums[right]); // Pair found: 2 and 9
                found = true;
                break;
            }
            else if (sum < target) { left++; }  // Need bigger sum 
            else { right--;  } // Need smaller sum
        }

        if (!found) {
            System.out.println("No pair found.");
        }
    }
}
```
------------------------

## Two Pointer approach Application : Move Zeros to End:
- `Problem:` Move all zeroes in an array to the end while maintaining the relative order of the non-zero elements.
- `Solution:` Use two indexes, one to track the position of non-zero elements and one to traverse the array.

```
[0, 1, 0, 3, 12]
↓
count zeros → 2
remove zeros → [1, 3, 12]
add zeros → [1, 3, 12, 0, 0]
```

```java

import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> list = new ArrayList<>(Arrays.asList(0, 1, 0, 3, 12));

        // Step 1: count zeros
        int zeroCount = Collections.frequency(list, 0);

        // Step 2: remove zeros
        list.removeAll(Collections.singleton(0));

        // Step 3: add zeros at end
        for (int i = 0; i < zeroCount; i++) {
            list.add(0);
        }

        System.out.println(list); // [1, 3, 12, 0, 0]
    }
}

```
------------


##  Even-odd sorter: Even First, Then Odd
- [ 9, 2, 3, 6, 1, 8, 5, 4, 7 ] ===>  Output: [2, 4, 6, 8, 1, 3, 5, 7, 9]
  
```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> nums = new ArrayList<>(Arrays.asList(9, 2, 3, 6, 1, 8, 5, 4, 7));

        // Even first, then odd — ascending inside each group
        nums.sort(
                Comparator
                        .comparingInt((Integer x) -> x % 2)  // Even (0) first, Odd (1) after
                        .thenComparingInt(x -> x)            // Sort ascending within group
        );

        System.out.println(nums);
        // Output: [2, 4, 6, 8, 1, 3, 5, 7, 9]
    }
}
```
--------------------------------------------------
## Sort and Merge Two Arrays

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> arr1 = Arrays.asList(5, 2, 8, 1);
        List<Integer> arr2 = Arrays.asList(3, 8, 6, 1);

        // TreeSet automatically sorts + removes duplicates
        Set<Integer> unique = new TreeSet<>(arr1);

        unique.addAll(arr2);

        // Convert back to List (like vector)
        List<Integer> merged = new ArrayList<>(unique);

        System.out.println("Merged & Sorted:");
        System.out.println(merged);
        // Output: [1, 2, 3, 5, 6, 8]
    }
}

```

------------------------------------

## Union of two List: Using TreeSet (Sorted)

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> arr1 = Arrays.asList(5, 1, 3, 7);
        List<Integer> arr2 = Arrays.asList(2, 3, 6, 7);

        // TreeSet automatically sorts + removes duplicates
        Set<Integer> union = new TreeSet<>();

        union.addAll(arr1);
        union.addAll(arr2);

        System.out.println("Sorted Union:");
        System.out.println(union);
        // Output: [1, 2, 3, 5, 6, 7]
    }
}
```

##  Intersection Using TreeSet (Sorted)

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<Integer> arr1 = Arrays.asList(5, 1, 3, 7);
        List<Integer> arr2 = Arrays.asList(2, 3, 6, 7);

        Set<Integer> set1 = new TreeSet<>(arr1);
        Set<Integer> set2 = new TreeSet<>(arr2);

        // Keep only common elements
        set1.retainAll(set2);

        System.out.println("Sorted Intersection:");
        System.out.println(set1);
        // Output: [3, 7]
    }
}
```

------------------

## Reverse Array in-place using XOR swap (no extra variable)

```java
/*
XOR swap
a = a ^ b
b = a ^ b
a = a ^ b
*/

public class ReverseXOR {

    public static void reverse(int[] arr) {

        int left = 0;
        int right = arr.length - 1;

        while (left < right) {

            // XOR swap
            arr[left] = arr[left] ^ arr[right];
            arr[right] = arr[left] ^ arr[right];
            arr[left] = arr[left] ^ arr[right];

            left++;
            right--;
        }
    }

    public static void main(String[] args) {

        int[] arr = {1, 2, 3, 4, 5, 6};

        reverse(arr);

        for (int n : arr)
            System.out.print(n + " ");
    }
}

// 6 5 4 3 2 1
```
-----------------------------------

## Rotate Array Right by k steps:
```
// Rotate Array Right by 3 steps #--> start of original array
Original : #1 2 3 4 5 6 7
Step 1   : 7 #1 2 3 4 5 6
Step 2   : 6 7 #1 2 3 4 5
Step 3   : 5 6 7 #1 2 3 4

// Rotate Array Left by 2 steps #--> last of original array
Original : 1 2 3 4 5 6 7#
Step 1   : 2 3 4 5 6 7# 1
Step 2   : 3 4 5 6 7# 1 2
```

```java
 List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7));

 int k = 3;
// using built-in utility: rotates right when k is positive.
Collections.rotate(list, k);
// [5, 6, 7, 1, 2, 3, 4]

// Left Rotation pass k = -2 (negative)
Collections.rotate(list, -2);
// [3, 4, 5, 6, 7, 1, 2]

```

-----------------------

## Find the Missing Number in Array/List

```boolean
Input: nums = [3, 0, 1]  output: Missing number in nums[] = 2

Full range XOR   : 0^1^2^3
Array XOR        : 3^0^1
Final XOR        : (0 ^ 1 ^ 2 ^ 3) ^ (3 ^ 0 ^ 1) =  2 (remaining)
```

```java
public class Test {

    public static void main(String[] args) {

        int[] nums = {3, 0, 1};   // missing number = 2

        int A = 0, B = 0;
        int n = nums.length;

        // XOR from 0 to n
        for (int i = 0; i <= n; i++) {
            A ^= i;
        }

        // XOR array elements
        for (int num : nums) {
            B ^= num;
        }

        int missing = A ^ B;

        System.out.println("Missing number = " + missing);  // Missing number = 2
    }
}
```

## 1234 => One Thousand Two Hundred Thirty Four

```java
import java.util.HashMap;
import java.util.Map;

public class SimpleConverter {

    static Map<Integer, String> map = new HashMap<>();

    // Static block runs once -> fills dictionary automatically
    static {
        String[] ones = {
                "", "One", "Two", "Three", "Four", "Five",
                "Six", "Seven", "Eight", "Nine", "Ten",
                "Eleven", "Twelve", "Thirteen", "Fourteen",
                "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"
        };

        String[] tens = {
                "", "", "Twenty", "Thirty", "Forty",
                "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"
        };

        // Fill map using loop
        for (int i = 1; i < ones.length; i++)
            map.put(i, ones[i]);

        for (int i = 2; i < tens.length; i++)
            map.put(i * 10, tens[i]);
    }

    public static void main(String[] args) {
        int number = 1234;
        System.out.println(number + " => " + convertToWords(number));
    }

    public static String convertToWords(int n) {
        String result = "";

        if (n >= 1000) {
            result += map.get(n / 1000) + " Thousand ";
            n %= 1000;
        }

        if (n >= 100) {
            result += map.get(n / 100) + " Hundred ";
            n %= 100;
        }

        if (n > 0) {
            if (n <= 19)
                result += map.get(n);
            else
                result += map.get((n / 10) * 10) + " " + map.getOrDefault(n % 10, "");
        }

        return result.trim();
    }
}
```
