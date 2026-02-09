# LAB 07 - ABSTRACTION (TRỪU TƯỢNG) VÀ ENCAPSULATION (ĐÓNG GÓI) TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta sẽ học hai pillar cuối cùng của OOP: Abstraction (Trừu tượng hóa) và Encapsulation (Đóng gói). Đây là những kỹ thuật giúp thiết kế code chuyên nghiệp."

*   **[Hùng (Intern)]:** "Dạ anh ơi, 'abstraction' là gì vậy anh? Em nghe nói abstract class và interface, nhưng không hiểu khác nhau."

*   **[Anh Đô (Senior)]:** "Hùng hỏi câu quan trọng! Abstraction là giấu DETAILS và chỉ hiển thị ESSENTIAL FEATURES. Ví dụ: Khi lái xe, bạn biết bấm ga để đi, nhưng không cần biết động cơ hoạt động thế nào."

*   **[Nam (Intern)]:** "Dạ vậy abstraction giống như 'remote control' - chỉ cần bấm nút, không cần biết bên trong có gì?"

*   **[Anh Vương (Performance)]:** "Nam hiểu đúng rồi! Abstraction ẩn implementation phức tạp, chỉ cung cấp interface đơn giản để tương tác."

*   **[Em Hải (Clean Code)]:** "Encapsulation là đóng gói dữ liệu và methods thành một unit (class), và kiểm soát truy cập thông qua access modifiers. Đây là nền tảng của data hiding."

*   **[Việt (Intern)]:** "Dạ vậy abstract class khác gì interface anh?"

*   **[Anh Khánh]:** "Việt hỏi hay! Đây là câu hỏi phỏng vấn kinh điển. Sẽ giải thích chi tiết trong bài học hôm nay."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên (cho default methods)
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab07

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab07/
    └── src/
        └── com/
            └── javazero/
                └── lab07/
                    ├── Shape.java
                    ├── Circle.java
                    ├── Rectangle.java
                    ├── Drawable.java
                    ├── Paintable.java
                    ├── Animal.java
                    └── AbstractionDemo.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Abstract Class

*   **Hội ý:**

*   **[Anh Khánh]:** "Abstract class là class không thể instantiate (tạo object trực tiếp). Nó dùng làm base class cho các classes khác."

*   **[Anh Đô]:** "Abstract class có thể có: 1) Abstract methods (không có body), 2) Concrete methods (có body), 3) Variables, 4) Constructors."

*   **[Em Hải (Clean Code)]:** "Abstract class dùng khi các subclasses có CHUNG behavior (concrete methods) và CẦN override một số methods (abstract methods)."

*   **[Hùng (Intern)]:** "Dạ abstract method là gì anh?"

*   **[Anh Vương]:** "Abstract method là method được khai báo nhưng KHÔNG có implementation (không có body). Subclass BẮT BUỘC phải override tất cả abstract methods."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo abstract class đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: Shape.java
// Package: com.javazero.lab07

// ========== ABSTRACT CLASS ==========
// Shape là abstract - không thể tạo object trực tiếp
public abstract class Shape {
    // ========== VARIABLES ==========
    protected String color;
    protected String name;
    
    // ========== CONSTRUCTOR ==========
    public Shape(String name, String color) {
        this.name = name;
        this.color = color;
        System.out.println("Shape constructor called for: " + name);
    }
    
    // ========== ABSTRACT METHOD ==========
    // Không có body - subclasses PHẢI override
    public abstract double getArea();
    public abstract double getPerimeter();
    
    // ========== CONCRETE METHOD ==========
    // Có body - subclasses có thể dùng hoặc override
    public void displayInfo() {
        System.out.println("=== " + name + " ===");
        System.out.println("Color: " + color);
    }
    
    // ========== FINAL METHOD ==========
    // Subclass không thể override
    public final void showColor() {
        System.out.println("This " + name + " is " + color);
    }
}
```

```java
// File: Circle.java
// Package: com.javazero.lab07

// ========== CIRCLE KẾ THỪA TỪ SHAPE ==========
public class Circle extends Shape {
    private double radius;
    
    // ========== CONSTRUCTOR ==========
    public Circle(String color, double radius) {
        super("Circle", color); // Gọi Shape constructor
        this.radius = radius;
        System.out.println("Circle constructor completed");
    }
    
    // ========== OVERRIDE ABSTRACT METHODS ==========
    // BẮT BUỘC phải override!
    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    public double getPerimeter() {
        return 2 * Math.PI * radius;
    }
    
    // ========== ADDITIONAL METHODS ==========
    public void displayCircleInfo() {
        System.out.println("=== Circle Info ===");
        System.out.println("Radius: " + radius);
        System.out.println("Area: " + getArea());
        System.out.println("Perimeter: " + getPerimeter());
    }
}
```

```java
// File: Rectangle.java
// Package: com.javazero.lab07

// ========== RECTANGLE KẾ THỪA TỪ SHAPE ==========
public class Rectangle extends Shape {
    private double width;
    private double height;
    
    public Rectangle(String color, double width, double height) {
        super("Rectangle", color);
        this.width = width;
        this.height = height;
        System.out.println("Rectangle constructor completed");
    }
    
    // ========== OVERRIDE ABSTRACT METHODS ==========
    @Override
    public double getArea() {
        return width * height;
    }
    
    @Override
    public double getPerimeter() {
        return 2 * (width + height);
    }
    
    // ========== OVERRIDE CONCRETE METHOD ==========
    @Override
    public void displayInfo() {
        System.out.println("=== Rectangle Override ===");
        System.out.println("Name: " + name);
        System.out.println("Color: " + color);
        System.out.println("Width x Height: " + width + " x " + height);
    }
}
```

```java
// File: AbstractionDemo.java
// Package: com.javazero.lab07

public class AbstractionDemo {
    public static void main(String[] args) {
        System.out.println("=== ABSTRACT CLASS DEMO ===");
        
        // ========== ABSTRACT CLASS CANNOT BE INSTANTIATED ==========
        System.out.println("\n--- LỖI: Cannot instantiate Shape ---");
        // Shape shape = new Shape("Test", "Red"); // COMPILE ERROR!
        System.out.println("Shape là abstract - không thể tạo object!");
        
        // ========== TẠO CONCRETE SUBCLASSES ==========
        System.out.println("\n--- Tạo Circle ---");
        Circle circle = new Circle("Red", 5.0);
        
        System.out.println("\n--- Tạo Rectangle ---");
        Rectangle rectangle = new Rectangle("Blue", 4.0, 6.0);
        
        // ========== POLYMORPHISM VỚI ABSTRACT CLASS ==========
        System.out.println("\n--- Polymorphism với Abstract Class ---");
        Shape shape1 = new Circle("Green", 3.0);
        Shape shape2 = new Rectangle("Yellow", 5.0, 2.0);
        
        shape1.displayInfo();
        System.out.println("Area: " + shape1.getArea());
        System.out.println("Perimeter: " + shape1.getPerimeter());
        
        shape2.displayInfo();
        System.out.println("Area: " + shape2.getArea());
        System.out.println("Perimeter: " + shape2.getPerimeter());
        
        // ========== POLYMORPHIC ARRAY ==========
        System.out.println("\n--- Polymorphic Array ---");
        Shape[] shapes = {
            new Circle("Red", 5.0),
            new Rectangle("Blue", 4.0, 6.0),
            new Circle("Green", 3.0),
            new Rectangle("Yellow", 2.0, 8.0)
        };
        
        double totalArea = 0;
        for (Shape shape : shapes) {
            System.out.println(shape.getClass().getSimpleName() + 
                             " area: " + shape.getArea());
            totalArea += shape.getArea();
        }
        System.out.println("Total Area: " + totalArea);
        
        // ========== ABSTRACT CLASS WITH CONCRETE METHODS ==========
        System.out.println("\n--- Abstract Class Features ---");
        Circle c = new Circle("Purple", 2.5);
        c.displayInfo();     // Concrete method từ Shape
        c.showColor();      // Final method
        c.displayCircleInfo(); // Method riêng của Circle
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab07/Shape.java com/javazero/lab07/Circle.java com/javazero/lab07/Rectangle.java com/javazero/lab07/AbstractionDemo.java
// java com.javazero.lab07.AbstractionDemo

// Output:
// === ABSTRACT CLASS DEMO ===
// 
// --- LỖI: Cannot instantiate Shape ---
// Shape là abstract - không thể tạo object!
// 
// --- Tạo Circle ---
// Shape constructor called for: Circle
// Circle constructor completed
// 
// --- Tạo Rectangle ---
// Shape constructor called for: Rectangle
// Rectangle constructor completed
// 
// --- Polymorphism với Abstract Class ---
// Shape constructor called for: Green
// === Circle Info ===
// Color: Green
// Area: 28.274333882308138
// Perimeter: 18.84955592153876
// 
// === Rectangle Override ===
// Name: Rectangle
// Color: Yellow
// Width x Height: 5.0 x 2.0
// Area: 10.0
// Perimeter: 14.0
// 
// --- Polymorphic Array ---
// Circle area: 78.53981633974483
// Rectangle area: 24.0
// Circle area: 28.274333882308138
// Rectangle area: 16.0
// Total Area: 146.81481722185283
// 
// --- Abstract Class Features ---
// === Circle Info ===
// Color: Purple
// Purple
// Radius: 2.5
// Area: 19.634954084936208
// Perimeter: 15.707963267948966
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! Shape là abstract nên không thể new Shape()!"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! Abstract class chỉ dùng làm BASE CLASS. Muốn dùng, phải extend và override abstract methods."

*   **[Nam (Intern)]:** "Dạ Circle phải override getArea() và getPerimeter()?"

*   **[Em Hải]:** "Đúng rồi! Bất kỳ concrete subclass nào cũng phải implement TẤT CẢ abstract methods từ abstract class cha."

*   **[Hùng (Intern)]:** "Dạ còn Shape có constructor?"

*   **[Anh Vương]:** "Abstract class có thể có constructor! Constructor được gọi khi subclass được instantiated."

---

### BƯỚC 2: Interface

*   **Hội ý:**

*   **[Anh Khánh]:** "Interface là blueprint hoàn toàn abstract. Từ Java 8+, interface có thể có default và static methods."

*   **[Anh Đô]:** "Interface chỉ chứa: 1) Abstract methods (trước Java 8), 2) Constants (public static final), 3) Default methods (Java 8+), 4) Static methods (Java 8+), 5) Private methods (Java 9+)."

*   **[Em Hải (Clean Code)]:** "Interface dùng để định nghĩa CONTRACT - những gì class PHẢI có. Class implement interface PHẢI override tất cả abstract methods."

*   **[Hùng (Intern)]:** "Dạ interface khác gì abstract class?"

*   **[Anh Vương]:** "Khác biệt chính: 1) Abstract class có STATE (variables), interface không. 2) Java chỉ cho EXTENDS một abstract class, nhưng IMPLEMENTS nhiều interfaces. 3) Interface nhẹ hơn, linh hoạt hơn."

---

*   **Thực hiện:**

```java
// File: Drawable.java
// Package: com.javazero.lab07

// ========== INTERFACE ==========
// Contract mà implementers PHẢI tuân theo
public interface Drawable {
    // ========== CONSTANTS ==========
    // Tất cả variables trong interface đều là public static final
    int MIN_SIZE = 1;
    int MAX_SIZE = 1000;
    String DRAWING_TOOL = "Pencil";
    
    // ========== ABSTRACT METHODS (trước Java 8) ==========
    // Các class implement PHẢI override
    public void draw();
    public void erase();
    
    // ========== DEFAULT METHODS (Java 8+) ==========
    // Có implementation - implementers có thể dùng hoặc override
    default void display() {
        System.out.println("Drawing something...");
    }
    
    default void setColor(String color) {
        System.out.println("Setting color to: " + color);
    }
    
    // ========== STATIC METHODS (Java 8+) ==========
    // Thuộc về interface, không cần instance
    public static void showToolInfo() {
        System.out.println("Default drawing tool: " + DRAWING_TOOL);
    }
    
    public static int getMinSize() {
        return MIN_SIZE;
    }
    
    // ========== PRIVATE METHODS (Java 9+) ==========
    // Helper cho default methods
    private void validateSize(int size) {
        if (size < MIN_SIZE || size > MAX_SIZE) {
            throw new IllegalArgumentException("Size must be between " + 
                                              MIN_SIZE + " and " + MAX_SIZE);
        }
    }
    
    // Private method có thể được gọi từ default methods
    default int processSize(int size) {
        validateSize(size);
        return size * 2;
    }
}
```

```java
// File: Paintable.java
// Package: com.javazero.lab07

// ========== INTERFACE KHÁC ==========
public interface Paintable {
    public void paint(String color);
    public void applyCoating();
    
    default void prepareSurface() {
        System.out.println("Preparing surface for painting...");
    }
}
```

```java
// File: Circle.java (UPDATE)
// Package: com.javazero.lab07

// ========== CIRCLE IMPLEMENTS MULTIPLE INTERFACES ==========
public class Circle implements Drawable, Paintable {
    private double radius;
    private String color;
    
    public Circle(double radius, String color) {
        this.radius = radius;
        this.color = color;
    }
    
    // ========== OVERRIDE TỪ DRAWABLE ==========
    @Override
    public void draw() {
        System.out.println("Drawing Circle with radius: " + radius);
    }
    
    @Override
    public void erase() {
        System.out.println("Erasing Circle");
    }
    
    // Override default method
    @Override
    public void display() {
        System.out.println("Displaying Circle: Radius=" + radius + ", Color=" + color);
    }
    
    // ========== OVERRIDE TỪ PAINTABLE ==========
    @Override
    public void paint(String newColor) {
        System.out.println("Painting Circle with color: " + newColor);
        this.color = newColor;
    }
    
    @Override
    public void applyCoating() {
        System.out.println("Applying coating to Circle");
    }
    
    // ========== GETTERS ==========
    public double getRadius() {
        return radius;
    }
    
    public String getColor() {
        return color;
    }
    
    // ========== AREA METHOD ==========
    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```

```java
// File: InterfaceDemo.java
// Package: com.javazero.lab07

public class InterfaceDemo {
    public static void main(String[] args) {
        System.out.println("=== INTERFACE DEMO ===");
        
        // ========== INTERFACE CANNOT BE INSTANTIATED ==========
        System.out.println("\n--- Cannot instantiate interface ---");
        // Drawable d = new Drawable(); // COMPILE ERROR!
        System.out.println("Interface là abstract - không thể tạo object!");
        
        // ========== TẠO CLASS IMPLEMENT INTERFACE ==========
        System.out.println("\n--- Create Circle (implements Drawable & Paintable) ---");
        Circle circle = new Circle(5.0, "Red");
        
        // ========== CALL INTERFACE METHODS ==========
        System.out.println("\n--- Call interface methods ---");
        circle.draw();
        circle.erase();
        circle.paint("Blue");
        circle.applyCoating();
        
        // ========== DEFAULT METHODS ==========
        System.out.println("\n--- Default methods ---");
        circle.display();           // Override default
        circle.setColor("Green");   // Default từ Drawable
        circle.prepareSurface();   // Default từ Paintable
        
        // ========== STATIC METHODS ==========
        System.out.println("\n--- Static methods ---");
        Drawable.showToolInfo();
        System.out.println("Min size: " + Drawable.getMinSize());
        
        // ========== POLYMORPHISM VỚI INTERFACE ==========
        System.out.println("\n--- Polymorphism với Interface ---");
        Drawable drawable = new Circle(3.0, "Yellow");
        drawable.draw(); // Gọi Circle's draw()
        // drawable.paint("Red"); // LỖI! paint() không có trong Drawable
        
        Paintable paintable = new Circle(4.0, "Purple");
        paintable.paint("Orange");
        // paintable.draw(); // LỖI! draw() không có trong Paintable
        
        // ========== MULTIPLE INTERFACES ==========
        System.out.println("\n--- Implement multiple interfaces ---");
        Circle c = new Circle(2.0, "Pink");
        c.draw();
        c.paint("Black");
        c.prepareSurface();
        
        // ========== PRIVATE METHODS ==========
        System.out.println("\n--- Private methods in interface ---");
        // circle.validateSize(50); // LỖI! Private
        System.out.println("Processed size: " + circle.processSize(50));
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab07/Drawable.java com/javazero/lab07/Paintable.java com/javazero/lab07/Circle.java com/javazero/lab07/InterfaceDemo.java
// java com.javazero.lab07.InterfaceDemo

// Output:
// === INTERFACE DEMO ===
// 
// --- Cannot instantiate interface ---
// Interface là abstract - không thể tạo object!
// 
// --- Create Circle (implements Drawable & Paintable) ---
// 
// --- Call interface methods ---
// Drawing Circle with radius: 5.0
// Erasing Circle
// Painting Circle with color: Blue
// Applying coating to Circle
// 
// --- Default methods ---
// Displaying Circle: Radius=5.0, Color=Blue
// Setting color to: Green
// Preparing surface for painting...
// 
// --- Static methods ---
// Default drawing tool: Pencil
// Min size: 1
// 
// --- Polymorphism với Interface ---
// Drawing Circle with radius: 3.0
// Painting Circle with color: Orange
// 
// --- Implement multiple interfaces ---
// Drawing Circle with radius: 2.0
// Painting Circle with color: Black
// Preparing surface for painting...
// 
// --- Private methods in interface ---
// Processed size: 100
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! Circle implements cả Drawable và Paintable! Java cho phép implements nhiều interfaces!"

*   **[Anh Đô]:** "Nam hiểu đúng rồi! Đây là cách Java hỗ trợ 'multiple inheritance' - thông qua interfaces. Class chỉ extends một class, nhưng implements nhiều interfaces."

*   **[Việt (Intern)]:** "Dạ default methods có thể override?"

*   **[Em Hải]:** "Đúng rồi! Default methods có thể override trong implementing class."

*   **[Hùng (Intern)]:** "Dạ còn static methods của interface?"

*   **[Anh Vương]:** "Interface static methods thuộc về interface, gọi bằng InterfaceName.methodName(). Không cần instance."

---

### BƯỚC 3: Abstract Class vs Interface

*   **Hội ý:**

*   **[Anh Khánh]:** "Đây là câu hỏi phỏng vấn kinh điển! Abstract class và interface khác nhau ở nhiều điểm."

*   **[Anh Đô]:** "Bảng so sánh:"

| Aspect | Abstract Class | Interface |
|--------|---------------|-----------|
| Methods | Abstract + Concrete | Trước Java 8: chỉ abstract. Java 8+: + default + static |
| Variables | Có thể có | Chỉ public static final |
| Constructors | Có | Không |
| Access modifiers | Tất cả | Chỉ public (trước Java 9) |
| Inheritance | Chỉ 1 | Nhiều |
| State | Có (instance variables) | Không |

*   **[Em Hải]:** "Chọn abstract class khi: 1) Classes có quan hệ IS-A chặt chẽ, 2) Cần chia sẻ code giữa subclasses, 3) Cần non-public members."

*   **[Anh Vương]:** "Chọn interface khi: 1) Định nghĩa CONTRACT, 2) Hỗ trợ multiple inheritance, 3) Các classes không liên quan nhưng cùng contract."

---

*   **Thực hiện:**

```java
// File: AbstractVsInterfaceDemo.java
// Package: com.javazero.lab07

// ========== ABSTRACT CLASS - CÓ STATE ==========
abstract class Animal {
    protected String name;
    protected int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Abstract methods
    public abstract void makeSound();
    
    // Concrete method
    public void sleep() {
        System.out.println(name + " is sleeping...");
    }
    
    // Getter
    public String getName() {
        return name;
    }
}

// ========== INTERFACE - CONTRACT ONLY ==========
interface Pet {
    void play();
    void beFriendly();
    
    default void showLove() {
        System.out.println("Showing love...");
    }
}

// ========== DOG EXTENDS ANIMAL IMPLEMENTS PET ==========
class Dog extends Animal implements Pet {
    public Dog(String name, int age) {
        super(name, age);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " says: Gừ gừ!");
    }
    
    @Override
    public void play() {
        System.out.println(name + " is playing fetch!");
    }
    
    @Override
    public void beFriendly() {
        System.out.println(name + " is being friendly!");
    }
}

public class AbstractVsInterfaceDemo {
    public static void main(String[] args) {
        System.out.println("=== ABSTRACT CLASS VS INTERFACE DEMO ===");
        
        Dog dog = new Dog("Buddy", 3);
        
        // Từ Animal (abstract class)
        System.out.println("\n--- From Animal (Abstract Class) ---");
        System.out.println("Name: " + dog.getName());
        dog.makeSound();
        dog.sleep();
        
        // Từ Pet (interface)
        System.out.println("\n--- From Pet (Interface) ---");
        dog.play();
        dog.beFriendly();
        dog.showLove();
        
        // Polymorphism
        System.out.println("\n--- Polymorphism ---");
        Animal animal = new Dog("Max", 5);
        animal.makeSound();
        // animal.play(); // LỖI! Animal không có play()
        
        Pet pet = new Dog("Charlie", 2);
        pet.play();
        pet.beFriendly();
        // pet.getName(); // LỖI! Pet không có getName()
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab07/AbstractVsInterfaceDemo.java
// java com.javazero.lab07.AbstractVsInterfaceDemo

// Output:
// === ABSTRACT CLASS VS INTERFACE DEMO ===
// 
// --- From Animal (Abstract Class) ---
// Name: Buddy
// Buddy says: Gừ gừ!
// Buddy is sleeping...
// 
// --- From Pet (Interface) ---
// Buddy is playing fetch!
// Buddy is being friendly!
// Showing love...
// 
// --- Polymorphism ---
// Max says: Gừ gừ!
```

---

### BƯỚC 4: Encapsulation (Đóng gói)

*   **Hội ý:**

*   **[Anh Khánh]:** "Encapsulation là đóng gói dữ liệu và methods vào một unit (class), và kiểm soát truy cập thông qua access modifiers."

*   **[Anh Đô]:** "Encapsulation = Data Hiding + Methods to Access Data. Giấu implementation details, chỉ expose interface."

*   **[Em Hải (Clean Code)]:** "Quy tắc VÀNG: 1) LUÔN private fields, 2) Public getters và setters với validation, 3) Không expose internal implementation."

*   **[Hùng (Intern)]:** "Dạ access modifiers có mấy loại?"

*   **[Anh Vương]:** "4 Access Modifiers:"

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| private | ✓ | ✗ | ✗ | ✗ |
| (default) | ✓ | ✓ | ✗ | ✗ |
| protected | ✓ | ✓ | ✓ | ✗ |
| public | ✓ | ✓ | ✓ | ✓ |

---

*   **Thực hiện:**

```java
// File: BankAccount.java
// Package: com.javazero.lab07

// ========== FULL ENCAPSULATION ==========
public class BankAccount {
    // ========== PRIVATE FIELDS (DATA HIDING) ==========
    private String accountNumber;
    private String accountHolder;
    private double balance;
    private boolean isActive;
    
    // ========== PUBLIC CONSTANTS ==========
    public static final double MIN_BALANCE = 100.0;
    public static final double MAX_WITHDRAWAL = 10000.0;
    
    // ========== CONSTRUCTOR VỚI VALIDATION ==========
    public BankAccount(String accountNumber, String accountHolder, double initialBalance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.isActive = true;
        
        if (initialBalance >= MIN_BALANCE) {
            this.balance = initialBalance;
        } else {
            System.out.println("Initial balance too low. Setting to MIN_BALANCE.");
            this.balance = MIN_BALANCE;
        }
    }
    
    // ========== PUBLIC GETTERS (READ-ONLY) ==========
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
    
    // ========== PUBLIC SETTERS VỚI VALIDATION ==========
    public void setAccountHolder(String newHolder) {
        if (newHolder != null && !newHolder.trim().isEmpty()) {
            this.accountHolder = newHolder;
            System.out.println("Account holder updated to: " + newHolder);
        } else {
            System.out.println("Invalid account holder name!");
        }
    }
    
    // ========== BUSINESS METHODS VỚI VALIDATION ==========
    public void deposit(double amount) {
        if (amount > 0 && isActive) {
            balance += amount;
            System.out.println("Deposited: " + amount);
            System.out.println("New balance: " + balance);
        } else {
            System.out.println("Invalid deposit amount or inactive account!");
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance && amount <= MAX_WITHDRAWAL && isActive) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
            System.out.println("New balance: " + balance);
        } else {
            System.out.println("Invalid withdrawal!");
        }
    }
    
    public void transfer(BankAccount target, double amount) {
        if (this.balance >= amount && amount > 0 && this.isActive && target.isActive) {
            this.balance -= amount;
            target.balance += amount;
            System.out.println("Transferred " + amount + " to " + target.accountHolder);
        } else {
            System.out.println("Transfer failed!");
        }
    }
    
    // ========== PRIVATE HELPER METHOD ==========
    private void validateAccount() {
        if (balance < MIN_BALANCE) {
            isActive = false;
            System.out.println("Account deactivated due to low balance!");
        }
    }
    
    // ========== DISPLAY METHOD ==========
    public void displayInfo() {
        System.out.println("\n=== Bank Account Info ===");
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Holder: " + accountHolder);
        System.out.println("Balance: " + balance);
        System.out.println("Status: " + (isActive ? "Active" : "Inactive"));
    }
}
```

```java
// File: EncapsulationDemo.java
// Package: com.javazero.lab07

public class EncapsulationDemo {
    public static void main(String[] args) {
        System.out.println("=== ENCAPSULATION DEMO ===");
        
        // ========== CREATE ACCOUNT ==========
        BankAccount account1 = new BankAccount("123456", "Nguyễn Văn A", 500);
        account1.displayInfo();
        
        // ========== ACCESS THROUGH GETTERS ==========
        System.out.println("\n--- Access through getters ---");
        System.out.println("Account Number: " + account1.getAccountNumber());
        System.out.println("Holder: " + account1.getAccountHolder());
        System.out.println("Balance: " + account1.getBalance());
        
        // ========== MODIFY THROUGH SETTERS ==========
        System.out.println("\n--- Modify through setters ---");
        account1.setAccountHolder("Trần Thị B");
        
        // ========== BUSINESS METHODS ==========
        System.out.println("\n--- Business operations ---");
        account1.deposit(1000);
        account1.withdraw(500);
        
        // ========== ATTEMPT DIRECT ACCESS (LỖI!) ==========
        System.out.println("\n--- Direct access (LỖI!) ---");
        // account1.balance = 9999999; // COMPILE ERROR!
        // account1.accountNumber = "111111"; // COMPILE ERROR!
        System.out.println("→ Cannot access private fields directly!");
        System.out.println("→ Must use public methods!");
        
        // ========== TRANSFER BETWEEN ACCOUNTS ==========
        System.out.println("\n--- Transfer between accounts ---");
        BankAccount account2 = new BankAccount("789012", "Lê Văn C", 200);
        account1.transfer(account2, 300);
        
        account1.displayInfo();
        account2.displayInfo();
        
        // ========== VALIDATION DEMO ==========
        System.out.println("\n--- Validation demo ---");
        account1.withdraw(100000); // Vượt MAX_WITHDRAWAL
        account1.deposit(-100);   // Số âm
        
        // ========== COMPILE-TIME SAFETY ==========
        System.out.println("\n--- Compile-time safety ---");
        account1.setAccountHolder("");   // Invalid - rejected
        account1.setAccountHolder(null); // Invalid - rejected
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab07/BankAccount.java com/javazero/lab07/EncapsulationDemo.java
// java com.javazero.lab07.EncapsulationDemo

// Output:
// === ENCAPSULATION DEMO ===
// 
// === Bank Account Info ===
// Account Number: 123456
// Holder: Nguyễn Văn A
// Balance: 500.0
// Status: Active
// 
// --- Access through getters ---
// Account Number: 123456
// Holder: Nguyễn Văn A
// Balance: 500.0
// 
// --- Modify through setters ---
// Account holder updated to: Trần Thị B
// 
// --- Business operations ---
// Deposited: 1000.0
// New balance: 1500.0
// Withdrawn: 500.0
// New balance: 1000.0
// 
// --- Direct access (LỖI!) ---
// → Cannot access private fields directly!
// → Must use public methods!
// 
// --- Transfer between accounts ---
// Transferred 300.0 to Lê Văn C
// 
// === Bank Account Info ===
// Account Number: 123456
// Holder: Trần Thị B
// Balance: 700.0
// Status: Active
// 
// === Bank Account Info ===
// Account Number: 789012
// Holder: Lê Văn C
// Balance: 500.0
// Status: Regular
// 
// --- Validation demo ---
// Invalid withdrawal!
```

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ phá abstraction và encapsulation! Mỗi người gây 1 bug."

---

*   **Case 1: Abstract Method Not Implemented**

```java
// File: AbstractMethodBugDemo.java
// Package: com.javazero.lab07

abstract class Animal {
    public abstract void makeSound();
    public abstract void eat();
    public abstract void sleep();
}

// LỖI! Animal có 3 abstract methods, nhưng Dog chỉ implement 2!
// abstract class Dog extends Animal {
//     @Override
//     public void makeSound() {
//         System.out.println("Gừ gừ!");
//     }
//     
//     @Override
//     public void eat() {
//         System.out.println("Dog eating...");
//     }
//     // sleep() CHƯA implement!
// }

// Fix: Implement TẤT CẢ abstract methods
class DogFixed extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Gừ gừ!");
    }
    
    @Override
    public void eat() {
        System.out.println("Dog eating...");
    }
    
    @Override
    public void sleep() {
        System.out.println("Dog sleeping...");
    }
}
```

---

*   **Case 2: Interface Implementation Bug**

```java
// File: InterfaceBugDemo.java
// Package: com.javazero.lab07

interface Drawable {
    void draw();
    void erase();
}

// LỖI! Circle không implement erase()!
// class Circle implements Drawable {
//     @Override
//     public void draw() {
//         System.out.println("Drawing circle...");
//     }
//     // erase() chưa implement!
// }

// Fix:
class CircleFixed implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing circle...");
    }
    
    @Override
    public void erase() {
        System.out.println("Erasing circle...");
    }
}
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: Abstract class dùng khi có code chung, interface dùng khi chỉ cần contract. Abstract class có state, interface không."

*   **[Nam (Intern)]:** "Dạ em học được: Encapsulation là private fields + public getters/setters với validation. Bảo vệ dữ liệu."

*   **[Việt (Intern)]:** "Dạ em học được: Java 8+ cho phép default và static methods trong interface."

*   **[Cường (Intern)]:** "Dạ em học được: Access modifiers kiểm soát visibility: private < default < protected < public."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| Abstract class | ☐ | ☐ |
| Abstract methods | ☐ | ☐ |
| Interface | ☐ | ☐ |
| Default methods | ☐ | ☐ |
| Static methods in interface | ☐ | ☐ |
| Abstract class vs Interface | ☐ | ☐ |
| Encapsulation | ☐ | ☐ |
| Access modifiers | ☐ | ☐ |
| Getters and Setters | ☐ | ☐ |
| Data validation | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Tạo abstract class Vehicle với subclasses Car và Motorcycle.
2.  Tạo interface Resizable với method resize().
3.  Implement full encapsulation với Student class.
4.  So sánh abstract class và interface bằng ví dụ.
5.  Tạo interface có default methods và static methods.

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Abstract Methods and Classes
*   Oracle Java Tutorials: Interfaces
*   Effective Java: Item 20: Prefer interfaces to abstract classes

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab08 - Exception Handling!**
