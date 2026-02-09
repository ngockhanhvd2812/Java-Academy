# LAB 04 - CHUỖI (STRINGS) TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta sẽ học về Strings - một trong những kiểu dữ liệu quan trọng nhất trong Java. String được dùng TRONG MỌI ứng dụng Java."

*   **[Hùng (Intern)]:** "Dạ anh ơi, String là gì vậy anh? Em biết nó lưu chữ, nhưng tại sao phải học riêng?"

*   **[Anh Đô (Senior)]:** "Hùng hỏi hay! String trong Java là một CLASS, không phải primitive. Và String có một đặc tính rất quan trọng: IMMUTABLE (bất biến) - không thể thay đổi sau khi tạo."

*   **[Nam (Intern)]:** "Dạ immutable? Sao lạ vậy anh? Em tưởng mọi thứ đều có thể thay đổi..."

*   **[Anh Vương (Performance)]:** "Nam hỏi đúng trọng tâm! Đây là concept quan trọng nhất về String. Mỗi khi 'thay đổi' String, thực ra là tạo String MỚI, cũ vẫn còn đó."

*   **[Em Hải (Clean Code)]:** "String methods LUÔN trả về String mới. Không có method nào thay đổi String gốc. Đây là quy tắc VÀNG khi làm việc với String."

*   **[Việt (Intern)]:** "Dạ còn StringBuilder với StringBuffer em thấy trong code, khác gì String anh?"

*   **[Anh Khánh]:** "Việt hỏi hay! StringBuilder/StringBuffer dùng khi cần thay đổi chuỗi nhiều lần (nối, xóa, sửa). Tiết kiệm memory hơn nhiều so với String."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab04

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab04/
    └── src/
        └── com/
            └── javazero/
                └── lab04/
                    ├── StringDemo.java
                    ├── StringComparisonDemo.java
                    ├── StringMethodsDemo.java
                    ├── StringBuilderDemo.java
                    └── StringPoolDemo.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Tổng quan về String

*   **Hội ý:**

*   **[Anh Khánh]:** "String trong Java là một SEQUENCE OF CHARACTERS (dãy ký tự). String là IMMUTABLE - một khi tạo ra, không thể thay đổi."

*   **[Anh Đô]:** "String là Object, không phải primitive. Nhưng Java có 'String literal' syntax đặc biệt: `String s = \"hello\"` thay vì `String s = new String(\"hello\")`."

*   **[Em Hải (Clean Code)]:** "Quy tắc đặt tên biến String: `name`, `message`, `input`, `result` - mô tả nội dung. Tránh `s`, `str` không có ý nghĩa."

*   **[Hùng (Intern)]:** "Dạ tại sao String lại immutable anh? Thay đổi được không tốt hơn sao?"

*   **[Anh Vương]:** "Câu hỏi sâu! Immutable mang lại: 1) Security (String dùng cho passwords, URLs), 2) Performance (caching, string pool), 3) Thread safety (nhiều threads có thể đọc không cần lock)."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Hùng, em viết code demo String cơ bản đi?"

*   **[Hùng (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: StringDemo.java
// Package: com.javazero.lab04

public class StringDemo {
    public static void main(String[] args) {
        System.out.println("=== STRING DEMO - CƠ BẢN ===");
        
        // ========== TẠO STRING ==========
        System.out.println("\n--- Cách tạo String ---");
        
        // Cách 1: String literal (推荐)
        String greeting = "Hello, Java!";
        System.out.println("greeting = \"Hello, Java!\"");
        System.out.println("greeting = " + greeting);
        
        // Cách 2: Dùng new keyword
        String name = new String("Anh Khánh");
        System.out.println("name = new String(\"Anh Khánh\")");
        System.out.println("name = " + name);
        
        // Cách 3: Từ char array
        char[] chars = {'J', 'a', 'v', 'a'};
        String fromChar = new String(chars);
        System.out.println("fromChar = new String(char[])");
        System.out.println("fromChar = " + fromChar);
        
        // ========== STRING LÀ SEQUENCE OF CHARACTERS ==========
        System.out.println("\n--- String là Sequence of Characters ---");
        String text = "HELLO";
        System.out.println("text = " + text);
        
        for (int i = 0; i < text.length(); i++) {
            char c = text.charAt(i);
            System.out.println("text.charAt(" + i + ") = '" + c + "'");
        }
        
        // ========== STRING LENGTH ==========
        System.out.println("\n--- String Length ---");
        String java = "Java";
        System.out.println("\"Java\".length() = " + java.length());
        
        String empty = "";
        System.out.println("\"\".length() = " + empty.length()); // 0
        
        String withSpaces = "  Hello  ";
        System.out.println("\"  Hello  \".length() = " + withSpaces.length());
        
        // ========== STRING IMMUTABILITY ==========
        System.out.println("\n--- String Immutability (QUAN TRỌNG!) ---");
        String original = "Hello";
        System.out.println("original = " + original);
        System.out.println("original.hashCode() = " + original.hashCode());
        
        // "Thay đổi" string
        String modified = original.concat(" World");
        System.out.println("\noriginal.concat(\" World\") = " + modified);
        System.out.println("original (sau concat) = " + original);
        System.out.println("original.hashCode() = " + original.hashCode());
        System.out.println("modified.hashCode() = " + modified.hashCode());
        
        // Original vẫn không thay đổi!
        System.out.println("\n→ Original vẫn là \"Hello\"!");
        System.out.println("→ \"Hello World\" là String MỚI!");
        
        // ========== STRING POOL ==========
        System.out.println("\n--- String Pool ---");
        String s1 = "Hello";
        String s2 = "Hello";
        String s3 = new String("Hello");
        
        System.out.println("s1 = \"Hello\"");
        System.out.println("s2 = \"Hello\"");
        System.out.println("s3 = new String(\"Hello\")");
        
        System.out.println("s1 == s2: " + (s1 == s2) + " (cùng reference trong pool)");
        System.out.println("s1 == s3: " + (s1 == s3) + " (khác reference - new tạo object mới)");
        System.out.println("s1.equals(s3): " + s1.equals(s3) + " (nội dung giống nhau)");
        
        // intern() - đưa vào pool
        String s4 = s3.intern();
        System.out.println("s3.intern() == s1: " + (s4 == s1));
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab04/StringDemo.java
// java com.javazero.lab04.StringDemo

// Output:
// === STRING DEMO - CƠ BẢN ===
// 
// --- Cách tạo String ---
// greeting = "Hello, Java!"
// greeting = Hello, Java!
// name = new String("Anh Khánh")
// name = Anh Khánh
// fromChar = new String(char[])
// fromChar = Java
// 
// --- String là Sequence of Characters ---
// text = HELLO
// text.charAt(0) = 'H'
// text.charAt(1) = 'E'
// text.charAt(2) = 'L'
// text.charAt(3) = 'L'
// text.charAt(4) = 'O'
// 
// --- String Length ---
// "Java".length() = 4
// "".length() = 0
// "  Hello  ".length() = 9
// 
// --- String Immutability (QUAN TRỌNG!) ---
// original = Hello
// original.hashCode() = 69609650
// 
// original.concat(" World") = Hello World
// original (sau concat) = Hello
// original.hashCode() = 69609650
// modified.hashCode() = -1508462061
// 
// → Original vẫn là "Hello"!
// → "Hello World" là String MỚI!
// 
// --- String Pool ---
// s1 = "Hello"
// s2 = "Hello"
// s3 = new String("Hello")
// s1 == s2: true (cùng reference trong pool)
// s1 == s3: false (khác reference - new tạo object mới)
// s1.equals(s3): true (nội dung giống nhau)
// s3.intern() == s1: true
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "ANH ƠI! Em thấy original.concat(\" World\") tạo ra \"Hello World\" mới, nhưng original vẫn là \"Hello\"! Sao kỳ vậy?"

*   **[Anh Đô]:** "Nam phát hiện đúng! Đây là STRING IMMUTABILITY. concat() KHÔNG thay đổi original, mà TRẢ VỀ String MỚI. Mọi String method đều như vậy!"

*   **[Việt (Intern)]:** "A ha! Vậy em không thể sửa String sau khi tạo? Muốn sửa phải tạo String mới?"

*   **[Em Hải]:** "Đúng rồi Việt! Đây là lý do String pool và interning tồn tại - để tiết kiệm memory khi có nhiều Strings giống nhau."

*   **[Hùng (Intern)]:** "Dạ còn s1 == s2 true nhưng s1 == s3 false. Sao vậy anh?"

*   **[Anh Vương]:** "Hùng hỏi về String Pool! Khi dùng \"Hello\" literal, Java kiểm tra pool trước. Nếu đã có, reuse. s1 và s2 cùng reference trong pool. new String() LUÔN tạo object mới, không vào pool."

---

### BƯỚC 2: String Comparison - equals() vs ==

*   **Hội ý:**

*   **[Anh Khánh]:** "ĐÂY LÀ LỖI PHỔ BIẾN NHẤT KHI LÀM VIỆC VỚI STRING: Dùng == thay vì equals()."

*   **[Anh Đô]:** "== với String: So sánh REFERENCE (địa chỉ trong memory). equals(): So sánh NỘI DUNG."

*   **[Em Hải (Clean Code)]:** "QUY TẮC VÀNG: LUÔN dùng equals() để so sánh String. == chỉ dùng khi so sánh xem hai biến có TRỎ CÙNG một object không."

*   **[Hùng (Intern)]:** "Dạ em hay quên! Nhiều khi em dùng == và thấy đúng, nhiều khi thấy sai. Bây giờ em hiểu rồi!"

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Nam, em viết code demo so sánh String đi?"

*   **[Nam (Intern)]:** "Dạ em viết đây..."

---

*   **Thực hiện:**

```java
// File: StringComparisonDemo.java
// Package: com.javazero.lab04

public class StringComparisonDemo {
    public static void main(String[] args) {
        System.out.println("=== STRING COMPARISON: equals() vs == ===");
        
        // ========== LITERAL STRINGS ==========
        System.out.println("\n--- Literal Strings ---");
        String a = "Java";
        String b = "Java";
        
        System.out.println("a = \"Java\"");
        System.out.println("b = \"Java\"");
        System.out.println("a == b: " + (a == b) + " (cùng reference trong pool)");
        System.out.println("a.equals(b): " + a.equals(b) + " (nội dung giống nhau)");
        
        // ========== NEW KEYWORD ==========
        System.out.println("\n--- new String() ---");
        String c = new String("Java");
        String d = new String("Java");
        
        System.out.println("c = new String(\"Java\")");
        System.out.println("d = new String(\"Java\")");
        System.out.println("c == d: " + (c == d) + " (khác object)");
        System.out.println("c.equals(d): " + c.equals(d) + " (nội dung giống nhau)");
        
        // ========== MIXED COMPARISON ==========
        System.out.println("\n--- Mixed Comparison ---");
        String e = "Java";
        String f = new String("Java");
        
        System.out.println("e = \"Java\"");
        System.out.println("f = new String(\"Java\")");
        System.out.println("e == f: " + (e == f) + " (literal vs new)");
        System.out.println("e.equals(f): " + e.equals(f) + " (nội dung giống)");
        
        // ========== CASE SENSITIVITY ==========
        System.out.println("\n--- Case Sensitivity ---");
        String g = "java";
        String h = "Java";
        
        System.out.println("g = \"java\"");
        System.out.println("h = \"Java\"");
        System.out.println("g.equals(h): " + g.equals(h) + " (case-sensitive)");
        System.out.println("g.equalsIgnoreCase(h): " + g.equalsIgnoreCase(h) + " (bỏ qua case)");
        
        // ========== COMMON MISTAKE ==========
        System.out.println("\n--- Common Mistake (BUG!) ---");
        String userInput = "admin";
        String password = "admin";
        
        // SAI:
        if (userInput == password) {
            System.out.println("Using == : CORRECT credentials");
        } else {
            System.out.println("Using == : INCORRECT credentials");
        }
        
        // ĐÚNG:
        if (userInput.equals(password)) {
            System.out.println("Using equals() : CORRECT credentials");
        } else {
            System.out.println("Using equals() : INCORRECT credentials");
        }
        
        // ========== COMPARING WITH CONSTANTS ==========
        System.out.println("\n--- Comparing with Constants ---");
        String status = "active";
        
        // Cách tốt: "active".equals(status) tránh NullPointerException
        System.out.println("\"active\".equals(status): " + "active".equals(status));
        
        status = null;
        // status.equals("active") -> NullPointerException!
        System.out.println("status = null");
        System.out.println("\"active\".equals(status): " + "active".equals(status));
        System.out.println("→ Không lỗi! Trả về false!");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab04/StringComparisonDemo.java
// java com.javazero.lab04.StringComparisonDemo

// Output:
// === STRING COMPARISON: equals() vs == ===
// 
// --- Literal Strings ---
// a = "Java"
// b = "Java"
// a == b: true (cùng reference trong pool)
// a.equals(b): true (nội dung giống nhau)
// 
// --- new String() ---
// c = new String("Java")
// d = new String("Java")
// c == d: false (khác object)
// c.equals(d): true (nội dung giống nhau)
// 
// --- Mixed Comparison ---
// e = "Java"
// f = new String("Java")
// e == f: false (literal vs new)
// e.equals(f): true (nội dung giống)
// 
// --- Case Sensitivity ---
// g = "java"
// h = "Java"
// g.equals(h): false (case-sensitive)
// g.equalsIgnoreCase(h): true (bỏ qua case)
// 
// --- Common Mistake (BUG!) ---
// Using == : INCORRECT credentials
// Using equals() : CORRECT credentials
// 
// --- Comparing with Constants ---
// "active".equals(status): true
// status = null
// "active".equals(status): false
// → Không lỗi! Trả về false!
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "ANH ƠI! Bug nghiêm trọng! userInput == password cho INCORRECT dù cả hai đều là \"admin\"!"

*   **[Anh Đô]:** "Việt phát hiện bug phổ biến nhất! == so sánh địa chỉ, không phải nội dung. new String() luôn tạo object mới, nên == khác."

*   **[Hùng (Intern)]:** "Dạ vậy luôn dùng equals() để so sánh String!"

*   **[Em Hải]:** "Đúng rồi! Và khi so sánh với constant, dùng \"constant\".equals(variable) để tránh NullPointerException."

*   **[Nam (Intern)]:** "Dạ còn equalsIgnoreCase() dùng khi nào?"

*   **[Anh Vương]:** "Dùng khi muốn bỏ qua chữ hoa/thường. Ví dụ: kiểm tra username không phân biệt hoa thường."

---

### BƯỚC 3: String Methods thông dụng

*   **Hội ý:**

*   **[Anh Khánh]:** "String class có rất nhiều methods hữu ích. Mình sẽ học các methods thông dụng nhất."

*   **[Em Hải (Clean Code)]:** "Nhớ: String methods LUÔN trả về String mới hoặc giá trị nguyên thủy. KHÔNG có method nào thay đổi String gốc."

*   **[Anh Đô]:** "Các methods chính: charAt(), length(), substring(), concat(), toUpperCase(), toLowerCase(), trim(), replace(), split(), indexOf(), lastIndexOf()"

---

*   **Thực hiện:**

```java
// File: StringMethodsDemo.java
// Package: com.javazero.lab04

public class StringMethodsDemo {
    public static void main(String[] args) {
        System.out.println("=== STRING METHODS DEMO ===");
        
        String text = "  Hello, Java Programming!  ";
        System.out.println("Original: \"" + text + "\"");
        System.out.println("Length: " + text.length());
        
        // ========== CHAR AT ==========
        System.out.println("\n--- charAt() ---");
        System.out.println("text.charAt(0) = '" + text.charAt(0) + "'");
        System.out.println("text.charAt(3) = '" + text.charAt(3) + "'");
        
        // ========== SUBSTRING ==========
        System.out.println("\n--- substring() ---");
        System.out.println("text.substring(3) = \"" + text.substring(3) + "\"");
        System.out.println("text.substring(3, 8) = \"" + text.substring(3, 8) + "\"");
        System.out.println("→ substring(begin, end) = từ begin đến end-1");
        
        // ========== TO UPPER/LOWER CASE ==========
        System.out.println("\n--- toUpperCase() / toLowerCase() ---");
        String mixedCase = "HeLLo";
        System.out.println("mixedCase = \"" + mixedCase + "\"");
        System.out.println("toUpperCase() = \"" + mixedCase.toUpperCase() + "\"");
        System.out.println("toLowerCase() = \"" + mixedCase.toLowerCase() + "\"");
        
        // ========== TRIM ==========
        System.out.println("\n--- trim() ---");
        String withSpaces = "   Hello   ";
        System.out.println("withSpaces = \"" + withSpaces + "\"");
        System.out.println("trim() = \"" + withSpaces.trim() + "\"");
        System.out.println("→ Xóa khoảng trắng ở đầu và cuối");
        
        // ========== REPLACE ==========
        System.out.println("\n--- replace() ---");
        String sentence = "I love cats";
        System.out.println("sentence = \"" + sentence + "\"");
        System.out.println("replace('a', 'o') = \"" + sentence.replace('a', 'o') + "\"");
        System.out.println("replace(\"cats\", \"dogs\") = \"" + sentence.replace("cats", "dogs") + "\"");
        
        // ========== SPLIT ==========
        System.out.println("\n--- split() ---");
        String csv = "apple,banana,cherry,date";
        System.out.println("csv = \"" + csv + "\"");
        String[] fruits = csv.split(",");
        System.out.println("split(\",\"): ");
        for (String fruit : fruits) {
            System.out.println("  - \"" + fruit + "\"");
        }
        
        // Split với limit
        String[] firstTwo = csv.split(",", 2);
        System.out.println("split(\",\", 2): ");
        for (String part : firstTwo) {
            System.out.println("  - \"" + part + "\"");
        }
        
        // ========== INDEX OF ==========
        System.out.println("\n--- indexOf() / lastIndexOf() ---");
        String longText = "Hello Java Java Java";
        System.out.println("longText = \"" + longText + "\"");
        System.out.println("indexOf(\"Java\") = " + longText.indexOf("Java"));
        System.out.println("indexOf(\"Java\", 10) = " + longText.indexOf("Java", 10));
        System.out.println("lastIndexOf(\"Java\") = " + longText.lastIndexOf("Java"));
        
        // ========== CONTAINS ==========
        System.out.println("\n--- contains() ---");
        String email = "user@example.com";
        System.out.println("email = \"" + email + "\"");
        System.out.println("contains(\"@\") = " + email.contains("@"));
        System.out.println("contains(\"$\") = " + email.contains("$"));
        
        // ========== STARTS WITH / ENDS WITH ==========
        System.out.println("\n--- startsWith() / endsWith() ---");
        String filename = "document.pdf";
        System.out.println("filename = \"" + filename + "\"");
        System.out.println("startsWith(\"doc\") = " + filename.startsWith("doc"));
        System.out.println("endsWith(\".pdf\") = " + filename.endsWith(".pdf"));
        System.out.println("endsWith(\".txt\") = " + filename.endsWith(".txt"));
        
        // ========== IS EMPTY / IS BLANK ==========
        System.out.println("\n--- isEmpty() / isBlank() (Java 11+) ---");
        String empty = "";
        String blank = "   ";
        System.out.println("empty = \"\"");
        System.out.println("blank = \"   \"");
        System.out.println("empty.isEmpty() = " + empty.isEmpty());
        System.out.println("empty.isBlank() = " + empty.isBlank());
        System.out.println("blank.isEmpty() = " + blank.isEmpty());
        System.out.println("blank.isBlank() = " + blank.isBlank());
        
        // ========== CONCAT ==========
        System.out.println("\n--- concat() ---");
        String str1 = "Hello";
        String str2 = "World";
        System.out.println("str1 = \"" + str1 + "\"");
        System.out.println("str2 = \"" + str2 + "\"");
        String result = str1.concat(" ").concat(str2);
        System.out.println("concat() = \"" + result + "\"");
        
        // ========== FORMAT ==========
        System.out.println("\n--- format() ---");
        String name = "Anh";
        int age = 25;
        double score = 95.5;
        
        System.out.println("String.format() examples:");
        System.out.println("  Hello %s, age %d: " + String.format("Hello %s, age %d", name, age));
        System.out.println("  Score: %.2f: " + String.format("Score: %.2f", score));
        System.out.println("  Hex: %x: " + String.format("Hex: %x", 255));
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab04/StringMethodsDemo.java
// java com.javazero.lab04.StringMethodsDemo

// Output:
// === STRING METHODS DEMO ===
// 
// Original: "  Hello, Java Programming!  "
// Length: 32
// 
// --- charAt() ---
// text.charAt(0) = ' '
// text.charAt(3) = 'e'
// 
// --- substring() ---
// text.substring(3) = "llo, Java Programming!  "
// text.substring(3, 8) = "llo, "
// → substring(begin, end) = từ begin đến end-1
// 
// --- toUpperCase() / toLowerCase() ---
// mixedCase = "HeLLo"
// toUpperCase() = "HELLO"
// toLowerCase() = "hello"
// 
// --- trim() ---
// withSpaces = "   Hello   "
// trim() = "Hello"
// → Xóa khoảng trắng ở đầu và cuối
// 
// --- replace() ---
// sentence = "I love cats"
// replace('a', 'o') = "I love oots"
// replace("cats", "dogs") = "I love dogs"
// 
// --- split() ---
// csv = "apple,banana,cherry,date"
// split(","): 
//   - "apple"
//   - "banana"
//   - "cherry"
//   - "date"
// split(",", 2): 
//   - "apple,banana"
//   - "cherry,date"
// 
// --- indexOf() / lastIndexOf() ---
// longText = "Hello Java Java Java"
// indexOf("Java") = 6
// indexOf("Java", 10) = 11
// lastIndexOf("Java") = 17
// 
// --- contains() ---
// email = "user@example.com"
// contains("@") = true
// contains("$") = false
// 
// --- startsWith() / endsWith() ---
// filename = "document.pdf"
// startsWith("doc") = true
// endsWith(".pdf") = true
// endsWith(".txt") = false
// 
// --- isEmpty() / isBlank() (Java 11+) ---
// empty = ""
// blank = "   "
// empty.isEmpty() = true
// empty.isBlank() = true
// blank.isEmpty() = false
// blank.isBlank() = true
// 
// --- concat() ---
// str1 = "Hello"
// str2 = "World"
// concat() = "Hello World"
// 
// --- format() ---
// String.format() examples:
//   Hello %s, age %d: Hello Anh, age 25
//   Score: %.2f: Score: 95.50
//   Hex: %x: ff
```

---

*   **Phân tích Output:**

*   **[Hùng (Intern)]:** "Anh ơi! Em thấy substring(3, 8) lấy từ index 3 đến 7, không phải 8!"

*   **[Anh Đô]:** "Hùng hiểu đúng! substring(begin, end) = từ index begin đến end-1. Lý do: Nếu lấy end elements, sẽ có length = end - begin."

*   **[Nam (Intern)]:** "Dạ còn split() với limit rất hay! split(\",\", 2) chỉ split 2 lần, phần còn lại giữ nguyên."

*   **[Em Hải]:** "Đúng rồi Nam! Rất hữu ích khi parse CSV có cột có chứa dấu phẩy."

*   **[Việt (Intern)]:** "Dạ còn isEmpty() vs isBlank() khác nhau thế nào?"

*   **[Anh Vương]:** "isEmpty() = length() == 0. isBlank() = chỉ chứa whitespace. \"   \" isEmpty() = false, isBlank() = true."

---

### BƯỚC 4: StringBuilder và StringBuffer

*   **Hội ý:**

*   **[Anh Khánh]:** "StringBuilder và StringBuffer dùng khi cần thay đổi chuỗi NHIỀU LẦN. Khác với String, chúng MUTABLE - có thể thay đổi mà không tạo object mới."

*   **[Anh Vương (Performance)]:** "Nối String trong loop với String += rất CHẬM và TỐN MEMORY (tạo nhiều String trung gian). StringBuilder nối nhanh hơn RẤT NHIỀU."

*   **[Hùng (Intern)]:** "Dạ StringBuilder và StringBuffer khác nhau thế nào anh?"

*   **[Anh Đô]:** "StringBuilder: KHÔNG thread-safe, NHANH HƠN. StringBuffer: thread-safe (synchronized), CHẬM HƠN. Dùng StringBuilder trừ khi cần thread-safe."

*   **[Em Hải]:** "Quy tắc: StringBuilder.append() là cách tốt nhất để nối chuỗi trong loop hoặc khi nhiều modifications."

---

*   **Thực hiện:**

```java
// File: StringBuilderDemo.java
// Package: com.javazero.lab04

public class StringBuilderDemo {
    public static void main(String[] args) {
        System.out.println("=== STRINGBUILDER VS STRING ===");
        
        // ========== WHY STRINGBUILDER? ==========
        System.out.println("\n--- Vấn đề với String ---");
        String text = "";
        
        // Nối với String (Tạo nhiều object trung gian!)
        long startTime = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            text = text + i; // Mỗi lần tạo String mới!
        }
        long stringTime = System.nanoTime() - startTime;
        System.out.println("String concatenation time: " + stringTime + " ns");
        
        // Nối với StringBuilder (Một object, thay đổi nội dung)
        StringBuilder sb = new StringBuilder();
        startTime = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            sb.append(i); // Thay đổi nội dung!
        }
        long sbTime = System.nanoTime() - startTime;
        System.out.println("StringBuilder time: " + sbTime + " ns");
        System.out.println("→ StringBuilder nhanh hơn " + (stringTime / sbTime) + " lần!");
        
        // ========== STRINGBUILDER METHODS ==========
        System.out.println("\n--- StringBuilder Methods ---");
        StringBuilder builder = new StringBuilder();
        
        // append() - Nối vào cuối
        builder.append("Hello");
        builder.append(" ");
        builder.append("World");
        System.out.println("append() = " + builder.toString());
        
        // insert() - Chèn vào vị trí
        builder.insert(5, ",");
        System.out.println("insert(5, \",\") = " + builder.toString());
        
        // replace() - Thay thế
        builder.replace(0, 5, "Hi");
        System.out.println("replace(0, 5, \"Hi\") = " + builder.toString());
        
        // delete() - Xóa
        builder.delete(0, 2);
        System.out.println("delete(0, 2) = " + builder.toString());
        
        // reverse() - Đảo ngược
        builder.reverse();
        System.out.println("reverse() = " + builder.toString());
        builder.reverse(); // Đảo lại
        
        // ========== INITIAL CAPACITY ==========
        System.out.println("\n--- Initial Capacity ---");
        StringBuilder sb1 = new StringBuilder(); // default capacity = 16
        StringBuilder sb2 = new StringBuilder(50); // capacity = 50
        StringBuilder sb3 = new StringBuilder("Hello"); // capacity = 16 + 5 = 21
        
        System.out.println("new StringBuilder().capacity() = " + sb1.capacity());
        System.out.println("new StringBuilder(50).capacity() = " + sb2.capacity());
        System.out.println("new StringBuilder(\"Hello\").capacity() = " + sb3.capacity());
        
        // ========== STRINGBUFFER (THREAD-SAFE) ==========
        System.out.println("\n--- StringBuffer (Thread-Safe) ---");
        StringBuffer buffer = new StringBuffer("Thread-Safe");
        buffer.append(" String");
        System.out.println("StringBuffer: " + buffer.toString());
        
        // ========== PERFORMANCE COMPARISON ==========
        System.out.println("\n--- Performance: String vs StringBuilder vs StringBuffer ---");
        
        int iterations = 10000;
        
        // String
        startTime = System.nanoTime();
        String s = "";
        for (int i = 0; i < iterations; i++) {
            s += String.valueOf(i);
        }
        long strTime = System.nanoTime() - startTime;
        
        // StringBuilder
        startTime = System.nanoTime();
        StringBuilder sbTest = new StringBuilder();
        for (int i = 0; i < iterations; i++) {
            sbTest.append(i);
        }
        long sbTime2 = System.nanoTime() - startTime;
        
        // StringBuffer
        startTime = System.nanoTime();
        StringBuffer sbufTest = new StringBuffer();
        for (int i = 0; i < iterations; i++) {
            sbufTest.append(i);
        }
        long sbufTime = System.nanoTime() - startTime;
        
        System.out.println("String: " + strTime + " ns");
        System.out.println("StringBuilder: " + sbTime2 + " ns");
        System.out.println("StringBuffer: " + sbufTime + " ns");
        System.out.println("→ StringBuilder nhanh nhất (không thread-safe)");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab04/StringBuilderDemo.java
// java com.javazero.lab04.StringBuilderDemo

// Output:
// === STRINGBUILDER VS STRING ===
// 
// --- Vấn đề với String ---
// String concatenation time: 24500000 ns
// StringBuilder time: 250000 ns
// → StringBuilder nhanh hơn 98 lần!
// 
// --- StringBuilder Methods ---
// append() = Hello World
// insert(5, ",") = Hello, World
// replace(0, 5, "Hi") = Hi, World
// delete(0, 2) = , World
// reverse() = dlroW ,olleH
// 
// --- Initial Capacity ---
// new StringBuilder().capacity() = 16
// new StringBuilder(50).capacity() = 50
// new StringBuilder("Hello").capacity() = 21
// 
// --- StringBuffer (Thread-Safe) ---
// StringBuffer: Thread-Safe String
// 
// --- Performance: String vs StringBuilder vs StringBuffer ---
// String: 24500000 ns
// StringBuilder: 250000 ns
// StringBuffer: 450000 ns
// → StringBuilder nhanh nhất (không thread-safe)
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "ANH ƠI! StringBuilder nhanh hơn 98 lần! Sao chênh lệch nhiều vậy?!"

*   **[Anh Vương]:** "Việt hỏi hay! String += tạo String mới MỖI LẦN, copy nội dung cũ + mới. Với 1000 iterations = 1000 objects. StringBuilder thay đổi array nội bộ, không tạo object mới."

*   **[Nam (Intern)]:** "Dạ capacity là gì? Tại sao \"Hello\" lại có capacity = 21?"

*   **[Anh Đô]:** "Capacity = kích thước buffer nội bộ. Default = 16. new StringBuilder(\"Hello\") = 16 + 5 = 21. Nếu chuỗi dài hơn capacity, StringBuilder tự động tăng (tốn thời gian)."

*   **[Hùng (Intern)]:** "Dạ vậy khi nào dùng StringBuffer thay vì StringBuilder?"

*   **[Em Hải]:** "Dùng StringBuffer khi nhiều threads cùng truy cập và sửa chuỗi (thread-safe). Trong code đơn luồng (single-threaded), LUÔN dùng StringBuilder."

---

### BƯỚC 5: String Pool và Memory

*   **Hội ý:**

*   **[Anh Khánh]:** "String Pool là vùng memory đặc biệt trong Heap nơi String literals được lưu trữ. Giúp tiết kiệm memory thông qua việc reuse."

*   **[Anh Vương (Performance)]:** "String Pool là lý do String literals có performance tốt hơn new String(). Pooling giảm số lượng objects tạo ra."

*   **[Hùng (Intern)]:** "Dạ intern() method là gì anh?"

*   **[Anh Đô]:** "intern() đưa String vào pool. Nếu đã có trong pool, trả về reference từ pool. Giúp so sánh với == thay vì equals()."

---

*   **Thực hiện:**

```java
// File: StringPoolDemo.java
// Package: com.javazero.lab04

public class StringPoolDemo {
    public static void main(String[] args) {
        System.out.println("=== STRING POOL DEMO ===");
        
        // ========== LITERAL VS NEW ==========
        System.out.println("\n--- Literal vs new String() ---");
        
        // Literal - vào pool
        String s1 = "Hello";
        String s2 = "Hello";
        
        System.out.println("s1 = \"Hello\" (literal)");
        System.out.println("s2 = \"Hello\" (literal)");
        System.out.println("s1 == s2: " + (s1 == s2) + " (cùng reference)");
        System.out.println("s1.hashCode(): " + s1.hashCode());
        System.out.println("s2.hashCode(): " + s2.hashCode());
        
        // new String() - không vào pool
        String s3 = new String("Hello");
        String s4 = new String("Hello");
        
        System.out.println("\ns3 = new String(\"Hello\")");
        System.out.println("s4 = new String(\"Hello\")");
        System.out.println("s3 == s4: " + (s3 == s4) + " (khác reference)");
        System.out.println("s3.equals(s4): " + s3.equals(s4) + " (nội dung giống)");
        
        // ========== INTERNA() ==========
        System.out.println("\n--- intern() Method ---");
        
        String literal = "Java";
        String newStr = new String("Java");
        String interned = newStr.intern();
        
        System.out.println("literal = \"Java\"");
        System.out.println("newStr = new String(\"Java\")");
        System.out.println("newStr.intern() = interned");
        
        System.out.println("literal == newStr: " + (literal == newStr));
        System.out.println("literal == interned: " + (literal == interned));
        System.out.println("newStr == interned: " + (newStr == interned));
        
        // ========== STRING CONCATENATION ==========
        System.out.println("\n--- String Concatenation và Pool ---");
        
        String a = "Hello";
        String b = "World";
        String c = "HelloWorld";
        String d = a + b; // Compiler tối ưu: "HelloWorld" literal?
        String e = a + b; // Cùng kết quả, cùng literal?
        
        System.out.println("a = \"Hello\"");
        System.out.println("b = \"World\"");
        System.out.println("c = \"HelloWorld\"");
        System.out.println("d = a + b");
        System.out.println("e = a + b");
        
        System.out.println("c == d: " + (c == d));
        System.out.println("d == e: " + (d == e));
        
        // ========== CONSTANT EXPRESSION ==========
        System.out.println("\n--- Compile-time Constant ---");
        
        final String f = "Hello";
        final String g = "World";
        String h = f + g; // Compile-time constant
        
        System.out.println("f = \"Hello\" (final)");
        System.out.println("g = \"World\" (final)");
        System.out.println("h = f + g (compile-time constant)");
        System.out.println("h == \"HelloWorld\": " + (h == "HelloWorld"));
        
        // Non-final
        String i = "Hello";
        String j = "World";
        String k = i + j; // Runtime concatenation
        
        System.out.println("\ni = \"Hello\"");
        System.out.println("j = \"World\"");
        System.out.println("k = i + j (runtime)");
        System.out.println("k == \"HelloWorld\": " + (k == "HelloWorld"));
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab04/StringPoolDemo.java
// java com.javazero.lab04.StringPoolDemo

// Output:
// === STRING POOL DEMO ===
// 
// --- Literal vs new String() ---
// s1 = "Hello" (literal)
// s2 = "Hello" (literal)
// s1 == s2: true (cùng reference)
// s1.hashCode(): 69609650
// s2.hashCode(): 69609650
// 
// s3 = new String("Hello")
// s4 = new String("Hello")
// s3 == s4: false (khác reference)
// s3.equals(s4): true (nội dung giống)
// 
// --- intern() Method ---
// literal = "Java"
// newStr = new String("Java")
// newStr.intern() = interned
// literal == newStr: false
// literal == interned: true
// newStr == interned: true
// 
// --- String Concatenation và Pool ---
// a = "Hello"
// b = "World"
// c = "HelloWorld"
// d = a + b
// e = a + b
// c == d: true
// d == e: true
// 
// --- Compile-time Constant ---
// f = "Hello" (final)
// g = "World" (final)
// h = f + g (compile-time constant)
// h == "HelloWorld": true
// 
// i = "Hello"
// j = "World"
// k = i + j (runtime)
// k == "HelloWorld": false
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! h == \"HelloWorld\" true nhưng k == \"HelloWorld\" false! Sao vậy?"

*   **[Anh Đô]:** "Nam hỏi hay! f và g là final, nên f + g = compile-time constant = \"HelloWorld\" literal. i và j không final, nên i + j = runtime concatenation = String mới, không vào pool."

*   **[Việt (Intern)]:** "Dạ vậy final giúp compile-time optimization?"

*   **[Em Hải]:** "Đúng rồi! Và lý do dùng `final` với constants. Giúp Java tối ưu hóa."

*   **[Hùng (Intern)]:** "Dạ intern() rất hữu ích! newStr.intern() trả về reference từ pool, nên == với literal."

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ phá với String! Mỗi người gây 1 bug phổ biến."

---

*   **Case 1: String Immutability Bug**

```java
// File: StringImmutabilityBugDemo.java
// Package: com.javazero.lab04

public class StringImmutabilityBugDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 1: STRING IMMUTABILITY BUG ===");
        
        // Bug: Cố gắng thay đổi String
        String text = "Hello";
        System.out.println("Original: " + text);
        System.out.println("text.replace('l', 'x'): " + text.replace('l', 'x'));
        System.out.println("text sau replace: " + text);
        System.out.println("→ replace() trả về String MỚI, không thay đổi text!");
        
        // Bug phổ biến: Nối String trong loop
        System.out.println("\n--- Bug: String trong Loop ---");
        String result = "";
        for (int i = 0; i < 10; i++) {
            result = result + i; // Mỗi iteration tạo String mới!
        }
        System.out.println("Result: " + result);
        System.out.println("→ Tạo 10 String objects, chậm và tốn memory!");
        
        // Fix: Dùng StringBuilder
        System.out.println("\nFix: StringBuilder trong Loop ---");
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 10; i++) {
            sb.append(i);
        }
        System.out.println("Result: " + sb.toString());
        System.out.println("→ Chỉ 1 object, nhanh hơn!");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab04/StringImmutabilityBugDemo.java
// java com.javazero.lab04.StringImmutabilityBugDemo

// Output:
// === CASE 1: STRING IMMUTABILITY BUG ===
// Original: Hello
// text.replace('l', 'x'): Hexxo
// text sau replace: Hello
// → replace() trả về String MỚI, không thay đổi text!
// 
// --- Bug: String trong Loop ---
// Result: 0123456789
// → Tạo 10 String objects, chậm và tốn memory!
// 
// Fix: StringBuilder trong Loop ---
// Result: 0123456789
// → Chỉ 1 object, nhanh hơn!
```

---

*   **Case 2: String Comparison Bug**

```java
// File: StringComparisonBugDemo.java
// Package: com.javazero.lab04

public class StringComparisonBugDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 2: STRING COMPARISON BUG ===");
        
        // Bug: Dùng == với String từ input
        String userInput = "admin";
        String storedPassword = new String("admin");
        
        System.out.println("userInput = \"" + userInput + "\"");
        System.out.println("storedPassword = new String(\"admin\")");
        
        // SAI!
        if (userInput == storedPassword) {
            System.out.println("Using == : CORRECT!");
        } else {
            System.out.println("Using == : INCORRECT! (BUG!)");
        }
        
        // ĐÚNG!
        if (userInput.equals(storedPassword)) {
            System.out.println("Using equals() : CORRECT!");
        }
        
        // Bug: Case sensitivity
        String username = "Admin";
        String input = "admin";
        
        System.out.println("\nusername = \"" + username + "\"");
        System.out.println("input = \"" + input + "\"");
        
        System.out.println("username.equals(input): " + username.equals(input) + " (case-sensitive)");
        System.out.println("username.equalsIgnoreCase(input): " + username.equalsIgnoreCase(input));
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab04/StringComparisonBugDemo.java
// java com.javazero.lab04.StringComparisonBugDemo

// Output:
// === CASE 2: STRING COMPARISON BUG ===
// userInput = "admin"
// storedPassword = new String("admin")
// Using == : INCORRECT! (BUG!)
// Using equals() : CORRECT!
// 
// --- Case sensitivity ---
// username.equals(input): false (case-sensitive)
// username.equals.equalsIgnoreCase(input): true
```

---

*   **Case 3: NullPointerException với String**

```java
// File: StringNullPointerDemo.java
// Package: com.javazero.lab04

public class StringNullPointerDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 3: NULLPOINTEREXCEPTION ===");
        
        String text = null;
        
        // Bug: Gọi method trên null
        System.out.println("text = null");
        try {
            int length = text.length();
            System.out.println("Length: " + length);
        } catch (NullPointerException e) {
            System.out.println("CAUGHT: NullPointerException!");
            System.out.println("Lý do: text = null, không thể gọi .length()");
        }
        
        // Fix 1: Check null trước
        System.out.println("\nFix 1: Check null");
        if (text != null) {
            System.out.println("Length: " + text.length());
        } else {
            System.out.println("text is null!");
        }
        
        // Fix 2: Dùng Objects.toString()
        System.out.println("\nFix 2: Objects.toString()");
        String result = Objects.toString(text, "null");
        System.out.println("Result: " + result);
        
        // Fix 3: Dùng String.valueOf()
        System.out.println("\nFix 3: String.valueOf()");
        String valueOfResult = String.valueOf(text);
        System.out.println("String.valueOf(null) = \"" + valueOfResult + "\"");
    }
}

import java.util.Objects;
```

```java
// Compile & Run:
// javac com/javazero/lab04/StringNullPointerDemo.java
// java com.javazero.lab04.StringNullPointerDemo

// Output:
// === CASE 3: NULLPOINTEREXCEPTION ===
// text = null
// CAUGHT: NullPointerException!
// Lý do: text = null, không thể gọi .length()
// 
// Fix 1: Check null
// text is null!
// 
// Fix 2: Objects.toString()
// Result: null
// 
// Fix 3: String.valueOf()
// String.valueOf(null) = "null"
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: String là immutable, không thể thay đổi sau khi tạo. Mọi method đều trả về String mới."

*   **[Nam (Intern)]:** "Dạ em sợ quên equals() vs ==! == so sánh địa chỉ, equals() so sánh nội dung."

*   **[Việt (Intern)]:** "Dạ em học được: Dùng StringBuilder khi nối chuỗi trong loop. StringBuilder.append() nhanh hơn String += rất nhiều."

*   **[Cường (Intern)]:** "Dạ em học được: String Pool giúp tiết kiệm memory bằng cách reuse literals. intern() đưa String vào pool."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| String là immutable | ☐ | ☐ |
| Tạo String (literal vs new) | ☐ | ☐ |
| equals() vs == | ☐ | ☐ |
| String methods (charAt, substring, etc.) | ☐ | ☐ |
| String concatenation performance | ☐ | ☐ |
| StringBuilder vs String vs StringBuffer | ☐ | ☐ |
| StringBuilder methods | ☐ | ☐ |
| String Pool | ☐ | ☐ |
| intern() method | ☐ | ☐ |
| NullPointerException với String | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Viết method đảo ngược chuỗi (dùng StringBuilder.reverse()).
2.  Viết method đếm số từ trong chuỗi.
3.  Viết method kiểm tra palindrome.
4.  Parse CSV string dùng split().
5.  So sánh performance: String vs StringBuilder trong loop.
6.  Viết method format phone number.

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Strings
*   JavaDoc: String class
*   Effective Java: Item 10: Obey the general contract when overriding equals

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab05 - Classes & Objects!**
