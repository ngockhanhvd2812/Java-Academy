# LAB 08 - XỬ LÝ NGOẠI LỆ (EXCEPTION HANDLING) TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta sẽ học về Exception Handling - xử lý ngoại lệ. Đây là kỹ năng BẮT BUỘC phải có nếu muốn viết code chuyên nghiệp."

*   **[Hùng (Intern)]:** "Dạ anh ơi, 'exception' là gì vậy anh? Em nghe nói NullPointerException, ArrayIndexOutOfBoundsException..."

*   **[Anh Đô (Senior)]:** "Hùng hỏi hay! Exception là 'sự kiện bất thường' xảy ra khi chương trình chạy. Exception phá vỡ flow bình thường của chương trình."

*   **[Nam (Intern)]:** "Dạ em sợ exceptions lắm! Khi thấy NullPointerException, em không biết phải làm gì!"

*   **[Anh Vương (Performance)]:** "Nam sợ đúng rồi! Nhưng exception là cơ chế bảo vệ của Java. Nó báo cho biết có vấn đề, thay vì để chương trình chạy tiếp với dữ liệu sai."

*   **[Em Hải (Clean Code)]:** "Exception handling giúp code an toàn và có thể tin cậy được. Nhưng KHÔNG nên dùng exception cho control flow bình thường."

*   **[Việt (Intern)]:** "Dạ checked exception và unchecked exception khác nhau thế nào anh?"

*   **[Anh Khánh]:** "Việt hỏi câu phỏng vấn kinh điển! Sẽ giải thích chi tiết trong bài học hôm nay."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab08

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab08/
    └── src/
        └── com/
            └── javazero/
                └── lab08/
                    ├── ExceptionHierarchyDemo.java
                    ├── TryCatchDemo.java
                    ├── ThrowThrowsDemo.java
                    ├── CustomException.java
                    └── ExceptionHandlingDemo.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Exception Hierarchy

*   **Hội ý:**

*   **[Anh Khánh]:** "Trong Java, tất cả exceptions đều kế thừa từ Throwable class. Throwable có hai nhánh chính: Error và Exception."

*   **[Anh Đô]:** "Exception Hierarchy: Throwable -> Error (system errors) và Throwable -> Exception (application errors). Exception bao gồm RuntimeException (unchecked) và các checked exceptions khác."

*   **[Em Hải (Clean Code)]:** "Bảng Exception Hierarchy:"

| Type | Handling Required | Examples |
|------|------------------|----------|
| Error | Không nên handle | OutOfMemoryError, StackOverflowError |
| RuntimeException | Unchecked (không bắt buộc handle) | NullPointerException, ArrayIndexOutOfBoundsException |
| Checked Exception | Bắt buộc handle | IOException, SQLException |

*   **[Hùng (Intern)]:** "Dạ Error khác gì Exception anh?"

*   **[Anh Vương]:** "Error là lỗi hệ thống nghiêm trọng mà chương trình không thể phục hồi (như hết memory). Exception là lỗi ứng dụng mà có thể xử lý."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Việt, em viết code demo exception hierarchy đi?"

*   **[Việt (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: ExceptionHierarchyDemo.java
// Package: com.javazero.lab08

public class ExceptionHierarchyDemo {
    public static void main(String[] args) {
        System.out.println("=== EXCEPTION HIERARCHY DEMO ===");
        
        // ========== RUNTIME EXCEPTIONS (UNCHECKED) ==========
        System.out.println("\n--- Runtime Exceptions (Unchecked) ---");
        
        // NullPointerException
        try {
            String text = null;
            System.out.println(text.length()); // NullPointerException!
        } catch (NullPointerException e) {
            System.out.println("CAUGHT: NullPointerException");
            System.out.println("  Message: " + e.getMessage());
        }
        
        // ArrayIndexOutOfBoundsException
        try {
            int[] arr = new int[5];
            arr[10] = 100; // ArrayIndexOutOfBoundsException!
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("CAUGHT: ArrayIndexOutOfBoundsException");
            System.out.println("  Message: " + e.getMessage());
        }
        
        // ArithmeticException (divide by zero)
        try {
            int result = 10 / 0; // ArithmeticException!
        } catch (ArithmeticException e) {
            System.out.println("CAUGHT: ArithmeticException");
            System.out.println("  Message: " + e.getMessage());
        }
        
        // IllegalArgumentException
        try {
            setAge(-5); // Invalid argument!
        } catch (IllegalArgumentException e) {
            System.out.println("CAUGHT: IllegalArgumentException");
            System.out.println("  Message: " + e.getMessage());
        }
        
        // ========== CHECKED EXCEPTIONS ==========
        System.out.println("\n--- Checked Exceptions ---");
        System.out.println("Checked Exceptions require try-catch or throws declaration");
        System.out.println("Examples: IOException, SQLException, ClassNotFoundException");
        
        // ========== ERRORS (USUALLY NOT HANDLED) ==========
        System.out.println("\n--- Errors (Usually Not Handled) ---");
        System.out.println("Errors are severe system problems:");
        System.out.println("  - OutOfMemoryError: JVM hết memory");
        System.out.println("  - StackOverflowError: Stack overflow");
        System.out.println("  - VirtualMachineError: JVM errors");
        
        // ========== PRINT EXCEPTION HIERARCHY ==========
        System.out.println("\n--- Exception Class Hierarchy ---");
        System.out.println("java.lang.Object");
        System.out.println("  └── java.lang.Throwable");
        System.out.println("        ├── java.lang.Error (Unchecked)");
        System.out.println("        │     ├── OutOfMemoryError");
        System.out.println("        │     ├── StackOverflowError");
        System.out.println("        │     └── ...");
        System.out.println("        └── java.lang.Exception");
        System.out.println("              ├── RuntimeException (Unchecked)");
        System.out.println("              │     ├── NullPointerException");
        System.out.println("              │     ├── IllegalArgumentException");
        System.out.println("              │     └── ...");
        System.out.println("              └── Other Exceptions (Checked)");
        System.out.println("                    ├── IOException");
        System.out.println("                    ├── SQLException");
        System.out.println("                    └── ...");
    }
    
    public static void setAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative: " + age);
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab08/ExceptionHierarchyDemo.java
// java com.javazero.lab08.ExceptionHierarchyDemo

// Output:
// === EXCEPTION HIERARCHY DEMO ===
// 
// --- Runtime Exceptions (Uncaught) ---
// CAUGHT: NullPointerException
//   Message: null
// CAUGHT: ArrayIndexOutOfBoundsException
//   Message: Index 10 out of bounds for length 5
// CAUGHT: ArithmeticException
//   Message: / by zero
// CAUGHT: IllegalArgumentException
//   Message: Age cannot be negative: -5
// 
// --- Checked Exceptions ---
// Checked Exceptions require try-catch or throws declaration
// Examples: IOException, SQLException, ClassNotFoundException
// 
// --- Errors (Usually Not Handled) ---
// Errors are severe system problems:
//   - OutOfMemoryError: JVM hết memory
//   - StackOverflowError: Stack overflow
//   - VirtualMachineError: JVM errors
// 
// --- Exception Class Hierarchy ---
// java.lang.Object
//   └── java.lang.Throwable
//         ├── java.lang.Error (Unchecked)
//         │     ├── OutOfMemoryError
//         │     ├── StackOverflowError
//         │     └── ...
//         └── java.lang.Exception
//               ├── RuntimeException (Unchecked)
//               │     ├── NullPointerException
//               │     ├── IllegalArgumentException
//               │     └── ...
//               └── Other Exceptions (Checked)
//                     ├── IOException
//                     └── ...
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! Em thấy NullPointerException, ArrayIndexOutOfBoundsException, ArithmeticException đều là RuntimeException!"

*   **[Anh Đô]:** "Nam hiểu đúng rồi! RuntimeException và các subclasses của nó là Unchecked Exceptions. Compiler KHÔNG bắt buộc phải handle."

*   **[Hùng (Intern)]:** "Dạ còn checked exceptions?"

*   **[Em Hải]:** "Checked Exceptions (như IOException, SQLException) BẮT BUỘC phải handle bằng try-catch hoặc khai báo throws. Compiler sẽ báo lỗi nếu không handle."

*   **[Việt (Intern)]:** "Dạ tại sao có sự phân biệt này?"

*   **[Anh Vương]:** "Logic: RuntimeException thường do lỗi programmer (bug), nên nên fix code. Checked Exception thường do external factors (file không tồn tại, network lỗi), cần handle."

---

### BƯỚC 2: Try-Catch-Finally

*   **Hội ý:**

*   **[Anh Khánh]:** "Try-catch-finally là cơ chế xử lý exception trong Java. Try = thử code có thể gây lỗi. Catch = xử lý nếu lỗi. Finally = luôn chạy dù có lỗi hay không."

*   **[Anh Đô]:** "Cú pháp: try { // code có thể lỗi } catch (ExceptionType e) { // xử lý } finally { // luôn chạy }"

*   **[Em Hải (Clean Code)]:** "Quy tắc: Catch từ specific đến general. IOException trước Exception. Cuối cùng catch Exception hoặc Throwable."

*   **[Hùng (Intern)]:** "Dạ finally luôn chạy? Kể cả khi có return trong try?"

*   **[Anh Vương]:** "Đúng rồi! Finally chạy TRƯỚC KHI method return. Là nơi tốt để cleanup resources (close file, close connection)."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo try-catch-finally đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: TryCatchDemo.java
// Package: com.javazero.lab08

import java.io.FileReader;
import java.io.IOException;

public class TryCatchDemo {
    
    // ========== BASIC TRY-CATCH ==========
    public static void basicTryCatch() {
        System.out.println("=== Basic Try-Catch ===");
        try {
            int result = 10 / 2;
            System.out.println("10 / 2 = " + result);
            
            String text = null;
            System.out.println(text.length()); // NullPointerException!
        } catch (ArithmeticException e) {
            System.out.println("CAUGHT ArithmeticException: " + e.getMessage());
        } catch (NullPointerException e) {
            System.out.println("CAUGHT NullPointerException: " + e.getMessage());
        }
    }
    
    // ========== TRY-CATCH-FINALLY ==========
    public static void tryCatchFinally() {
        System.out.println("\n=== Try-Catch-Finally ===");
        
        try {
            System.out.println("TRY: Bắt đầu");
            int[] arr = new int[3];
            arr[5] = 100; // ArrayIndexOutOfBoundsException!
            System.out.println("TRY: Sau lỗi (không chạy)");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("CATCH: Xử lý lỗi - " + e.getClass().getSimpleName());
        } finally {
            System.out.println("FINALLY: Luôn chạy!");
        }
        
        System.out.println("Tiếp tục chương trình...");
    }
    
    // ========== FINALLY WITH RETURN ==========
    public static int finallyWithReturn() {
        System.out.println("\n=== Finally with Return ===");
        
        try {
            System.out.println("TRY: Return 1");
            return 1;
        } catch (Exception e) {
            System.out.println("CATCH: Exception");
            return 2;
        } finally {
            System.out.println("FINALLY: Chạy trước khi return!");
            // return 3; // TRÁNH return trong finally!
        }
    }
    
    // ========== MULTIPLE CATCH BLOCKS ==========
    public static void multipleCatch() {
        System.out.println("\n=== Multiple Catch Blocks ===");
        
        Object[] objects = {10, "text", null, 3.14};
        
        for (Object obj : objects) {
            try {
                String str = (String) obj;
                System.out.println("String length: " + str.length());
            } catch (ClassCastException e) {
                System.out.println("CATCH ClassCastException: " + obj + " is not a String");
            } catch (NullPointerException e) {
                System.out.println("CATCH NullPointerException: Cannot cast null");
            } catch (RuntimeException e) {
                System.out.println("CATCH RuntimeException: " + e.getClass().getSimpleName());
            }
        }
    }
    
    // ========== TRY-WITH-RESOURCES (Java 7+) ==========
    public static void tryWithResources() {
        System.out.println("\n=== Try-with-Resources (Java 7+) ===");
        System.out.println("Auto-close resources without finally block");
        
        // FileReader sẽ tự động đóng trong finally
        try (FileReader reader = new FileReader("nonexistent.txt")) {
            System.out.println("File opened successfully");
        } catch (IOException e) {
            System.out.println("CAUGHT IOException: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        basicTryCatch();
        tryCatchFinally();
        
        int result = finallyWithReturn();
        System.out.println("Result: " + result);
        
        multipleCatch();
        tryWithResources();
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab08/TryCatchDemo.java
// java com.javazero.lab08.TryCatchDemo

// Output:
// === Basic Try-Catch ===
// 10 / 2 = 5
// CAUGHT NullPointerException: null
// 
// === Try-Catch-Finally ===
// TRY: Bắt đầu
// CATCH: Xử lý lỗi - ArrayIndexOutOfBoundsException
// FINALLY: Luôn chạy!
// Tiếp tục chương trình...
// 
// === Finally with Return ===
// TRY: Return 1
// FINALLY: Chạy trước khi return!
// Result: 1
// 
// === Multiple Catch Blocks ===
// String length: 2
// CATCH ClassCastException: 10 is not a String
// CATCH NullPointerException: Cannot cast null
// CATCH RuntimeException: 3.14 is not a String
// 
// === Try-with-Resources (Java 7+) ===
// CAUGHT IOException: nonexistent.txt (The system cannot find the file)
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! finally chạy TRƯỚC khi return! Em thấy 'FINALLY: Chạy trước khi return!' in ra TRƯỚC 'Result: 1'"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! Finally luôn chạy TRƯỚC bất kỳ return hay throw nào."

*   **[Nam (Intern)]:** "Dạ còn finally có return thì sao?"

*   **[Em Hải]:** "KHÔNG BAO GIỜ return trong finally! Sẽ override return trong try/catch. Đây là bad practice!"

*   **[Hùng (Intern)]:** "Dạ try-with-resources là gì?"

*   **[Anh Vương]:** "Java 7+ feature. Tự động close resources (như File, Connection) khi try block kết thúc. Tránh resource leaks."

---

### BƯỚC 3: Throw và Throws

*   **Hội ý:**

*   **[Anh Khánh]:** "throw dùng để NÉM exception. throws dùng để KHAI BÁO exception có thể được ném từ method."

*   **[Anh Đô]:** "throw = tạo và ném exception object. throws = method signature, báo cho caller biết method có thể ném exception."

*   **[Em Hải (Clean Code)**: "Quy tắc: Checked exceptions phải khai báo throws. Unchecked exceptions (RuntimeException) không cần."

*   **[Hùng (Intern)]:** "Dạ throw và throws khác nhau thế nào anh?"

*   **[Anh Vương]:** "throw (động từ) = ném exception. throws (số nhiều) = khai báo exception method có thể ném."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Nam, em viết code demo throw và throws đi?"

*   **[Nam (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: ThrowThrowsDemo.java
// Package: com.javazero.lab08

import java.io.IOException;

public class ThrowThrowsDemo {
    
    // ========== THROW - NÉM EXCEPTION ==========
    public static void throwExample() {
        System.out.println("=== throw - Ném Exception ===");
        
        try {
            validateAge(-5);
            System.out.println("Age is valid");
        } catch (IllegalArgumentException e) {
            System.out.println("CAUGHT: " + e.getMessage());
        }
        
        try {
            validateAge(25);
            System.out.println("Age is valid");
        } catch (IllegalArgumentException e) {
            System.out.println("CAUGHT: " + e.getMessage());
        }
    }
    
    // Method với throw
    public static void validateAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative: " + age);
        }
        // Nếu age hợp lệ, không ném exception
    }
    
    // ========== THROWS - KHAI BÁO EXCEPTION ==========
    public static void readFile(String filename) throws IOException {
        System.out.println("THROWS: Attempting to read file: " + filename);
        
        if (filename == null) {
            throw new IOException("Filename cannot be null");
        }
        
        if (!filename.endsWith(".txt")) {
            throw new IOException("Only .txt files are supported");
        }
        
        System.out.println("File content would be read here...");
    }
    
    // ========== THROWS VỚI MULTIPLE EXCEPTIONS ==========
    public static void complexMethod() throws IOException, ArithmeticException {
        System.out.println("\n=== throws với Multiple Exceptions ===");
        
        // Có thể ném IOException hoặc ArithmeticException
        throw new IOException("Simulated IO error");
        // throw new ArithmeticException("Simulated math error");
    }
    
    // ========== CALLER HANDLES EXCEPTION ==========
    public static void callerHandlesException() {
        System.out.println("\n=== Caller Handles Exception ===");
        
        try {
            readFile("data.txt");
        } catch (IOException e) {
            System.out.println("CAUGHT in caller: " + e.getMessage());
            // Xử lý lỗi ở đây
        }
    }
    
    // ========== PROPAGATE EXCEPTION ==========
    public static void propagateException() throws IOException {
        System.out.println("\n=== Propagate Exception ===");
        System.out.println("Throwing exception to caller...");
        throw new IOException("Exception propagated from method");
    }
    
    // ========== DEMO MAIN ==========
    public static void main(String[] args) {
        throwExample();
        callerHandlesException();
        
        // Propagate exception
        try {
            propagateException();
        } catch (IOException e) {
            System.out.println("CAUGHT propagated exception: " + e.getMessage());
        }
        
        // Multiple exceptions
        try {
            complexMethod();
        } catch (IOException | ArithmeticException e) {
            System.out.println("CAUGHT: " + e.getClass().getSimpleName() + " - " + e.getMessage());
        }
        
        // NESTED TRY-CATCH
        System.out.println("\n=== Nested Try-Catch ===");
        try {
            try {
                int result = 10 / 0;
            } catch (ArithmeticException e) {
                System.out.println("Inner catch: Division by zero");
                throw new IOException("Converted to IO exception");
            }
        } catch (IOException e) {
            System.out.println("Outer catch: " + e.getMessage());
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab08/ThrowThrowsDemo.java
// java com.javazero.lab08.ThrowThrowsDemo

// Output:
// === throw - Ném Exception ===
// CAUGHT: Age cannot be negative: -5
// Age is valid
// 
// === Caller Handles Exception ===
// THROWS: Attempting to read file: data.txt
// CAUGHT in caller: Only .txt files are supported
// 
// === Propagate Exception ===
// Throwing exception to caller...
// CAUGHT propagated exception: Exception propagated from method
// 
// === throws với Multiple Exceptions ===
// CAUGHT: IOException - Simulated IO error
// 
// === Nested Try-Catch ===
// Inner catch: Division by zero
// Outer catch: Converted to IO exception
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! throw new Exception() tạo và ném exception ngay lập tức!"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! throw dừng execution và nhảy đến catch tương ứng."

*   **[Hùng (Intern)**: "Dạ throws trong method signature là gì?"

*   **[Em Hải]:** "throws báo cho Java compiler và caller biết method có thể ném exception. Caller phải handle bằng try-catch hoặc tiếp tục throws."

*   **[Nam (Intern)]:** "Dạ checked exception phải khai báo throws?"

*   **[Anh Vương]:** "Đúng rồi! IOException, SQLException là checked. RuntimeException (NullPointer, etc.) là unchecked, không cần throws."

---

### BƯỚC 4: Custom Exceptions

*   **Hội ý:**

*   **[Anh Khánh]:** "Java cho phép tạo exception riêng bằng cách extend Exception (checked) hoặc RuntimeException (unchecked)."

*   **[Anh Đô]:** "Custom exceptions giúp code rõ ràng và business-specific. Thay vì generic Exception, ném InvalidAgeException."

*   **[Em Hải (Clean Code)]:** "Quy tắc: Đặt tên exception kết thúc bằng Exception. Bao gồm meaningful message. Override các constructors hữu ích."

*   **[Hùng (Intern)]:** "Dạ tạo custom exception như thế nào anh?"

*   **[Anh Vương]:** "Extend Exception (checked) hoặc RuntimeException (unchecked). Override constructors."

---

*   **Thực hiện:**

```java
// File: CustomException.java
// Package: com.javazero.lab08

// ========== CUSTOM CHECKED EXCEPTION ==========
class InvalidAgeException extends Exception {
    private int age;
    
    public InvalidAgeException() {
        super("Invalid age");
    }
    
    public InvalidAgeException(String message) {
        super(message);
    }
    
    public InvalidAgeException(String message, int age) {
        super(message);
        this.age = age;
    }
    
    public InvalidAgeException(String message, Throwable cause) {
        super(message, cause);
    }
    
    public int getAge() {
        return age;
    }
}

// ========== CUSTOM UNCHECKED EXCEPTION ==========
class InsufficientBalanceException extends RuntimeException {
    private double balance;
    private double withdraw;
    
    public InsufficientBalanceException(double balance, double withdraw) {
        super("Insufficient balance. Balance: " + balance + ", Withdraw: " + withdraw);
        this.balance = balance;
        this.withdraw = withdraw;
    }
    
    public double getBalance() {
        return balance;
    }
    
    public double getWithdrawAmount() {
        return withdraw;
    }
}

// ========== CUSTOM EXCEPTION DEMO ==========
class BankAccount {
    private String accountNumber;
    private double balance;
    
    public BankAccount(String accountNumber, double balance) {
        this.accountNumber = accountNumber;
        this.balance = balance;
    }
    
    public void setAge(int age) throws InvalidAgeException {
        if (age < 0 || age > 150) {
            throw new InvalidAgeException("Age must be between 0 and 150", age);
        }
        System.out.println("Age set to: " + age);
    }
    
    public void withdraw(double amount) {
        if (amount > balance) {
            throw new InsufficientBalanceException(balance, amount);
        }
        balance -= amount;
        System.out.println("Withdrew: " + amount + ", New balance: " + balance);
    }
}

public class CustomExceptionDemo {
    public static void main(String[] args) {
        System.out.println("=== CUSTOM EXCEPTION DEMO ===");
        
        BankAccount account = new BankAccount("12345", 1000);
        
        // ========== HANDLING CUSTOM CHECKED EXCEPTION ==========
        System.out.println("\n--- Custom Checked Exception ---");
        try {
            account.setAge(-5);
        } catch (InvalidAgeException e) {
            System.out.println("CAUGHT InvalidAgeException: " + e.getMessage());
            System.out.println("Invalid age value: " + e.getAge());
        }
        
        try {
            account.setAge(25);
        } catch (InvalidAgeException e) {
            System.out.println("CAUGHT: " + e.getMessage());
        }
        
        // ========== HANDLING CUSTOM UNCHECKED EXCEPTION ==========
        System.out.println("\n--- Custom Unchecked Exception ---");
        account.withdraw(500);
        
        try {
            account.withdraw(1000); // More than balance!
        } catch (InsufficientBalanceException e) {
            System.out.println("CAUGHT InsufficientBalanceException: " + e.getMessage());
            System.out.println("Balance: " + e.getBalance() + ", Requested: " + e.getWithdrawAmount());
        }
        
        // ========== BEST PRACTICES ==========
        System.out.println("\n--- Custom Exception Best Practices ---");
        System.out.println("1. Kế thừa Exception (checked) hoặc RuntimeException (unchecked)");
        System.out.println("2. Đặt tên kết thúc bằng Exception");
        System.out.println("3. Override các constructors hữu ích");
        System.out.println("4. Thêm fields để lưu exception details");
        System.out.println("5. Cung cấp getters cho details");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab08/CustomException.java
// java com.javazero.lab08.CustomExceptionDemo

// Output:
// === CUSTOM EXCEPTION DEMO ===
// 
// --- Custom Checked Exception ---
// CAUGHT InvalidAgeException: Age must be between 0 and 150
// Invalid age value: -5
// Age set to: 25
// 
// --- Custom Unchecked Exception ---
// Withdrew: 500.0, New balance: 500.0
// CAUGHT InsufficientBalanceException: Insufficient balance. Balance: 500.0, Requested: 1000.0
// Balance: 500.0, Requested: 1000.0
// 
// --- Custom Exception Best Practices ---
// 1. Kế thừa Exception (checked) hoặc RuntimeException (unchecked)
// 2. Đặt tên kết thúc bằng Exception
// 3. Override các constructors hữu ích
// 4. Thêm fields để lưu exception details
// 5. Cung cấp getters cho details
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! InvalidAgeException extends Exception nên là checked, phải try-catch!"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! InsufficientBalanceException extends RuntimeException nên là unchecked, không cần try-catch."

*   **[Nam (Intern)]:** "Dạ custom exception có constructors như Exception cha?"

*   **[Em Hải]:** "Đúng rồi! Nên override các constructors: không tham số, message, message+cause, cause."

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ phá exception handling! Mỗi người gây 1 bug phổ biến."

---

*   **Case 1: Swallowing Exception**

```java
// File: ExceptionSwallowingBugDemo.java
// Package: com.javazero.lab08

public class ExceptionSwallowingBugDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 1: SWALLOWING EXCEPTION (BAD!) ===");
        
        try {
            int result = 10 / 0;
        } catch (Exception e) {
            // BAD: Swallowing exception - không làm gì cả!
            System.out.println("Exception caught but ignored!");
        }
        
        // Code tiếp tục chạy như chưa có chuyện gì
        System.out.println("Program continues...");
        System.out.println("→ LỖI NGHIÊM TRỌNG! Exception bị nuốt chửng!");
        
        // FIX: Luôn xử lý hoặc re-throw
        try {
            int result = 10 / 0;
        } catch (Exception e) {
            System.out.println("FIX: Log exception: " + e.getMessage());
            throw new RuntimeException("Wrapped exception", e);
        }
    }
}
```

---

*   **Case 2: Catching Wrong Exception Type**

```java
// File: WrongCatchOrderBugDemo.java
// Package: com.javazero.lab08

public class WrongCatchOrderBugDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 2: WRONG CATCH ORDER (BAD!) ===");
        
        try {
            Object obj = null;
            String str = (String) obj; // NullPointerException
        } catch (RuntimeException e) {
            System.out.println("CAUGHT RuntimeException");
        } catch (Exception e) {
            // NEVER REACHED! Exception đã bắt ở trên!
            System.out.println("CAUGHT Exception");
        }
        
        System.out.println("\n→ WRONG! Catch general exception TRƯỚC sẽ catch tất cả!");
        System.out.println("→ CORRECT: Catch specific trước, general sau!");
        
        // CORRECT ORDER
        try {
            Object obj = null;
            String str = (String) obj;
        } catch (NullPointerException e) {
            System.out.println("CAUGHT NullPointerException (correct order)");
        } catch (RuntimeException e) {
            System.out.println("CAUGHT RuntimeException");
        } catch (Exception e) {
            System.out.println("CAUGHT general Exception");
        }
    }
}
```

---

*   **Case 3: Return trong Finally**

```java
// File: ReturnInFinallyBugDemo.java
// Package: com.javazero.lab08

public class ReturnInFinallyBugDemo {
    
    public static int badReturnInFinally() {
        try {
            System.out.println("TRY: Return 1");
            return 1;
        } finally {
            System.out.println("FINALLY: Return 2 (BAD PRACTICE!)");
            return 2; // Override return trong try!
        }
    }
    
    public static int correctFinally() {
        try {
            System.out.println("TRY: Return 1");
            return 1;
        } finally {
            System.out.println("FINALLY: Cleanup (không return)");
            // KHÔNG return trong finally
        }
    }
    
    public static void main(String[] args) {
        System.out.println("=== CASE 3: RETURN IN FINALLY (BAD!) ===");
        
        int result = badReturnInFinally();
        System.out.println("Result: " + result); // = 2, KHÔNG PHẢI 1!
        
        result = correctFinally();
        System.out.println("Result: " + result); // = 1
        
        System.out.println("\n→ Return trong finally OVERRIDE return trong try!");
        System.out.println("→ KHÔNG BAO GIỜ return trong finally!");
    }
}
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: Exception hierarchy - Throwable -> Error/Exception -> RuntimeException. Checked exceptions phải handle, unchecked không cần."

*   **[Nam (Intern)]:** "Dạ em học được: try-catch-finally. Finally luôn chạy. Catch từ specific đến general."

*   **[Việt (Intern)]:** "Dạ em học được: throw ném exception, throws khai báo. Custom exceptions giúp code rõ ràng."

*   **[Cường (Intern)**: "Dạ em học được: Không swallow exceptions, không return trong finally."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| Exception hierarchy | ☐ | ☐ |
| Checked vs Unchecked | ☐ | ☐ |
| Try-catch-finally | ☐ | ☐ |
| Finally always executes | ☐ | ☐ |
| Multiple catch blocks | ☐ | ☐ |
| throw keyword | ☐ | ☐ |
| throws keyword | ☐ | ☐ |
| Custom exceptions | ☐ | ☐ |
| Try-with-resources | ☐ | ☐ |
| Exception propagation | ☐ | ☐ |
| Best practices | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Tạo method với checked exception và handle bằng try-catch.
2.  Tạo custom exception cho validation.
3.  Thực hành exception propagation.
4.  Viết calculator với exception handling.
5.  So sánh checked vs unchecked exceptions.

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Exceptions
*   Effective Java: Item 70: Use checked exceptions for recoverable conditions
*   Effective Java: Item 71: Avoid unnecessary use of checked exceptions

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab09 - Collections Framework!**
