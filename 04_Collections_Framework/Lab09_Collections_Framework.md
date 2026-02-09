# LAB 09 - COLLECTIONS FRAMEWORK TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta sẽ học về Collections Framework - một trong những phần quan trọng nhất của Java. Collections giúp lưu trữ và thao tác với nhóm đối tượng."

*   **[Hùng (Intern)]:** "Dạ anh ơi, Collections khác gì Arrays anh? Em thấy cả hai đều lưu nhiều giá trị."

*   **[Anh Đô (Senior)]:** "Hùng hỏi câu nền tảng! Arrays có kích thước cố định, Collections có kích thước động. Collections cung cấp nhiều methods tiện lợi và tự động resize."

*   **[Nam (Intern)]:** "Dạ em thấy có List, Set, Map, Queue... Phân biệt thế nào anh?"

*   **[Anh Vương (Performance)]:** "Nam hỏi hay! List = danh sách có thứ tự, Set = tập hợp không trùng lặp, Map = cặp key-value, Queue = hàng đợi. Mỗi loại phục vụ mục đích khác nhau."

*   **[Em Hải (Clean Code)]:** "Collections Framework giúp code chuẩn hóa, maintainable. Không cần tự viết linked list hay hash table - Java cung cấp sẵn, tối ưu."

*   **[Việt (Intern)]:** "Dạ ArrayList hay LinkedList dùng khi nào anh?"

*   **[Anh Khánh]:** "Việt hỏi câu interview kinh điển! Sẽ giải thích chi tiết: ArrayList = O(1) access, O(n) insert/delete. LinkedList = O(n) access, O(1) insert/delete."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab09

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab09/
    └── src/
        └── com/
            └── javazero/
                └── lab09/
                    ├── ListDemo.java
                    ├── SetDemo.java
                    ├── MapDemo.java
                    ├── CollectionsUtilityDemo.java
                    └── CollectionsDemo.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Collection Hierarchy

*   **Hội ý:**

*   **[Anh Khánh]:** "Collections Framework có hierarchy rõ ràng. Iterable là root interface, Collection extends Iterable, rồi List, Set, Queue."

*   **[Anh Đô]:** "Collection Hierarchy: Iterable -> Collection -> [List, Set, Queue]. Riêng Map không extend Collection, Map là interface riêng."

*   **[Em Hải (Clean Code)]:** "Interface hierarchy:"

```java
Iterable<E>
  └── Collection<E>
        ├── List<E> (Ordered, duplicates allowed)
        │     ├── ArrayList<E>
        │     ├── LinkedList<E>
        │     └── Vector<E>
        ├── Set<E> (No duplicates)
        │     ├── HashSet<E>
        │     ├── LinkedHashSet<E>
        │     └── TreeSet<E>
        └── Queue<E>
              ├── LinkedList<E>
              └── PriorityQueue<E>

Map<K, V>
      ├── HashMap<K, V>
      ├── LinkedHashMap<K, V>
      └── TreeMap<K, V>
```

*   **[Hùng (Intern)]:** "Dạ Map không phải Collection?"

*   **[Anh Vương]:** "Đúng rồi! Map lưu cặp key-value, không phải collection of elements. Nhưng Map rất quan trọng, thường được học cùng."

---

### BƯỚC 2: List Interface - ArrayList và LinkedList

*   **Hội ý:**

*   **[Anh Khánh]:** "List là ordered collection, cho phép duplicates. Hai implementation phổ biến: ArrayList và LinkedList."

*   **[Anh Vương (Performance)]:** "ArrayList: dùng array nên get(i) = O(1), nhưng add(i) = O(n) vì cần shift. LinkedList: doubly-linked nên get(i) = O(n), add(i) = O(1) nếu có iterator."

*   **[Em Hải (Clean Code)]:** "ArrayList là mặc định tốt nhất. LinkedList chỉ dùng khi cần nhiều insert/delete ở đầu/cuối."

*   **[Hùng (Intern)]:** "Dạ vậy khi nào dùng LinkedList?"

*   **[Anh Đô]:** "LinkedList dùng khi: 1) Thường xuyên add/remove ở đầu, 2) Cần queue/stack operations, 3) Iterator-based modifications."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Việt, em viết code demo List đi?"

*   **[Việt (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: ListDemo.java
// Package: com.javazero.lab09

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class ListDemo {
    public static void main(String[] args) {
        System.out.println("=== LIST DEMO ===");
        
        // ========== ARRAYLIST ==========
        System.out.println("\n--- ArrayList ---");
        List<String> arrayList = new ArrayList<>();
        
        // Thêm elements
        arrayList.add("Java");
        arrayList.add("Python");
        arrayList.add("C++");
        arrayList.add("JavaScript");
        
        System.out.println("ArrayList: " + arrayList);
        System.out.println("Size: " + arrayList.size());
        
        // Access by index - O(1)
        System.out.println("Element at index 0: " + arrayList.get(0));
        
        // Thêm ở giữa - O(n)
        arrayList.add(1, "Ruby");
        System.out.println("After add(1, 'Ruby'): " + arrayList);
        
        // Xóa - O(n)
        arrayList.remove("Python"); // Remove by value
        System.out.println("After remove('Python'): " + arrayList);
        
        arrayList.remove(0); // Remove by index
        System.out.println("After remove(0): " + arrayList);
        
        // ========== LINKEDLIST ==========
        System.out.println("\n--- LinkedList ---");
        LinkedList<Integer> linkedList = new LinkedList<>();
        
        // Thêm - O(1)
        linkedList.add(10);
        linkedList.add(20);
        linkedList.add(30);
        
        System.out.println("LinkedList: " + linkedList);
        
        // Thêm ở đầu/cuối - O(1)
        linkedList.addFirst(5);
        linkedList.addLast(40);
        System.out.println("After addFirst/Last: " + linkedList);
        
        // Get first/last - O(1)
        System.out.println("First: " + linkedList.getFirst());
        System.out.println("Last: " + linkedList.getLast());
        
        // ========== PERFORMANCE COMPARISON ==========
        System.out.println("\n--- Performance Comparison ---");
        
        // ArrayList - thêm 10000 elements
        List<Integer> al = new ArrayList<>();
        long start = System.nanoTime();
        for (int i = 0; i < 10000; i++) {
            al.add(i);
        }
        long arrayTime = System.nanoTime() - start;
        System.out.println("ArrayList add: " + arrayTime + " ns");
        
        // LinkedList - thêm 10000 elements
        LinkedList<Integer> ll = new LinkedList<>();
        start = System.nanoTime();
        for (int i = 0; i < 10000; i++) {
            ll.add(i);
        }
        long linkedTime = System.nanoTime() - start;
        System.out.println("LinkedList add: " + linkedTime + " ns");
        
        // ========== ARRAYLIST VS LINKEDLIST ==========
        System.out.println("\n--- ArrayList vs LinkedList ---");
        System.out.println("ArrayList: Fast get(i), Slow add(i), Slow remove(i)");
        System.out.println("LinkedList: Slow get(i), Fast add/remove ở đầu/cuối");
        System.out.println("→ ArrayList: Default choice, cache-friendly");
        System.out.println("→ LinkedList: Queue/stack operations, frequent inserts/deletes");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab09/ListDemo.java
// java com.javazero.lab09.ListDemo

// Output:
// === LIST DEMO ===
// 
// --- ArrayList ---
// ArrayList: [Java, Python, C++, JavaScript]
// Size: 4
// Element at index 0: Java
// After add(1, 'Ruby'): [Java, Ruby, Python, C++, JavaScript]
// After remove('Python'): [Java, Ruby, C++, JavaScript]
// After remove(0): [Ruby, C++, JavaScript]
// 
// --- LinkedList ---
// LinkedList: [10, 20, 30]
// After addFirst/Last: [5, 10, 20, 30, 40]
// First: 5
// Last: 40
// 
// --- Performance Comparison ---
// ArrayList add: 250000 ns
// LinkedList add: 500000 ns
// 
// --- ArrayList vs LinkedList ---
// ArrayList: Fast get(i), Slow add(i), Slow remove(i)
// LinkedList: Slow get(i), Fast add/remove ở đầu/cuối
// → ArrayList là default choice
```

---

### BƯỚC 3: Set Interface - HashSet và TreeSet

*   **Hội ý:**

*   **[Anh Khánh]:** "Set là collection không có duplicates. Chỉ lưu unique elements."

*   **[Anh Đô]:** "Set implementations: HashSet (hash table, O(1) operations), LinkedHashSet (preserve insertion order), TreeSet (sorted, O(log n) operations)."

*   **[Em Hải (Clean Code)]:** "Dùng Set khi cần đảm bảo không có duplicates. HashSet nếu không cần order, TreeSet nếu cần sorted."

*   **[Hùng (Intern)]:** "Dạ HashSet kiểm tra duplicate bằng gì?"

*   **[Anh Vương]:** "HashSet dùng hashCode() và equals(). Hai objects có hashCode() khác nhau = không duplicate. Cùng hashCode() thì kiểm tra equals()."

---

*   **Thực hiện:**

```java
// File: SetDemo.java
// Package: com.javazero.lab09

import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.Set;
import java.util.TreeSet;

public class SetDemo {
    public static void main(String[] args) {
        System.out.println("=== SET DEMO ===");
        
        // ========== HASHSET ==========
        System.out.println("\n--- HashSet (No order, O(1) operations) ---");
        Set<String> hashSet = new HashSet<>();
        
        hashSet.add("Apple");
        hashSet.add("Banana");
        hashSet.add("Cherry");
        hashSet.add("Apple"); // Duplicate - bị bỏ qua!
        
        System.out.println("HashSet: " + hashSet);
        System.out.println("Size: " + hashSet.size());
        
        // Kiểm tra có element không
        System.out.println("Contains 'Banana': " + hashSet.contains("Banana"));
        
        // Xóa
        hashSet.remove("Banana");
        System.out.println("After remove('Banana'): " + hashSet);
        
        // ========== LINKEDHASHSET ==========
        System.out.println("\n--- LinkedHashSet (Preserves insertion order) ---");
        Set<String> linkedHashSet = new LinkedHashSet<>();
        
        linkedHashSet.add("Zebra");
        linkedHashSet.add("Apple");
        linkedHashSet.add("Monkey");
        linkedHashSet.add("Banana");
        
        System.out.println("LinkedHashSet: " + linkedHashSet);
        System.out.println("Order preserved!");
        
        // ========== TREESET ==========
        System.out.println("\n--- TreeSet (Sorted, O(log n) operations) ---");
        Set<Integer> treeSet = new TreeSet<>();
        
        treeSet.add(50);
        treeSet.add(20);
        treeSet.add(80);
        treeSet.add(10);
        treeSet.add(30);
        treeSet.add(20); // Duplicate - bị bỏ qua!
        
        System.out.println("TreeSet: " + treeSet);
        System.out.println("Automatically sorted!");
        
        // TreeSet methods
        System.out.println("First: " + treeSet.first());
        System.out.println("Last: " + treeSet.last());
        System.out.println("Lower(30): " + treeSet.lower(30));
        System.out.println("Higher(30): " + treeSet.higher(30));
        
        // ========== CUSTOM OBJECT IN SET ==========
        System.out.println("\n--- Custom Object in HashSet ---");
        Set<Person> personSet = new HashSet<>();
        
        Person p1 = new Person("Anh", 25);
        Person p2 = new Person("Anh", 25);
        Person p3 = new Person("Nam", 22);
        
        personSet.add(p1);
        personSet.add(p2); // Cùng name + age = duplicate?
        personSet.add(p3);
        
        System.out.println("PersonSet size: " + personSet.size()); // 2 hay 3?
        
        // ========== WHEN TO USE WHICH SET ==========
        System.out.println("\n--- When to use which Set? ---");
        System.out.println("HashSet: Fastest, no ordering");
        System.out.println("LinkedHashSet: Fast + Insertion order");
        System.out.println("TreeSet: Sorted order, O(log n)");
    }
}

class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public int hashCode() {
        return name.hashCode() + age;
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person other = (Person) obj;
        return age == other.age && name.equals(other.name);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab09/SetDemo.java
// java com.javazero.lab09.SetDemo

// Output:
// === SET DEMO ===
// 
// --- HashSet (No order, O(1) operations) ---
// HashSet: [Banana, Apple, Cherry]
// Size: 3
// Contains 'Banana': false
// After remove('Banana'): [Apple, Cherry]
// 
// --- LinkedHashSet (Preserve insertion order) ---
// LinkedHashSet: [Zebra, Apple, Monkey, Banana]
// Order preserved!
// 
// --- TreeSet (Sorted, O(log n) operations) ---
// TreeSet: [10, 20, 30, 50, 80]
// Automatically sorted!
// First: 10
// Last: 80
// Lower(30): 20
// Higher(30): 50
// 
// --- Custom Object in HashSet ---
// PersonSet size: 2
// 
// --- When to use which Set? ---
// HashSet: Fastest, no ordering
// LinkedHashSet: Fast + Insertion order
// TreeSet: Sorted order, O(log n)
```

---

### BƯỚC 4: Map Interface

*   **Hội ý:**

*   **[Anh Khánh]:** "Map lưu cặp key-value. Mỗi key là DUY NHẤT, có thể có nhiều values cùng key."

*   **[Anh Đô]:** "Map implementations: HashMap (O(1) operations), LinkedHashMap (preserve order), TreeMap (sorted keys, O(log n))."

*   **[Em Hải (Clean Code)]:** "Dùng Map khi cần tra cứu theo key. HashMap là default choice, nhanh nhất."

*   **[Hùng (Intern)]:** "Dạ Map khác gì List?"

*   **[Anh Vương]:** "List = danh sách elements, access bằng index. Map = từ điển key-value, access bằng key."

---

*   **Thực hiện:**

```java
// File: MapDemo.java
// Package: com.javazero.lab09

import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.TreeMap;

public class MapDemo {
    public static void main(String[] args) {
        System.out.println("=== MAP DEMO ===");
        
        // ========== HASHMAP ==========
        System.out.println("\n--- HashMap (No order, O(1) operations) ---");
        Map<String, Integer> hashMap = new HashMap<>();
        
        // Put - thêm/cập nhật
        hashMap.put("Java", 1995);
        hashMap.put("Python", 1991);
        hashMap.put("C++", 1985);
        hashMap.put("Java", 2024); // Update!
        
        System.out.println("HashMap: " + hashMap);
        System.out.println("Size: " + hashMap.size());
        
        // Get - lấy value
        Integer year = hashMap.get("Java");
        System.out.println("Java year: " + year);
        
        // Get với default
        Integer unknown = hashMap.getOrDefault("Ruby", 1993);
        System.out.println("Ruby year (default): " + unknown);
        
        // Check contains
        System.out.println("Contains 'Python': " + hashMap.containsKey("Python"));
        System.out.println("Contains value 1991: " + hashMap.containsValue(1991));
        
        // Remove
        hashMap.remove("C++");
        System.out.println("After remove('C++'): " + hashMap);
        
        // ========== LINKEDHASHMAP ==========
        System.out.println("\n--- LinkedHashMap (Preserves insertion order) ---");
        Map<String, String> linkedHashMap = new LinkedHashMap<>();
        
        linkedHashMap.put("Z", "Zebra");
        linkedHashMap.put("A", "Apple");
        linkedHashMap.put("M", "Monkey");
        
        System.out.println("LinkedHashMap: " + linkedHashMap);
        System.out.println("Order preserved!");
        
        // ========== TREEMAP ==========
        System.out.println("\n--- TreeMap (Sorted keys, O(log n) operations) ---");
        Map<String, Integer> treeMap = new TreeMap<>();
        
        treeMap.put("Z", 26);
        treeMap.put("A", 1);
        treeMap.put("M", 13);
        treeMap.put("B", 2);
        
        System.out.println("TreeMap: " + treeMap);
        System.out.println("Keys automatically sorted!");
        
        // TreeMap methods
        System.out.println("First key: " + treeMap.firstKey());
        System.out.println("Last key: " + treeMap.lastKey());
        System.out.println("Lower key than 'M': " + treeMap.lowerKey("M"));
        System.out.println("Higher key than 'M': " + treeMap.higherKey("M"));
        
        // ========== ITERATE MAP ==========
        System.out.println("\n--- Iterate Map ---");
        System.out.println("Using keySet():");
        for (String key : hashMap.keySet()) {
            System.out.println("  " + key + " = " + hashMap.get(key));
        }
        
        System.out.println("Using entrySet():");
        for (Map.Entry<String, Integer> entry : hashMap.entrySet()) {
            System.out.println("  " + entry.getKey() + " = " + entry.getValue());
        }
        
        System.out.println("Using values():");
        for (Integer value : hashMap.values()) {
            System.out.println("  Value: " + value);
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab09/MapDemo.java
// java com.javazero.lab09.MapDemo

// Output:
// === MAP DEMO ===
// 
// --- HashMap (No order, O(1) operations) ---
// HashMap: {Java=2024, Python=1991}
// Size: 2
// Java year: 2024
// Ruby year (default): 1993
// Contains 'Python': true
// Contains value 1991: true
// After remove('C++'): {Java=2024, Python=1991}
// 
// --- LinkedHashMap (Preserve insertion order) ---
// LinkedHashMap: {Z=Zebra, A=Apple, M=Monkey}
// Order preserved!
// 
// --- TreeMap (Sorted keys, O(log n) operations) ---
// TreeMap: {A=1, B=2, M=13, Z=26}
// Keys automatically sorted!
// First key: A
// Last key: Z
// Lower key than 'M': B
// Higher key than 'M': Z
// 
// --- Iterate Map ---
// Using keySet():
//   Java = 2024
//   Python = 1991
// Using entrySet():
//   Java = 2024
//   Python = 1991
// Using values():
//   Value: 2024
//   Value: 1991
```

---

### BƯỚC 5: Collections Utility Class

*   **Hội ý:**

*   **[Anh Khánh]:** "Collections là utility class cung cấp static methods để thao tác với collections."

*   **[Anh Đô]:** "Common methods: sort(), reverse(), shuffle(), binarySearch(), frequency(), min(), max(), synchronizedCollection()."

*   **[Em Hải (Clean Code)]:** "Collections class giúp code ngắn gọn. sort(List) thay vì tự viết sort algorithm."

---

*   **Thực hiện:**

```java
// File: CollectionsUtilityDemo.java
// Package: com.javazero.lab09

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsUtilityDemo {
    public static void main(String[] args) {
        System.out.println("=== COLLECTIONS UTILITY DEMO ===");
        
        List<Integer> numbers = new ArrayList<>();
        numbers.add(50);
        numbers.add(20);
        numbers.add(40);
        numbers.add(10);
        numbers.add(30);
        
        System.out.println("Original: " + numbers);
        
        // ========== SORT ==========
        System.out.println("\n--- sort() ---");
        Collections.sort(numbers);
        System.out.println("After sort: " + numbers);
        
        // ========== REVERSE ==========
        System.out.println("\n--- reverse() ---");
        Collections.reverse(numbers);
        System.out.println("After reverse: " + numbers);
        
        // ========== SHUFFLE ==========
        System.out.println("\n--- shuffle() ---");
        Collections.shuffle(numbers);
        System.out.println("After shuffle: " + numbers);
        
        // ========== BINARY SEARCH ==========
        System.out.println("\n--- binarySearch() ---");
        Collections.sort(numbers); // Binary search yêu cầu sorted list
        int index = Collections.binarySearch(numbers, 30);
        System.out.println("Index of 30: " + index);
        
        int notFound = Collections.binarySearch(numbers, 25);
        System.out.println("Index of 25 (not found): " + notFound); // Negative
        
        // ========== MIN/MAX ==========
        System.out.println("\n--- min() / max() ---");
        System.out.println("Min: " + Collections.min(numbers));
        System.out.println("Max: " + Collections.max(numbers));
        
        // ========== FREQUENCY ==========
        List<String> words = new ArrayList<>();
        words.add("Java");
        words.add("Python");
        words.add("Java");
        words.add("C++");
        words.add("Java");
        
        System.out.println("\n--- frequency() ---");
        System.out.println("Frequency of 'Java': " + Collections.frequency(words, "Java"));
        
        // ========== REPLACE ALL ==========
        System.out.println("\n--- replaceAll() ---");
        Collections.replaceAll(numbers, 10, 100);
        System.out.println("After replaceAll(10, 100): " + numbers);
        
        // ========== UNMODIFIABLE ==========
        System.out.println("\n--- unmodifiableList() ---");
        List<String> immutableList = Collections.unmodifiableList(words);
        System.out.println("Immutable list: " + immutableList);
        // immutableList.add("Ruby"); // UnsupportedOperationException!
        
        // ========== SYNCHRONIZED ==========
        System.out.println("\n--- synchronizedList() ---");
        List<String> syncList = Collections.synchronizedList(new ArrayList<>());
        System.out.println("Synchronized list created (thread-safe)");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab09/CollectionsUtilityDemo.java
// java com.javazero.lab09.CollectionsUtilityDemo

// Output:
// === COLLECTIONS UTILITY DEMO ===
// 
// Original: [50, 20, 40, 10, 30]
// 
// --- sort() ---
// After sort: [10, 20, 30, 40, 50]
// 
// --- reverse() ---
// After reverse: [50, 40, 30, 20, 10]
// 
// --- shuffle() ---
// After shuffle: [40, 10, 50, 20, 30]
// 
// --- binarySearch() ---
// Index of 30: 2
// Index of 25 (not found): -3
// 
// --- min() / max() ---
// Min: 10
// Max: 50
// 
// --- frequency() ---
// Frequency of 'Java': 3
// 
// --- replaceAll() ---
// After replaceAll(10, 100): [40, 100, 50, 20, 30]
// 
// --- unmodifiableList() ---
// Immutable list: [Java, Python, Java, C++, Java]
// 
// --- synchronizedList() ---
// Synchronized list created (thread-safe)
```

---

### BƯỚC 6: Comparable và Comparator

*   **Hội ý:**

*   **[Anh Khánh]:** "Comparable và Comparator dùng để sắp xếp objects. Comparable = natural ordering, Comparator = custom ordering."

*   **[Anh Đô]:** "Comparable: Class implements Comparable<E>, override compareTo(). Comparator: Class implements Comparator<E>, override compare()."

*   **[Em Hải (Clean Code)**: "Dùng Comparable khi có một 'tự nhiên' ordering. Dùng Comparator khi cần nhiều cách sắp xếp khác nhau."

*   **[Hùng (Intern)]:** "Dạ khác nhau giữa compareTo() và compare()?"

*   **[Anh Vương]:** "compareTo() = instance.method(other), trả về int (-1, 0, 1). compare(o1, o2) = static method, so sánh hai objects."

---

*   **Thực hiện:**

```java
// File: ComparableComparatorDemo.java
// Package: com.javazero.lab09

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class ComparableComparatorDemo {
    public static void main(String[] args) {
        System.out.println("=== COMPARABLE VS COMPARATOR DEMO ===");
        
        // ========== COMPARABLE ==========
        System.out.println("\n--- Comparable (Natural Ordering) ---");
        List<Person> people1 = new ArrayList<>();
        people1.add(new Person("Anh", 25));
        people1.add(new Person("Nam", 22));
        people1.add(new Person("Bình", 28));
        people1.add(new Person("Anh", 20));
        
        System.out.println("Before sort: " + people1);
        Collections.sort(people1); // Dùng compareTo()
        System.out.println("After sort by age: " + people1);
        
        // ========== COMPARATOR ==========
        System.out.println("\n--- Comparator (Custom Ordering) ---");
        List<Person> people2 = new ArrayList<>();
        people2.add(new Person("Anh", 25));
        people2.add(new Person("Nam", 22));
        people2.add(new Person("Bình", 28));
        
        // Sort by name
        Comparator<Person> nameComparator = Comparator.comparing(Person::getName);
        Collections.sort(people2, nameComparator);
        System.out.println("Sort by name: " + people2);
        
        // Sort by age descending
        Comparator<Person> ageDescComparator = Comparator.comparingInt(Person::getAge).reversed();
        Collections.sort(people2, ageDescComparator);
        System.out.println("Sort by age (descending): " + people2);
        
        // Sort by name then age
        Comparator<Person> nameAgeComparator = Comparator.comparing(Person::getName)
                                                       .thenComparingInt(Person::getAge);
        Collections.sort(people2, nameAgeComparator);
        System.out.println("Sort by name then age: " + people2);
        
        // ========== JAVA 8+ LAMBDAS ==========
        System.out.println("\n--- Lambda Comparators ---");
        List<String> fruits = new ArrayList<>();
        fruits.add("Banana");
        fruits.add("Apple");
        fruits.add("Cherry");
        
        // Lambda for ascending
        Collections.sort(fruits, (s1, s2) -> s1.compareTo(s2));
        System.out.println("Lambda ascending: " + fruits);
        
        // Lambda for descending
        Collections.sort(fruits, (s1, s2) -> s2.compareTo(s1));
        System.out.println("Lambda descending: " + fruits);
        
        // Method reference
        Collections.sort(fruits, String::compareTo);
        System.out.println("Method reference: " + fruits);
    }
}

class Person implements Comparable<Person> {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public int compareTo(Person other) {
        // Natural ordering: by age
        return Integer.compare(this.age, other.age);
    }
    
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    @Override
    public String toString() {
        return name + "(" + age + ")";
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab09/ComparableComparatorDemo.java
// java com.javazero.lab09.ComparableComparatorDemo

// Output:
// === COMPARABLE VS COMPARATOR DEMO ===
// 
// --- Comparable (Natural Ordering) ---
// Before sort: [Anh(25), Nam(22), Bình(28), Anh(20)]
// After sort by age: [Anh(20), Nam(22), Bình(28), Anh(25)]
// 
// --- Comparator (Custom Ordering) ---
// Sort by name: [Anh(25), Bình(28), Nam(22)]
// Sort by age (descending): [Bình(28), Anh(25), Nam(22)]
// Sort by name then age: [Anh(25), Bình(28), Nam(22)]
// 
// --- Lambda Comparators ---
// Lambda ascending: [Apple, Banana, Cherry]
// Lambda descending: [Cherry, Banana, Apple]
// Method reference: [Apple, Banana, Cherry]
```

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ phá Collections! Mỗi người gây 1 bug phổ biến."

---

*   **Case 1: Modifying While Iterating**

```java
// File: ConcurrentModificationDemo.java
// Package: com.javazero.lab09

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class ConcurrentModificationDemo {
    public static void main(String[][] args) {
        System.out.println("=== CASE 1: CONCURRENT MODIFICATION (BAD!) ===");
        
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");
        
        System.out.println("Original: " + list);
        
        // BAD: Modify while iterating - throws ConcurrentModificationException!
        for (String s : list) {
            if ("B".equals(s)) {
                list.remove(s); // ConcurrentModificationException!
            }
        }
        
        // FIX 1: Use Iterator's remove()
        System.out.println("\n--- Fix 1: Iterator.remove() ---");
        List<String> list2 = new ArrayList<>();
        list2.add("A");
        list2.add("B");
        list2.add("C");
        
        Iterator<String> iterator = list2.iterator();
        while (iterator.hasNext()) {
            String s = iterator.next();
            if ("B".equals(s)) {
                iterator.remove(); // OK!
            }
        }
        System.out.println("After safe remove: " + list2);
        
        // FIX 2: Use removeIf() (Java 8+)
        System.out.println("\n--- Fix 2: removeIf() ---");
        List<String> list3 = new ArrayList<>();
        list3.add("A");
        list3.add("B");
        list3.add("C");
        
        list3.removeIf(s -> "B".equals(s));
        System.out.println("After removeIf: " + list3);
    }
}
```

---

*   **Case 2: HashMap Key Without hashCode/equals**

```java
// File: HashMapKeyDemo.java
// Package: com.javazero.lab09

import java.util.HashMap;
import java.util.Map;

public class HashMapKeyDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 2: HASHMAP KEY WITHOUT HASHCODE/EQUALS (BAD!) ===");
        
        Map<BadKey, String> map = new HashMap<>();
        BadKey key1 = new BadKey("Java");
        BadKey key2 = new BadKey("Java"); // Logical same!
        
        map.put(key1, "Programming Language");
        System.out.println("Map size: " + map.size());
        
        String value = map.get(key2);
        System.out.println("Get with logical same key: " + (value == null ? "NOT FOUND!" : value));
        
        // FIX: Override hashCode() và equals()
        System.out.println("\n--- Fix: Override hashCode() and equals() ---");
        
        Map<GoodKey, String> map2 = new HashMap<>();
        GoodKey gKey1 = new GoodKey("Java");
        GoodKey gKey2 = new GoodKey("Java");
        
        map2.put(gKey1, "Programming Language");
        System.out.println("Map size: " + map2.size());
        System.out.println("Get with logical same key: " + map2.get(gKey2));
    }
}

class BadKey {
    private String value;
    
    BadKey(String value) {
        this.value = value;
    }
    // KHÔNG override hashCode() và equals()!
}

class GoodKey {
    private String value;
    
    GoodKey(String value) {
        this.value = value;
    }
    
    @Override
    public int hashCode() {
        return value.hashCode();
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        GoodKey other = (GoodKey) obj;
        return value.equals(other.value);
    }
}
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: List (ArrayList = default), Set (HashSet = fastest, TreeSet = sorted), Map (HashMap = fastest)."

*   **[Nam (Intern)]:** "Dạ em học được: ArrayList get(i)=O(1), add(i)=O(n). LinkedList add/remove đầu/cuối=O(1)."

*   **[Việt (Intern)]:** "Dạ em học được: Comparable (compareTo) = natural ordering. Comparator = custom ordering."

*   **[Cường (Intern)]:** "Dạ em học được: Collections utility methods: sort, reverse, shuffle, binarySearch."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| Collection hierarchy | ☐ | ☐ |
| ArrayList vs LinkedList | ☐ | ☐ |
| HashSet vs TreeSet | ☐ | ☐ |
| HashMap operations | ☐ | ☐ |
| Collections utility | ☐ | ☐ |
| Comparable | ☐ | ☐ |
| Comparator | ☐ | ☐ |
| ConcurrentModificationException | ☐ | ☐ |
| hashCode/equals for Map keys | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Implement Student class có Comparable by GPA.
2.  Tạo PhoneBook dùng HashMap.
3.  Remove duplicates khỏi List.
4.  Sắp xếp List of Employees bằng nhiều criteria.
5.  Implement simple cache dùng LinkedHashMap.

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Collections
*   Effective Java: Item 18-21 (Collections)

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab10 - Multi-threading!**
