# Java Collections types

### 1️⃣ Sequential Collection: 
   -  `INDEX based :` ArrayList, Vector
   -  `NON-Index based :` LinkedList 

### 2️⃣ Unique Collection : Set 
  
  - `HashSet :` Unpredictable storing order ( Based on Hashing Function )
  - `LinkedHashSet :` Preserve insertion order
  - `TreeSet :`- Automatically sorted at insertion (Red-Black Balnced BST)
    
### 3️⃣ Key-Value Collection — Separate Hierarchy: Map :
  - `HashMap :` Unpredictable storing order ( Based on Hashing Function )
  - `LinkedHashMap :` Preserve insertion order 
  - `TreeMap :` Automatically sorted at insertion  (Red-Black Balnced BST) ]
### 4️⃣ Data Processing Order Collection: 
  - `FIFO (First-In-First-Out) Processing Order :` PriorityQueue, ArrayDeque
  - `LIFO (Last-In-First-Out) Processing Order :` Stack

----------------------------------------------------------------------------------------------------
# 1️⃣ Sequential Collection: INDEX based

Examples: ArrayList, LinkedList, Vector

__Properties__
- Maintains insertion order
- Allows duplicates
- Index based access
- Dynamic size

__Use case__
- When order matters and duplicate data is allowed

## Fixed Size Array
- Continuous memory block

```java
int[] arr = new int[5];
arr[0] = 10;
arr[1] = 20;
```
- Provide Faster index based random access.
- Maintains insertion order
- Size cannot change after creation.
- You can not insert 6th element in this aaray, It will throw excaption "Out-of-bound"
- Array is not thread safe.


## Dynamic Array:

<img width="500" height="217" alt="image" src="https://github.com/user-attachments/assets/3833efcf-a83c-478f-ada7-7903a87b60e2" />
<img width="1280" height="1510" alt="image" src="https://github.com/user-attachments/assets/fdfcacc3-18d3-478d-ac6f-9ae730f41a36" />

## ArrayList:

ArrayList in Java is a `dynamically resizable` array provided in the `java.util package`. Unlike fixed sized arrays, ArrayList's size `can grow (1.5x grow) or shrink dynamically` as elements are added or removed.

- ArrayList default capacity becomes 10 x size_of_element - on first insertion , and grows by 50% (1.5x) when full.
- Elements can be accessed using their index, just like arrays.
- Duplicate elements are allowed.
- Maintains insertion order
- Elements are stored in the order they are inserted.
- ArrayList is not thread-safe. To make it thread-safe, you must wrap it manually using Collections.synchronizedList().
- Proved Balanced memory usages + performance

```java
import java.util.ArrayList;

ArrayList<Integer> list = new ArrayList<>();
list.add(10);
list.add(20);
list.remove(0);

```
- Resizable automatically.

## Vector :
Vector is a legacy dynamic array in java.util that is synchronized (thread-safe) by default.

<img width="523" height="292" alt="image" src="https://github.com/user-attachments/assets/8c21bb32-9aeb-485b-a406-11c59f80cad3" />



```java
import java.util.Vector;

Vector<Integer> v = new Vector<>();
v.add(10);
v.add(20);
v.add(30);
```
- Default capacity = 10
- Performance: Slower than ArrayList, and wastes memory.
- Multithreaded legacy system.

<img width="1782" height="833" alt="image" src="https://github.com/user-attachments/assets/19bc1e9f-8899-4df4-8cff-4e63436604be" />
<img width="1784" height="8039" alt="image" src="https://github.com/user-attachments/assets/02e5d819-10b8-44a3-b799-a325a1ba44e4" />



### Array is fixed size and fastest but cannot grow.
### ArrayList is dynamic, non-synchronized, and most commonly used.
### Vector is dynamic but synchronized, making it thread-safe but slower, and mostly legacy.

--------------------------------------------


# Linked List:

Like arrays, Linked List is a linear data structure.But linked list elements are not stored at the contiguous location, the elements are linked using pointers as shown below. 


<img width="899" height="188" alt="image" src="https://github.com/user-attachments/assets/c5a57fb9-3b0b-4392-85a3-291a8b2d7797" />
<img width="679" height="251" alt="image" src="https://github.com/user-attachments/assets/7b60fa1b-aa64-474e-825e-33ae3a81c0c6" />

-  Linked List not continuous memory, elements/nodes are scattered in memory, Direct index access not possible , but itterative traversal or access is sequential.

```
 for(Integer n : list)
    System.out.println(n);
```

- `Key Strength of LinkedList:` Adding Element to list shifting is not required as It is required in Array/ArrayList/Vector, we can directly add node at the begining and update head refernce.  

<img width="745" height="333" alt="image" src="https://github.com/user-attachments/assets/7e9c4537-a162-4295-b1b1-5b83729dbd4b" />

- `Doubly linked List:` can travarse both direction ( Left -> right) or (right->left)

<img width="801" height="401" alt="image" src="https://github.com/user-attachments/assets/cc46dc06-cb5e-4239-9a4e-8b6b408de7fe" />


```java
    /* Linked list Node*/
    static class Node {
        int data;
        Node next;

        // Constructor to create a new node
        // Next is by default initialized
        // as null
        Node(int d) { data = d; }
    }
```

```java
class LinkedList {
    Node head; // head of list
    
}
```

- A linked list is a collection of nodes where each node contains data and a reference to the next node. The head pointer stores the first node. Traversal is sequential (O(n)),
- but insertion and deletion are efficient because only pointer manipulation is required.

## Types of LinkedList:
- `Singly Linked List` - Has single - `next` reference link
- `Doubly Linked List` - Has double - `next` and `prev` reference links
- `Circular Linked List` - is a linked list where the last node pointing to the firdt node - and does NOT point to null - Used in Circular Queue / Ring Buffer concept - where data Overwriten after reaching max capacity.

## LinkedList collection in Java offering fast insertion and deletion but slow random access.
LinkedList implements 

```
List interface
Deque interface
```
- It is based on a doubly linked list data structure.
- That means each node contains:
- `| previous ← data → next |`


```java
import java.util.LinkedList;

public class Demo {
    public static void main(String[] args) {

        LinkedList<String> list = new LinkedList<>();

        // Add elements
        list.add("Apple");
        list.add("Banana");
        list.addFirst("Mango");
        list.addLast("Orange");

        System.out.println(list);

        // Access
        System.out.println(list.get(1));

        // Remove
        list.removeFirst();
        list.removeLast();

        System.out.println(list);
    }
}
```

` Usage:`
- LinkedList is bad for random access - so where random index based access required - LinkedList is not used
- LinkedList is used where frequent user data insert/delete operations required on-demand basis.

------------------------------------------------------------------------------- 

##  Binary Search Tree (BST): 

- `Binary Search Tree (BST)` - is a type of binary tree data structure in which each node contains a unique key and satisfies a specific ordering property:

- All nodes in the `left subtree` of a node contain values strictly less than the node’s value.
- All nodes in the `right subtree` of a node contain values strictly greater than the node’s value.
- __`LeftValue < RootValue < RightValue`__

 <img width="1200" height="600" alt="image" src="https://github.com/user-attachments/assets/09db9a49-707b-426f-86eb-b3b6acfb80a3" />
<img width="1001" height="471" alt="image" src="https://github.com/user-attachments/assets/67acb1ea-f28d-4605-a8af-24eef8f2621e" />
<img width="2100" height="1500" alt="image" src="https://github.com/user-attachments/assets/4dcf88d3-9034-412f-8cd4-ef8cbb1772b2" />


  
## Red-Black Tree Rules (Very Important)

- `Red-Black Tree:` - A Red-Black Tree (RBT) is a self-balancing Binary Search Tree, enabling Faster search algo, insertion, and deletion operations in O(logN) time, unlike standard binary search trees which can take O(N) time.
- `RED-BLCAK color:` Each node has an additional attribute: a color, which can be either red or black.
- These colors are used to maintain balance during insertions and deletions, ensuring efficient data retrieval and manipulation.

After every insertion (or deletion) it automatically fixes itself using recoloring + rotations so that the tree height always stays O(log n). Every time you insert a node, these 5 properties must always hold: 

- Every node is either RED or BLACK
- The root is always BLACK
- 🔴 New node is ALWAYS inserted as RED , Because inserting BLACK would change black-height of all paths.
- No two RED nodes can be adjacent (Red node cannot have Red parent or Red child)
- Every path from node → NULL has same number of BLACK nodes (Black Height property)
- NULL leaves are considered BLACK

👉 After inserting a node, if any rule breaks → we fix using Recoloring or Rotation


<img width="688" height="505" alt="image" src="https://github.com/user-attachments/assets/a43f5b76-d92c-416f-b419-7f894f15aabf" />
<img width="876" height="760" alt="image" src="https://github.com/user-attachments/assets/072180d3-cc08-44f2-9608-e89e05a155e9" />

--------------------------------------------------------------------
## Hashing :

1️⃣ Concept

- In Java HashMap (or HashSet), each key is stored in a “bucket” inside an array.
- Array insertion index = Position : which bucket the key belongs to.

To compute the index, we use: HashFunction()

__HashFunction:__
```java
index = HashFunction(key, tableSize) {
 int idx = key.hashCode() % tableSize
 return idx;
}

// hashCode ---> Java’s way of converting a key object to an integer.
// table size ---> the number of buckets (array length).

ArrayList[index] = Node(key1->value1)  // Node(key1->value1) inserted in @index of ArrayList
```

Example: Hotel Layout
- Each floor has 3 rooms:

- `1st Floor:` → R101 R102 R103
- `2nd Floor:` → R201 R202 R203
- `3rd Floor:` → R301 R302 R303

## Separate Chaining (Linked List inside each drawer)
```
Drawer[1]: [R101 | Guest A] , [R201 | Guest D], [R301 | Guest G]
Drawer[2]: [R102 | Guest B], [R202 | Guest E], [R302 | Guest H]
Drawer[3]: [R103 | Guest C], [R203 | Guest F], [R303 | Guest I]
```

```
// Let's asume We have a fixed-size array (say 16 buckets).
// The hashCode of a key can be any integer (positive or negative, huge numbers).

String key = "R101";
int tableSize = 10;

index = HashFunction("R101", 16) 

// hashCode = key.hashCode();  // asume hashCode = 101
// index = hashCode % tableSize;  // 101 % 10 = 1

✅ So "R101" goes into bucket 1.

ArrayList[1] = Node("R101" -> "Guest A") --> Node("R201" -> "Guest D") --> Node("R301" -> "Guest G")
ArrayList[2] = Node("R102" -> "Guest B") --> Node("R202" -> "Guest E") --> Node("R302" -> "Guest H")
ArrayList[3] = Node("R103" -> "Guest C") --> Node("R203" -> "Guest F") --> Node("R303" -> "Guest I")

```
<img width="686" height="386" alt="image" src="https://github.com/user-attachments/assets/a8d652e1-ced1-40fa-b444-3b767884e7e4" />

```
- 1. Compute hash of key.
- 2.  Compute bucket index from hash
- 3. Check if key already exists in the bucket:
     - If yes → update value.
     - If no →  create new Node:
           - If bucket empty → directly add Node.
                 - if collsion occured:
   
                  - Approach 1: Separate Chaining:
                               <1a> create Linked list for the bucket, for ≤ 8 entries in a bucket
                               <1b> convert to Red-Black Tree for > 8 entries for faster search.
       
                  - Approach 2: Open Addressing or Double Hashing:
                                 index next bucket as =  HashFuntion1(key) + [i * HashFuntion2(key) ]
           - If bucket has nodes → add Node at head (or in tree if converted).
       
- 4. Resize check:
          - If size > threshold (lets say 12), the table resizes (doubles array size + Rehash all existing entries into new buckets)

- 5. Iterates over buckets from 0 → (n-1) and within bucket nodes.
        - If bucket converted to tree → iterates tree nodes in order.
```

---------------------------------------------------------


__Hash Map Inetrface:__

```java
Node ( key | value | link) 
ArrayList[1] = Node("R101" -> "Guest A") --> Node("R201" -> "Guest D") --> Node("R301" -> "Guest G")
ArrayList[2] = Node("R102" -> "Guest B") --> Node("R202" -> "Guest E") --> Node("R302" -> "Guest H")
ArrayList[3] = Node("R103" -> "Guest C") --> Node("R203" -> "Guest F") --> Node("R303" -> "Guest I")
```

__Hash Set Interface:__

```java
Node ( value | link) 
ArrayList[1] = Node("Guest A") --> Node("Guest D") --> Node("Guest G")
ArrayList[2] = Node("Guest B") --> Node("Guest E") --> Node("Guest H")
ArrayList[3] = Node("Guest C") --> Node("Guest F") --> Node("Guest I")
```

----------------------------------------------------------------------------
## 2️⃣ Set (Unique Collection)

- Examples: HashSet, LinkedHashSet, TreeSet

__Properties:__

- No duplicates allowed
- No index
- Faster search
- Used for uniqueness

- `HashSet` ==== > store value in `Unpredictable order` at insertion, Order may change after rehashing.
- `LinkedHashSet` ====> Manintain The `Insertion order`, Elements appear exactly as inserted
- `TreeSet` ===> Manintain Automatically `sorted order` at insertion 

__HashSet:__
```java
Set<Integer> set = new HashSet<>();
set.add(30);
set.add(10);
set.add(10); // ignored -as it is a duplicate
set.add(20);
System.out.println(set); // [20, 30, 10]
```
__LinkedHashSet:__

```java
Set<Integer> set = new LinkedHashSet<>();
set.add(30);
set.add(10);
set.add(10); // ignored -as it is a duplicate
set.add(20);
System.out.println(set); // [30, 10, 20]
```
__TreeSet:__ : Uses Red-Black Tree (Self-balancing BST), BST = Binary Search Tree

```java
Set<Integer> set = new TreeSet<>(); 
set.add(30);
set.add(10);
set.add(20);
System.out.println(set); // [10, 20, 30]
```

-------------------------------------------------------------------

## 3️⃣ Key-Value Collection — Separate Hierarchy: Map type

- Examples: HashMap, LinkedHashMap, TreeMap

__Properties:__

- Stores key-value pairs
- Keys unique
- Values duplicate allowed
- Not part of Collection interface

```java
Map<Integer,String> map = new HashMap<>();
map.put(1,"A");
map.put(1,"B"); // replaces value
```
----------------------------------------------------------------------------------------

## 4️⃣ Processing Order Collection: FIFO and LIFO order
- `FIFO (First-In-First-Out) Processing Order :` PriorityQueue, ArrayDeque
- `LIFO (Last-In-First-Out) Processing Order :` Stack

__FIFO order collections:  PriorityQueue, ArrayDeque Properties:__

- FIFO processing: 👉 First inserted element comes out first, 👉 Like a ticket counter line
- No random access

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/64e6da49-bda4-424a-addf-1aa8d3c85a9c" />


__Used in:__

- Task scheduling
- Request processing
- Printer queue
- BFS traversal

__ArrayDeque:__
- ✔ __First inserted__ → __First removed__
```java
import java.util.*;

public class Test {
    public static void main(String[] args) {

        Queue<String> queue = new ArrayDeque<>();
        queue.add("A");
        queue.add("B");
        queue.add("C");

        System.out.println(queue.poll()); // removes A First, then
        System.out.println(queue.poll()); // removes B ,then
        System.out.println(queue.poll()); // removes C 
    }
}
```

## Special FIFO — Sorted FIFO

- It does NOT follow insertion order
- It follows priority (smallest first)

```java
import java.util.*;

public class Test {

        public static void main(String[] args) {
            
        
        class Task implements Comparable<Task> {
    
            String task_name;
            int task_priority;
        
            public Task(String name, int priority) {
                this.task_name = name;
                this.task_priority = priority;
            }
        
            // Define priority logic
            @Override
            public int compareTo(Task other) {
                return this.task_priority - other.task_priority; // smaller value = higher priority
            }
        
            @Override
            public String toString() {
                return task_name + " (Priority " + task_priority + ")";
            }
        }



        PriorityQueue<Task> pq = new PriorityQueue<>();

        pq.add(new Task("Fix Production Bug", 1));
        pq.add(new Task("Code Review", 3));
        pq.add(new Task("Write Documentation", 4));
        pq.add(new Task("Team Meeting", 2));

        System.out.println("Processing tasks by priority:");
        while (!pq.isEmpty()) {
            System.out.println(pq.poll());
        }
    }
}
```
- ✔ __Removed by priority, not insertion order.__
```
Processing tasks by priority:
Fix Production Bug (Priority 1)
Team Meeting (Priority 2)
Code Review (Priority 3)
Write Documentation (Priority 4)
```

## LIFO — Last In First Out (Stack behavior):
- 👉 Last inserted element comes out first
- 👉 Like a plate stack
<img width="1438" height="479" alt="image" src="https://github.com/user-attachments/assets/1f57e7fc-848b-485c-9719-ab85261f3e3f" />

<img width="1478" height="1238" alt="image" src="https://github.com/user-attachments/assets/54b2aa35-445a-4a5a-8e63-64f638e5bfe2" />

```
Push: A → B → C → D
Pop : D → C → B → A
```

__Used in:__

- Undo operation
- Recursion/Backtracking
- Function call stack
- DFS traversal

```java
import java.util.*;

public class Test {
    public static void main(String[] args) {

        Stack<String> stack = new Stack<>();

        stack.push("A");
        stack.push("B");
        stack.push("C");

        System.out.println(stack.pop()); // C
        System.out.println(stack.pop()); // B
        System.out.println(stack.pop()); // A
    }
}
```
✔ __Last inserted → First removed__

## Stack vs Queue :

<img width="355" height="142" alt="image" src="https://github.com/user-attachments/assets/03bba76a-dbf0-423c-aa77-030800385905" />
<img width="755" height="534" alt="image" src="https://github.com/user-attachments/assets/32d3a8d2-d15e-49d7-9970-9d34eb6e8c6b" />

