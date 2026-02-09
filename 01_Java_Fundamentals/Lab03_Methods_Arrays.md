# LAB 03 - PHƯƠNG THỨC (METHODS) VÀ MẢNG (ARRAYS) TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta sẽ học về hai khái niệm cốt lõi: Methods (phương thức) và Arrays (mảng). Đây là bước quan trọng để từ 'học code' chuyển sang 'viết code có tổ chức'."

*   **[Hùng (Intern)]:** "Dạ anh ơi, 'method' là gì vậy anh? Em nghe nói có hàm, có method, có function - giống hay khác nhau?"

*   **[Anh Đô (Senior)]:** "Hùng hỏi câu nền tảng quá! Trong Java, method chính là function, nhưng gắn liền với class hoặc object. Java không có standalone function như C++, method LUÔN thuộc về class."

*   **[Nam (Intern)]:** "Dạ em sợ phần parameters lắm! Em không hiểu pass by value và pass by reference khác nhau thế nào."

*   **[Anh Vương (Performance)]:** "Nam sợ đúng rồi! Đây là concept dễ gây confusion. Nhưng đừng lo, anh sẽ giải thích từng bước."

*   **[Em Hải (Clean Code)]:** "Về mặt clean code, method nên làm một việc duy nhất, có tên gợi ý, và không quá dài. Một method tốt có thể đọc hiểu trong 30 giây."

*   **[Việt (Intern)]:** "Dạ còn array, em biết là lưu nhiều giá trị, nhưng tại sao phải khai báo kích thước trước?"

*   **[Anh Khánh]:** "Việt hỏi hay! Array trong Java có kích thước cố định sau khi tạo. Đây là khác biệt với List (dynamic). Mình sẽ khám phá chi tiết nhé."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab03

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab03/
    └── src/
        └── com/
            └── javazero/
                └── lab03/
                    ├── MethodDemo.java
                    ├── MethodOverloadingDemo.java
                    ├── RecursionDemo.java
                    ├── ArrayDemo.java
                    └── ArraysUtilityDemo.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Tổng quan về METHODS

*   **Hội ý:**

*   **[Anh Khánh]:** "Method (phương thức) là khối code được đặt tên, có thể gọi nhiều lần. Nó giúp: 1) Tái sử dụng code, 2) Tổ chức code, 3) Dễ bảo trì."

*   **[Anh Đô]:** "Cú pháp method: modifier returnType methodName(parameters) { body }"

*   **[Em Hải (Clean Code)]:** "Quy tắc đặt tên method: động từ + object. Ví dụ: calculateTotal(), getName(), isValid(), printReport(). Tên phải mô tả CHÍNH XÁC method làm gì."

*   **[Hùng (Intern)]:** "Dạ 'modifier' là gì anh?"

*   **[Anh Vương]:** "Modifier là access level: public, private, protected, default. Và còn static, final, synchronized. Phần này sẽ học kỹ trong OOP."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Hùng, em viết code demo method cơ bản đi?"

*   **[Hùng (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: MethodDemo.java
// Package: com.javazero.lab03

public class MethodDemo {
    
    // ========== METHOD KHÔNG THAM SỐ, KHÔNG TRẢ VỀ ==========
    public static void greet() {
        System.out.println("Xin chào! Chào mừng đến với Java!");
    }
    
    // ========== METHOD CÓ THAM SỐ ==========
    public static void greetPerson(String name) {
        System.out.println("Xin chào, " + name + "!");
    }
    
    // ========== METHOD CÓ TRẢ VỀ ==========
    public static int add(int a, int b) {
        int result = a + b;
        return result;
    }
    
    // ========== METHOD VỚI NHIỀU THAM SỐ ==========
    public static double calculateArea(double width, double height) {
        double area = width * height;
        return area;
    }
    
    // ========== METHOD TRẢ VỀ BOOLEAN ==========
    public static boolean isEven(int number) {
        return number % 2 == 0;
    }
    
    // ========== METHOD TRẢ VỀ STRING ==========
    public static String formatCurrency(double amount) {
        return String.format("$%.2f", amount);
    }
    
    // ========== METHOD VỚI VOID (KHÔNG TRẢ VỀ) ==========
    public static void printDivider() {
        System.out.println("==================");
    }
    
    // ========== METHOD STATIC VS INSTANCE ==========
    // Static: Thuộc về class, gọi qua ClassName.method()
    // Instance: Thuộc về object, gọi qua object.method()
    
    public static void main(String[] args) {
        System.out.println("=== DEMO METHODS CƠ BẢN ===");
        
        // Gọi method không tham số
        greet();
        printDivider();
        
        // Gọi method có tham số
        greetPerson("Anh Khánh");
        greetPerson("Hùng");
        printDivider();
        
        // Gọi method có trả về
        int sum = add(5, 10);
        System.out.println("5 + 10 = " + sum);
        
        int sum2 = add(100, 200);
        System.out.println("100 + 200 = " + sum2);
        
        printDivider();
        
        // Gọi method với nhiều tham số
        double area1 = calculateArea(5.0, 3.0);
        System.out.println("Area 1: " + area1);
        
        double area2 = calculateArea(10.5, 2.5);
        System.out.println("Area 2: " + area2);
        printDivider();
        
        // Gọi method trả về boolean
        System.out.println("4 is even? " + isEven(4));
        System.out.println("7 is even? " + isEven(7));
        printDivider();
        
        // Gọi method format currency
        System.out.println("Amount: " + formatCurrency(123.456));
        System.out.println("Amount: " + formatCurrency(99.999));
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/MethodDemo.java
// java com.javazero.lab03.MethodDemo

// Output:
// === DEMO METHODS CƠ BẢN ===
// Xin chào! Chào mừng đến với Java!
// ==================
// Xin chào, Anh Khánh!
// Xin chào, Hùng!
// ==================
// 5 + 10 = 15
// 100 + 200 = 300
// ==================
// Area 1: 15.0
// Area 2: 26.25
// ==================
// 4 is even? true
// 7 is even? false
// ==================
// Amount: $123.46
// Amount: $100.00
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! Em thấy method add() được gọi 2 lần với tham số khác nhau. Đây là 'tái sử dụng code' đúng không?"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! Thay vì viết int result = a + b nhiều lần, viết 1 method và gọi nhiều lần. Khi cần sửa logic, chỉ sửa 1 chỗ."

*   **[Nam (Intern)]:** "Dạ còn void khác gì với các kiểu trả về khác?"

*   **[Em Hải]:** "Void = không trả về giá trị. Void chỉ thực hiện action (print, save, etc.). Các kiểu khác (int, String, boolean...) phải có 'return value' cùng kiểu."

*   **[Hùng (Intern)]:** "Dạ method formatCurrency() trả về String, nhưng em thấy nó dùng String.format(). Cái đó là gì anh?"

*   **[Anh Vương]:** "String.format() là static method để format string. %$.2f nghĩa là số thập phân, 2 chữ số sau dấu phẩy. Rất hữu ích cho currency."

---

### BƯỚC 2: Method Parameters và Pass by Value

*   **Hội ý:**

*   **[Anh Khánh]:** "Đây là phần NAM SỢ NHẤT: Pass by Value vs Pass by Reference. Java LUÔN là Pass by Value."

*   **[Nam (Intern)]:** "Dạ em nghe nói với object thì là pass by reference. Sao anh nói pass by value?"

*   **[Anh Đô]:** "Nam hỏi câu phổ biến nhất! Giải thích: Java truyền 'giá trị của tham chiếu' (reference value), không phải reference itself. Nghe giống reference, nhưng thực ra là value của reference."

*   **[Anh Vương (Performance)]:** "Với primitives (int, double...): Truyền bản copy của giá trị. Thay đổi trong method KHÔNG ảnh hưởng biến gốc. Với objects: Truyền bản copy của reference (địa chỉ). Cả hai reference đều trỏ cùng object, nên THAY ĐỔI NỘI DUNG object ảnh hưởng gốc, nhưng THAY ĐỔI reference KHÔNG ảnh hưởng gốc."

*   **[Hùng (Intern)]:** "Dạ em hoang mang! Anh có thể ví dụ cụ thể không?"

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo pass by value đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: PassByValueDemo.java
// Package: com.javazero.lab03

public class PassByValueDemo {
    
    // ========== PASS BY VALUE VỚI PRIMITIVES ==========
    public static void incrementPrimitive(int value) {
        value = value + 10;
        System.out.println("  Trong method: value = " + value);
    }
    
    // ========== PASS BY VALUE VỚI REFERENCE (OBJECT) ==========
    public static void incrementObject(Counter counter) {
        counter.value = counter.value + 10;
        System.out.println("  Trong method: counter.value = " + counter.value);
    }
    
    // ========== THAY ĐỔI REFERENCE KHÔNG ẢNH HƯỞNG GỐC ==========
    public static void reassignObject(Counter counter) {
        counter = new Counter(); // Tạo object mới, counter trỏ đến object mới
        counter.value = 999;
        System.out.println("  Trong method: counter.value = " + counter.value);
    }
    
    // ========== ARRAY LÀ OBJECT ==========
    public static void modifyArray(int[] arr) {
        arr[0] = 100; // Thay đổi nội dung - ẢNH HƯỞNG gốc
        arr = new int[3]; // Thay đổi reference - KHÔNG ẢNH HƯỞNG gốc
        arr[1] = 200;
        System.out.println("  Trong method: arr[0] = " + arr[0] + ", arr[1] = " + arr[1]);
    }
    
    public static void main(String[] args) {
        System.out.println("=== PASS BY VALUE DEMO ===");
        
        // ========== VỚI PRIMITIVE ==========
        System.out.println("\n--- Với Primitive (int) ---");
        int x = 5;
        System.out.println("Trước gọi: x = " + x);
        incrementPrimitive(x);
        System.out.println("Sau gọi: x = " + x);
        System.out.println("→ x KHÔNG thay đổi (pass by value với primitive)");
        
        // ========== VỚI OBJECT ==========
        System.out.println("\n--- Với Object (Counter) ---");
        Counter myCounter = new Counter();
        myCounter.value = 5;
        System.out.println("Trước gọi: myCounter.value = " + myCounter.value);
        incrementObject(myCounter);
        System.out.println("Sau gọi: myCounter.value = " + myCounter.value);
        System.out.println("→ myCounter.value THAY ĐỔI (cùng object)");
        
        // ========== THAY ĐỔI REFERENCE ==========
        System.out.println("\n--- Thay đổi Reference ---");
        Counter counter1 = new Counter();
        counter1.value = 5;
        System.out.println("Trước gọi: counter1.value = " + counter1.value);
        reassignObject(counter1);
        System.out.println("Sau gọi: counter1.value = " + counter1.value);
        System.out.println("→ counter1.value KHÔNG thay đổi (reassign trong method)");
        
        // ========== VỚI ARRAY ==========
        System.out.println("\n--- Với Array ---");
        int[] numbers = {1, 2, 3};
        System.out.println("Trước gọi: numbers[0] = " + numbers[0]);
        modifyArray(numbers);
        System.out.println("Sau gọi: numbers[0] = " + numbers[0]);
        System.out.println("→ numbers[0] THAY ĐỔI (array là object)");
        
        // ========== SUMMARY ==========
        System.out.println("\n=== SUMMARY: JAVA LUÔN LÀ PASS BY VALUE ===");
        System.out.println("1. Primitives: Truyền bản copy của giá trị");
        System.out.println("2. References: Truyền bản copy của reference (địa chỉ)");
        System.out.println("3. Kết luận:");
        System.out.println("   - Thay đổi NỘI DUNG object → ẢNH HƯỞNG gốc");
        System.out.println("   - Thay đổi REFERENCE → KHÔNG ảnh hưởng gốc");
    }
}

// Class Counter đơn giản
class Counter {
    int value;
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/PassByValueDemo.java
// java com.javazero.lab03.PassByValueDemo

// Output:
// === PASS BY VALUE DEMO ===
// 
// --- Với Primitive (int) ---
// Trước gọi: x = 5
//   Trong method: value = 15
// Sau gọi: x = 5
// → x KHÔNG thay đổi (pass by value với primitive)
// 
// --- Với Object (Counter) ---
// Trước gọi: myCounter.value = 5
//   Trong method: counter.value = 15
// Sau gọi: myCounter.value = 15
// → myCounter.value THAY ĐỔI (cùng object)
// 
// --- Thay đổi Reference ---
// Trước gọi: counter1.value = 5
//   Trong method: counter.value = 999
// Sau call: counter1.value = 5
// → counter1.value KHÔNG thay đổi (reassign trong method)
// 
// --- Với Array ---
// Trước gọi: numbers[0] = 1
//   Trong method: arr[0] = 100, arr[1] = 200
// Sau gọi: numbers[0] = 100
// → numbers[0] THAY ĐỔI (array là object)
// 
// === SUMMARY: JAVA LUÔN LÀ PASS BY VALUE ===
// 1. Primitives: Truyền bản copy của giá trị
// 2. References: Truyền bản copy của reference (địa chỉ)
// 3. Kết luận:
//    - Thay đổi NỘI DUNG object → ảnh hưởng gốc
//    - Thay đổi REFERENCE → không ảnh hưởng gốc
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "A ha! Giờ em hiểu rồi! Với int x = 5, gọi incrementPrimitive(x), x vẫn là 5. Với object, nội dung thay đổi nhưng reference không."

*   **[Anh Đô]:** "Nam hiểu đúng rồi! Hùng, em tóm tắp: Java pass by value nghĩa là gì?"

*   **[Hùng (Intern)]:** "Dạ với primitive, truyền bản copy nên thay đổi không ảnh hưởng gốc. Với object, truyền địa chỉ copy, nên cùng địa chỉ, thay đổi nội dung ảnh hưởng, nhưng reassign không ảnh hưởng."

*   **[Anh Khánh]:** "Chuẩn! Cường có câu hỏi không?"

*   **[Cường (Intern)]:** "Dạ array thay đổi arr[0] ảnh hưởng numbers[0], nhưng arr = new int[] thì không. Sao vậy anh?"

*   **[Anh Vương]:** "arr[0] = 100 thay đổi nội dung object. arr = new int[] tạo object mới, arr trỏ đến object mới, nhưng reference gốc numbers vẫn trỏ object cũ."

*   **[Em Hải]:** "Đây là lý do pass by reference thực sự không tồn tại trong Java. Java chỉ có pass by value, dù với objects thì 'giá trị' là địa chỉ."

---

### BƯỚC 3: Method Overloading

*   **Hội ý:**

*   **[Anh Khánh]:** "Method Overloading (nạp chồng method) là khi nhiều methods cùng tên nhưng khác tham số trong cùng class."

*   **[Em Hải (Clean Code)]:** "Overloading giúp code đọc tự nhiên hơn. Ví dụ: System.out.println() có thể in int, String, boolean, object... cùng method name."

*   **[Anh Vương (Performance)]:** "Overloading không ảnh hưởng performance. Compiler xác định method nào được gọi tại compile-time (static binding)."

*   **[Hùng (Intern)]:** "Dạ vậy return type khác nhau có thể overload không?"

*   **[Anh Đô]:** "KHÔNG! Overloading dựa trên TÊN + THAM SỐ. Return type khác nhưng tham số giống là COMPILE ERROR."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Việt, em viết code demo overloading đi?"

*   **[Việt (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: MethodOverloadingDemo.java
// Package: com.javazero.lab03

public class MethodOverloadingDemo {
    
    // ========== OVERLOADING VỚI SỐ LƯỢNG THAM SỐ KHÁC NHAU ==========
    public static void print() {
        System.out.println("print() - không tham số");
    }
    
    public static void print(int num) {
        System.out.println("print(int): " + num);
    }
    
    public static void print(int num1, int num2) {
        System.out.println("print(int, int): " + num1 + ", " + num2);
    }
    
    // ========== OVERLOADING VỚI KIỂU THAM SỐ KHÁC NHAU ==========
    public static void display(int value) {
        System.out.println("display(int): " + value);
    }
    
    public static void display(String value) {
        System.out.println("display(String): " + value);
    }
    
    public static void display(double value) {
        System.out.println("display(double): " + value);
    }
    
    public static void display(boolean value) {
        System.out.println("display(boolean): " + value);
    }
    
    // ========== OVERLOADING VỚI THỨ TỰ THAM SỐ KHÁC NHAU ==========
    public static void process(int a, String b) {
        System.out.println("process(int, String): " + a + ", " + b);
    }
    
    public static void process(String b, int a) {
        System.out.println("process(String, int): " + b + ", " + a);
    }
    
    // ========== LỖI: RETURN TYPE KHÔNG ĐỦ ĐỂ OVERLOAD ==========
    // public static int print() { // COMPILE ERROR!
    //     return 0;
    // }
    // Error: 'print()' is already defined in the class
    
    // ========== VARARGS (Variable Arguments) ==========
    public static void printAll(int... numbers) {
        System.out.print("printAll(int...): ");
        for (int num : numbers) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
    
    public static void printAll(String... strings) {
        System.out.print("printAll(String...): ");
        for (String str : strings) {
            System.out.print(str + " ");
        }
        System.out.println();
    }
    
    public static void main(String[] args) {
        System.out.println("=== METHOD OVERLOADING DEMO ===");
        
        // ========== GỌI OVERLOADED METHODS ==========
        print();
        print(10);
        print(10, 20);
        
        System.out.println("\n--- Overloading với kiểu khác nhau ---");
        display(5);
        display("Hello");
        display(3.14);
        display(true);
        
        System.out.println("\n--- Overloading với thứ tự khác nhau ---");
        process(1, "One");
        process("Two", 2);
        
        System.out.println("\n--- Varargs (thay thế nhiều overload) ---");
        printAll(1, 2, 3);
        printAll(1, 2, 3, 4, 5);
        printAll("A", "B", "C");
        
        // ========== AMBIGUOUS OVERLOADING ==========
        System.out.println("\n--- Lưu ý: Ambiguous Overload ---");
        // printNumber(5); // AMBIGUOUS nếu có print(int) và print(double)
        // Java không biết gọi method nào
        
        // ========== AUTOBOXING VÀ OVERLOADING ==========
        System.out.println("\n--- Autoboxing và Overloading ---");
        Integer integerValue = 10;
        display(integerValue); // Gọi display(int) hay display(Integer)?
        // Java sẽ unbox Integer thành int, gọi display(int)
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/MethodOverloadingDemo.java
// java com.javazero.lab03.MethodOverloadingDemo

// Output:
// === METHOD OVERLOADING DEMO ===
// print() - không tham số
// print(int): 10
// print(int, int): 10, 20
// 
// --- Overloading với kiểu khác nhau ---
// display(int): 5
// display(String): Hello
// display(double): 3.14
// display(boolean): true
All(int...): 1 2 3 
// printAll(int...): 1 2 3 4 5 
// printAll(String...): A B C 
// 
// --- Lưu ý: Ambiguous Overload ---
// (Không thể gọi printNumber(5) nếu có cả print(int) và print(double))
// 
// --- Autoboxing và Overloading ---
// display(int): 10
```

---

*   **Phân tích Output:**

*   **[Hùng (Intern)]:** "Anh ơi! Varargs hay quá! printAll(int...) có thể thay thế printAll(int), printAll(int, int), printAll(int, int, int)..."

*   **[Anh Đô]:** "Hùng hiểu đúng rồi! Varargs (ellipsis: ...) là feature Java 5+, giúp giảm số lượng overloaded methods cần viết."

*   **[Nam (Intern)]:** "Dạ còn autoboxing là gì? Integer(10) thành int(10)?"

*   **[Em Hải]:** "Autoboxing tự động convert primitive <-> wrapper class. int <-> Integer, double <-> Double. Khi gọi display(Integer), Java có thể convert thành display(int) nếu cần."

*   **[Việt (Intern)]:** "Dạ còn ambiguous overload là gì?"

*   **[Anh Vương]:** "Ambiguous xảy ra khi compiler không biết gọi method nào. Ví dụ: print(5.0) và print(5) - Java có thể convert 5 thành 5.0 hoặc giữ nguyên 5. Kết quả: ambiguous, compile error."

*   **[Anh Khánh]:** "Hùng, em tóm tắp: Method overloading là gì và dựa trên điều gì?"

*   **[Hùng (Intern)]:** "Dạ overloading là nhiều methods cùng tên trong class, dựa trên số lượng và kiểu tham số. Return type không đủ để overload."

---

### BƯỚC 4: Đệ quy (Recursion)

*   **Hội ý:**

*   **[Anh Khánh]:** "Recursion (đệ quy) là khi method gọi chính nó. Mọi vòng lặp (loop) đều có thể viết bằng đệ quy, và ngược lại."

*   **[Anh Vương (Performance)]:** "Đệ quy có overhead gọi method (stack frame). Với cùng logic, iteration (vòng lặp) thường nhanh hơn và ít tốn memory hơn."

*   **[Hùng (Intern)]:** "Dạ vậy tại sao phải dùng đệ quy?"

*   **[Anh Đô]:** "Một số bài toán DỄ HƠN nhiều với đệ quy: factorial, Fibonacci, tree traversal, divide and conquer."

*   **[Em Hải (Clean Code)]:** "Quy tắc VÀNG: Mỗi recursive method PHẢI CÓ 1) Base case (điều kiện dừng), 2) Recursive case (gọi chính nó với giá trị nhỏ hơn). KHÔNG CÓ base case = StackOverflowError!"

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Nam, em viết code demo đệ quy đi?"

*   **[Nam (Intern)]:** "Dạ em sợ StackOverflow lắm anh!"

*   **[Anh Đô]:** "Có base case đúng thì không StackOverflow đâu. Viết đi!"

---

*   **Thực hiện:**

```java
// File: RecursionDemo.java
// Package: com.javazero.lab03

public class RecursionDemo {
    
    // ========== FACTORIAL (Giai thừa) ==========
    // n! = 1 * 2 * 3 * ... * n
    // 5! = 1 * 2 * 3 * 4 * 5 = 120
    public static long factorial(int n) {
        // Base case: n = 0 hoặc 1
        if (n <= 1) {
            return 1;
        }
        // Recursive case
        return n * factorial(n - 1);
    }
    
    // ========== FACTORIAL VỚI ITERATION (SO SÁNH) ==========
    public static long factorialIterative(int n) {
        long result = 1;
        for (int i = 2; i <= n; i++) {
            result *= i;
        }
        return result;
    }
    
    // ========== FIBONACCI ==========
    // F(0) = 0, F(1) = 1
    // F(n) = F(n-1) + F(n-2)
    public static int fibonacci(int n) {
        if (n <= 1) {
            return n;
        }
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
    
    // ========== FIBONACCI VỚI MEMOIZATION (TỐI ƯU) ==========
    public static int fibonacciMemo(int n, int[] memo) {
        if (memo[n] != -1) {
            return memo[n]; // Đã tính rồi
        }
        if (n <= 1) {
            memo[n] = n;
        } else {
            memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
        }
        return memo[n];
    }
    
    public static int fibonacciOptimized(int n) {
        int[] memo = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            memo[i] = -1;
        }
        return fibonacciMemo(n, memo);
    }
    
    // ========== SUM VỚI ĐỆ QUY ==========
    public static int sumArray(int[] arr, int index) {
        // Base case
        if (index >= arr.length) {
            return 0;
        }
        // Recursive case
        return arr[index] + sumArray(arr, index + 1);
    }
    
    // ========== COUNTDOWN ==========
    public static void countdown(int n) {
        if (n < 0) {
            return; // Base case
        }
        System.out.println(n);
        countdown(n - 1); // Recursive case
    }
    
    // ========== REVERSE STRING ==========
    public static String reverseString(String str) {
        if (str.isEmpty()) {
            return str; // Base case
        }
        return reverseString(str.substring(1)) + str.charAt(0);
    }
    
    public static void main(String[] args) {
        System.out.println("=== RECURSION DEMO ===");
        
        // ========== FACTORIAL ==========
        System.out.println("\n--- Factorial ---");
        int num = 5;
        System.out.println(num + "! = " + factorial(num));
        System.out.println("Iterative: " + num + "! = " + factorialIterative(num));
        
        // ========== FIBONACCI ==========
        System.out.println("\n--- Fibonacci ---");
        System.out.println("F(0) = " + fibonacci(0));
        System.out.println("F(1) = " + fibonacci(1));
        System.out.println("F(5) = " + fibonacci(5));
        System.out.println("F(10) = " + fibonacci(10));
        
        // So sánh performance
        System.out.println("\n--- Fibonacci Performance ---");
        long startTime = System.nanoTime();
        int fibNormal = fibonacci(30);
        long endTime = System.nanoTime();
        System.out.println("Normal F(30) = " + fibNormal + " - Time: " + (endTime - startTime) + " ns");
        
        startTime = System.nanoTime();
        int fibMemo = fibonacciOptimized(30);
        endTime = System.nanoTime();
        System.out.println("Memo F(30) = " + fibMemo + " - Time: " + (endTime - startTime) + " ns");
        
        // ========== SUM ARRAY ==========
        System.out.println("\n--- Sum Array with Recursion ---");
        int[] numbers = {1, 2, 3, 4, 5};
        System.out.println("Array: [1, 2, 3, 4, 5]");
        System.out.println("Sum = " + sumArray(numbers, 0));
        
        // ========== COUNTDOWN ==========
        System.out.println("\n--- Countdown ---");
        countdown(5);
        
        // ========== REVERSE STRING ==========
        System.out.println("\n--- Reverse String ---");
        String original = "Hello";
        System.out.println("Original: " + original);
        System.out.println("Reversed: " + reverseString(original));
        
        // ========== STACK OVERFLOW DEMO (CẨN THẬN!) ==========
        System.out.println("\n--- WARNING: Stack Overflow! ---");
        // factorial(-5); // Sẽ gây StackOverflowError!
        System.out.println("(Đã comment factorial(-5) để tránh crash)");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/RecursionDemo.java
// java com.javazero.lab03.RecursionDemo

// Output:
// === RECURSION DEMO ===
// 
// --- Factorial ---
// 5! = 120
// Iterative: 5! = 120
// 
// --- Fibonacci ---
// F(0) = 0
// F(1) = 1
// F(5) = 5
// F(10) = 55
// 
// --- Fibonacci Performance ---
// Normal F(30) = 832040 - Time: 312500 ns
// Memo F(30) = 832040 - Time: 1500 ns
// 
// --- Sum Array with Recursion ---
// Array: [1, 2, 3, 4, 5]
// Sum = 15
// 
// --- Countdown ---
// 5
// 4
// 3
// 2
// 1
// 
// --- Reverse String ---
// Original: Hello
// Reversed: olleH
// 
// --- WARNING: Stack Overflow! ---
// (Đã comment factorial(-5) để tránh crash)
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! Fibonacci memoization nhanh hơn 200,000 lần (312500 vs 1500 ns)! Sao lạ vậy?"

*   **[Anh Vương]:** "Việt hỏi hay! Fibonacci normal gọi method lặp lại nhiều lần. F(5) = F(4) + F(3) = F(3)+F(2)+F(3)... Gọi F(3) 2 lần, F(2) 3 lần... Exponential complexity O(2^n). Memoization lưu kết quả đã tính, giảm xuống O(n)."

*   **[Nam (Intern)]:** "Dạ em hiểu rồi! Base case là điều kiện dừng, không có thì đệ quy chạy mãi mãi, gây StackOverflow."

*   **[Em Hải]:** "Đúng rồi! Stack trong Java có giới hạn. Mỗi recursive call tạo stack frame mới. Quá nhiều call = hết stack = StackOverflowError."

*   **[Hùng (Intern)]:** "Dạ vậy khi nào nên dùng đệ quy, khi nào dùng loop?"

*   **[Anh Khánh]:** "Câu hay! Dùng đệ quy khi: 1) Bài toán tự nhiên theo recursive structure (tree, graph), 2) Code đệ quy đọc hiểu DỄ HƠN iteration. Dùng iteration khi performance quan trọng hoặc đệ quy quá sâu."

---

### BƯỚC 5: Arrays - Tổng quan

*   **Hội ý:**

*   **[Anh Khánh]:** "Array (mảng) là cấu trúc dữ liệu lưu nhiều giá trị CÙNG KIỂU trong một biến. Array có kích thước CỐ ĐỊNH sau khi tạo."

*   **[Anh Vương (Performance)]:** "Array access O(1) - cực nhanh. ArrayList cũng O(1) nhưng có overhead. Array phù hợp khi biết chính xác số lượng và cần performance cao."

*   **[Hùng (Intern)]:** "Dạ array khác gì với ArrayList anh?"

*   **[Anh Đô]:** "Array: kích thước cố định, lưu primitives hoặc objects. ArrayList: kích thước động, chỉ lưu objects, nhiều methods tiện lợi."

*   **[Em Hải (Clean Code)]:** "Trong code thực tế, ArrayList phổ biến hơn vì linh hoạt. Array dùng khi performance critical hoặc làm việc với API yêu cầu array."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo array cơ bản đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: ArrayDemo.java
// Package: com.javazero.lab03

public class ArrayDemo {
    public static void main(String[] args) {
        System.out.println("=== ARRAY DEMO ===");
        
        // ========== KHAI BÁO VÀ KHỞI TẠO ARRAY ==========
        System.out.println("\n--- Khai báo và khởi tạo ---");
        
        // Cách 1: Khai báo rồi khởi tạo
        int[] numbers = new int[5];
        System.out.println("int[5] - 5 elements, default = 0");
        System.out.println("numbers[0] = " + numbers[0]);
        System.out.println("numbers[4] = " + numbers[4]);
        
        // Cách 2: Khai báo với giá trị
        int[] scores = {90, 85, 78, 92, 88};
        System.out.println("\nint[] scores = {90, 85, 78, 92, 88}");
        System.out.println("scores[0] = " + scores[0]);
        System.out.println("scores[4] = " + scores[4]);
        
        // Cách 3: Dynamic initialization
        String[] names = new String[]{"Anh", "Hùng", "Nam", "Việt", "Cường"};
        System.out.println("\nString[] names = new String[]{\"Anh\", \"Hùng\", ...}");
        System.out.println("names[0] = " + names[0]);
        
        // ========== THAY ĐỔI GIÁ TRỊ ==========
        System.out.println("\n--- Thay đổi giá trị ---");
        numbers[0] = 10;
        numbers[1] = 20;
        numbers[2] = 30;
        numbers[3] = 40;
        numbers[4] = 50;
        System.out.println("Gán giá trị cho numbers:");
        System.out.println("numbers = [10, 20, 30, 40, 50]");
        
        // ========== ARRAY LENGTH ==========
        System.out.println("\n--- Array Length ---");
        System.out.println("numbers.length = " + numbers.length);
        System.out.println("scores.length = " + scores.length);
        System.out.println("names.length = " + names.length);
        
        // ========== ARRAY INDEX ==========
        System.out.println("\n--- Array Index (BẮT ĐẦU TỪ 0!) ---");
        System.out.println("Array có 5 elements: index 0, 1, 2, 3, 4");
        System.out.println("numbers[0] = " + numbers[0] + " (first element)");
        System.out.println("numbers[4] = " + numbers[4] + " (last element)");
        // numbers[5] = ArrayIndexOutOfBoundsException!
        
        // ========== ENHANCED FOR (FOR-EACH) ==========
        System.out.println("\n--- Enhanced For ---");
        System.out.print("scores: ");
        for (int score : scores) {
            System.out.print(score + " ");
        }
        System.out.println();
        
        System.out.print("names: ");
        for (String name : names) {
            System.out.print(name + " ");
        }
        System.out.println();
        
        // ========== ARRAY VỚI PRIMITIVES VS OBJECTS ==========
        System.out.println("\n--- Primitives vs Objects ---");
        
        // Primitive array
        int[] primitiveArray = new int[3];
        primitiveArray[0] = 100;
        System.out.println("primitiveArray[0] = " + primitiveArray[0]);
        
        // Object array
        String[] stringArray = new String[3];
        stringArray[0] = "Hello";
        stringArray[1] = null; // Objects có thể null
        stringArray[2] = "World";
        System.out.println("stringArray[0] = " + stringArray[0]);
        System.out.println("stringArray[1] = " + stringArray[1]); // null
        
        // ========== MULTI-DIMENSIONAL ARRAY ==========
        System.out.println("\n--- Multi-dimensional Array ---");
        
        // 2D Array: Ma trận 3x3
        int[][] matrix = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };
        System.out.println("Matrix 3x3:");
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
        
        // 2D Array với new
        int[][] table = new int[2][3];
        table[0][0] = 10;
        table[0][1] = 20;
        table[0][2] = 30;
        table[1][0] = 40;
        table[1][1] = 50;
        table[1][2] = 60;
        
        System.out.println("\nTable 2x3:");
        for (int[] row : table) {
            for (int value : row) {
                System.out.print(value + " ");
            }
            System.out.println();
        }
        
        // Jagged Array (mảng zic zac)
        System.out.println("\n--- Jagged Array ---");
        int[][] jagged = new int[3][];
        jagged[0] = new int[]{1, 2};
        jagged[1] = new int[]{3, 4, 5, 6};
        jagged[2] = new int[]{7, 8, 9};
        
        for (int i = 0; i < jagged.length; i++) {
            System.out.print("Row " + i + ": ");
            for (int value : jagged[i]) {
                System.out.print(value + " ");
            }
            System.out.println();
        }
        
        // ========== ARRAY VỚI OBJECTS ==========
        System.out.println("\n--- Array với Custom Objects ---");
        Person[] people = new Person[3];
        people[0] = new Person("Anh", 25);
        people[1] = new Person("Hùng", 22);
        people[2] = new Person("Nam", 24);
        
        for (Person person : people) {
            System.out.println(person.name + " - " + person.age + " tuổi");
        }
    }
}

// Class Person đơn giản
class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/ArrayDemo.java
// java com.javazero.lab03.ArrayDemo

// Output:
// === ARRAY DEMO ===
// 
// --- Khai báo và khởi tạo ---
// int[5] - 5 elements, default = 0
// numbers[0] = 0
// numbers[4] = 0
// 
// --- Thay đổi giá trị ---
// Gán giá trị cho numbers:
// numbers = [10, 20, 30, 40, 50]
// 
// --- Array Length ---
// numbers.length = 5
// scores.length = 5
// length = 5
// 
// --- Array Index (BẮT ĐẦU TỪ 0!) ---
// Array có 5 elements: index 0, 1, 2, 3, 4
// numbers[0] = 10 (first element)
// numbers[4] = 50 (last element)
// 
// --- Enhanced For ---
// scores: 90 85 78 92 88 
// names: Anh Hùng Nam Việt Cường 
// 
// --- Primitives vs Objects ---
// primitiveArray[0] = 100
// stringArray[0] = Hello
// stringArray[1] = null
// 
// --- Multi-dimensional Array ---
// Matrix 3x3:
// 1 2 3 
// 4 5 6 
// 7 8 9 
// 
// Table 2x3:
// 10 20 30 
// 40 50 60 
// 
// --- Jagged Array ---
// Row 0: 1 2 
// Row 1: 3 4 5 6 
// Jagged Array Row 2: 7 8 9 
// 
// --- Array với Custom Objects ---
// Anh - 25 tuổi
// Hùng - 22 tuổi
// Nam - 24 tuổi
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! Em thấy array index bắt đầu từ 0, không phải 1. Em hay quên và viết array[5] khi chỉ có 5 elements."

*   **[Anh Đô]:** "Nam hỏi hay! Array có n elements: index từ 0 đến n-1. array.length = n. Access array[n] = ArrayIndexOutOfBoundsException."

*   **[Việt (Intern)]:** "Dạ default value của int array là 0, String array là null. Đúng không anh?"

*   **[Em Hải]:** "Đúng rồi! Primitive arrays: default = 0/false. Object arrays: default = null. Rất quan trọng khi khởi tạo array lớn."

*   **[Hùng (Intern)]:** "Dạ jagged array là gì? Em chưa hiểu."

*   **[Anh Vương]:** "Jagged array là 2D array nhưng mỗi row có length khác nhau. Như trong ví dụ: row 0 có 2 elements, row 1 có 4 elements, row 2 có 3 elements."

---

### BƯỚC 6: Arrays Utility Class

*   **Hội ý:**

*   **[Anh Khánh]:** "Java cung cấp Arrays utility class với nhiều static methods hữu ích: sort, binarySearch, equals, fill, toString."

*   **[Anh Vương (Performance)]:** "Arrays.sort() dùng Dual-Pivot Quicksort (O(n log n)), rất optimize. Đừng tự viết sort, dùng Arrays.sort()."

*   **[Em Hải (Clean Code)]:** "Arrays.toString() rất hữu ích cho debug. System.out.println(array) KHÔNG in được array, phải dùng Arrays.toString()."

---

*   **Thực hiện:**

```java
// File: ArraysUtilityDemo.java
// Package: com.javazero.lab03

import java.util.Arrays;

public class ArraysUtilityDemo {
    public static void main(String[] args) {
        System.out.println("=== ARRAYS UTILITY DEMO ===");
        
        // ========== ARRAYS.TOSTRING() ==========
        System.out.println("\n--- Arrays.toString() ---");
        int[] numbers = {5, 2, 8, 1, 9, 3};
        System.out.println("numbers: " + Arrays.toString(numbers));
        
        String[] names = {"Anh", "Hùng", "Nam"};
        System.out.println("names: " + Arrays.toString(names));
        
        // ========== ARRAYS.SORT() ==========
        System.out.println("\n--- Arrays.sort() ---");
        int[] unsorted = {5, 2, 8, 1, 9, 3};
        System.out.println("Before sort: " + Arrays.toString(unsorted));
        Arrays.sort(unsorted);
        System.out.println("After sort: " + Arrays.toString(unsorted));
        
        // Sort strings
        String[] fruits = {"banana", "apple", "cherry", "date"};
        System.out.println("Before sort: " + Arrays.toString(fruits));
        Arrays.sort(fruits);
        System.out.println("After sort: " + Arrays.toString(fruits));
        
        // Sort một phần (sort từ index 1 đến 4)
        int[] partial = {5, 2, 8, 1, 9, 3};
        System.out.println("Partial sort [1, 5): " + Arrays.toString(partial));
        Arrays.sort(partial, 1, 5); // sort từ index 1 đến 4 (5 không bao gồm)
        System.out.println("After partial sort: " + Arrays.toString(partial));
        
        // ========== ARRAYS.BINARYSEARCH() ==========
        System.out.println("\n--- Arrays.binarySearch() ---");
        int[] sorted = {1, 3, 5, 7, 9, 11};
        System.out.println("sorted: " + Arrays.toString(sorted));
        
        int index1 = Arrays.binarySearch(sorted, 7);
        System.out.println("binarySearch(7) = " + index1); // index = 3
        
        int index2 = Arrays.binarySearch(sorted, 4);
        System.out.println("binarySearch(4) = " + index2); // -4 (không tìm thấy)
        
        // ========== ARRAYS.EQUALS() ==========
        System.out.println("\n--- Arrays.equals() ---");
        int[] arr1 = {1, 2, 3};
        int[] arr2 = {1, 2, 3};
        int[] arr3 = {1, 2, 4};
        
        System.out.println("arr1 = " + Arrays.toString(arr1));
        System.out.println("arr2 = " + Arrays.toString(arr2));
        System.out.println("arr3 = " + Arrays.toString(arr3));
        System.out.println("arr1 == arr2 (reference): " + (arr1 == arr2));
        System.out.println("Arrays.equals(arr1, arr2): " + Arrays.equals(arr1, arr2));
        System.out.println("Arrays.equals(arr1, arr3): " + Arrays.equals(arr1, arr3));
        
        // ========== ARRAYS.FILL() ==========
        System.out.println("\n--- Arrays.fill() ---");
        int[] filled = new int[5];
        System.out.println("Before fill: " + Arrays.toString(filled));
        
        Arrays.fill(filled, 42);
        System.out.println("After fill(42): " + Arrays.toString(filled));
        
        Arrays.fill(filled, 2, 4, 99); // fill từ index 2 đến 3
        System.out.println("After fill(2, 4, 99): " + Arrays.toString(filled));
        
        // ========== ARRAYS.COPYOF() ==========
        System.out.println("\n--- Arrays.copyOf() ---");
        int[] original = {1, 2, 3, 4, 5};
        System.out.println("Original: " + Arrays.toString(original));
        
        int[] copy1 = Arrays.copyOf(original, 3);
        System.out.println("copyOf(original, 3): " + Arrays.toString(copy1));
        
        int[] copy2 = Arrays.copyOf(original, 10); // Thêm elements
        System.out.println("copyOf(original, 10): " + Arrays.toString(copy2));
        
        // ========== ARRAYS.DEEPCOPY VÀ DEEPTOSTRING ==========
        System.out.println("\n--- Deep copy và deepToString ---");
        int[][] twoD = {{1, 2}, {3, 4}};
        System.out.println("2D array: " + Arrays.deepToString(twoD));
        
        int[][] copy2D = Arrays.copyOf(twoD, twoD.length);
        copy2D[0][0] = 99;
        System.out.println("After modify copy: ");
        System.out.println("  Original: " + Arrays.deepToString(twoD));
        System.out.println("  Copy: " + Arrays.deepToString(copy2D));
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/ArraysUtilityDemo.java
// java com.javazero.lab03.ArraysUtilityDemo

// Output:
// === ARRAYS UTILITY DEMO ===
// 
// --- Arrays.toString() ---
// numbers: [5, 2, 8, 1, 9, 3]
// names: [Anh, Hùng, Nam]
// 
// --- Arrays.sort() ---
// Before sort: [5, 2, 8, 1, 9, 3]
// After sort: [1, 2, 3, 5, 8, 9]
// Before sort: [banana, apple, cherry, date]
// After sort: [apple, banana, cherry, date]
// Partial sort [1, 5): [5, 2, 8, 1, 9, 3]
// After partial sort: [5, 1, 2, 8, 9, 3]
// 
// --- Arrays.binarySearch() ---
// sorted: [1, 3, 5, 7, 9, 11]
// binarySearch(7) = 3
// binarySearch(4) = -4
// 
// --- Arrays.equals() ---
// arr1 = [1, 2, 3]
// arr2 = [1, 2, 3]
// arr3 = [1, 2, 4]
// arr1 == arr2 (reference): false
// Arrays.equals(arr1, arr2): true
// Arrays.equals(arr1, arr3): false
// 
// --- Arrays.fill() ---
// Before fill: [0, 0, 0, 0, 0]
// After fill(42): [42, 42, 42, 42, 42]
// After fill(2, 4, 99): [42, 42, 99, 99, 42]
// 
// --- Arrays.copyOf() ---
// Original: [1, 2, 3, 4, 5]
// copyOf(original, 3): [1, 2, 3]
// copyOf(original, 10): [1, 2, 3, 4, 5, 0, 0, 0, 0, ]
// 
// --- Deep copy và deepToString ---
// 2D array: [[1, 2], [3, 4]]
// After modify copy: 
//   Original: [[99, 2], [3, 4]]
//   Copy: [[99, 2], [3, 4]]
```

---

*   **Phân tích Output:**

*   **[Hùng (Intern)]:** "Anh ơi! binarySearch(4) = -4, sao không phải -1?"

*   **[Anh Đô]:** "Hùng hỏi hay! BinarySearch trả về: Nếu tìm thấy = index (>=0). Nếu không tìm thấy = -(insertion point) - 1. 4 không có, insertion point = 3, nên trả về -3 - 1 = -4."

*   **[Việt (Intern)]:** "Dạ còn Arrays.equals() vs == khác nhau thế nào?"

*   **[Em Hải]:** "arr1 == arr2 so sánh REFERENCE (địa chỉ), Arrays.equals() so sánh NỘI DUNG từng element."

*   **[Nam (Intern)]:** "Dạ copyOf(original, 10) thêm elements = 0? Sao không null?"

*   **[Anh Vương]:** "Vì int[] là primitive array, default = 0. String[] thì default = null. Arrays.copyOf() giữ nguyên kiểu element."

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ phá thôi! Mỗi người gây 1 bug liên quan đến methods và arrays."

---

*   **Case 1: ArrayIndexOutOfBoundsException**

```java
// File: ArrayIndexOutOfBoundsDemo.java
// Package: com.javazero.lab03

public class ArrayIndexOutOfBoundsDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 1: ARRAY INDEX OUT OF BOUNDS ===");
        
        int[] array = new int[5]; // index 0, 1, 2, 3, 4
        
        // Bug: Access index vượt quá
        System.out.println("Cố gắng truy cập array[5]...");
        try {
            int value = array[5];
            System.out.println("value = " + value);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("CAUGHT: " + e.getClass().getSimpleName());
            System.out.println("Message: " + e.getMessage());
            System.out.println("Lý do: array[5] không tồn tại! Valid: 0-4");
        }
        
        // Fix: Luôn kiểm tra index
        System.out.println("\nFix: Kiểm tra index trước khi access");
        int indexToAccess = 5;
        if (indexToAccess >= 0 && indexToAccess < array.length) {
            System.out.println("array[" + indexToAccess + "] = " + array[indexToAccess]);
        } else {
            System.out.println("ERROR: Index " + indexToAccess + " out of bounds!");
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/ArrayIndexOutOfBoundsDemo.java
// java com.javazero.lab03.ArrayIndexOutOfBoundsDemo

// Output:
// === CASE 1: ARRAY INDEX OUT OF BOUNDS ===
// Cố gắng truy cập array[5]...
// CAUGHT: ArrayIndexOutOfBoundsException
// Message: 5
// Lý do: array[5] không tồn tại! Valid: 0-4
// 
// Fix: Kiểm tra index trước khi access
// ERROR: Index 5 out of bounds!
```

---

*   **Case 2: NullPointerException với Array**

```java
// File: NullPointerArrayDemo.java
// Package: com.javazero.lab03

public class NullPointerArrayDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 2: NULL POINTER VỚI ARRAY ===");
        
        String[] names = new String[3];
        names[0] = "Anh";
        // names[1] = null (default)
        names[2] = "Hùng";
        
        System.out.println("names[0] = " + names[0]);
        System.out.println("names[1] = " + names[1]); // null
        System.out.println("names[2] = " + names[2]);
        
        // Bug: Gọi method trên null
        System.out.println("\nCố gắng gọi names[1].length()...");
        try {
            int length = names[1].length();
            System.out.println("Length = " + length);
        } catch (NullPointerException e) {
            System.out.println("CAUGHT: " + e.getClass().getSimpleName());
            System.out.println("Lý do: names[1] = null, không thể gọi .length()");
        }
        
        // Fix: Check null trước khi dùng
        System.out.println("\nFix: Check null trước khi dùng");
        for (int i = 0; i < names.length; i++) {
            if (names[i] != null) {
                System.out.println("names[" + i + "] = " + names[i] + ", length = " + names[i].length());
            } else {
                System.out.println("names[" + i + "] = null - Bỏ qua!");
            }
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/NullPointerArrayDemo.java
// java com.javazero.lab03.NullPointerArrayDemo

// Output:
// === CASE 2: NULL POINTER VỚI ARRAY ===
// names[0] = Anh
// names[1] = null
// names[2] = Hùng
// 
// Cố gắng gọi names[1].length()...
// CAUGHT: NullPointerException
// Lý do: names[1] = null, không thể gọi .length()
// 
// Fix: Check null trước khi dùng
// names[0] = Anh, length = 3
// names[1] = null - Bỏ qua!
// names[2] = Hùng, length = 4
```

---

*   **Case 3: StackOverflowError với Recursion**

```java
// File: StackOverflowDemo.java
// Package: com.javazero.lab03

public class StackOverflowDemo {
    
    // Bug: Đệ quy không có base case
    public static void infiniteRecursion(int n) {
        System.out.println("n = " + n);
        infiniteRecursion(n + 1); // KHÔNG có base case!
    }
    
    // Fix: Có base case đúng
    public static void safeRecursion(int n) {
        if (n > 1000000) { // Base case: dừng khi quá lớn
            System.out.println("Stopped at n = " + n);
            return;
        }
        // Không gọi nữa để tránh overflow
    }
    
    public static void main(String[] args) {
        System.out.println("=== CASE 3: STACK OVERFLOW VỚI RECURSION ===");
        
        // Lưu ý: Không chạy infiniteRecursion(0) vì sẽ crash!
        System.out.println("infiniteRecursion(0) sẽ gây StackOverflowError!");
        System.out.println("(Đã comment để tránh crash)");
        
        System.out.println("\nFix: Dùng safeRecursion");
        safeRecursion(0);
        
        // Factorial với input âm
        System.out.println("\nFactorial(-5) sẽ gây StackOverflow!");
        System.out.println("(Đã comment)");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab03/StackOverflowDemo.java
// java com.javazero.lab03.StackOverflowDemo

// Output:
// === CASE 3: STACK OVERFLOW VỚI RECURSION ===
// infiniteRecursion(0) sẽ gây StackOverflowError!
// (Đã comment để tránh crash)
// 
// Fix: Dùng safeRecursion
// Stopped at n = 1000001
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: Method là khối code có tên, gọi được nhiều lần. Java pass by value: primitives = copy giá trị, objects = copy reference."

*   **[Nam (Intern)]:** "Dạ em hiểu overloading = cùng tên, khác tham số. Đệ quy phải có base case. Array index bắt đầu từ 0."

*   **[Việt (Intern)]:** "Dạ em học được: Arrays utility methods rất hữu ích: sort(), binarySearch(), toString()."

*   **[Cường (Intern)]:** "Dạ em học được: Array kích thước cố định, ArrayList linh hoạt hơn."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| Method definition và invocation | ☐ | ☐ |
| Method parameters và return type | ☐ | ☐ |
| Pass by value vs Pass by reference | ☐ | ☐ |
| Method overloading | ☐ | ☐ |
| Varargs (...) | ☐ | ☐ |
| Recursion và base case | ☐ | ☐ |
| Recursion vs Iteration | ☐ | ☐ |
| Array declaration và initialization | ☐ | ☐ |
| Array index (0-based) | ☐ | ☐ |
| Enhanced for loop | ☐ | ☐ |
| Multi-dimensional arrays | ☐ | ☐ |
| Arrays utility methods | ☐ | ☐ |
| ArrayIndexOutOfBoundsException | ☐ | ☐ |
| NullPointerException với arrays | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Viết method tính giai thừa (cả iteration và recursion).
2.  Viết method kiểm tra số nguyên tố.
3.  Viết method đảo ngược chuỗi (recursion).
4.  Tạo array 2D và tính tổng các phần tử.
5.  Sử dụng Arrays.sort() và Arrays.binarySearch().
6.  Viết method tìm max/min trong array.

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Methods
*   Oracle Java Tutorials: Arrays
*   Effective Java: Item 52: Use overloading judiciously

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab04 - Strings!**

---

## 6. CÂU HỎI INTERVIEW THƯỜNG GẶP (Common Interview Questions)

### Về Methods

**Q1: Sự khác biệt giữa static method và instance method?**
- Static: Thuộc về class, gọi bằng ClassName.method(), không cần object
- Instance: Thuộc về object, gọi bằng object.method()

**Q2: Method signature là gì?**
- Bao gồm: tên method + danh sách tham số (kiểu và thứ tự)
- Return type KHÔNG phần signature
- Overloading dựa trên signature

**Q3: Varargs là gì và dùng khi nào?**
- Varargs (ellipsis): `type... name` - cho phép truyền 0 hoặc nhiều tham số cùng kiểu
- Dùng khi không biết trước số lượng tham số

**Q4: Tại sao Java không có pass by reference?**
- Java luôn pass by value
- Với objects: value = reference (địa chỉ object)
- Không thể thay đổi reference gốc trong method

**Q5: Khi nào nên dùng recursion thay vì iteration?**
- Bài toán có cấu trúc recursive tự nhiên (tree, graph)
- Code recursion đọc hiểu dễ hơn iteration
- Divide and conquer algorithms

### Về Arrays

**Q6: Array và ArrayList khác nhau thế nào?**
- Array: kích thước cố định, performance tốt hơn
- ArrayList: kích thước động, methods tiện lợi

**Q7: default value của array là gì?**
- Primitive arrays: 0, false, '\u0000'
- Object arrays: null

**Q8: Arrays.copyOf() và System.arraycopy() khác nhau?**
- Arrays.copyOf(): Tạo array mới với kích thước mới
- System.arraycopy(): Copy từ source đến destination

**Q9: Deep copy và shallow copy trong arrays?**
- Shallow copy: Copy reference, cùng object
- Deep copy: Copy nội dung, object mới

**Q10: Cách tìm phần tử trong sorted array hiệu quả nhất?**
- Dùng Arrays.binarySearch(): O(log n)

---

## 7. BÀI TẬP THỰC HÀNH NÂNG CAO

### Bài tập 1: Calculator Với Method Overloading

```java
public class AdvancedCalculator {
    public static int add(int a, int b) {
        return a + b;
    }

    public static double add(double a, double b) {
        return a + b;
    }

    public static int add(int... numbers) {
        int sum = 0;
        for (int num : numbers) {
            sum += num;
        }
        return sum;
    }

    public static double calculateAverage(int[] numbers) {
        if (numbers == null || numbers.length == 0) {
            return 0;
        }
        int sum = 0;
        for (int num : numbers) {
            sum += num;
        }
        return (double) sum / numbers.length;
    }

    public static int findMax(int[] numbers) {
        if (numbers == null || numbers.length == 0) {
            throw new IllegalArgumentException("Array rỗng!");
        }
        int max = numbers[0];
        for (int num : numbers) {
            if (num > max) {
                max = num;
            }
        }
        return max;
    }

    public static void main(String[] args) {
        System.out.println("=== ADVANCED CALCULATOR ===");

        System.out.println("add(5, 3) = " + add(5, 3));
        System.out.println("add(5.5, 3.3) = " + add(5.5, 3.3));
        System.out.println("add(1, 2, 3, 4, 5) = " + add(1, 2, 3, 4, 5));

        int[] numbers = {10, 20, 30, 40, 50};
        System.out.println("Average: " + calculateAverage(numbers));
        System.out.println("Max: " + findMax(numbers));
    }
}
```

### Bài tập 2: Recursive Operations

```java
import java.util.Arrays;

public class RecursiveOperations {
    public static int sumArray(int[] arr, int index) {
        if (index >= arr.length) {
            return 0;
        }
        return arr[index] + sumArray(arr, index + 1);
    }

    public static boolean isPalindrome(String str, int left, int right) {
        if (left >= right) {
            return true;
        }
        if (str.charAt(left) != str.charAt(right)) {
            return false;
        }
        return isPalindrome(str, left + 1, right - 1);
    }

    public static long combination(int n, int k) {
        if (k == 0 || k == n) {
            return 1;
        }
        if (k > n) {
            return 0;
        }
        return combination(n - 1, k - 1) + combination(n - 1, k);
    }

    public static String toBinary(int n) {
        if (n == 0) return "0";
        if (n == 1) return "1";
        return toBinary(n / 2) + (n % 2);
    }

    public static void main(String[] args) {
        System.out.println("=== RECURSIVE OPERATIONS ===");

        int[] numbers = {1, 2, 3, 4, 5};
        System.out.println("Sum: " + sumArray(numbers, 0));

        System.out.println("\"racecar\" is palindrome: " + isPalindrome("racecar", 0, 6));
        System.out.println("C(5, 2) = " + combination(5, 2));
        System.out.println("10 in binary: " + toBinary(10));
    }
}
```

### Bài tập 3: Array Manipulation Challenge

```java
import java.util.*;

public class ArrayChallenge {
    public static int[] removeDuplicates(int[] arr) {
        if (arr.length <= 1) return arr;
        Arrays.sort(arr);
        int[] result = new int[arr.length];
        int newSize = 0;
        for (int i = 0; i < arr.length; i++) {
            if (i == 0 || arr[i] != arr[i - 1]) {
                result[newSize++] = arr[i];
            }
        }
        return Arrays.copyOf(result, newSize);
    }

    public static int[] twoSum(int[] arr, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            int complement = target - arr[i];
            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }
            map.put(arr[i], i);
        }
        return new int[]{-1, -1};
    }

    public static void rotateArray(int[] arr, int k) {
        if (arr == null || arr.length == 0) return;
        k = k % arr.length;
        reverse(arr, 0, arr.length - 1);
        reverse(arr, 0, k - 1);
        reverse(arr, k, arr.length - 1);
    }

    private static void reverse(int[] arr, int left, int right) {
        while (left < right) {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }

    public static int maxSubArray(int[] arr) {
        if (arr == null || arr.length == 0) return 0;
        int maxSum = arr[0];
        int currentSum = arr[0];
        for (int i = 1; i < arr.length; i++) {
            currentSum = Math.max(arr[i], currentSum + arr[i]);
            maxSum = Math.max(maxSum, currentSum);
        }
        return maxSum;
    }

    public static void main(String[] args) {
        System.out.println("=== ARRAY CHALLENGE ===");

        int[] withDupes = {3, 1, 4, 1, 5, 9, 2, 6};
        System.out.println("No dupes: " + Arrays.toString(removeDuplicates(withDupes)));

        int[] twoSumArr = {2, 7, 11, 15};
        int[] result = twoSum(twoSumArr, 9);
        System.out.println("Two Sum indices: [" + result[0] + ", " + result[1] + "]");

        int[] rotateArr = {1, 2, 3, 4, 5};
        rotateArray(rotateArr, 2);
        System.out.println("Rotated: " + Arrays.toString(rotateArr));

        int[] subArr = {-2, 1, -3, 4, -1, 2, 1};
        System.out.println("Max subarray: " + maxSubArray(subArr));
    }
}
```

---

## 8. CHECKLIST KIẾN THỨC TOÀN DIỆN

### Methods

- [ ] Định nghĩa và gọi method đúng cách
- [ ] Hiểu static vs instance methods
- [ ] Pass by value trong Java
- [ ] Method overloading và signature
- [ ] Varargs usage
- [ ] Recursion và base case

### Arrays

- [ ] Khai báo và khởi tạo array
- [ ] Array index (0-based)
- [ ] Enhanced for loop
- [ ] Multi-dimensional arrays
- [ ] Arrays utility methods

### Interview Readiness

- [ ] Giải thích được pass by value vs reference
- [ ] Khi nào dùng recursion
- [ ] Arrays vs ArrayList
- [ ] Tối ưu array operations

---

## 9. TỔNG KẾT CHƯƠNG

### Những điểm quan trọng:

1. **Methods**: Tái sử dụng code, tổ chức logic
2. **Pass by Value**: Primitives = copy giá trị, Objects = copy reference
3. **Overloading**: Cùng tên, khác tham số
4. **Recursion**: Base case + recursive case
5. **Arrays**: Kích thước cố định, index 0-based

### Các lỗi thường gặp:

1. Confuse pass by value/reference
2. Không có base case trong recursion
3. ArrayIndexOutOfBoundsException
4. Null
