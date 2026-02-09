# LAB 05 - CLASSES VÀ OBJECTS TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta bước vào thế giới Lập trình Hướng đối tượng (OOP) - paradigm chính của Java. Đây là bước quan trọng nhất trong hành trình Java của anh em."

*   **[Hùng (Intern)]:** "Dạ anh ơi, 'class' và 'object' là gì vậy anh? Em nghe nói 'object-oriented' mãi mà không hiểu."

*   **[Anh Đô (Senior)]:** "Hùng hỏi nền tảng quá! Hãy tưởng tượng: CLASS là BẢN VẼ (blueprint), còn OBJECT là NGÔI NHÀ được xây từ bản vẽ đó. Một bản vẽ có thể xây nhiều ngôi nhà."

*   **[Nam (Intern)]:** "Dạ vậy class là khuôn mẫu, còn object là sản phẩm từ khuôn mẫu đó?"

*   **[Anh Vương (Performance)]:** "Nam hiểu đúng rồi! Object trong Java là instance của class. Khi tạo object, JVM allocate memory trên Heap cho object đó."

*   **[Em Hải (Clean Code)]:** "Quy tắc đặt tên class: UpperCamelCase. Ví dụ: Student, Person, BankAccount, OrderProcessor. Class nên là danh từ hoặc cụm danh từ."

*   **[Việt (Intern)]:** "Dạ em hay thấy `public class MyClass`. `public` là gì anh?"

*   **[Anh Khánh]:** "Việt hỏi về Access Modifier. Đây là khái niệm quan trọng về Encapsulation. Sẽ học chi tiết sau."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab05

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab05/
    └── src/
        └── com/
            └── javazero/
                └── lab05/
                    ├── Person.java
                    ├── Student.java
                    ├── Car.java
                    └── OOPDemo.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Tổng quan về CLASS và OBJECT

*   **Hội ý:**

*   **[Anh Khánh]:** "Class là blueprint - định nghĩa trạng thái (variables) và hành vi (methods) của một loại object."

*   **[Anh Đô]:** "Object là instance - thực thể thực tế được tạo từ class. Object có trạng thái riêng, hành vi chung."

*   **[Em Hải (Clean Code)]:** "Một class tốt nên: 1) Có trách nhiệm duy nhất (Single Responsibility), 2) Đặt tên mô tả rõ ràng, 3) Có methods và variables có ý nghĩa."

*   **[Hùng (Intern)]:** "Dạ ví dụ class Person có gì anh?"

*   **[Anh Vương]:** "Person có: Trạng thái (name, age, address) và Hành vi (eat(), sleep(), walk())."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo class và object đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: Person.java
// Package: com.javazero.lab05

// ========== CLASS DEFINITION ==========
public class Person {
    // ========== INSTANCE VARIABLES (Trạng thái) ==========
    // Đây là properties của mỗi Person
    
    String name;       // Tên
    int age;           // Tuổi
    String address;   // Địa chỉ
    
    // ========== METHODS (Hành vi) ==========
    
    // Method không tham số
    public void eat() {
        System.out.println(name + " đang ăn...");
    }
    
    // Method có tham số
    public void speak(String message) {
        System.out.println(name + " nói: " + message);
    }
    
    // Method trả về giá trị
    public int getBirthYear() {
        // Giả sử năm hiện tại là 2024
        return 2024 - age;
    }
    
    // Method có điều kiện
    public String getStatus() {
        if (age < 18) {
            return "Chưa trưởng thành";
        } else {
            return "Đã trưởng thành";
        }
    }
}
```

```java
// File: OOPDemo.java
// Package: com.javazero.lab05

public class OOPDemo {
    public static void main(String[] args) {
        System.out.println("=== CLASS VÀ OBJECT DEMO ===");
        
        // ========== TẠO OBJECT ==========
        System.out.println("\n--- Tạo Objects ---");
        
        // Tạo object bằng new keyword
        Person person1 = new Person();
        System.out.println("person1 = new Person()");
        
        // Tạo object thứ 2
        Person person2 = new Person();
        System.out.println("person2 = new Person()");
        
        // ========== GÁN GIÁ TRỊ CHO PROPERTIES ==========
        System.out.println("\n--- Gán giá trị cho properties ---");
        
        person1.name = "Anh Khánh";
        person1.age = 25;
        person1.address = "Hà Nội";
        
        person2.name = "Hùng";
        person2.age = 22;
        person2.address = "TP. Hồ Chí Minh";
        
        System.out.println("person1.name = \"" + person1.name + "\"");
        System.out.println("person1.age = " + person1.age);
        System.out.println("person1.address = \"" + person1.address + "\"");
        
        System.out.println("\nperson2.name = \"" + person2.name + "\"");
        System.out.println("person2.age = " + person2.age);
        System.out.println("person2.address = \"" + person2.address + "\"");
        
        // ========== GỌI METHODS ==========
        System.out.println("\n--- Gọi methods ---");
        
        person1.eat();
        person2.eat();
        
        person1.speak("Chào các bạn!");
        person2.speak("Em mới học Java!");
        
        // ========== TRẢ VỀ GIÁ TRỊ TỪ METHOD ==========
        System.out.println("\n--- Methods trả về giá trị ---");
        
        int birthYear1 = person1.getBirthYear();
        System.out.println(person1.name + " sinh năm: " + birthYear1);
        
        int birthYear2 = person2.getBirthYear();
        System.out.println(person2.name + " sinh năm: " + birthYear2);
        
        // ========== NHIỀU OBJECTS TỪ CÙNG CLASS ==========
        System.out.println("\n--- Nhiều objects ---");
        
        Person person3 = new Person();
        Person person4 = new Person();
        
        person3.name = "Nam";
        person3.age = 20;
        
        person4.name = "Việt";
        person4.age = 18;
        
        System.out.println(person3.name + " - " + person3.getStatus());
        System.out.println(person4.name + " - " + person4.getStatus());
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab05/Person.java com/javazero/lab05/OOPDemo.java
// java com.javazero.lab05.OOPDemo

// Output:
// === CLASS VÀ OBJECT DEMO ===
// 
// --- Tạo Objects ---
// person1 = new Person()
// person2 = new Person()
// 
// --- Gán giá trị cho properties ---
// person1.name = "Anh Khánh"
// person1.age = 25
// person1.address = "Hà Nội"
// 
// person2.name = "Hùng"
// person2.age = 22
// person2.address = "Hà Nội"
// 
// --- Gọi methods ---
// Anh Khánh đang ăn...
// Hùng đang ăn...
// Anh Khánh nói: Chào các bạn!
// Hùng nói: Em mới học Java!
// 
// --- Methods trả về giá trị ---
// Anh Khánh sinh năm: 1999
// Hùng sinh năm: 2002
// 
// --- Nhiều objects ---
// Nam - Đã trưởng thành
// Việt - Đã trưởng thành
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! Em thấy person1 và person2 cùng class Person nhưng name, age khác nhau!"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! Mỗi object có TRẠNG THÁI RIÊNG (state). Class chỉ định nghĩa structure, object lưu actual data."

*   **[Nam (Intern)]:** "Dạ còn `new Person()` là gì anh?"

*   **[Anh Vương]:** "new là keyword quan trọng: 1) Allocate memory trên Heap, 2) Gọi constructor (sẽ học sau), 3) Trả về reference. new Person() = tạo object mới."

*   **[Hùng (Intern)]:** "Dạ mỗi object có properties riêng, nhưng methods gọi cùng một logic?"

*   **[Em Hải]:** "Đúng rồi! Methods định nghĩa trong class, tất cả objects share cùng methods. Nhưng this trong method trỏ đến object hiện tại."

---

### BƯỚC 2: CONSTRUCTORS

*   **Hội ý:**

*   **[Anh Khánh]:** "Constructor là special method được gọi khi tạo object bằng new. Dùng để khởi tạo object's state."

*   **[Anh Đô]:** "Constructor có đặc điểm: 1) Tên TRÙNG với class name, 2) KHÔNG có return type (kể cả void), 3) Được gọi tự động khi dùng new."

*   **[Em Hải (Clean Code)]:** "Quy tắc: Dùng constructor để initialize tất cả required fields. Đặt parameters theo thứ tự logic. Overload constructors khi cần nhiều cách khởi tạo."

*   **[Hùng (Intern)]:** "Dạ sao constructor không có return type?"

*   **[Anh Vương]:** "Constructor không có return type vì nó không trả về gì cả - nó tạo và trả về object instance (implicitly). Đây là syntax rule của Java."

---

*   **Thực hiện:**

```java
// File: Student.java
// Package: com.javazero.lab05

public class Student {
    // ========== INSTANCE VARIABLES ==========
    String name;
    int age;
    String major;
    double gpa;
    boolean isActive;
    
    // ========== DEFAULT CONSTRUCTOR ==========
    // Không có constructor nào? Java tạo default constructor
    // Default khởi tạo: name = null, age = 0, gpa = 0.0, isActive = false
    
    // ========== PARAMETERIZED CONSTRUCTOR ==========
    public Student(String name, int age, String major) {
        this.name = name;
        this.age = age;
        this.major = major;
        this.gpa = 0.0;      // Default
        this.isActive = true; // Default
    }
    
    // ========== OVERLOADED CONSTRUCTOR ==========
    public Student(String name, int age, String major, double gpa) {
        this.name = name;
        this.age = age;
        this.major = major;
        this.gpa = gpa;
        this.isActive = true;
    }
    
    // ========== CONSTRUCTOR VỚI TẤT CẢ FIELDS ==========
    public Student(String name, int age, String major, double gpa, boolean isActive) {
        this.name = name;
        this.age = age;
        this.major = major;
        this.gpa = gpa;
        this.isActive = isActive;
    }
    
    // ========== COPY CONSTRUCTOR ==========
    public Student(Student other) {
        this.name = other.name;
        this.age = other.age;
        this.major = other.major;
        this.gpa = other.gpa;
        this.isActive = other.isActive;
    }
    
    // ========== METHODS ==========
    public void displayInfo() {
        System.out.println("=== Thông tin sinh viên ===");
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        System.out.println("Ngành: " + major);
        System.out.println("GPA: " + gpa);
        System.out.println("Trạng thái: " + (isActive ? "Đang học" : "Đã nghỉ"));
    }
    
    public void study(int hours) {
        System.out.println(name + " đang học " + hours + " giờ.");
    }
    
    public void updateGpa(double newGpa) {
        gpa = newGpa;
        System.out.println(name + " có GPA mới: " + gpa);
    }
}
```

```java
// File: ConstructorDemo.java
// Package: com.javazero.lab05

public class ConstructorDemo {
    public static void main(String[] args) {
        System.out.println("=== CONSTRUCTOR DEMO ===");
        
        // ========== DEFAULT CONSTRUCTOR ==========
        System.out.println("\n--- Default Constructor ---");
        Student student1 = new Student();
        System.out.println("student1 = new Student()");
        System.out.println("student1.name = " + student1.name);
        System.out.println("student1.age = " + student1.age);
        System.out.println("student1.gpa = " + student1.gpa);
        System.out.println("student1.isActive = " + student1.isActive);
        
        // ========== PARAMETERIZED CONSTRUCTOR ==========
        System.out.println("\n--- Parameterized Constructor ---");
        Student student2 = new Student("Anh Hùng", 20, "Công nghệ thông tin");
        System.out.println("new Student(\"Anh Hùng\", 20, \"Công nghệ thông tin\")");
        student2.displayInfo();
        
        // ========== OVERLOADED CONSTRUCTOR ==========
        System.out.println("\n--- Overloaded Constructor (với GPA) ---");
        Student student3 = new Student("Ngọc Nam", 21, "Khoa học máy tính", 3.75);
        student3.displayInfo();
        
        // ========== FULL CONSTRUCTOR ==========
        System.out.println("\n--- Full Constructor ---");
        Student student4 = new Student("Minh Việt", 22, "Kỹ thuật phần mềm", 3.5, true);
        student4.displayInfo();
        
        // ========== COPY CONSTRUCTOR ==========
        System.out.println("\n--- Copy Constructor ---");
        Student student5 = new Student(student4);
        System.out.println("Copy từ student4:");
        student5.displayInfo();
        
        // ========== MODIFYING OBJECTS ==========
        System.out.println("\n--- Modify Object ---");
        student2.study(5);
        student2.updateGpa(3.8);
        System.out.println("Sau khi update:");
        student2.displayInfo();
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab05/Student.java com/javazero/lab05/ConstructorDemo.java
// java com.javazero.lab05.ConstructorDemo

// Output:
// === CONSTRUCTOR DEMO ===
// 
// --- Default Constructor ---
// student1 = new Student()
// student1.name = null
// student1.age = 0
// student1.gpa = 0.0
// student1.isActive = false
// 
// --- Parameterized Constructor ---
// new Student("Anh Hùng", 20, "Công nghệ thông tin")
// === Thông tin sinh viên ===
// Tên: Anh Hùng
// Tuổi: 20
// Ngành: Công nghệ thông tin
// GPA: 0.0
// Trạng thái: Đang học
// 
// --- Overloaded Constructor (với GPA) ---
// === Thông tin sinh viên ===
// Tên: Ngọc Nam
// Tuổi: 21
// Ngành: Khoa học máy tính
// GPA: 3.75
// Trạng thái: Đang học
// 
// --- Full Constructor ---
// === Thông tin sinh viên ===
// Tên: Minh Việt
// Tuổi: 22
// Ngành: Kỹ thuật phần mềm
// GPA: 3.5
// Trạng thái: Đang học
// 
// --- Copy Constructor ---
// Copy từ student4:
// === Thông tin sinh viên ===
// Tên: Minh Việt
// Tuổi: 22
// Ngành: Kỹ thuật phần mềm
// GPA: 3.5
// Trạng thái: Đang học
// 
// --- Modify Object ---
// Anh Hùng đang học 5 giờ.
// Anh Hùng có GPA mới: 3.8
// Sau khi update:
// === Thông tin sinh viên ===
// Tên: Hùng
// Tuổi: 22
// Ngành: Công nghệ thông tin
// GPA: 3.8
// Trạng thái: Đang học
```

---

*   **Phân tích Output:**

*   **[Hùng (Intern)]:** "Anh ơi! Constructor có thể có nhiều versions với parameters khác nhau - gọi là overloading?"

*   **[Anh Đô]:** "Hùng hiểu đúng rồi! Đây là Constructor Overloading. Java phân biệt bằng số lượng và kiểu parameters."

*   **[Nam (Intern)]:** "Dạ còn `this()` trong constructor?"

*   **[Em Hải]:** "`this()` gọi constructor khác trong cùng class. Giúp tránh duplicate code khi constructors có common logic."

*   **[Việt (Intern)]:** "Dạ copy constructor hữu ích khi nào?"

*   **[Anh Vương]:** "Copy constructor tạo object mới với data giống object cũ. Hữu ích khi cần independent copy, không ảnh hưởng original."

---

### BƯỚC 3: THIS KEYWORD

*   **Hội ý:**

*   **[Anh Khánh]:** "this là reference variable trỏ đến CURRENT OBJECT - object hiện tại đang được thao tác."

*   **[Anh Đô]:** "this có 4 công dụng chính: 1) Phân biệt instance variable với local variable, 2) Gọi constructor khác (this()), 3) Truyền object hiện tại làm parameter, 4) Return object hiện tại."

*   **[Em Hải (Clean Code)]:** "Quy tắc: Khi parameter/trường cùng tên, DÙNG this để chỉ instance variable. Không dùng this khi không cần thiết (code rõ ràng hơn)."

*   **[Hùng (Intern)]:** "Dạ khi nào parameter cùng tên với instance variable?"

*   **[Anh Vương]:** "Khi dùng constructor với parameters, thường đặt tên parameter giống instance variable để code dễ đọc: `public Student(String name, int age) { this.name = name; this.age = age; }`"

---

*   **Thực hiện:**

```java
// File: ThisKeywordDemo.java
// Package: com.javazero.lab05

public class ThisKeywordDemo {
    String name;
    int age;
    
    // ========== THIS ĐỂ PHÂN BIỆT INSTANCE VÀ LOCAL ==========
    public void setData(String name, int age) {
        // name và age ở đây là parameters (local)
        // this.name và this.age là instance variables
        
        this.name = name;     // Gán parameter 'name' vào instance variable 'name'
        this.age = age;       // Gán parameter 'age' vào instance variable 'age'
    }
    
    // ========== THIS() GỌI CONSTRUCTOR KHÁC ==========
    public ThisKeywordDemo() {
        this("Default Name", 0); // Gọi constructor 2 tham số
        System.out.println("Constructor không tham số hoàn thành");
    }
    
    public ThisKeywordDemo(String name) {
        this(name, 18); // Gọi constructor 2 tham số
        System.out.println("Constructor 1 tham số hoàn thành");
    }
    
    public ThisKeywordDemo(String name, int age) {
        this.name = name; // Gán vào instance variable
        this.age = age;
        System.out.println("Constructor 2 tham số hoàn thành");
    }
    
    // ========== THIS ĐỂ RETURN OBJECT HIỆN TẠI ==========
    public ThisKeywordDemo setName(String name) {
        this.name = name;
        return this; // Return object hiện tại
    }
    
    public ThisKeywordDemo setAge(int age) {
        this.age = age;
        return this;
    }
    
    // ========== THIS LÀM PARAMETER ==========
    public void display() {
        System.out.println("Name: " + this.name + ", Age: " + this.age);
    }
    
    // Method nhận object hiện tại làm parameter
    public void compare(ThisKeywordDemo other) {
        if (this == other) {
            System.out.println("Cùng một object!");
        } else {
            System.out.println("Khác object!");
        }
    }
    
    public static void main(String[] args) {
        System.out.println("=== THIS KEYWORD DEMO ===");
        
        // ========== THIS PHÂN BIỆT ==========
        System.out.println("\n--- Phân biệt Instance vs Local ---");
        ThisKeywordDemo obj1 = new ThisKeywordDemo();
        obj1.setData("Anh Hùng", 25);
        System.out.println("obj1.name = " + obj1.name);
        System.out.println("obj1.age = " + obj1.age);
        
        // ========== THIS() GỌI CONSTRUCTOR ==========
        System.out.println("\n--- this() gọi constructor ---");
        System.out.println("Tạo object với constructor không tham số:");
        ThisKeywordDemo obj2 = new ThisKeywordDemo();
        
        System.out.println("\nTạo object với constructor 1 tham số:");
        ThisKeywordDemo obj3 = new ThisKeywordDemo("Ngọc Nam");
        
        System.out.println("\nTạo object với constructor 2 tham số:");
        ThisKeywordDemo obj4 = new ThisKeywordDemo("Minh Việt", 22);
        
        // ========== METHOD CHAINING ==========
        System.out.println("\n--- Method Chaining ---");
        ThisKeywordDemo obj5 = new ThisKeywordDemo();
        obj5.setName("Hoàng Anh")
           .setAge(24)
           .display();
        
        // ========== THIS LÀM PARAMETER ==========
        System.out.println("\n--- this làm parameter ---");
        ThisKeywordDemo obj6 = new ThisKeywordDemo("Test", 30);
        obj6.compare(obj6); // Same object
        obj6.compare(obj5); // Different object
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab05/ThisKeywordDemo.java
// java com.javazero.lab05.ThisKeywordDemo

// Output:
// === THIS KEYWORD DEMO ===
// 
// --- Phân biệt Instance vs Local ---
// obj1.name = Anh Hùng
// obj1.age = 25
// 
// --- this() gọi constructor ---
// Tạo object với constructor không tham số:
// Constructor 2 tham số hoàn thành
// Constructor không tham số hoàn thành
// 
// Tạo object với constructor 1 tham số:
// Constructor 2 tham số hoàn thành
// Constructor 1 tham số hoàn thành
// 
// Tạo object với constructor 2 tham số:
// Constructor 2 tham số hoàn thành
 methods
// Name: Hoàng Anh, Age: 24
// 
// --- this làm parameter ---
// obj6.compare(obj6): Cùng một object!
// obj6.compare(obj5): Khác object!
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! this() gọi constructor rất hay! Constructor không tham số gọi constructor 2 tham số!"

*   **[Anh Đô]:** "Nam hiểu đúng! this() phải là dòng ĐẦU TIÊN trong constructor. Đảm bảo constructor được gọi đúng thứ tự."

*   **[Việt (Intern)]:** "Dạ method chaining với return this rất tiện! obj.setName().setAge().display()"

*   **[Em Hải]:** "Đúng rồi! Đây gọi là Fluent Interface. Code đọc như câu tiếng Anh: setName, setAge, display."

*   **[Hùng (Intern)]:** "Dạ còn `this` làm parameter khác gì `this()`?"

*   **[Anh Vương]:** "Khác hoàn toàn! `this` = reference đến object hiện tại. `this()` = gọi constructor khác. `this.param` = access field/method của object."

---

### BƯỚC 4: STATIC KEYWORD

*   **Hội ý:**

*   **[Anh Khánh]:** "static means 'thuộc về class, không thuộc về object'. Static members được share giữa tất cả objects."

*   **[Anh Vương (Performance)]:** "Static methods được load vào memory khi class được load (第一次). Không cần tạo object để gọi static method."

*   **[Em Hải (Clean Code)]:** "Quy tắc: Dùng static cho constants (final static), utility methods (Math.random()), factory methods. KHÔNG dùng static khi cần polymorphism."

*   **[Hùng (Intern)]:** "Dạ static variable khác gì instance variable?"

*   **[Anh Đô]:** "Instance variable: mỗi object có bản riêng. Static variable: tất cả objects chia sẻ cùng một biến. Thay đổi ở đâu cũng ảnh hưởng."

---

*   **Thực hiện:**

```java
// File: StaticDemo.java
// Package: com.javazero.lab05

public class StaticDemo {
    // ========== INSTANCE VARIABLE ==========
    // Mỗi object có bản riêng
    String instanceName;
    int instanceCounter;
    
    // ========== STATIC VARIABLE ==========
    // Tất cả objects chia sẻ cùng một biến
    static String className = "StaticDemo Class";
    static int totalObjects = 0;
    
    // ========== STATIC FINAL (CONSTANT) ==========
    public static final double PI = 3.14159;
    public static final int MAX_STUDENTS = 100;
    
    // ========== CONSTRUCTOR ==========
    public StaticDemo(String name) {
        this.instanceName = name;
        this.instanceCounter = ++totalObjects; // Tăng mỗi khi tạo object
    }
    
    // ========== INSTANCE METHOD ==========
    public void display() {
        System.out.println("Instance: " + instanceName);
        System.out.println("Instance Counter: " + instanceCounter);
        System.out.println("Class Name: " + className);
        System.out.println("Total Objects: " + totalObjects);
    }
    
    // ========== STATIC METHOD ==========
    public static void displayClassInfo() {
        // Chỉ có thể truy cập static members
        System.out.println("Class Name: " + className);
        System.out.println("Total Objects Created: " + totalObjects);
        System.out.println("PI = " + PI);
        
        // LỖI! Không thể truy cập instance variable
        // System.out.println(instanceName); // COMPILE ERROR!
    }
    
    // ========== STATIC BLOCK ==========
    static {
        // Khởi tạo static variables
        System.out.println("Static block executed!");
        className = "StaticDemo (Initialized)";
        // Có thể thực hiện logic phức tạp
    }
    
    public static void main(String[] args) {
        System.out.println("=== STATIC KEYWORD DEMO ===");
        
        // ========== STATIC METHOD KHÔNG CẦN OBJECT ==========
        System.out.println("\n--- Gọi static method ---");
        StaticDemo.displayClassInfo();
        
        // ========== STATIC CONSTANTS ==========
        System.out.println("\n--- Static Constants ---");
        System.out.println("PI = " + StaticDemo.PI);
        System.out.println("MAX_STUDENTS = " + StaticDemo.MAX_STUDENTS);
        
        // ========== INSTANCE VS STATIC ==========
        System.out.println("\n--- So sánh Instance vs Static ---");
        
        StaticDemo obj1 = new StaticDemo("Object 1");
        StaticDemo obj2 = new StaticDemo("Object 2");
        StaticDemo obj3 = new StaticDemo("Object 3");
        
        System.out.println("\nObj1:");
        obj1.display();
        
        System.out.println("\nObj2:");
        obj2.display();
        
        System.out.println("\nObj3:");
        obj3.display();
        
        // ========== MODIFYING STATIC ==========
        System.out.println("\n--- Modify Static Variable ---");
        System.out.println("obj1.instanceCounter = " + obj1.instanceCounter);
        System.out.println("obj2.instanceCounter = " + obj2.instanceCounter);
        System.out.println("StaticDemo.totalObjects = " + StaticDemo.totalObjects);
        
        // Thay đổi static variable
        StaticDemo.totalObjects = 999;
        System.out.println("\nSau khi đổi StaticDemo.totalObjects = 999:");
        System.out.println("obj3.instanceCounter = " + obj3.instanceCounter);
        System.out.println("StaticDemo.totalObjects = " + StaticDemo.totalObjects);
        
        // ========== STATIC VÀ MEMORY ==========
        System.out.println("\n--- Memory View ---");
        System.out.println("Có 3 objects, nhưng chỉ có 1 'className' và 1 'totalObjects' trong memory!");
        System.out.println("Static members được lưu trong Method Area (hoặc Metaspace trong Java 8+)");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab05/StaticDemo.java
// java com.javazero.lab05.StaticDemo

// Output:
// === STATIC KEYWORD DEMO ===
// Static block executed!
// 
// --- Gọi static method ---
// Class Name: StaticDemo (Initialized)
// Total Objects Created: 0
// PI = 3.14159
// 
// --- Static Constants ---
// PI = 3.14159
// MAX_STUDENTS = 100
// 
// --- So sánh Instance vs Static ---
// 
// Obj1:
// Instance: Object 1
// Instance Counter: 1
// Class Name: StaticDemo (Initialized)
// Total Objects: 3
// 
// Obj2:
// Instance: Object 2
// Instance Counter: 2
// Class Name: StaticDemo
// Total Objects: 3
// 
// Obj3:
// Instance: Object 3
// Instance Counter: 3
// Class Name: StaticDemo
// Total Objects: 3
// 
// --- Modify Static Variable ---
// obj1.instanceCounter = 1
// obj2.instanceCounter = 3
// StaticDemo.totalObjects = 3
// 
// Sau khi đổi StaticDemo.totalObjects = 999:
// obj3.instanceCounter = 3
// StaticDemo.totalObjects = 999
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! static totalObjects = 0 ban đầu, nhưng khi tạo 3 objects, totalObjects = 3 cho tất cả!"

*   **[Anh Vương]:** "Việt hiểu đúng rồi! static variable được SHARED. Mỗi khi tạo object mới, constructor tăng totalObjects. Tất cả objects thấy cùng giá trị."

*   **[Nam (Intern)]:** "Dạ còn static block chạy khi nào?"

*   **[Em Hải]:** "Static block chạy một lần khi class được LOAD vào memory. Dùng để khởi tạo static variables phức tạp."

*   **[Hùng (Intern)]:** "Dạ static method không thể dùng instance variable?"

*   **[Anh Đô]:** "Đúng rồi! Static method không có 'this' (không thuộc object nào), nên không thể truy cập instance variables/methods. Chỉ truy cập static members."

---

### BƯỚC 5: ACCESS MODIFIERS (Giới thiệu)

*   **Hội ý:**

*   **[Anh Khánh]:** "Access modifiers kiểm soát AI có thể truy cập class, variables, và methods. Đây là nền tảng của ENCAPSULATION."

*   **[Anh Đô]:** "4 Access Modifiers: private, (default - package-private), protected, public."

*   **[Em Hải (Clean Code)]:** "Nguyên tắc: 1) Luôn private fields (data hiding), 2) Public methods để access (getter/setter), 3) Chỉ public khi cần thiết (API)."

*   **[Hùng (Intern)]:** "Dạ sao phải ẩn dữ liệu anh?"

*   **[Anh Vương]:** "Encapsulation bảo vệ data: 1) Validate trước khi gán, 2) Ngăn chặn truy cập trái phép, 3) Thay đổi implementation không ảnh hưởng users."

---

*   **Thực hiện:**

```java
// File: EncapsulationDemo.java
// Package: com.javazero.lab05

public class BankAccount {
    // ========== PRIVATE FIELDS (DATA HIDING) ==========
    private String accountNumber;
    private String accountHolder;
    private double balance;
    private boolean isActive;
    
    // ========== PUBLIC CONSTANTS ==========
    public static final String BANK_NAME = "Java Bank";
    public static final double MIN_BALANCE = 100.0;
    
    // ========== CONSTRUCTORS ==========
    public BankAccount(String accountNumber, String accountHolder, double initialBalance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.isActive = true;
        
        // Validate balance
        if (initialBalance >= MIN_BALANCE) {
            this.balance = initialBalance;
        } else {
            System.out.println("Số dư ban đầu phải >= " + MIN_BALANCE + ". Đặt = " + MIN_BALANCE);
            this.balance = MIN_BALANCE;
        }
    }
    
    // ========== PUBLIC METHODS (INTERFACE) ==========
    
    // Getter methods (read-only)
    public String getAccountNumber() {
        return accountNumber;
    }
    
    public String getAccountHolder() {
        return accountHolder;
    }
    
    public double getBalance() {
        return balance;
    }
    
    public boolean isActive() {
        return isActive;
    }
    
    // Setter với validation
    public void setAccountHolder(String newHolder) {
        if (newHolder != null && !newHolder.trim().isEmpty()) {
            this.accountHolder = newHolder;
        } else {
            System.out.println("Tên không hợp lệ!");
        }
    }
    
    // Business methods
    public void deposit(double amount) {
        if (amount > 0 && isActive) {
            balance += amount;
            System.out.println("Nạp " + amount + " thành công!");
            System.out.println("Số dư mới: " + balance);
        } else {
            System.out.println("Lỗi: Số tiền không hợp lệ hoặc tài khoản bị khóa!");
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance && isActive) {
            balance -= amount;
            System.out.println("Rút " + amount + " thành công!");
            System.out.println("Số dư mới: " + balance);
        } else {
            System.out.println("Lỗi: Số tiền không hợp lệ hoặc số dư không đủ!");
        }
    }
    
    // ========== PRIVATE METHOD ==========
    private void validateAccount() {
        // Logic nội bộ, không exposed ra ngoài
        if (balance < MIN_BALANCE) {
            isActive = false;
            System.out.println("Tài khoản bị khóa do số dư quá thấp!");
        }
    }
    
    // ========== DISPLAY METHOD ==========
    public void displayInfo() {
        System.out.println("\n=== Thông tin tài khoản ===");
        System.out.println("Ngân hàng: " + BANK_NAME);
        System.out.println("Số tài khoản: " + accountNumber);
        System.out.println("Chủ tài khoản: " + accountHolder);
        System.out.println("Số dư: " + balance);
        System.out.println("Trạng thái: " + (isActive ? "Hoạt động" : "Bị khóa"));
    }
}
```

```java
// File: EncapsulationRunner.java
// Package: com.javazero.lab05

public class EncapsulationRunner {
    public static void main(String[] args) {
        System.out.println("=== ENCAPSULATION DEMO ===");
        
        // ========== TẠO ACCOUNT ==========
        BankAccount account = new BankAccount("123456789", "Nguyễn Văn A", 1000);
        account.displayInfo();
        
        // ========== TRUY CẬP QUA GETTERS ==========
        System.out.println("\n--- Truy cập qua getters ---");
        System.out.println("Số tài khoản: " + account.getAccountNumber());
        System.out.println("Chủ tài khoản: " + account.getAccountHolder());
        System.out.println("Số dư: " + account.getBalance());
        
        // ========== THAY ĐỔI QUA SETTER ==========
        System.out.println("\n--- Thay đổi qua setter ---");
        account.setAccountHolder("Trần Thị B");
        System.out.println("Chủ tài khoản mới: " + account.getAccountHolder());
        
        // ========== THỰC HIỆN GIAO DỊCH ==========
        System.out.println("\n--- Giao dịch ---");
        account.deposit(500);
        account.withdraw(200);
        
        // ========== VALIDATION ==========
        System.out.println("\n--- Validation ---");
        account.deposit(-100); // Lỗi: số tiền không hợp lệ
        
        // ========== LỖI: TRUY CẬP PRIVATE DIRECTLY ==========
        System.out.println("\n--- LỖI: Private fields ---");
        // account.balance = 9999999; // COMPILE ERROR!
        // account.accountNumber = "111"; // COMPILE ERROR!
        
        System.out.println("→ KHÔNG thể truy cập private fields trực tiếp!");
        System.out.println("→ Phải dùng public methods (getter/setter)");
        
        // ========== STATIC CONSTANTS ==========
        System.out.println("\n--- Static Constants ---");
        System.out.println("Bank Name: " + BankAccount.BANK_NAME);
        System.out.println("Min Balance: " + BankAccount.MIN_BALANCE);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab05/BankAccount.java com/javazero/lab05/EncapsulationRunner.java
// java com.javazero.lab05.EncapsulationRunner

// Output:
// === ENCAPSULATION DEMO ===
// 
// === Thông tin tài khoản ===
// Ngân hàng: Java Bank
// Số tài khoản: 123456789
// Chủ tài khoản: Nguyễn Văn A
// Số dư: 1000.0
// Trạng thái: Hoạt động
// 
// --- Truy cập qua getters ---
// Số tài khoản: 123456789
// Chủ tài khoản: Trần Thị B
// Số dư: 1000.0
// 
// --- Thay đổi qua setter ---
// Chủ tài khoản mới: Trần Thị B
// 
// --- Giao dịch ---
// Nạp 500 thành công!
// Số dư mới: 1500.0
// Rút 200 thành công!
// Số dư mới: 1300.0
// 
// --- Validation ---
// Lỗi: Số tiền không hợp lệ hoặc tài khoản bị khóa!
// 
// --- LỖI: Private fields ---
// → KHÔNG thể truy cập private fields trực tiếp!
// → Phải dùng public methods (getter/setter)
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! Em thấy account.balance = 9999999 báo lỗi! Sao phải phức tạp vậy?"

*   **[Anh Đô]:** "Nam hỏi hay! Đây là DATA HIDING. Private fields chỉ accessible trong class. Bên ngoài phải dùng public methods. Điều này cho phép VALIDATE dữ liệu."

*   **[Việt (Intern)]:** "Dạ ví dụ deposit(-100) bị từ chối!"

*   **[Em Hải]:** "Đúng rồi! Setter/Deposit methods có logic validation. Không ai có thể set balance = -1000 hay deposit() tiền âm."

*   **[Hùng (Intern)]:** "Dạ còn static constants dùng làm gì?"

*   **[Anh Vương]:** "BANK_NAME, MIN_BALANCE là constants - không thay đổi. public static để mọi nơi truy cập, không cần tạo object."

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ phá OOP! Mỗi người gây 1 bug phổ biến."

---

*   **Case 1: NullPointerException với Objects**

```java
// File: NullObjectBugDemo.java
// Package: com.javazero.lab05

public class NullObjectBugDemo {
    String name;
    
    public NullObjectBugDemo(String name) {
        this.name = name;
    }
    
    public void display() {
        System.out.println("Name: " + name);
    }
    
    public static void main(String[] args) {
        System.out.println("=== CASE 1: NULL OBJECT BUG ===");
        
        // Bug: Object chưa được khởi tạo
        NullObjectBugDemo obj;
        // obj.display(); // COMPILE ERROR: variable obj might not have been initialized
        
        // Bug phổ biến: Gán null
        System.out.println("\n--- Gán null ---");
        NullObjectBugDemo person = null;
        System.out.println("person = null");
        
        try {
            person.display(); // NullPointerException!
        } catch (NullPointerException e) {
            System.out.println("CAUGHT: NullPointerException!");
            System.out.println("Lý do: person = null, không thể gọi .display()");
        }
        
        // Fix: Khởi tạo object
        System.out.println("\nFix: Khởi tạo object");
        person = new NullObjectBugDemo("Anh Hùng");
        person.display();
    }
}
```

---

*   **Case 2: Static vs Instance Confusion**

```java
// File: StaticInstanceBugDemo.java
// Package: com.javazero.lab05

public class StaticInstanceBugDemo {
    String instanceVar = "Instance Variable";
    static String staticVar = "Static Variable";
    
    public void instanceMethod() {
        System.out.println(instanceVar); // OK
        System.out.println(staticVar);    // OK
    }
    
    public static void staticMethod() {
        // System.out.println(instanceVar); // COMPILE ERROR!
        System.out.println(staticVar);    // OK
    }
    
    public static void main(String[] args) {
        System.out.println("=== CASE 2: STATIC VS INSTANCE CONFUSION ===");
        
        // Gọi static method
        staticMethod();
        
        // Tạo object để gọi instance method
        StaticInstanceBugDemo obj = new StaticInstanceBugDemo();
        obj.instanceMethod();
        
        System.out.println("\n→ Static methods chỉ truy cập được static members!");
        System.out.println("→ Instance methods truy cập được cả hai!");
    }
}
```

---

*   **Case 3: Constructor Chaining Bug**

```java
// File: ConstructorChainingBugDemo.java
// Package: com.javazero.lab05

public class ConstructorChainingBugDemo {
    String name;
    int age;
    
    // Bug: this() không phải dòng đầu tiên
    public ConstructorChainingBugDemo() {
        System.out.println("Constructor bắt đầu");
        // this("Default", 0); // COMPILE ERROR: Constructor call must be first statement
    }
    
    public ConstructorChainingBugDemo(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("Constructor 2 params hoàn thành");
    }
    
    public static void main(String[] args) {
        System.out.println("=== CASE 3: CONSTRUCTOR CHAINING BUG ===");
        
        // ConstructorChainingBugDemo obj = new ConstructorChainingBugDemo();
        // Sẽ báo lỗi nếu uncomment dòng this()
        
        ConstructorChainingBugDemo obj2 = new ConstructorChainingBugDemo("Anh", 25);
    }
}
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: Class là blueprint, object là instance từ blueprint. Class định nghĩa state và behavior."

*   **[Nam (Intern)]:** "Dạ em học được: Constructor là method đặc biệt để khởi tạo object. Constructor không có return type."

*   **[Việt (Intern)]:** "Dạ em học được: this là reference đến object hiện tại. Dùng this.name để phân biệt với parameter."

*   **[Cường (Intern)]:** "Dạ em học được: static members thuộc về class, shared giữa tất cả objects. instance members thuộc về từng object."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| Class vs Object | ☐ | ☐ |
| Instance variables | ☐ | ☐ |
| Instance methods | ☐ | ☐ |
| Constructor | ☐ | ☐ |
| Default constructor | ☐ | ☐ |
| Parameterized constructor | ☐ | ☐ |
| Constructor overloading | ☐ | ☐ |
| this keyword | ☐ | ☐ |
| this() constructor call | ☐ | ☐ |
| static variables | ☐ | ☐ |
| static methods | ☐ | ☐ |
| static constants | ☐ | ☐ |
| static block | ☐ | ☐ |
| Access modifiers | ☐ | ☐ |
| Encapsulation | ☐ | ☐ |
| Getter/Setter | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Tạo class Rectangle với fields width, height và methods getArea(), getPerimeter().
2.  Tạo class Book với constructor, getters, và business methods.
3.  Tạo class Counter với static variable để đếm số objects đã tạo.
4.  Tạo class BankAccount với private fields và public methods (deposit, withdraw, getBalance).
5.  Tạo class Circle với static constant PI và method tính diện tích.

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Classes and Objects
*   Effective Java: Item 1: Consider static factory methods instead of constructors
*   Effective Java: Item 19: Design and document for inheritance or else prohibit it

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab06 - Inheritance & Polymorphism!**
