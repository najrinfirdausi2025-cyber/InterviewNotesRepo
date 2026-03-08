# Linear Search Or Sequential Search :
- Linear Search is a searching algorithm -- To find key value present or not in arrays -- where -- We check each element one by one Sequential , until we find the key value.
- `Linear/Sequential access or travarsal to array` :
  
<img width="1001" height="471" alt="image" src="https://github.com/user-attachments/assets/5c48543f-b4b3-4a0b-9aa9-e6be17b70935" />
<img width="800" height="427" alt="image" src="https://github.com/user-attachments/assets/66e0fcd7-01d4-4c27-9a90-4d20669a4daa" />

## How It Works:
- Input Array: [10, 20, 30, 40, 50]
- Search Key = 40

```
Step 1 → compare 40 == 10 ? ❌
Step 2 → compare 40 == 20 ? ❌
Step 3 → compare 40 == 30 ? ❌
Step 4 → compare 40 == 40  ? ✔ (found) → @ index 3

It checks elements sequentially.
```

```java
public class Test {

    public static void main(String[] args) {

        int[] arr = {10, 20, 30, 40, 50};

        int key = 40;     // element to search
        int pos = -1;     // default: not found

        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == key) {
                pos = i;
                break;
            }
        }

        if (pos != -1)
            System.out.println("Key found at index: " + pos);
        else
            System.out.println("Key not found");
    }
}

// Key found at index: 3

```

- `key` → element we want to search
- `pos` → stores location
- `break` → stops unnecessary comparisons


--------------------------------------------------------------------------------------

# Binary Search : 
Binary Search is a searching algorithm To find whether a key value is present or not in a `sorted array`
- Where we divide the array into two halves and compare the key with the middle element,
- If the key is smaller, search the left half,
- If the key is greater, search the right half,
- Repeat this process until the key is found or the range becomes empty

## Binary Search access/traversal technique :
- Use `Divide and Conquer approach`
- It does not check elements sequentially
- Binary Search works on sorted data and repeatedly divides the search range in half, -- Making Faster search, then Linear Search.

<img width="985" height="656" alt="image" src="https://github.com/user-attachments/assets/4650d462-1a0c-43e5-ac78-6fb4c121e89c" />
<img width="889" height="487" alt="image" src="https://github.com/user-attachments/assets/dc413f00-bb0a-4b93-b964-b152f07960b3" />
<img width="1782" height="1204" alt="image" src="https://github.com/user-attachments/assets/33c52d64-43b3-4e88-8ea2-a6eb30faf732" />



- InputArray: [10, 20, 30, 40, 50, 60, 70]
- Search key = 50

```
////////////////////////  Step #1  ////////////////////////////////////
low = 0 // Arr starting index 0
high = Arr.size() -1 = 6 // Arr Last index
mid = (low + high)/2  => ( 0 + 6 )/2 =3

 [10, 20, 30] , [40], [50, 60, 70]
  0   1   2      3     4   5    6

Middle = Arr[3] = 40  ==> Now compare key(50) > mid(40) → search right side

//////////////////////////////////// Step #2 ////////////////////////////////////
low =  mid(3) + 1 = 4
high = Arr.size() -1 = 6 // Arr Last index 
mid = (low + high)/2  => ( 4 + 6 )/2 = 5

[50, 60, 70]
 4   5    6

Middle = Arr[5] = 60  ==>  Now compare key(50) < Arr[mid](60) → → search left side

//////////////////////////////////// Step #3 ////////////////////////////////////
low = 4
high = mid(5) -1 = 4
mid = (low + high)/2  => ( 4 + 4 )/2 = 4
Middle = arr[4] =  Now compare key(50) == Arr[mid](50) → Found ✔
```

```java
public class Test {

    public static void main(String[] args) {

        int[] arr = {10, 20, 30, 40, 50, 60, 70};
        int key = 50;

        int low = 0;
        int high = arr.length - 1;
        int pos = -1;

        while (low <= high) {

            int mid = (low + high) / 2;

            if (arr[mid] == key) {
                pos = mid;
                break;
            }
            else if (key > arr[mid]) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }

        if (pos != -1)
            System.out.println("Key found at index: " + pos);
        else
            System.out.println("Key not found");
    }
}
```

## Real World Analogy:


```
Phonebook: [A ... F] [G ... L] [M ... R] [S ... Z]
Search Eliza's phone number?

Step 1: Open middle page: Middle letters = M
Compare: "Eliza" < M  → search LEFT half


Remaining search space:
[A ... F] [G ... L]

Step 2: Find middle again : Middle letters = G
Compare: "Eliza" < G → search LEFT half


Remaining:
[A ... F]

Step 3: Find middle again: Middle letters = C
Compare: "Eliza" > C → search Right half
[A, B] [C] [D, E,F]

Remaining: 
[D, E,F]

Step 4: Middle letters = E
Compare:Eliza page found  →  Eliza matches  FOUND ✅
```
