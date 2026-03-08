```java
class Student {
    private int id;
    private String name;
    private double scoreGPA; // 1-10

    public Student(int id, String name, double scoreGPA) {
        this.id = id;
        this.name = name;
        this.scoreGPA = scoreGPA;
    }

    // Getters
    public int getId() { return id; }
    public String getName() { return name; }
    public double getScoreGPA() { return scoreGPA; }

    @Override
    public String toString() {
        return "Student{id=" + id + ", name='" + name + "', scoreGPA=" + scoreGPA + "}";
    }
}

```
## Lamda filter example
- Given a Java Student class with fields id, name, and scoreGPA (1–10) and a List<Student>, 
- implement methods to search for students by id, by name, or by scoreGPA exceeding a specified cutoff,
- returning either a single Student or a list of Student objects that match the criteria.
  
```java

import java.util.stream.Collectors;

class StudentUtils {

    // Search by name
    public static List<Student> searchByName(List<Student> students, String name) {
        return students.stream()
                .filter(s -> s.getName().equalsIgnoreCase(name))
                .collect(Collectors.toList());
    }

    // Search by id
    public static Student searchById(List<Student> students, int id) {
        return students.stream()
                .filter(s -> s.getId() == id)
                .findFirst()
                .orElse(null); // returns null if not found
    }

    // Search by GPA cutoff
    public static List<Student> searchByGpaAbove(List<Student> students, double cutoff) {
        return students.stream()
                .filter(s -> s.getScoreGPA() > cutoff)
                .collect(Collectors.toList());
    }
}

````

```java
import java.util.*;
public class Main {
    public static void main(String[] args) {
        List<Student> studentsList = new ArrayList<>();
        studentsList.add(new Student(1, "Alice", 8.5));
        studentsList.add(new Student(2, "Bob", 6.7));
        studentsList.add(new Student(3, "Charlie", 9.1));
        studentsList.add(new Student(4, "Alice", 7.2));

        // Search examples
        System.out.println("Search by name 'Alice': " + StudentUtils.searchByName(studentsList, "Alice"));
        System.out.println("Search by id 2: " + StudentUtils.searchById(studentsList, 2));
        System.out.println("Search by GPA above 7.0: " + StudentUtils.searchByGpaAbove(studentsList, 7.0));
    }
}
```
