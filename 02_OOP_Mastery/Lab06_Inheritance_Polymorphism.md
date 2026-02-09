# LAB 06 - INHERITANCE (KẾ THỪA) VÀ POLYMORPHISM (ĐA HÌNH) TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta sẽ học hai pillar quan trọng nhất của OOP: Inheritance (Kế thừa) và Polymorphism (Đa hình). Đây là những concept làm nên sức mạnh của Java."

*   **[Hùng (Intern)]:** "Dạ anh ơi, 'inheritance' là gì vậy anh? Em nghe nói nó giúp tái sử dụng code."

*   **[Anh Đô (Senior)]:** "Hùng hỏi hay! Inheritance là quan hệ IS-A (là-một). Ví dụ: Dog IS-A Animal, Car IS-A Vehicle. Class con kế thừa từ class cha, nhận được tất cả properties và methods của cha."

*   **[Nam (Intern)]:** "Dạ vậy nếu có class Animal với eat() và sleep(), class Dog kế thừa thì Dog cũng có eat() và sleep()?"

*   **[Anh Vương (Performance)]:** "Đúng rồi Nam! Dog sẽ có eat() và sleep() từ Animal. Ngoài ra, Dog có thể thêm methods riêng như bark() hoặc ghi đè (override) methods của cha."

*   **[Em Hải (Clean Code)]:** "Quy tắc: Inheritance giảm duplicate code. Nhưng KHÔNG nên lạm dụng - chỉ khi thực sự có quan hệ IS-A. Nếu chỉ có quan hệ HAS-A (có), dùng Composition thay vì Inheritance."

*   **[Việt (Intern)]:** "Dạ còn 'polymorphism' là gì anh? Nghe rất fancy!"

*   **[Anh Khánh]:** "Việt hỏi về polymorphism - đa hình. Đây là khả năng một object có thể có nhiều hình thức. Ví dụ: Dog object có thể được xem là Animal."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab06

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab06/
    └── src/
        └── com/
            └── javazero/
                └── lab06/
                    ├── Animal.java
                    ├── Dog.java
                    ├── Cat.java
                    ├── Bird.java
                    ├── Shape.java
                    ├── Circle.java
                    └── InheritanceDemo.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Inheritance cơ bản

*   **Hội ý:**

*   **[Anh Khánh]:** "Inheritance trong Java dùng từ khóa `extends`. Class con kế thừa từ class cha. Java chỉ hỗ trợ SINGLE INHERITANCE (một class chỉ kế thừa từ một class cha)."

*   **[Anh Đô]:** "Cú pháp: `class Child extends Parent { }`. Class con gọi là SUB CLASS hoặc DERIVED CLASS. Class cha gọi là SUPER CLASS hoặc BASE CLASS."

*   **[Em Hải (Clean Code)]:** "Quy tắc đặt tên: Class cha nên có tên tổng quát hơn (Animal, Vehicle), class con cụ thể hơn (Dog, Car)."

*   **[Hùng (Intern)]:** "Dạ Java không hỗ trợ multiple inheritance với classes?"

*   **[Anh Vương]:** "Đúng rồi Hùng! Java chỉ cho phép một parent class. Lý do là tránh 'Diamond Problem' - xung đột khi hai cha có cùng method. Tuy nhiên, một class có thể implement nhiều interfaces."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo inheritance cơ bản đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: Animal.java
// Package: com.javazero.lab06

// ========== SUPER CLASS (BASE CLASS) ==========
public class Animal {
    // ========== INSTANCE VARIABLES ==========
    protected String name;      // protected: accessible trong subclass
    protected int age;
    
    // ========== DEFAULT CONSTRUCTOR ==========
    public Animal() {
        System.out.println("Animal constructor called");
        this.name = "Unknown";
        this.age = 0;
    }
    
    // ========== PARAMETERIZED CONSTRUCTOR ==========
    public Animal(String name, int age) {
        System.out.println("Animal constructor with params called");
        this.name = name;
        this.age = age;
    }
    
    // ========== INSTANCE METHODS ==========
    public void eat() {
        System.out.println(name + " đang ăn...");
    }
    
    public void sleep() {
        System.out.println(name + " đang ngủ...");
    }
    
    public void makeSound() {
        System.out.println(name + " phát ra âm thanh...");
    }
    
    // ========== GETTER METHODS ==========
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public void displayInfo() {
        System.out.println("=== Thông tin Animal ===");
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
    }
}
```

```java
// File: Dog.java
// Package: com.javazero.lab06

// ========== SUB CLASS (DERIVED CLASS) ==========
// Dog kế thừa từ Animal
public class Dog extends Animal {
    // ========== ADDITIONAL VARIABLES ==========
    private String breed; // Breed chỉ có ở Dog
    
    // ========== DEFAULT CONSTRUCTOR ==========
    public Dog() {
        // super() được gọi ngầm định nếu không gọi tường minh
        System.out.println("Dog constructor called");
        this.breed = "Unknown";
    }
    
    // ========== PARAMETERIZED CONSTRUCTOR ==========
    public Dog(String name, int age, String breed) {
        super(name, age); // Gọi constructor của cha tường minh
        System.out.println("Dog constructor with params called");
        this.breed = breed;
    }
    
    // ========== OVERRIDING METHOD ==========
    // Ghi đè makeSound() của Animal
    @Override
    public void makeSound() {
        System.out.println(name + " sủa: Gừ gừ!");
    }
    
    // ========== METHODS RIÊNG Của DOG ==========
    public void bark() {
        System.out.println(name + " đang sủa!");
    }
    
    public void fetch() {
        System.out.println(name + " đang đi lấy bóng!");
    }
    
    // ========== GETTER/SETTER CHO BREED ==========
    public String getBreed() {
        return breed;
    }
    
    public void setBreed(String breed) {
        this.breed = breed;
    }
    
    // ========== DISPLAY OVERRIDE ==========
    @Override
    public void displayInfo() {
        System.out.println("=== Thông tin Dog ===");
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        System.out.println("Giống: " + breed);
    }
}
```

```java
// File: InheritanceDemo.java
// Package: com.javazero.lab06

public class InheritanceDemo {
    public static void main(String[] args) {
        System.out.println("=== INHERITANCE DEMO ===");
        
        // ========== TẠO ANIMAL ==========
        System.out.println("\n--- Tạo Animal ---");
        Animal animal = new Animal("Generic Animal", 3);
        animal.displayInfo();
        animal.eat();
        animal.sleep();
        animal.makeSound();
        
        // ========== TẠO DOG ==========
        System.out.println("\n--- Tạo Dog ---");
        Dog dog = new Dog("Buddy", 5, "Golden Retriever");
        dog.displayInfo();
        
        // ========== DOG CÓ METHODS TỪ ANIMAL ==========
        System.out.println("\n--- Dog có methods từ Animal ---");
        dog.eat();      // Từ Animal
        dog.sleep();    // Từ Animal
        dog.makeSound(); // Override của Dog
        
        // ========== DOG CÓ METHODS RIÊNG ==========
        System.out.println("\n--- Dog có methods riêng ---");
        dog.bark();     // Riêng của Dog
        dog.fetch();    // Riêng của Dog
        
        // ========== DOG IS-AN ANIMAL ==========
        System.out.println("\n--- Polymorphism: Dog IS-AN Animal ---");
        Animal myDog = new Dog("Max", 3, "Poodle");
        myDog.eat();      // Animal.eat() được gọi
        myDog.sleep();    // Animal.sleep() được gọi
        // myDog.bark();  // LỖI! Animal không có bark()
        
        System.out.println("\n--- Access methods riêng của Dog ---");
        if (myDog instanceof Dog) {
            Dog castedDog = (Dog) myDog;
            castedDog.bark(); // Bây giờ có thể gọi
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab06/Animal.java com/javazero/lab06/Dog.java com/javazero/lab06/InheritanceDemo.java
// java com.javazero.lab06.InheritanceDemo

// Output:
// === INHERITANCE DEMO ===
// 
// --- Tạo Animal ---
// Animal constructor with params called
// === Thông tin Animal ===
// Tên: Generic Animal
// Tuổi: 3
// Generic Animal đang ăn...
// Generic Animal đang ngủ...
// Generic Animal phát ra âm thanh...
// 
// --- Tạo Dog ---
// Animal constructor with params called
// Dog constructor with params called
// === Thông tin Dog ===
// Tên: Buddy
// Tuổi: 5
// Giống: Golden Retriever
// 
// --- Dog có methods từ Animal ---
// Buddy đang ăn...
// Buddy đang ngủ...
// Buddy sủa: Gừ gừ!
// 
// --- Dog có methods riêng ---
// Buddy đang sủa!
// Buddy đang đi lấy bóng!
// 
// --- Polymorphism: Dog IS-AN Animal ---
// Animal constructor with params called
// Dog constructor with params called
// Max đang ăn...
// Max đang ngủ...
// 
// --- Access methods riêng của Dog ---
// Buddy đang sủa!
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! Khi tạo Dog, Animal constructor được gọi trước! Sao vậy?"

*   **[Anh Đô]:** "Việt phát hiện hay! Constructor của cha luôn được gọi TRƯỚC khi constructor của con chạy. Đây gọi là constructor chaining."

*   **[Nam (Intern)]:** "Dạ super() là gì anh?"

*   **[Em Hải]:** "super() gọi constructor của cha. Nếu không gọi tường minh, Java sẽ gọi super() không tham số ngầm định."

*   **[Hùng (Intern)]:** "Dạ còn @Override là gì anh?"

*   **[Anh Vương]:** "@Override là annotation, báo cho Java biết method này đang ghi đè method của cha. Nếu method cha không tồn tại, compiler báo lỗi."

*   **[Cường (Intern)]:** "Dạ Polymorphism là gì? myDog.eat() gọi Animal hay Dog?"

*   **[Anh Khánh]:** "Cường hỏi hay! Đây là RUNTIME POLYMORPHISM. Khi gọi myDog.eat(), JVM xem actual object type (Dog), nếu Dog có override eat(), gọi Dog's eat()."

---

### BƯỚC 2: SUPER keyword

*   **Hội ý:**

*   **[Anh Khánh]:** "super là reference đến parent class object. Dùng để truy cập methods và variables của cha."

*   **[Anh Đô]:** "super có 3 công dụng chính: 1) Gọi parent constructor (super()), 2) Gọi parent method (super.methodName()), 3) Truy cập parent variable (super.variableName())."

*   **[Em Hải (Clean Code)]:** "Dùng super khi cần gọi logic của cha trong method đã override. Ví dần: super.calculate() trong subclass calculate()."

*   **[Hùng (Intern)]:** "Dạ super khác gì this anh?"

*   **[Anh Vương]:** "this = reference đến object hiện tại. super = reference đến parent class của object hiện tại."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Việt, em viết code demo super keyword đi?"

*   **[Việt (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: SuperDemo.java
// Package: com.javazero.lab06

class Animal {
    protected String name = "Animal";
    protected int age = 10;
    
    public Animal(String name) {
        this.name = name;
        System.out.println("Animal constructor: " + name);
    }
    
    public void speak() {
        System.out.println("Animal speaks: ...");
    }
    
    public void eat() {
        System.out.println(name + " đang ăn...");
    }
}

class Cat extends Animal {
    private String color;
    
    public Cat(String name, String color) {
        super(name); // Gọi Animal constructor
        this.color = color;
        System.out.println("Cat constructor: " + color);
    }
    
    @Override
    public void speak() {
        System.out.println(name + " kêu: Meo meo!");
    }
    
    public void showInfo() {
        // super để truy cập parent's variables
        System.out.println("Tên (this): " + this.name);
        System.out.println("Tên (super): " + super.name);
        System.out.println("Tuổi: " + super.age);
        System.out.println("Màu lông: " + this.color);
    }
    
    public void callParentMethod() {
        // Gọi method của cha
        System.out.println("\n--- Gọi parent method ---");
        this.speak();     // Cat's speak()
        super.speak();    // Animal's speak()
        this.eat();       // Cat's eat() hoặc Animal's eat()
        super.eat();      // Animal's eat()
    }
}

public class SuperDemo {
    public static void main(String[] args) {
        System.out.println("=== SUPER KEYWORD DEMO ===");
        
        // ========== SUPER TRONG CONSTRUCTOR ==========
        System.out.println("\n--- Constructor với super() ---");
        Cat cat = new Cat("Kitty", "Vàng");
        
        // ========== SUPER ĐỂ TRUY CẬP PARENT ==========
        System.out.println("\n--- super để truy cập parent ---");
        cat.showInfo();
        
        // ========== SUPER ĐỂ GỌI PARENT METHOD ==========
        System.out.println("\n--- super để gọi parent method ---");
        cat.callParentMethod();
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab06/SuperDemo.java
// java com.javazero.lab06.SuperDemo

// Output:
// === SUPER KEYWORD DEMO ===
// 
// --- Constructor với super() ---
// Animal constructor: Kitty
// Cat constructor: Vàng
// 
// --- super để truy cập parent ---
// Tên (this): Kitty
// Tên (super): Kitty
// Tuổi: 10
// Màu lông: Vàng
// 
// --- super để gọi parent method ---
// 
// --- Gọi parent method ---
// Kitty kêu: Meo meo!
// Kitty đang ăn...
// Kitty đang ăn...
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! super.speak() gọi Animal's speak() trong khi this.speak() gọi Cat's speak()!"

*   **[Anh Đô]:** "Nam hiểu đúng rồi! super.methodName() gọi method TỪ CHA, bất kể con có override hay không."

*   **[Hùng (Intern)]:** "Dạ super() phải là dòng đầu tiên trong constructor?"

*   **[Em Hải]:** "Đúng rồi! super() hoặc this() phải là statement đầu tiên trong constructor. Không thể gọi cả hai."

*   **[Việt (Intern)]:** "Dạ còn super.name và this.name đều in 'Kitty'?"

*   **[Anh Vương]:** "Vì cat.name được set = 'Kitty' trong Animal constructor (super(name)). Nên cả this.name và super.name đều = 'Kitty'."

---

### BƯỚC 3: Method Overriding

*   **Hội ý:**

*   **[Anh Khánh]:** "Method Overriding (ghi đè) là khi subclass cung cấp implementation cụ thể hơn cho method đã được định nghĩa trong superclass."

*   **[Anh Đô]:** "Quy tắc Overriding: 1) Phương thức phải CÓ TRONG CHA, 2) Cùng TÊN, 3) Cùng THAM SỐ, 4) Cùng hoặc WIDER RETURN TYPE, 5) KHÔNG thể override static method."

*   **[Em Hải (Clean Code)]:** "@Override annotation giúp phát hiện lỗi. LUÔN dùng @Override khi ghi đè method."

*   **[Hùng (Intern)]:** "Dạ sao không thể override static method anh?"

*   **[Anh Vương]:** "Static methods thuộc về CLASS, không phải OBJECT. Subclass không override static method - nó có thể HIDING (che khuất) static method của cha."

---

*   **Thực hiện:**

```java
// File: MethodOverridingDemo.java
// Package: com.javazero.lab06

class Vehicle {
    public void start() {
        System.out.println("Vehicle đang khởi động...");
    }
    
    public void stop() {
        System.out.println("Vehicle đang dừng...");
    }
    
    public static void test() {
        System.out.println("Vehicle static test");
    }
}

class Car extends Vehicle {
    @Override
    public void start() {
        System.out.println("Car đang khởi động: Bật máy!");
    }
    
    @Override
    public void stop() {
        System.out.println("Car đang dừng: Tắt máy!");
    }
    
    // STATIC HIDING (không phải overriding!)
    public static void test() {
        System.out.println("Car static test");
    }
    
    public void drive() {
        System.out.println("Car đang lái...");
    }
}

class Motorcycle extends Vehicle {
    @Override
    public void start() {
        System.out.println("Motorcycle đang khởi động: Đề xe!");
    }
    
    // KHÔNG override stop() - dùng của Vehicle
}

public class MethodOverridingDemo {
    public static void main(String[] args) {
        System.out.println("=== METHOD OVERRIDING DEMO ===");
        
        // ========== OVERRIDING ==========
        System.out.println("\n--- Overriding Methods ---");
        Vehicle vehicle = new Vehicle();
        vehicle.start();
        
        Car car = new Car();
        car.start();
        
        Motorcycle motorcycle = new Motorcycle();
        motorcycle.start();
        
        // ========== POLYMORPHISM ==========
        System.out.println("\n--- Polymorphism ---");
        Vehicle myCar = new Car();
        myCar.start(); // Gọi Car's start()
        
        Vehicle myMotor = new Motorcycle();
        myMotor.start(); // Gọi Motorcycle's start()
        
        // ========== STATIC METHOD HIDING ==========
        System.out.println("\n--- Static Method Hiding ---");
        Vehicle.test(); // Vehicle's test
        Car.test();    // Car's test
        
        Vehicle myCar2 = new Car();
        myCar2.test(); // Vehicle's test (reference type!)
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab06/MethodOverridingDemo.java
// java com.javazero.lab06.MethodOverridingDemo

// Output:
// === METHOD OVERRIDING DEMO ===
// 
// --- Overriding Methods ---
// Vehicle đang khởi động...
// Car đang khởi động: Bật máy!
// Motorcycle đang khởi động: Đề xe!
// 
// --- Polymorphism ---
// Car đang khởi động: Bật máy!
// Motorcycle đang khởi động: Đề xe!
// 
// --- Static Method Hiding ---
// Vehicle static test
// Car static test
// Vehicle static test
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "ANH ƠI! myCar.start() gọi Car.start() dù myCar là Vehicle type!"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! Đây là RUNTIME POLYMORPHISM. JVM xem actual object type (new Car()), không phải reference type (Vehicle)."

*   **[Nam (Intern)]:** "Dạ static method thì khác! myCar2.test() gọi Vehicle.test()!"

*   **[Em Hải]:** "Nam phát hiện hay! Static methods được RESOLVE dựa trên REFERENCE TYPE, không phải object type. Đây là STATIC BINDING."

*   **[Hùng (Intern)]:** "Dạ vậy khi nào dùng overriding, khi nào dùng overloading?"

*   **[Anh Vương]:** "Overloading (cùng class, khác params) = COMPILE TIME. Overriding (cha-con, cùng signature) = RUNTIME."

---

### BƯỚC 4: Polymorphism (Đa hình)

*   **Hội ý:**

*   **[Anh Khánh]:** "Polymorphism là khả năng một object có thể được xem là nhiều kiểu khác nhau. Cùng một method, nhiều hành vi khác nhau."

*   **[Anh Đô]:** "Hai loại polymorphism: 1) Compile-time (Overloading, Early binding), 2) Runtime (Overriding, Late binding)."

*   **[Em Hải (Clean Code)]:** "Polymorphism giúp code LINH HOẠT và MỞ RỘNG. Thay vì viết nhiều if-else, dùng polymorphism với interface/abstraction."

*   **[Hùng (Intern)]:** "Dạ ví dụ thực tế của polymorphism?"

*   **[Anh Vương]:** "Ví dụ: Shape với draw() được Circle, Rectangle, Triangle override. Graphics code chỉ gọi shape.draw(), không cần biết shape là gì."

---

*   **Thực hiện:**

```java
// File: Shape.java
// Package: com.javazero.lab06

// ========== ABSTRACT CLASS (SẼ HỌC TRONG LAB SAU) ==========
// Đây là BASE CLASS cho tất cả hình
abstract class Shape {
    protected String color;
    
    public Shape(String color) {
        this.color = color;
    }
    
    // Abstract method - phải được override
    public abstract double getArea();
    
    // Concrete method
    public void display() {
        System.out.println("Hình màu: " + color);
    }
}

class Circle extends Shape {
    private double radius;
    
    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }
    
    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    public void display() {
        System.out.println("Hình tròn - Màu: " + color + ", Bán kính: " + radius);
    }
}

class Rectangle extends Shape {
    private double width;
    private double height;
    
    public Rectangle(String color, double width, double height) {
        super(color);
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double getArea() {
        return width * height;
    }
    
    @Override
    public void display() {
        System.out.println("Hình chữ nhật - Màu: " + color + ", W: " + width + ", H: " + height);
    }
}

class Triangle extends Shape {
    private double base;
    private double height;
    
    public Triangle(String color, double base, double height) {
        super(color);
        this.base = base;
        this.height = height;
    }
    
    @Override
    public double getArea() {
        return 0.5 * base * height;
    }
}

public class PolymorphismDemo {
    // ========== POLYMORPHIC METHOD ==========
    public static void printShapeInfo(Shape shape) {
        // shape có thể là Circle, Rectangle, hoặc Triangle
        System.out.println("\n=== Thông tin Shape ===");
        shape.display();
        System.out.println("Diện tích: " + shape.getArea());
    }
    
    public static void main(String[] args) {
        System.out.println("=== POLYMORPHISM DEMO ===");
        
        // ========== TẠO CÁC SHAPES ==========
        Circle circle = new Circle("Đỏ", 5.0);
        Rectangle rectangle = new Rectangle("Xanh", 4.0, 6.0);
        Triangle triangle = new Triangle("Vàng", 3.0, 4.0);
        
        // ========== POLYMORPHIC ARRAY ==========
        System.out.println("\n--- Polymorphic Array ---");
        Shape[] shapes = {circle, rectangle, triangle};
        
        for (Shape shape : shapes) {
            shape.display();
            System.out.println("Diện tích: " + shape.getArea());
            System.out.println("---");
        }
        
        // ========== POLYMORPHIC PARAMETER ==========
        System.out.println("\n--- Polymorphic Parameter ---");
        printShapeInfo(circle);
        printShapeInfo(rectangle);
        printShapeInfo(triangle);
        
        // ========== LỢI ÍCH CỦA POLYMORPHISM ==========
        System.out.println("\n--- Lợi ích của Polymorphism ---");
        System.out.println("1. Code viết một lần, dùng cho nhiều kiểu");
        System.out.println("2. Dễ mở rộng (thêm hình mới không sửa code cũ)");
        System.out.println("3. Code LINH HOẠT và DỄ BẢO TRÌ");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab06/PolymorphismDemo.java
// java com.javazero.lab06.PolymorphismDemo

// Output:
// === POLYMORPHISM DEMO ===
// 
// --- Polymorphic Array ---
// Hình tròn - Màu: Đỏ, Bán kính: 5.0
// Diện tích: 78.53981633974483
// 
// Hình chữ nhật - Màu: Xanh, W: 4.0, H: 6.0
// Diện tích: 24.0
// 
// Hình chữ nhật - Màu: Vàng, B: 3.0, H: 4.0
// Diện tích: 6.0
// 
// --- Polymorphic Parameter ---
// 
// === Thông tin Shape ===
// Hình tròn - Màu: Đỏ, Bán kính: 5.0
// Diện tích: 78.53981633974483
// 
// === Thông tin Shape ===
// Hình chữ nhật - Màu: Xanh, W: 4.0, H: 6.0
// Diện tích:  Inheritance

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! printShapeInfo(Shape shape) nhận Circle, Rectangle, Triangle! Sao thế?"

*   **[Anh Đô]:** "Nam hiểu đúng rồi! Circle IS-A Shape, Rectangle IS-A Shape, Triangle IS-A Shape. Nên có thể truyền subclass object vào method expecting superclass."

*   **[Việt (Intern)]:** "Dạ cái này gọi là gì anh?"

*   **[Em Hải]:** "Gọi là UP-CASTING (ngầm định, không cần cast). Subclass được tự động convert thành superclass type."

*   **[Hùng (Intern)]:** "Dạ còn DOWN-CASTING?"

*   **[Anh Vương]:** "Down-casting là ngược lại: Superclass -> Subclass. Cần CAST TƯỜNG MINH và CÓ THỂ throw ClassCastException nếu không đúng kiểu."

---

### BƯỚC 5: instanceof và Type Casting

*   **Hội ý:**

*   **[Anh Khánh]:** "instanceof kiểm tra object có phải là instance của một class cụ thể không. Trả về true/false."

*   **[Anh Đô]:** "Casting chuyển đổi kiểu. Up-casting (con -> cha) tự động. Down-casting (cha -> con) cần cast tường minh."

*   **[Em Hải]:** "Trước khi down-cast, LUÔN kiểm tra instanceof. Tránh ClassCastException."

*   **[Hùng (Intern)]:** "Dạ ClassCastException là gì?"

*   **[Anh Vương]:** "Exception khi cố cast object sang kiểu không tương thích. Ví dụ: Circle không phải Rectangle."

---

*   **Thực hiện:**

```java
// File: TypeCastingDemo.java
// Package: com.javazero.lab06

class Animal {
    public void makeSound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Gừ gừ!");
    }
    
    public void bark() {
        System.out.println("Gâu gâu!");
    }
}

class Cat extends Animal {
    @Override
    public void sound() {
        System.out.println("Meo meo!");
    }
    
    public void meow() {
        System.out.println("Meo meo!");
    }
}

public class TypeCastingDemo {
    public static void main(String[] Up-Casting (Implicit) ---
        Animal animal = new Dog(); // Dog -> Animal
        animal.makeSound(); // Gọi Dog's makeSound()
        
        // ========== DOWN-CASTING (EXPLICIT) ==========
        System.out.println("\n--- Down-Casting ---");
        Animal myAnimal = new Dog();
        
        // Cách 1: Không kiểm tra (NGUY HIỂM!)
        // Dog d = (Dog) myAnimal; // OK vì myAnimal thực ra là Dog
        
        // Cách 2: Kiểm tra với instanceof (AN TOÀN!)
        if (myAnimal instanceof Dog) {
            Dog d = (Dog) myAnimal;
            d.bark(); // Bây giờ có thể gọi Dog methods
        } else {
            System.out.println("myAnimal không phải Dog!");
        }
        
        // ========== POLYMORPHIC PROCESSING ==========
        System.out.println("\n--- Polymorphic Processing ---");
        Animal[] animals = {
            new Dog(),
            new Cat(),
            new Dog(),
            new Cat()
        };
        
        for (Animal a : animals) {
            a.makeSound();
            
            // Kiểm tra kiểu cụ thể
            if (a instanceof Dog) {
                ((Dog) a).bark();
            } else if (a instanceof Cat) {
                ((Cat) a).meow();
            }
        }
        
        // ========== CLASS CAST EXCEPTION DEMO ==========
        System.out.println("\n--- ClassCastException (NGUY HIỂM!) ---");
        Animal cat = new Cat();
        
        // LỖI! Cat không phải Dog
        // Dog dog = (Dog) cat; // ClassCastException!
        
        // Fix: Kiểm tra trước
        if (cat instanceof Dog) {
            Dog dog = (Dog) cat;
        } else {
            System.out.println("Cat không phải Dog!");
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab06/TypeCastingDemo.java
// java com.javazero.lab06.TypeCastingDemo

// Output:
// === TYPE CASTING DEMO ===
// 
// --- Up-Casting (Implicit) ---
// Gừ gừ!
// 
// --- Down-Casting ---
// Gâu gâu!
// 
// --- Polymorphic Processing ---
// Gừ gừ!
// Gâu gâu!
// Meo meo!
// Gừ gừ!
// Gâu gâu!
// 
// --- ClassCastException (NGUY HIỂM!) ---
// Cat không phải Dog!
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! instanceof rất hữu ích! Tránh ClassCastException!"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! instanceof kiểm tra trước khi cast. LUÔN dùng instanceof trước down-casting."

*   **[Nam (Intern)]:** "Dạ sao a.makeSound() gọi Dog's hay Cat's makeSound()?"

*   **[Em Hải]:** "Đó là polymorphism! a là Dog hay Cat (thực tế), nên gọi method tương ứng."

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ phá inheritance! Mỗi người gây 1 bug."

---

*   **Case 1: Constructor Chaining Bug**

```java
// File: ConstructorChainingBugDemo.java
// Package: com.javazero.lab06

class Parent {
    public Parent() {
        System.out.println("Parent constructor");
    }
}

class Child extends Parent {
    public Child() {
        // super() được gọi ngầm định
        System.out.println("Child constructor");
    }
    
    public Child(String name) {
        System.out.println("Child constructor: " + name);
        // super() được gọi ngầm định ở đây
    }
}

// NẾU parent không có default constructor
class Parent2 {
    private String name;
    
    public Parent2(String name) {
        this.name = name;
    }
}

// LỖI! Parent2 không có default constructor
// class Child2 extends Parent2 {
//     public Child2() {
//         super(); // LỖI! Parent2 không có default constructor
//     }
// }
```

---

*   **Case 2: Override vs Overload Bug**

```java
// File: OverrideOverloadBugDemo.java
// Package: com.javazero.lab06

class Base {
    public void display(String msg) {
        System.out.println("Base: " + msg);
    }
}

class Derived extends Base {
    // ĐÂY LÀ OVERLOAD, KHÔNG PHẢI OVERRIDE!
    public void display(int num) {
        System.out.println("Derived: " + num);
    }
    
    // ĐÂY LÀ OVERRIDE
    @Override
    public void display(String msg) {
        System.out.println("Derived Override: " + msg);
    }
}

public class OverrideOverloadBugDemo {
    public static void main(String[] args) {
        Derived d = new Derived();
        d.display("Hello");  // Gọi display(String) - override
        d.display(123);     // Gọi display(int) - overload
    }
}
```

---

*   **Case 3: Access Modifier Bug**

```java
// File: AccessModifierBugDemo.java
// Package: com.javazero.lab06

class BaseClass {
    private void privateMethod() {
        System.out.println("Private method");
    }
    
    void defaultMethod() {
        System.out.println("Default method");
    }
    
    protected void protectedMethod() {
        System.out.println("Protected method");
    }
    
    public void publicMethod() {
        System.out.println("Public method");
    }
}

class SubClass extends BaseClass {
    public void test() {
        // privateMethod(); // LỖI! Private không accessible
        defaultMethod();      // OK
        protectedMethod();   // OK
        publicMethod();      // OK
    }
}

public class AccessModifierBugDemo {
    public static void main(String[] args) {
        SubClass obj = new SubClass();
        // obj.privateMethod();   // LỖI!
        // obj.defaultMethod();   // LỖI! (khác package)
        obj.protectedMethod();  // OK (subclass)
        obj.publicMethod();    // OK
    }
}
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: Inheritance là quan hệ IS-A. Class con kế thừa từ class cha dùng extends."

*   **[Nam (Intern)]:** "Dạ em học được: super để gọi constructor và method của cha. @Override để ghi đè method."

*   **[Việt (Intern)]:** "Dạ em học được: Polymorphism là một object có nhiều hình thức. Runtime polymorphism dùng method overriding."

*   **[Cường (Intern)]:** "Dạ em học được: instanceof kiểm tra kiểu object. Down-casting cần instanceof và cast tường minh."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| Inheritance (extends) | ☐ | ☐ |
| super keyword | ☐ | ☐ |
| super() constructor | ☐ | ☐ |
| Method Overriding | ☐ | ☐ |
| @Override annotation | ☐ | ☐ |
| Polymorphism | ☐ | ☐ |
| Runtime vs Compile-time | ☐ | ☐ |
| instanceof operator | ☐ | ☐ |
| Up-casting | ☐ | ☐ |
| Down-casting | ☐ | ☐ |
| ClassCastException | ☐ | ☐ |
| Static binding vs Dynamic | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Tạo class Employee với subclasses Manager và Developer.
2.  Override toString() method.
3.  Tạo class Shape với các subclasses.
4.  Thực hành instanceof và type casting.
5.  Tạo class Animal với các subclasses và polymorphic array.

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Inheritance
*   Effective Java: Item 18: Favor composition over inheritance
*   Effective Java: Item 19: Design and document for inheritance or else prohibit it

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab07 - Abstraction & Encapsulation!**
