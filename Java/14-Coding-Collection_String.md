## convert User Input Strings into ArrayList:
- `Strings`: "Apple" , "Bananan", "Mango", "Apple"   ==Convert==>   ArrayList: ["Apple", "Bananan", "Mango", "Apple"]

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {
        
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter words separated by comma:");
        String input = scanner.nextLine();

        String[] items = input.split(",");

        ArrayList<String> words = new ArrayList<>();

        for (String item : items) {
            words.add(item.trim());
        }

        System.out.println("ArrayList: " + words);
    }
}

```
-------------------------------------
### String sorting

```java
import java.util.*;

public class Test {

    public static void main(String[] args) {

        List<String> names = new ArrayList<>(
                Arrays.asList("Banana", "Apple", "Mango", "Cherry"));

        System.out.println("Original: " + names);
        // Original: [Banana, Apple, Mango, Cherry]

        // 1️⃣ Ascending (Default - Lexicographical Order)
        Collections.sort(names);
        System.out.println("Ascending: " + names);
        // Ascending: [Apple, Banana, Cherry, Mango]

        // 2️⃣ Descending
        Collections.sort(names, Collections.reverseOrder());
        System.out.println("Descending: " + names);
        // Descending: [Mango, Cherry, Banana, Apple]

        // 3️⃣ Case-Insensitive Sorting
        List<String> names2 = new ArrayList<>(
                Arrays.asList("banana", "Apple", "mango", "Cherry"));

        names2.sort(String.CASE_INSENSITIVE_ORDER);
        System.out.println("Case-Insensitive Sort: " + names2);
        // Case-Insensitive Sort: [Apple, banana, Cherry, mango]

        // 4️⃣ Sort by Length
        names2.sort(Comparator.comparingInt(String::length));
        System.out.println("Sorted by Length: " + names2);
        // Sorted by Length: [Apple, mango, banana, Cherry]
    }
}
````
