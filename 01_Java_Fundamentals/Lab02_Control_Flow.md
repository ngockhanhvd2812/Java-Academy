# LAB 02 - CẤU TRÚC ĐIỀU KHIỂN (CONTROL FLOW) TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta sẽ học về Control Flow - cấu trúc điều khiển. Đây là xương sống của mọi chương trình. Không có control flow, code chỉ chạy từ trên xuống dưới một cách máy móc."

*   **[Hùng (Intern)]:** "Dạ anh ơi, 'control flow' là gì vậy anh? Em nghe nói có if-else, for, while, nhưng không hiểu lắm."

*   **[Anh Đô (Senior)]:** "Hùng hỏi câu nền tảng quá! Control flow giống như 'bộ não' của chương trình. Nó quyết định: ĐOẠN NÀY CHẠY HAY KHÔNG, CHẠY BAO LÂU, CHẠY THEO ĐIỀU KIỆN NÀO."

*   **[Nam (Intern)]:** "Dạ em sợ nhất là mấy cái vòng lặp. Em từng viết while(true) mà quên break, chương trình chạy mãi không dừng!"

*   **[Anh Vương (Performance)]:** "Nam nói đúng! Vòng lặp vô tận là bug phổ biến. Nhưng trước khi sợ, mình phải hiểu cơ bản đã. Hùng, em thử đoán xem: if-else dùng để làm gì?"

*   **[Hùng (Intern)]:** "Dạ... để kiểm tra điều kiện? Nếu đúng thì làm việc này, sai thì làm việc khác?"

*   **[Anh Khánh]:** "Chính xác! Đó là tư duy cơ bản nhất của lập trình. Máy tính phải 'quyết định' dựa trên 'điều kiện'."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab02

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab02/
    └── src/
        └── com/
            └── javazero/
                └── lab02/
                    ├── IfElseDemo.java
                    ├── SwitchDemo.java
                    ├── LoopDemo.java
                    └── ControlFlowExercises.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Cấu trúc IF-ELSE

*   **Hội ý:**

*   **[Anh Khánh]:** "IF-ELSE là cấu trúc điều kiện cơ bản nhất trong Java. Nó hoạt động như thế này: NẾU (điều kiện đúng) THÌ làm A, NGƯỢC LẠI làm B."

*   **[Em Hải (Clean Code)]:** "Quy tắc đặt tên điều kiện: Tên biến/điều kiện nên bắt đầu bằng động từ hoặc tính từ. Ví dụ: isValid, hasPermission, isGreaterThan, canLogin."

*   **[Anh Vương (Performance)]:** "Về mặt hiệu năng, if-else không có overhead đáng kể. Nhưng nên đặt điều kiện có khả năng fail (null check) lên TRƯỚC để tận dụng short-circuit."

*   **[Hùng (Intern)]:** "Dạ em thấy có if không có else, có if-else, có else-if. Khác nhau thế nào anh?"

*   **[Anh Đô]:** "Hùng hỏi hay! If không có else: nếu điều kiện đúng thì chạy, sai thì bỏ qua. If-else: chọn 1 trong 2. Else-if: kiểm tra nhiều điều kiện theo thứ tự."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Hùng, em viết code demo 3 loại if-else đi?"

*   **[Hùng (Intern)]:** "Dạ em viết đây..."

---

*   **Thực hiện:**

```java
// File: IfElseDemo.java
// Package: com.javazero.lab02

public class IfElseDemo {
    public static void main(String[] args) {
        System.out.println("=== CẤU TRÚC IF-ELSE ===");
        
        // ========== IF KHÔNG CÓ ELSE ==========
        System.out.println("\n--- IF không có else ---");
        int age = 20;
        System.out.println("Age = " + age);
        
        if (age >= 18) {
            System.out.println("Bạn đã đủ tuổi trưởng thành!");
        }
        // Nếu age < 18, không in gì cả
        
        // ========== IF-ELSE ==========
        System.out.println("\n--- IF-ELSE ---");
        int number = 7;
        System.out.println("Number = " + number);
        
        if (number % 2 == 0) {
            System.out.println("Số chẵn (Even)");
        } else {
            System.out.println("Số lẻ (Odd)");
        }
        
        // ========== ELSE-IF ==========
        System.out.println("\n--- ELSE-IF (nhiều điều kiện) ---");
        int score = 85;
        System.out.println("Score = " + score);
        
        if (score >= 90) {
            System.out.println("Grade: A - Xuất sắc!");
        } else if (score >= 80) {
            System.out.println("Grade: B - Giỏi!");
        } else if (score >= 70) {
            System.out.println("Grade: C - Khá!");
        } else if (score >= 60) {
            System.out.println("Grade: D - Trung bình!");
        } else {
            System.out.println("Grade: F - Cần cố gắng!");
        }
        
        // ========== LỒNG NHIỀU IF ==========
        System.out.println("\n--- IF lồng nhau ---");
        int x = 10;
        int y = 5;
        
        if (x > 0) {
            if (y > 0) {
                System.out.println("x dương VÀ y dương");
            } else if (y < 0) {
                System.out.println("x dương VÀ y âm");
            } else {
                System.out.println("x dương VÀ y = 0");
            }
        } else if (x < 0) {
            System.out.println("x âm");
        } else {
            System.out.println("x = 0");
        }
        
        // ========== SHORT-CIRCUIT DEMO ==========
        System.out.println("\n--- Short-circuit trong IF ---");
        String name = null;
        
        // CÁCH SAI: NullPointerException
        // if (name.length() > 0) { }
        
        // CÁCH ĐÚNG: Kiểm tra null trước
        if (name != null && name.length() > 0) {
            System.out.println("Tên: " + name);
        } else {
            System.out.println("Tên không hợp lệ!");
        }
        
        // ========== TOÁN TỬ TERNARY (if-else rút gọn) ==========
        System.out.println("\n--- Toán tử Ternary ---");
        int a = 10;
        int b = 20;
        
        int max = (a > b) ? a : b;
        System.out.println("Max của " + a + " và " + b + " là: " + max);
        
        String message = (age >= 18) ? "Người lớn" : "Trẻ em";
        System.out.println("Với age = " + age + ": " + message);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/IfElseDemo.java
// java com.javazero.lab02.IfElseDemo

// Output:
// === CẤU TRÚC IF-ELSE ===
// 
// --- IF không có else ---
// Age = 20
// Bạn đã đủ tuổi trưởng thành!
// 
// --- IF-ELSE ---
// Number = 7
// Số lẻ (Odd)
// 
// --- ELSE-IF (nhiều điều kiện) ---
// Score = 85
// Grade: B - Giỏi!
// 
// --- IF lồng nhau ---
// x dương VÀ y dương
// 
// --- Short-circuit trong IF ---
// Tên không hợp lệ!
// 
// --- Toán tử Ternary ---
// Max của 10 và 20 là: 20
// Với age = 20: Người lớn
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! Em thấy với score = 85, nó in 'Grade: B'. Sao không phải 'Grade: A'? 85 >= 90 mà!"

*   **[Anh Đô]:** "Việt hỏi hay! Đây là cách else-if hoạt động: Kiểm tra TỪ TRÊN XUỐNG DƯỚI. Score = 85, kiểm tra >= 90 (sai), rồi mới kiểm tra >= 80 (đúng!). Nếu đúng thì DỪNG, không kiểm tra tiếp."

*   **[Nam (Intern)]:** "A ha! Vậy thứ tự else-if rất quan trọng!"

*   **[Em Hải (Clean Code)]:** "Đúng rồi Nam! Luôn đặt điều kiện MONG MUỐN NHẤT hoặc CỤ THỂ NHẤT lên trước. Đừng đặt (x > 0 && y > 0) sau (x > 0), sẽ không bao giờ chạy được."

*   **[Hùng (Intern)]:** "Dạ còn chỗ short-circuit, nếu name = null thì name.length() có được gọi không?"

*   **[Anh Vương (Performance)]:** "Không! Java dùng short-circuit evaluation với &&. Nếu vế trái false, vế phải KHÔNG được thực thi. Đây là lý do LUÔN đặt null check ở bên trái."

*   **[Anh Khánh]:** "Cường, em tóm tắp: else-if khác gì với nhiều if riêng biệt?"

*   **[Cường (Intern)]:** "Dạ else-if chỉ chạy một nhánh (các điều kiện loại trừ lẫn nhau), còn nhiều if riêng thì có thể chạy nhiều nhánh nếu các điều kiện không loại trừ."

*   **[Anh Khánh]:** "Chuẩn! Nam còn thắc mắc gì không?"

*   **[Nam (Intern)]:** "Dạ ternary thì có ưu điểm gì so với if-else thường?"

*   **[Em Hải]:** "Ternary ngắn gọn, dùng cho gán đơn giản. Nhưng đừng lồng nhiều ternary hoặc gọi method có side-effect trong ternary. Code sẽ khó đọc."

---

### BƯỚC 2: Cấu trúc SWITCH-CASE

*   **Hội ý:**

*   **[Anh Khánh]:** "SWITCH-CASE là cấu trúc thay thế cho else-if khi có nhiều điều kiện dựa trên MỘT GIÁ TRỊ."

*   **[Anh Vương (Performance)]:** "Switch có hiệu năng tốt hơn else-if vì compiler có thể optimize thành 'lookup table' hoặc 'jump table'. Thời gian access là O(1) thay vì O(n)."

*   **[Hùng (Intern)]:** "Dạ switch dùng với kiểu dữ liệu nào anh?"

*   **[Anh Đô]:** "Java 7 trở lên: String, enum, và các primitive wrappers. Java 14+: có thể dùng với pattern matching (advanced)."

*   **[Em Hải (Clean Code)]:** "Quy tắc: Dùng switch khi có nhiều (>3) nhánh else-if trên cùng một biến. Nhưng nhớ LUÔN có default case!"

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Hùng, em viết code demo switch-case đi?"

*   **[Hùng (Intern)]:** "Dạ được!"

---

*   **Thực hiện:**

```java
// File: SwitchDemo.java
// Package: com.javazero.lab02

public class SwitchDemo {
    public static void main(String[] args) {
        System.out.println("=== CẤU TRÚC SWITCH-CASE ===");
        
        // ========== SWITCH VỚI INT ==========
        System.out.println("\n--- Switch với int ---");
        int day = 3;
        System.out.println("Day = " + day);
        
        switch (day) {
            case 1:
                System.out.println("Thứ Hai (Monday)");
                break;
            case 2:
                System.out.println("Thứ Ba (Tuesday)");
                break;
            case 3:
                System.out.println("Thứ Tư (Wednesday)");
                break;
            case 4:
                System.out.println("Thứ Năm (Thursday)");
                break;
            case 5:
                System.out.println("Thứ Sáu (Friday)");
                break;
            case 6:
                System.out.println("Thứ Bảy (Saturday)");
                break;
            case 7:
                System.out.println("Chủ Nhật (Sunday)");
                break;
            default:
                System.out.println("Ngày không hợp lệ!");
                break;
        }
        
        // ========== SWITCH VỚI STRING (Java 7+) ==========
        System.out.println("\n--- Switch với String ---");
        String fruit = "apple";
        System.out.println("Fruit = " + fruit);
        
        switch (fruit) {
            case "apple":
                System.out.println("Táo - Màu đỏ");
                break;
            case "banana":
                System.out.println("Chuối - Màu vàng");
                break;
            case "orange":
                System.out.println("Cam - Màu cam");
                break;
            default:
                System.out.println("Không biết loại quả này!");
        }
        
        // ========== SWITCH VỚI ENUM ==========
        System.out.println("\n--- Switch với enum ---");
        Level level = Level.MEDIUM;
        System.out.println("Level = " + level);
        
        switch (level) {
            case LOW:
                System.out.println("Mức thấp - Cẩn thận");
                break;
            case MEDIUM:
                System.out.println("Mức trung bình - Chấp nhận được");
                break;
            case HIGH:
                System.out.println("Mức cao - Nguy hiểm!");
                break;
        }
        
        // ========== NHIỀU CASE LIÊN TIẾP ==========
        System.out.println("\n--- Nhiều case liên tiếp ---");
        char grade = 'B';
        System.out.println("Grade = " + grade);
        
        switch (grade) {
            case 'A':
            case 'B':
            case 'C':
                System.out.println("Đạt - Qua môn!");
                break;
            case 'D':
            case 'F':
                System.out.println("Không đạt - Cần thi lại!");
                break;
            default:
                System.out.println("Grade không hợp lệ!");
        }
        
        // ========== SWITCH EXPRESSION (Java 14+) ==========
        System.out.println("\n--- Switch Expression (Java 14+) ---");
        int month = 4;
        String season = switch (month) {
            case 12, 1, 2 -> "Mùa Đông (Winter)";
            case 3, 4, 5 -> "Mùa Xuân (Spring)";
            case 6, 7, 8 -> "Mùa Hè (Summer)";
            case 9, 10, 11 -> "Mùa Thu (Fall)";
            default -> "Tháng không hợp lệ!";
        };
        System.out.println("Month " + month + " is in " + season);
        
        // ========== LỖI THƯỜNG GẶP: QUÊN BREAK ==========
        System.out.println("\n--- LỖI: Quên break (Fall-through) ---");
        int number = 2;
        System.out.println("Number = " + number);
        
        switch (number) {
            case 1:
                System.out.println("Case 1");
                // Quên break!
            case 2:
                System.out.println("Case 2");
                // Quên break!
            case 3:
                System.out.println("Case 3");
                break;
            default:
                System.out.println("Default");
        }
        // Kết quả: In cả Case 2 VÀ Case 3!
    }
    
    // Enum cho switch demo
    enum Level {
        LOW, MEDIUM, HIGH
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/SwitchDemo.java
// java com.javazero.lab02.SwitchDemo

// Output:
// === CẤU TRÚC SWITCH-CASE ===
// 
// --- Switch với int ---
// Day = 3
// Thứ Tư (Wednesday)
// 
// --- Switch với String ---
// Fruit = apple
// Táo - Màu đỏ
// 
// --- Switch với enum ---
// Level = MEDIUM
// Mức trung bình - Chấp nhận được
// 
// --- Nhiều case liên tiếp ---
// Grade = B
// Đạt - Qua môn!
// 
// --- Switch Expression (Java 14+) ---
// Month 4 is in Mùa Xuân (Spring)
// 
// --- LỖI: Quên break (Fall-through) ---
// Number = 2
// Case 2
// Case 3
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "ANH ƠI! Sao number = 2 mà in cả 'Case 2' VÀ 'Case 3' vậy?!"

*   **[Anh Đô]:** "Nam phát hiện bug phổ biến nhất khi dùng switch: FALL-THROUGH! Khi không có break, code sẽ 'rơi' xuống case tiếp theo."

*   **[Việt (Intern)]:** "Nguy hiểm quá! Vậy phải nhớ break sau mỗi case?"

*   **[Em Hải]:** "Đúng! Trừ khi EM MUỐN fall-through (như phần 'Nhiều case liên tiếp' ở trên). Đó là kỹ thuật có chủ đích, không phải bug."

*   **[Hùng (Intern)]:** "Dạ còn switch expression với -> là gì anh? Em thấy code ngắn gọn quá!"

*   **[Anh Vương]:** "Switch expression là feature mới từ Java 14. Nó trả về giá trị và tự động có break. Ngắn gọn hơn switch-throw的传统写法."

*   **[Cường (Intern)]:** "Dạ vậy nên dùng switch expression hay switch-thông thường?"

*   **[Anh Khánh]:** "Switch expression cho code ngắn gọn khi cần gán giá trị. Switch-thông thường khi cần thực hiện nhiều lệnh phức tạp."

---

### BƯỚC 3: Vòng lặp FOR

*   **Hội ý:**

*   **[Anh Khánh]:** "Vòng lặp FOR là vòng lặp được dùng NHIỀU NHẤT trong Java. Nó hoàn hảo khi biết trước số lần lặp."

*   **[Anh Vương (Performance)]:** "For loop có performance tốt nhất trong các vòng lặp vì index được quản lý tốt và compiler có thể optimize."

*   **[Em Hải (Clean Code)]:** "Quy tắc đặt tên biến index: i, j, k cho nested loops. Nếu loop phức tạp, dùng tên có ý nghĩa như index, counter, position."

*   **[Hùng (Intern)]:** "Dạ for loop có mấy phần anh?"

*   **[Anh Đô]:** "3 phần: Khởi tạo (initialization), Điều kiện (condition), Cập nhật (update). Cú pháp: for (khởi tạo; điều kiện; cập nhật) { body }"

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Hùng, em viết code demo for loop đi?"

*   **[Hùng (Intern)]:** "Dạ được!"

---

*   **Thực hiện:**

```java
// File: ForLoopDemo.java
// Package: com.javazero.lab02

public class ForLoopDemo {
    public static void main(String[] args) {
        System.out.println("=== VÒNG LẶP FOR ===");
        
        // ========== FOR CƠ BẢN ==========
        System.out.println("\n--- For cơ bản ---");
        System.out.println("In số từ 1 đến 5:");
        for (int i = 1; i <= 5; i++) {
            System.out.println("i = " + i);
        }
        
        // ========== FOR VỚI BƯỚC NHẢY ==========
        System.out.println("\n--- For với bước nhảy tùy chỉnh ---");
        System.out.println("Số chẵn từ 0 đến 10:");
        for (int i = 0; i <= 10; i += 2) {
            System.out.println("i = " + i);
        }
        
        // ========== FOR GIẢM ==========
        System.out.println("\n--- For giảm ---");
        System.out.println("Đếm ngược từ 10 đến 1:");
        for (int i = 10; i >= 1; i--) {
            System.out.println("i = " + i);
        }
        
        // ========== FOR KHÔNG CÓ PHẦN TÙY CHỌN ==========
        System.out.println("\n--- For không có các phần tùy chọn ---");
        int count = 0;
        // Khởi tạo ở ngoài
        for (; count < 3;) {
            System.out.println("Count = " + count);
            count++; // Cập nhật ở trong body
        }
        
        // For vô tận (CẨN THẬN!)
        System.out.println("\n--- For vô tận (DANGEROUS!) ---");
        // for (;;) {
        //     System.out.println("Vĩnh viễn!");
        // }
        System.out.println("(Đã comment để tránh infinite loop)");
        
        // ========== ENHANCED FOR (FOR-EACH) ==========
        System.out.println("\n--- Enhanced For (Java 5+) ---");
        int[] numbers = {10, 20, 30, 40, 50};
        System.out.println("Array: [10, 20, 30, 40, 50]");
        
        System.out.println("Dùng enhanced for:");
        for (int num : numbers) {
            System.out.println("Number = " + num);
        }
        
        // ========== NESTED FOR LOOPS ==========
        System.out.println("\n--- Nested For Loops ---");
        System.out.println("Bảng cửu chương 2 và 3:");
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 5; j++) {
                System.out.println(i + " x " + j + " = " + (i * j));
            }
        }
        
        // ========== FOR VỚI NHIỀU BIẾN ==========
        System.out.println("\n--- For với nhiều biến ---");
        for (int i = 0, j = 10; i <= 5 && j >= 5; i++, j--) {
            System.out.println("i = " + i + ", j = " + j);
        }
        
        // ========== BREAK TRONG FOR ==========
        System.out.println("\n--- Break trong For ---");
        System.out.println("Tìm số chẵn đầu tiên:");
        for (int i = 1; i <= 10; i++) {
            if (i % 2 == 0) {
                System.out.println("Tìm thấy: " + i);
                break; // Thoát ngay khi tìm thấy
            }
        }
        
        // ========== CONTINUE TRONG FOR ==========
        System.out.println("\n--- Continue trong For ---");
        System.out.println("In số lẻ từ 1 đến 10:");
        for (int i = 1; i <= 10; i++) {
            if (i % 2 == 0) {
                continue; // Bỏ qua số chẵn
            }
            System.out.println("i = " + i);
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/ForLoopDemo.java
// java com.javazero.lab02.ForLoopDemo

// Output:
// === VÒNG LẶP FOR ===
// 
// --- For cơ bản ---
// In số từ 1 đến 5:
// i = 1
// i = 2
// i = 3
// i = 4
// i = 5
// 
// --- For với bước nhảy tùy chỉnh ---
// Số chẵn từ 0 đến 10:
// i = 0
// i = 2
// i = 4
// i = 6
// i = 8
// i = 10
// 
// --- For giảm ---
// Đếm ngược từ 10 đến 1:
// i = 10
// i = 9
// 8
// 7
// 6
// 5
// 4
// 3
// 2
// 1
// 
// --- For không có các phần tùy chọn ---
// Count = 0
// Count = 1
// 2
// 
// --- Enhanced For (Java 5+) ---
// Array: [10, 20, 30, 40, 50]
// Dùng enhanced for:
// Number = 10
// Number = 20
// Number = 30
// Number = 40
// 50
// 
// --- Nested For Loops ---
// Bảng cửu chương 2 và 3:
// 1 x 1 = 1
// 1 x 2 = 2
// 1 x 3 = 3
// 1 x 4 = 4
// 1 x 5 = 5
// 2 x 1 = 2
// 2 x 2 = 4
// 2 x 3 = 6
// 2 x 4 = 8
// 2 x 5 = 10
// 3 x 1 = 3
// 3 x 2 = 6
// 3 x 3 = 9
// 3 x 4 = 12
// 3 x 5 = 15
// 
// --- For với nhiều biến ---
// i = 0, j = 10
// i = 1, j = 9
// i = 2, j = 8
// i = 3, j = 7
// i = 4, 6
// i = 5, 5
// 
// --- Break trong For ---
// Tìm số chẵn đầu tiên:
// Tìm thấy: 2
// 
// --- Continue trong For ---
// In số lẻ từ 1 đến 10:
// i = 1
// i = 3
// i = 5
// i = 7
// i = 9
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! Em thấy break và continue rất hay. Break thoát khỏi vòng lặp, còn continue bỏ qua lần hiện tại và tiếp tục?"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! Break = THOÁT HẴN vòng lặp. Continue = BỎ QUA lần này, SANG LẦN TIẾP."

*   **[Nam (Intern)]:** "Dạ enhanced for rất tiện! Không cần quan tâm đến index. Nhưng có thể thay đổi giá trị array không anh?"

*   **[Anh Vương]:** "KHÔNG! Enhanced for chỉ đọc, không sửa được. Nếu cần sửa giá trị, dùng for thường với index."

*   **[Hùng (Intern)]:** "Dạ nested for em hiểu rồi! For bên ngoài chạy 1 lần, for bên trong chạy hết. Nên 3 x 5 = 15 lần in!"

*   **[Em Hải]:** "Đúng rồi! Nhưng hãy cẩn thận với nested loops - độ phức tạp O(n*m) có thể làm chương trình chậm nếu n và m lớn."

*   **[Cường (Intern)]:** "Dạ for (;;) mà không có break thì chạy mãi mãi đúng không anh?"

*   **[Anh Khánh]:** "Đúng! Đó là infinite loop. Trong thực tế, chỉ dùng khi có break bên trong hoặc muốn chương trình chạy mãi (như server)."

---

### BƯỚC 4: Vòng lặp WHILE và DO-WHILE

*   **Hội ý:**

*   **[Anh Khánh]:** "WHILE và DO-WHILE dùng khi KHÔNG BIET TRƯỚC số lần lặp. While kiểm tra điều kiện TRƯỚC KHI chạy. Do-while kiểm tra điều kiện SAU KHI chạy ít nhất một lần."

*   **[Anh Vương (Performance)]:** "While và for có performance tương đương. Chọn loại nào phụ thuộc vào use case, không phải performance."

*   **[Hùng (Intern)]:** "Dạ khác nhau giữa while và do-while là gì anh?"

*   **[Anh Đô]:** "While: NẾU điều kiện đúng THÌ chạy. Có thể không chạy lần nào nếu điều kiện sai ngay từ đầu. Do-while: CHẠY TRƯỚC, rồi MỚI kiểm tra. LUÔN chạy ít nhất 1 lần."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Nam, em viết code demo while và do-while đi?"

*   **[Nam (Intern)]:** "Dạ em viết đây..."

---

*   **Thực hiện:**

```java
// File: WhileLoopDemo.java
// Package: com.javazero.lab02

public class WhileLoopDemo {
    public static void main(String[] args) {
        System.out.println("=== VÒNG LẶP WHILE ===");
        
        // ========== WHILE CƠ BẢN ==========
        System.out.println("\n--- While cơ bản ---");
        int counter = 1;
        while (counter <= 5) {
            System.out.println("Counter = " + counter);
            counter++;
        }
        
        // ========== WHILE VỚI ĐIỀU KIỆN PHỨC TẠP ==========
        System.out.println("\n--- While với điều kiện phức tạp ---");
        int sum = 0;
        int num = 1;
        while (sum < 50 && num <= 20) {
            sum += num;
            System.out.println("num = " + num + ", sum = " + sum);
            num++;
        }
        System.out.println("Final sum = " + sum);
        
        // ========== WHILE VỚI USER INPUT (SIMULATION) ==========
        System.out.println("\n--- While với validation ---");
        int userInput = 0;
        boolean isValid = false;
        
        // Giả lập user nhập 3 lần mới đúng
        int[] attempts = {150, -5, 25};
        int attemptIndex = 0;
        
        while (!isValid && attemptIndex < attempts.length) {
            userInput = attempts[attemptIndex];
            System.out.println("Lần " + (attemptIndex + 1) + ": Nhập số (0-100) = " + userInput);
            
            if (userInput >= 0 && userInput <= 100) {
                isValid = true;
                System.out.println("✓ Hợp lệ!");
            } else {
                System.out.println("✗ Không hợp lệ! Nhập lại.");
            }
            attemptIndex++;
        }
        
        // ========== DO-WHILE ==========
        System.out.println("\n=== VÒNG LẶP DO-WHILE ===");
        
        // Do-while luôn chạy ít nhất 1 lần
        System.out.println("\n--- Do-while cơ bản ---");
        int x = 10;
        do {
            System.out.println("x = " + x);
            x--;
        } while (x > 0);
        
        // ========== WHILE VS DO-WHILE: KHÁC BIỆT ==========
        System.out.println("\n--- While vs Do-While: Khác biệt quan trọng ---");
        
        // While: Điều kiện sai ngay từ đầu -> KHÔNG chạy
        System.out.println("While (điều kiện sai ngay):");
        int y = 10;
        while (y < 5) {
            System.out.println("This will never print!");
            y++;
        }
        System.out.println("y = " + y + " (không thay đổi!)");
        
        // Do-while: Chạy ít nhất 1 lần, dù điều kiện sai
        System.out.println("\nDo-while (điều kiện sai ngay):");
        y = 10;
        do {
            System.out.println("Chạy ít nhất 1 lần! y = " + y);
            y++;
        } while (y < 5);
        
        // ========== DO-WHILE VỚI MENU ==========
        System.out.println("\n--- Do-while cho Menu ---");
        int choice = 0;
        
        // Giả lập user chọn option 3 để thoát
        int[] userChoices = {1, 2, 3};
        int choiceIndex = 0;
        
        do {
            if (choiceIndex > 0) {
                System.out.println("\n--- Menu ---");
                System.out.println("1. Xem danh sách");
                System.out.println("2. Thêm mới");
                System.out.println("3. Thoát");
                System.out.print("Chọn: " + userChoices[choiceIndex] + " ");
            }
            
            choice = (choiceIndex < userChoices.length) ? userChoices[choiceIndex] : 3;
            
            switch (choice) {
                case 1:
                    System.out.println("→ Đang xem danh sách...");
                    break;
                case 2:
                    System.out.println("→ Đang thêm mới...");
                    break;
                case 3:
                    System.out.println("→ Thoát chương trình!");
                    break;
            }
            choiceIndex++;
        } while (choice != 3);
        
        // ========== INFINITE WHILE LOOP (DANGEROUS!) ==========
        System.out.println("\n--- Infinite While Loop (DANGER!) ---");
        // while (true) {
        //     System.out.println("Chạy mãi mãi!");
        // }
        System.out.println("(Đã comment để tránh infinite loop)");
        
        // ========== WHILE VỚI BREAK ==========
        System.out.println("\n--- While với break (Exit condition) ---");
        int secretNumber = 7;
        int guess = 0;
        int tries = 0;
        
        // Giả lập user đoán 3 lần
        int[] guesses = {3, 8, 7};
        
        while (true) {
            if (tries >= guesses.length) break;
            
            guess = guesses[tries];
            System.out.println("Lần " + (tries + 1) + ": Đoán số = " + guess);
            
            if (guess == secretNumber) {
                System.out.println("✓ Chúc mừng! Bạn đã đoán đúng!");
                break;
            } else {
                System.out.println("✗ Sai rồi! Thử lại.");
            }
            tries++;
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/WhileLoopDemo.java
// java com.javazero.lab02.WhileLoopDemo

// Output:
// === VÒNG LẶP WHILE ===
// 
// --- While cơ bản ---
// Counter = 1
// Counter = 2
// Counter = 3
// Counter = 4
// 5
// 
// --- While với điều kiện phức tạp ---
// num = 1, sum = 1
// num = 2, sum = 3
// num = 3, sum = 6
// num = 4, sum = 10
// num = 5, sum = 15
// num = 6, sum = 21
// num = 7, sum = 28
// num = 8, sum = 36
// num = 9, sum = 45
// Final sum = 45
// 
// --- While với validation ---
// Lần 1: Nhập số (0-100) = 150
// ✗ Không hợp lệ! Nhập lại.
// Lần 2: Nhập số (0-100) = -5
// ✗ Không hợp lệ! ạ
// Lần 3: chuẩn!
//
// --- Do-while cơ bản ---
// x = 10
// x = 9
// x = 8
// ...
// x = 1
// 
// --- While vs Do-While: Khác biệt quan trọng ---
// While (điều kiện sai ngay):
// y = 10 (không thay đổi!)
// 
// Do-while (điều kiện sai ngay):
// Chạy ít nhất 1 lần! y = 10
// 
// --- While với break (Exit condition) ---
// Lần 1: Đoán số = 3
// ✗ Sai rồi! Thử lại.
// Lần 2: Đoán số = 8
// ✗ Sai rồi! Thử lại.
// Lần 3: Đoán số = 7
// ✓ Chúc mừng! Bạn đã đoán đúng!
```

---

*   **Phân tích Output:**

*   **[Hùng (Intern)]:** "Anh ơi! Em thấy while (y < 5) với y = 10 không chạy, nhưng do-while lại chạy 1 lần. Sao lạ vậy?"

*   **[Anh Đô]:** "Hùng hỏi đúng trọng tâm! While kiểm tra TRƯỚC: NẾU (y < 5) thì chạy. Với y=10, (10 < 5) = false, nên KHÔNG chạy. Do-while CHẠY TRƯỚC, rồi MỚI kiểm tra: Chạy rồi mới hỏi 'còn chạy nữa không?'."

*   **[Việt (Intern)]:** "A ha! Vậy do-while dùng khi nào anh?"

*   **[Em Hải]:** "Do-while dùng khi CẦN CHẠY ÍT NHẤT 1 LẦN, ví dụ: menu, input validation, game loop."

*   **[Nam (Intern)]:** "Dạ em sợ while (true) lắm! Làm sao để tránh infinite loop?"

*   **[Anh Vương]:** "Nam hỏi hay! Luôn có exit condition rõ ràng: 1) Điều kiện trong while phải thay đổi trong body, 2) Hoặc dùng break, 3) Hoặc dùng flag."

*   **[Cường (Intern)]:** "Dạ code với break (while true + break) có phải là bad practice không anh?"

*   **[Anh Khánh]:** "Không hẳn! Đây là pattern phổ biến. Nó rõ ràng hơn while (condition) khi exit condition phức tạp. Nhưng phải đảm bảo break sẽ được gọi."

---

### BƯỚC 5: CÂU LỆNH BREAK và CONTINUE VỚI LABEL

*   **Hội ý:**

*   **[Anh Khánh]:** "Break và Continue với Label cho phép kiểm soát nested loops. Label là 'tên' của vòng lặp, giúp break/continue nhảy đến vòng lặp cụ thể."

*   **[Anh Vương (Performance)]:** "Labeled break/continue có thể thay thế flag variables, tránh kiểm tra điều kiện không cần thiết, cải thiện performance."

*   **[Hùng (Intern)]:** "Dạ em chưa hiểu label là gì. Anh có thể ví dụ không?"

*   **[Anh Đô]:** "Label giống như 'đánh dấu' vòng lặp. Ví dụ: outerLoop: for (...) { innerLoop: for (...) { break outerLoop; } }"

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo labeled break và continue đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: LabeledBreakContinueDemo.java
// Package: com.javazero.lab02

public class LabeledBreakContinueDemo {
    public static void main(String[] args) {
        System.out.println("=== LABELED BREAK VÀ CONTINUE ===");
        
        // ========== LABELED BREAK ==========
        System.out.println("\n--- Labeled Break ---");
        System.out.println("Tìm vị trí (i, j) đầu tiên khi i * j = 12");
        
        outerLoop:
        for (int i = 1; i <= 5; i++) {
            for (int j = 1; j <= 5; j++) {
                System.out.println("i = " + i + ", j = " + j + ", i * j = " + (i * j));
                if (i * j == 12) {
                    System.out.println("✓ Tìm thấy! i = " + i + ", j = " + j);
                    break outerLoop; // Thoát cả hai loops
                }
            }
        }
        
        // ========== LABELED CONTINUE ==========
        System.out.println("\n--- Labeled Continue ---");
        System.out.println("In bảng cửu chương, bỏ qua phép chia cho 5");
        
        outerLoop:
        for (int i = 1; i <= 3; i++) {
            System.out.println("\n--- Bảng " + i + " ---");
            for (int j = 1; j <= 10; j++) {
                if (j % 5 == 0) {
                    continue outerLoop; // Bỏ qua tất cả j=5,10
                }
                System.out.println(i + " x " + j + " = " + (i * j));
            }
        }
        
        // ========== BREAK KHÔNG CÓ LABEL (CHỈ THOÁT LOOP TRONG) ==========
        System.out.println("\n--- Break không có label (so sánh) ---");
        System.out.println("Tìm vị trí (i, j) khi i * j = 6 (KHÔNG dùng label)");
        
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 3; j++) {
                System.out.println("i = " + i + ", j = " + j);
                if (i * j == 6) {
                    System.out.println("✓ Tìm thấy! i = " + i + ", j = " + j);
                    break; // Chỉ thoát loop trong (j loop)
                }
            }
            // Sau khi break, i loop vẫn tiếp tục
        }
        
        // ========== TÌM SỐ NGUYÊN TỐ VỚI BREAK ==========
        System.out.println("\n--- Ứng dụng: Tìm số nguyên tố ---");
        int[] numbersToCheck = {4, 5, 7, 9, 11};
        
        for (int num : numbersToCheck) {
            boolean isPrime = true;
            
            if (num <= 1) {
                isPrime = false;
            } else {
                for (int i = 2; i <= Math.sqrt(num); i++) {
                    if (num % i == 0) {
                        isPrime = false;
                        break; // Không cần kiểm tra tiếp
                    }
                }
            }
            
            String result = (isPrime) ? "Là số nguyên tố" : "Không phải số nguyên tố";
            System.out.println(num + ": " + result);
        }
        
        // ========== VALIDATION VỚI CONTINUE ==========
        System.out.println("\n--- Validation với continue ---");
        String[] inputs = {"123", "abc", "456", "", "789"};
        
        System.out.println("Kiểm tra input hợp lệ (chỉ số):");
        for (String input : inputs) {
            if (input.isEmpty() || !input.matches("\\d+")) {
                System.out.println("  '" + input + "' -> Bỏ qua (không hợp lệ)");
                continue;
            }
            System.out.println("  '" + input + "' -> Hợp lệ! Converted: " + Integer.parseInt(input));
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/LabeledBreakContinueDemo.java
// java com.javazero.lab02.LabeledBreakContinueDemo

// Output:
// === LABELED BREAK VÀ CONTINUE ===
// 
// --- Labeled Break ---
// Tìm vị trí (i, j) đầu tiên khi i * j = 12
// i = 1, j = 1, i * j = 1
// i = 1, j = 2, i = 2
// ...
// i = 3, j = 4, i * j = 12
// ✓ Tìm thấy! i = 3, j = 4
// 
// --- Labeled Continue ---
// In bảng cửu chương, bỏ qua phép chia cho 5
// 
// --- Bảng 1 ---
// 1 x 1 = 1
// 1 x 2 = 2
// 1 x 3 = 3
// 1 x 4 = 4
// 1 x 5 = 5
// ... (bỏ qua j=5, j=10)
// 
// --- Break không có label (so sánh) ---
// Tìm vị trí (i, j) khi i * j = 6
// i = 1, j = 1
// ...
// i = 2, j = 3
// ✓ Tìm thấy! i = 2, j = 3
// (tiếp tục i=3 loop)
// 
// --- Ứng dụng: Tìm số nguyên tố ---
// 4: Không phải số nguyên tố
// 5: Là số nguyên tố
// 7: số nguyên tố
// 9: Không phải
// 11: số nguyên tố
// 
// --- Validation với continue ---
// Kiểm tra input hợp lệ (chỉ số):
// '123' -> Hợp lệ! Converted: 123
// 'abc' -> Bỏ qua (không hợp lệ)
// '456' -> Hợp lệ!
// '' -> Bỏ qua
// '789' -> Hợp lệ!
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! Labeled break và continue rất hữu ích! Nhưng em thấy nó làm code khó đọc hơn."

*   **[Em Hải]:** "Nam nói đúng! Labeled break/continue có thể làm code 'spaghetti'. Chỉ dùng khi thực sự cần thiết. Thường thì extract thành method và return là clean hơn."

*   **[Việt (Intern)]:** "Dạ thay vì labeled break, có thể dùng return không anh?"

*   **[Anh Đô]:** "Được! Ví dụ, nếu code trong nested loop, có thể extract thành method rồi return. Hoặc dùng flag variable. Nhiều cách, chọn cách clean nhất."

*   **[Hùng (Intern)]:** "Dạ em thấy phần tìm số nguyên tố rất hay! break giúp thoát sớm khi tìm thấy ước số."

*   **[Anh Vương]:** "Đúng rồi! Đây gọi là 'early exit optimization'. Thoát sớm khi biết kết quả, tránh làm việc không cần thiết."

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ mình sẽ phá để học! Mỗi người chọn 1 bug để thử."

*   **[Việt (Intern)]:** "Em thử infinite while loop!"

*   **[Nam (Intern)]:** "Em thử off-by-one error trong for loop!"

*   **[Hùng (Intern)]:** "Em thử confuse continue với break!"

---

*   **Case 1: Infinite While Loop**

```java
// File: InfiniteLoopBugDemo.java
// Package: com.javazero.lab02

public class InfiniteLoopBugDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 1: INFINITE LOOP BUG ===");
        
        // Bug 1: Quên cập nhật biến đếm
        System.out.println("Bug 1: Quên cập nhật counter");
        int counter = 0;
        // while (counter < 5) {
        //     System.out.println("Counter = " + counter);
        //     // QUÊN: counter++;
        // }
        System.out.println("(Đã comment - sẽ chạy mãi mãi!)");
        
        // Bug 2: Điều kiện luôn đúng
        System.out.println("\nBug 2: Điều kiện luôn đúng");
        double value = 0.1;
        // while (value != 1.0) {
        //     value += 0.1;
        //     System.out.println("Value = " + value);
        // }
        // Lưu ý: 0.1 + 0.1 + 0.1... KHÔNG bằng 1.0 chính xác!
        System.out.println("(Đã comment - floating point precision issue!)");
        
        // Fix: Dùng break hoặc điều kiện rõ ràng
        System.out.println("\nFix: Dùng break");
        counter = 0;
        int maxIterations = 5;
        while (true) {
            System.out.println("Counter = " + counter);
            counter++;
            if (counter >= maxIterations) {
                break;
            }
        }
        
        // Fix 2: Dùng integer thay vì floating point
        System.out.println("\nFix 2: Dùng integer");
        int iterations = 0;
        while (iterations < 10) {
            double fixedValue = (iterations + 1) * 0.1;
            System.out.println("Value = " + fixedValue);
            iterations++;
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/InfiniteLoopBugDemo.java
// java com.javazero.lab02.InfiniteLoopBugDemo

// Output:
// === CASE 1: INFINITE LOOP BUG ===
// Bug 1: Quên cập nhật counter
// (Đã comment - sẽ chạy mãi mãi!)
// 
// Bug 2: Điều kiện luôn đúng
// (Đã comment - floating point precision issue!)
// 
// Fix: Dùng break
// Counter = 0
// Counter = 1
// 2
// 3
// 4
// 
// Fix 2: Dùng integer
// Value = 0.1
// Value = 0.2
// ...
// Value = 1.0
```

---

*   **Case 2: Off-by-One Error**

```java
// File: OffByOneErrorDemo.java
// Package: com.javazero.lab02

public class OffByOneErrorDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 2: OFF-BY-ONE ERROR ===");
        
        int[] array = {10, 20, 30, 40, 50};
        System.out.println("Array size: " + array.length); // 5 elements
        
        // Bug 1: Index bắt đầu từ 1 thay vì 0
        System.out.println("\nBug 1: Loop từ 1 đến array.length");
        System.out.println("Cố gắng truy cập:");
        for (int i = 1; i <= array.length; i++) {
            // System.out.println("array[" + i + "] = " + array[i]);
            // array[5] = ArrayIndexOutOfBoundsException!
        }
        System.out.println("(array[5] sẽ gây ArrayIndexOutOfBoundsException!)");
        
        // Bug 2: Điều kiện sai (< thay vì <=)
        System.out.println("\nBug 2: i < array.length - 1");
        System.out.println("In tất cả element:");
        for (int i = 0; i < array.length - 1; i++) {
            System.out.println("array[" + i + "] = " + array[i]);
        }
        System.out.println("Element cuối cùng (index 4) bị BỎ QUA!");
        
        // Fix: Dùng < array.length
        System.out.println("\nFix: Dùng i < array.length");
        for (int i = 0; i < array.length; i++) {
            System.out.println("array[" + i + "] = " + array[i]);
        }
        
        // Fix 2: Enhanced for (không lo off-by-one)
        System.out.println("\nFix 2: Dùng enhanced for");
        for (int value : array) {
            System.out.println("Value = " + value);
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/OffByOneErrorDemo.java
// java com.javazero.lab02OffByOneErrorDemo

// Output:
// === CASE 2: OFF-BY-ONE ERROR ===
// Array size: 5
// 
// Bug 1: Loop từ 1 đến array.length
// (array[5] sẽ gây ArrayIndexOutOfBoundsException!)
// 
// Bug 2: i < array.length - 1
// In tất cả element:
// array[0] = 10
// array[1] = 20
// array[2] = 30
// array[3] = 40
// Element cuối cùng (index 4) bị BỎ QUA!
// 
// Fix: Dùng i < array.length
// array[0] = 10
// array[1] = 20
// ...
// array[4] = 50
// 
// Fix 2: Dùng enhanced for
// Value = 10
// ...
// Value = 50
```

---

*   **Case 3: Continue vs Break Confusion**

```java
// File: ContinueBreakConfusionDemo.java
// Package: com.javazero.lab02

public class ContinueBreakConfusionDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 3: CONTINUE VS BREAK CONFUSION ===");
        
        // Bug: Dùng continue thay vì break
        System.out.println("\nBug: Dùng continue khi nên dùng break");
        int target = 5;
        for (int i = 1; i <= 10; i++) {
            if (i == target) {
                continue; // Bỏ qua i=5, TIẾP TỤC loop!
            }
            System.out.println("i = " + i);
        }
        System.out.println("Kết quả: i=5 bị bỏ qua, KHÔNG phải dừng loop!");
        
        // Fix: Dùng break khi muốn dừng
        System.out.println("\nFix: Dùng break để dừng loop");
        for (int i = 1; i <= 10; i++) {
            if (i == target) {
                break; // Dừng loop TẠI i=5
            }
            System.out.println("i = " + i);
        }
        System.out.println("Kết quả: Loop dừng tại i=5!");
        
        // Bug phức tạp hơn
        System.out.println("\nBug phức tạp: Continue trong while");
        int count = 0;
        int limit = 3;
        
        while (count < 5) {
            count++;
            if (count == 2) {
                continue; // Quay lại while condition, count KHÔNG tăng!
            }
            System.out.println("count = " + count);
        }
        System.out.println("count = " + count + " (vòng lặp không bao giờ kết thúc nếu count == 2!)");
        
        // Fix: Đảm bảo biến đếm được cập nhật
        System.out.println("\nFix: Cập nhật trước continue");
        count = 0;
        while (count < 5) {
            if (count == 2) {
                count++; // Cập nhật TRƯỚC khi continue
                continue;
            }
            System.out.println("count = " + count);
            count++;
        }
        System.out.println("Kết quả: Loop kết thúc đúng!");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/ContinueBreakConfusionDemo.java
// java com.javazero.lab02.ContinueBreakConfusionDemo

// Output:
// === CASE 3: CONTINUE VS BREAK CONFUSION ===
// 
// Bug: Dùng continue khi nên dùng break
// i = 1
// i = 2
// i = 3
// i = 4
// Kết quả: i=5 bị bỏ qua, KHÔNG phải dừng loop!
// 
// Fix: Dùng break để dừng loop
// i = 1
// 2
// 3
// 4
// Kết quả: Loop dừng tại i=5!
// 
// Bug phức tạp: Continue trong while
// count = 1
// count = 3
// count = 4
// count = 5
// count = 5 (vòng lặp không bao giờ kết thúc nếu count == 2!)
// 
// Fix: Cập nhật trước continue
// count = 1
// count = 3
// count = 4
// Kết quả: Loop kết thúc đúng!
```

---

### The Panic - ĐỌC STACK TRACE

```java
// File: StackTraceLoopDemo.java
// Package: com.javazero.lab02

public class StackTraceLoopDemo {
    public static void main(String[] args) {
        System.out.println("=== DEMO: ĐỌC STACK TRACE TRONG LOOPS ===");
        
        // Tạo lỗi cố ý
        int[] array = new int[3];
        System.out.println("Array size: " + array.length);
        
        System.out.println("Cố gắng truy cập index 5...");
        for (int i = 0; i <= array.length; i++) { // Bug: i <= thay vì i <
            System.out.println("array[" + i + "] = " + array[i]);
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab02/StackTraceLoopDemo.java
// java com.javazero.lab02.StackTraceLoopDemo

// IDE Console (Output):
// Array size: 3
// Cố gắng truy cập index 5...
// array[0] = 0
// array[1] = 0
// array[2] = 0
// Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 3
//         at StackTraceLoopDemo.main(StackTraceLoopDemo.java:12)
// 
```

*   **[Nam (Intern)]:** "Dạ em thấy lỗi ArrayIndexOutOfBoundsException: 3 ở dòng 12. Nhưng em có 3 elements, sao index 3?"

*   **[Anh Đô]:** "Nam hỏi hay! Loop chạy với i = 0, 1, 2 (OK), rồi i = 3 (array.length = 3). Index 3 không tồn tại, nên exception."

*   **[Hùng (Intern)]:** "Dạ vậy bug ở dòng 12, điều kiện `i <= array.length` nên là `i < array.length`."

*   **[Anh Vương]:** "Đúng rồi! Off-by-one error. Loop chạy 1 lần quá số elements."

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: If-else cho điều kiện đơn giản, switch-case cho nhiều nhánh trên cùng biến, for khi biết số lần, while khi không biết."

*   **[Nam (Intern)]:** "Dạ em sợ infinite loop lắm! Phải luôn có exit condition hoặc break."

*   **[Việt (Intern)]:** "Dạ em học được break thoát hẳn, continue bỏ qua lần này. Enhanced for không sửa được array."

*   **[Cường (Intern)]:** "Dạ em học được labeled break/continue cho nested loops, nhưng nên tránh dùng nhiều."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| If-else (if, if-else, else-if) | ☐ | ☐ |
| Switch-case (với int, String, enum) | ☐ | ☐ |
| Switch expression (Java 14+) | ☐ | ☐ |
| For loop (cơ bản, với nhiều biến) | ☐ | ☐ |
| Enhanced for (for-each) | ☐ | ☐ |
| While loop | ☐ | ☐ |
| Do-while loop | ☐ | ☐ |
| While vs Do-while difference | ☐ | ☐ |
| Break (unlabeled và labeled) | ☐ | ☐ |
| Continue (unlabeled và labeled) | ☐ | ☐ |
| Nested loops | ☐ | ☐ |
| Off-by-one error | ☐ | ☐ |
| Infinite loop prevention | ☐ | ☐ |
| Short-circuit evaluation | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Viết chương trình in bảng cửu chương từ 1 đến 9.
2.  Tạo menu đơn giản với do-while loop.
3.  Viết chương trình kiểm tra số nguyên tố.
4.  Tạo game đoán số với while loop và break.
5.  Viết chương trình in tam giác số sử dụng nested loops.

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Control Flow Statements
*   Effective Java: Item 58: Prefer for-each loops to traditional for loops

---

## 6. CÂU HỎI INTERVIEW THƯỜNG GẶP (Common Interview Questions)

### Về If-Else và Switch-Case

**Q1: Khi nào nên dùng switch thay vì if-else?**
- Khi có nhiều (>3) nhánh else-if trên cùng một biến
- Switch với int, String, enum có performance tốt hơn (O(1) vs O(n))
- Code đọc dễ hơn, maintainable hơn

**Q2: Sự khác biệt giữa switch và switch expression (Java 14+)?**
- Switch expression trả về giá trị
- Dùng arrow (->) thay vì break
- Ngắn gọn hơn, ít code hơn

**Q3: Fall-through trong switch là gì?**
- Khi không có break, code sẽ tiếp tục chạy các case tiếp theo
- Có thể là bug (quên break) hoặc feature (nhiều case dùng chung code)

### Về Vòng lặp

**Q4: Sự khác biệt giữa for và while?**
- For: Biết trước số lần lặp
- While: Không biết trước số lần lặp
- For-each: Duyệt collection/array

**Q5: Enhanced for (for-each) có nhược điểm gì?**
- Không thể modify collection trong quá trình duyệt
- Không có index để truy cập
- Chỉ duyệt từ đầu đến cuối

**Q6: Khi nào xảy ra Infinite Loop?**
- Điều kiện luôn true và không có break/exit
- Biến đếm không được cập nhật
- Floating-point comparison không chính xác (0.1 + 0.1 + 0.1 != 0.3)

**Q7: Off-by-one error là gì?**
- Lỗi khi loop chạy 1 lần quá ít hoặc quá nhiều
- Thường do nhầm < thành <= hoặc index bắt đầu từ 1 thay vì 0

### Về Break và Continue

**Q8: Break và Continue khác nhau thế nào?**
- Break: Thoát hoàn toàn vòng lặp
- Continue: Bỏ qua lần hiện tại, sang lần tiếp theo

**Q9: Labeled break/continue dùng khi nào?**
- Khi cần break/continue từ nested loop ra ngoài
- Thay thế cho flag variables

**Q10: Có thể dùng break trong if không?**
- Không! Break chỉ dùng trong switch hoặc loop
- Dùng break trong if (không trong loop) = compile error

---

## 7. BÀI TẬP THỰC HÀNH NÂNG CAO (Advanced Practice Exercises)

### Bài tập 1: Game Đoán Số Với Độ Khó Tăng Dần

```java
// File: NumberGuessingGame.java
// Package: com.javazero.lab02.exercises

import java.util.Scanner;
import java.util.Random;

public class NumberGuessingGame {
    public static void main(String[] args) {
        System.out.println("=== GAME ĐOÁN SỐ ===");
        System.out.println("Hãy đoán số từ 1-100!\n");

        Random random = new Random();
        int secretNumber = random.nextInt(100) + 1;
        int attempts = 0;
        int maxAttempts = 7;
        boolean guessed = false;

        Scanner scanner = new Scanner(System.in);

        while (attempts < maxAttempts) {
            System.out.print("Lần " + (attempts + 1) + "/" + maxAttempts
                    + " - Nhập số: ");

            if (!scanner.hasNextInt()) {
                System.out.println("Vui lòng nhập số!");
                scanner.next(); // Bỏ input không hợp lệ
                continue;
            }

            int guess = scanner.nextInt();
            attempts++;

            if (guess == secretNumber) {
                System.out.println("✓ Chúc mừng! Bạn đoán đúng sau " + attempts + " lần!");
                guessed = true;
                break;
            } else if (guess < secretNumber) {
                System.out.println("✗ Số bí mật LỚN HƠN!");
            } else {
                System.out.println("✗ Số bí mật NHỎ HƠN!");
            }

            // Gợi ý
            if (Math.abs(secretNumber - guess) <= 5) {
                System.out.println("→ Rất gần rồi!");
            }
        }

        if (!guessed) {
            System.out.println("\n✗ Thua rồi! Số bí mật là: " + secretNumber);
        }

        scanner.close();
    }
}
```

### Bài tập 2: In Các Pattern Với Nested Loops

```java
// File: PatternPrinting.java
// Package: com.javazero.lab02.exercises

public class PatternPrinting {
    public static void main(String[] args) {
        System.out.println("=== IN CÁC PATTERN ===\n");

        // Pattern 1: Tam giác sao
        System.out.println("--- Tam giác sao ---");
        for (int i = 1; i <= 5; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print("* ");
            }
            System.out.println();
        }

        // Pattern 2: Tam giác sao ngược
        System.out.println("\n--- Tam giác sao ngược ---");
        for (int i = 5; i >= 1; i--) {
            for (int j = 1; j <= i; j++) {
                System.out.print("* ");
            }
            System.out.println();
        }

        // Pattern 3: Bảng số
        System.out.println("\n--- Bảng số ---");
        for (int i = 1; i <= 5; i++) {
            for (int j = 1; j <= 5; j++) {
                System.out.printf("%3d", i * j);
            }
            System.out.println();
        }

        // Pattern 4: Kim tự tháp
        System.out.println("\n--- Kim tự tháp ---");
        for (int i = 1; i <= 5; i++) {
            // In khoảng trắng
            for (int j = 5; j > i; j--) {
                System.out.print(" ");
            }
            // In sao
            for (int j = 1; j <= 2 * i - 1; j++) {
                System.out.print("*");
            }
            System.out.println();
        }

        // Pattern 5: Số tam giác
        System.out.println("\n--- Số tam giác ---");
        for (int i = 1; i <= 5; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(j + " ");
            }
            System.out.println();
        }
    }
}
```

### Bài tập 3: Menu Đa Cấp Với Switch

```java
// File: RestaurantMenu.java
// Package: com.javazero.lab02.exercises

import java.util.Scanner;

public class RestaurantMenu {
    public static void main(String[] args) {
        System.out.println("=== MENU NHÀ HÀNG ===\n");

        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n--- MENU CHÍNH ---");
            System.out.println("1. Món khai vị (Appetizers)");
            System.out.println("2. Món chính (Main Courses)");
            System.out.println("3. Tráng miệng (Desserts)");
            System.out.println("4. Đồ uống (Drinks)");
            System.out.println("0. Thoát (Exit)");
            System.out.print("Chọn: ");

            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    showAppetizers();
                    break;
                case 2:
                    showMainCourses();
                    break;
                case 3:
                    showDesserts();
                    break;
                case 4:
                    showDrinks();
                    break;
                case 0:
                    System.out.println("Cảm ơn! Hẹn gặp lại!");
                    break;
                default:
                    System.out.println("Lựa chọn không hợp lệ!");
            }
        } while (choice != 0);

        scanner.close();
    }

    static void showAppetizers() {
        System.out.println("\n--- KHAI VỊ ---");
        System.out.println("1. Gỏi cuốn - 50,000đ");
        System.out.println("2. Chả giò - 45,000đ");
        System.out.println("3. Súp bí đỏ - 40,000đ");
    }

    static void showMainCourses() {
        System.out.println("\n--- MÓN CHÍNH ---");
        System.out.println("1. Cơm gà xối mỡ - 75,000đ");
        System.out.println("2. Bún chả cá - 70,000đ");
        System.out.println("3. Mì xào bò - 85,000đ");
    }

    static void showDesserts() {
        System.out.println("\n--- TRÁNG MIỆNG ---");
        System.out.println("1. Chè thạch - 30,000đ");
        System.out.println("2. Bánh flan - 35,000đ");
        System.out.println("3. Trái cây - 40,000đ");
    }

    static void showDrinks() {
        System.out.println("\n--- ĐỒ UỐNG ---");
        System.out.println("1. Trà đá - 15,000đ");
        System.out.println("2. Cà phê sữa đá - 25,000đ");
        System.out.println("3. Nước cam - 35,000đ");
    }
}
```

### Bài tập 4: Tính Số Nguyên Tố Trong Range

```java
// File: PrimeNumberRange.java
// Package: com.javazero.lab02.exercises

public class PrimeNumberRange {
    public static void main(String[] args) {
        System.out.println("=== TÌM SỐ NGUYÊN TỐ ===\n");

        int start = 1;
        int end = 100;

        System.out.println("Các số nguyên tố từ " + start + " đến " + end + ":");

        int count = 0;
        for (int i = start; i <= end; i++) {
            if (isPrime(i)) {
                System.out.print(i + " ");
                count++;
                if (count % 10 == 0) {
                    System.out.println();
                }
            }
        }

        System.out.println("\n\nTổng số: " + count + " số nguyên tố");
    }

    static boolean isPrime(int n) {
        if (n <= 1) {
            return false;
        }
        if (n == 2) {
            return true;
        }
        if (n % 2 == 0) {
            return false;
        }
        // Chỉ cần kiểm tra đến sqrt(n)
        for (int i = 3; i <= Math.sqrt(n); i += 2) {
            if (n % i == 0) {
                return false;
            }
        }
        return true;
    }
}
```

### Bài tập 5: Phân Loại Tam Giác

```java
// File: TriangleClassifier.java
// Package: com.javazero.lab02.exercises

import java.util.Scanner;

public class TriangleClassifier {
    public static void main(String[] args) {
        System.out.println("=== PHÂN LOẠI TAM GIÁC ===\n");

        Scanner scanner = new Scanner(System.in);

        System.out.print("Nhập cạnh a: ");
        double a = scanner.nextDouble();

        System.out.print("Nhập cạnh b: ");
        double b = scanner.nextDouble();

        System.out.print("Nhập cạnh c: ");
        double c = scanner.nextDouble();

        // Kiểm tra tam giác hợp lệ
        if (a <= 0 || b <= 0 || c <= 0) {
            System.out.println("✗ Các cạnh phải lớn hơn 0!");
        } else if (a + b <= c || b + c <= a || a + c <= b) {
            System.out.println("✗ Không phải tam giác! (Tổng 2 cạnh phải lớn hơn cạnh còn lại)");
        } else {
            // Phân loại tam giác
            System.out.println("\n✓ Là tam giác hợp lệ!");

            // Phân loại theo cạnh
            if (a == b && b == c) {
                System.out.println("→ Tam giác ĐỀU (Equilateral)");
            } else if (a == b || b == c || a == c) {
                System.out.println("→ Tam giác CÂN (Isosceles)");
            } else {
                System.out.println("→ Tam giác THƯỜNG (Scalene)");
            }

            // Phân loại theo góc
            double a2 = a * a;
            double b2 = b * b;
            double c2 = c * c;

            if (a2 + b2 == c2 || b2 + c2 == a2 || a2 + c2 == b2) {
                System.out.println("→ Tam giác VUÔNG (Right-angled)");
            } else if (a2 + b2 > c2 && b2 + c2 > a2 && a2 + c2 > b2) {
                System.out.println("→ Tam giác NHỌN (Acute)");
            } else {
                System.out.println("→ Tam giác TÙ (Obtuse)");
            }
        }

        scanner.close();
    }
}
```

---

## 8. CHECKLIST KIẾN THỨC TOÀN DIỆN (Comprehensive Knowledge Checklist)

### Cấu trúc Điều kiện (Conditional Structures)

- [ ] Hiểu sự khác biệt giữa if, if-else, và else-if
- [ ] Biết khi nào dùng switch-case thay vì if-else
- [ ] Hiểu ternary operator (condition ? A : B)
- [ ] Biết short-circuit evaluation trong điều kiện
- [ ] Có thể phân tích và debug các lỗi điều kiện

### Vòng lặp (Loops)

- [ ] Phân biệt được for, while, do-while và khi nào dùng loại nào
- [ ] Biết enhanced for (for-each) và giới hạn của nó
- [ ] Hiểu nested loops và complexity
- [ ] Tránh được infinite loops
- [ ] Xử lý được off-by-one errors

### Control Statements

- [ ] Dùng break để thoát vòng lặp
- [ ] Dùng continue để bỏ qua lần lặp
- [ ] Dùng labeled break/continue cho nested loops
- [ ] Biết khi nào nên extract thành method thay vì labeled control

### Interview Readiness

- [ ] Trả lời được "Khi nào dùng switch thay vì if-else?"
- [ ] Trả lời được "Sự khác biệt giữa break và continue?"
- [ ] Trả lời được "Làm sao tránh infinite loop?"
- [ ] Trả lời được "Enhanced for có nhược điểm gì?"
- [ ] Có thể viết code pattern matching cơ bản

---

## 9. TỔNG KẾT CHƯƠNG (Chapter Summary)

### Những điểm quan trọng cần nhớ:

1. **If-Else**: Linh hoạt nhất, dùng cho điều kiện phức tạp
2. **Switch-Case**: Tối ưu cho nhiều nhánh, performance tốt hơn
3. **For Loop**: Dùng khi biết trước số lần lặp
4. **While Loop**: Dùng khi điều kiện phức tạp, không biết trước số lần
5. **Do-While**: Luôn chạy ít nhất 1 lần
6. **Enhanced For**: Duyệt collection/array, không thể modify
7. **Break**: Thoát vòng lặp/switch
8. **Continue**: Bỏ qua lần hiện tại, sang lần tiếp

### Các lỗi thường gặp:

1. Quên break trong switch → fall-through
2. Off-by-one error trong loop index
3. Infinite loop khi điều kiện không thay đổi
4. Dùng = thay vì == trong điều kiện
5. Dùng break trong if (không trong loop)
6. Confuse continue với break

### Best Practices:

1. Đặt điều kiện mong muốn/trường hợp phổ biến lên trước
2. Dùng switch khi có nhiều nhánh trên cùng biến
3. Luôn có exit condition rõ ràng
4. Dùng enhanced for khi chỉ cần duyệt
5. Extract complex logic thành methods

---

## 11. MERRID DIAGRAM - SƠ ĐỒ QUYẾT ĐỊNH (Decision Flowchart)

```mermaid
graph TD
    A[CHỌN CẤU TRÚC ĐIỀU KHIỂN] --> B{Có nhiều hơn 3 nhánh<br/>trên cùng 1 biến không?}
    B -->|Có| C{Switch hỗ trợ<br/>kiểu dữ liệu không?}
    C -->|Có (int, String, enum)| D[SWITCH-CASE]
    C -->|Không| E[IF-ELSE IF]
    B -->|Không| F{Điều kiện phức tạp<br/>hoặc nhiều biến?}
    F -->|Có| E
    F -->|Không| G{Đơn giản?}
    G -->|Có| H[TERNARY ? :]
    G -->|Không| I[IF-ELSE]

    J[CHỌN VÒNG LẶP] --> K{Biết trước<br/>số lần lặp?}
    K -->|Có| L{Duyệt array<br/>hoặc collection?}
    L -->|Có| M[ENHANCED FOR]
    L -->|Không| N[FOR]
    K -->|Không| O{Chạy ít nhất<br/>1 lần không?}
    O -->|Có| P[DO-WHILE]
    O -->|Không| Q[WHILE]

    R[CONTROL STATEMENTS] --> S{Break hay<br/>Continue?}
    S -->|Thoát vòng lặp| T[BREAK]
    S -->|Bỏ qua lần này| U[CONTINUE]
    S -->|Nested loop| V[LABELED BREAK/CONTINUE]
```

---

## 12. CÁC THUẬT NGỮ ANH-VIỆT (Glossary)

| Tiếng Anh | Tiếng Việt | Ý nghĩa |
|------------|------------|----------|
| Control Flow | Luồng điều khiển | Thứ tự thực thi code |
| Conditional | Điều kiện | Cấu trúc rẽ nhánh |
| Loop | Vòng lặp | Thực thi lặp lại |
| Iteration | Lần lặp | Một vòng chạy của loop |
| Index | Chỉ số | Vị trí trong array (bắt đầu từ 0) |
| Bound | Giới hạn | Điểm bắt đầu/kết thúc |
| Scope | Phạm vi | Vùng code có thể truy cập biến |
| Fall-through | Rơi qua | Tiếp tục case tiếp theo trong switch |
| Break | Thoát | Ra khỏi vòng lặp/switch |
| Continue | Tiếp tục | Sang lần lặp tiếp theo |
| Nested | Lồng ghép | Vòng lặp trong vòng lặp |
| Infinite | Vô tận | Không có điểm kết thúc |

---

## 13. PHỤ LỤC: MẸO GHI NHỚ (Memory Tips)

### Quy tắc 3W cho If-Else:
- **What**: Điều kiện là gì?
- **Then**: Nếu đúng thì làm gì?
- **Else**: Nếu sai thì làm gì?

### Quy tắc 3C cho Loop:
- **Condition**: Điều kiện dừng là gì?
- **Change**: Biến đếm thay đổi thế nào?
- **Count**: Bao nhiêu lần lặp?

### Nhớ Switch:
- **S**witch **W**orks **I**n **T**erms **C**onsistently (SWITC)
- S = Same variable, W = Works with int/String/enum, I = Integer/String/enum, T = Types, C = Cases

### Nhớ Break vs Continue:
- **Break** = **B**uộc ra ngoài (Break out)
- **Continue** = **C**uộn sang lần **t**iếp theo (Continue to next)

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab03 - Methods & Arrays!**
