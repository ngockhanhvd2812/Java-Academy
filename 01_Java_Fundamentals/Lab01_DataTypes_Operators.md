# LAB 01 - KIỂU DỮ LIỆU VÀ TOÁN TỬ TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta bắt đầu hành trình Java Zero-To-Hero. Đây là bước đầu tiên, nền tảng nhất, nhưng cũng là bước dễ bỏ qua nhất. Nhiều người nghĩ 'biến thì có gì đâu, khai báo rồi dùng thôi' - nhưng chính sự chủ quan này gây ra 80% lỗi khi mới học Java."

*   **[Hùng (Intern)]:** "Dạ anh ơi, 'kiểu dữ liệu' là gì vậy anh? Em nghe nói Java có kiểu nguyên thủy và kiểu tham chiếu, nhưng không hiểu lắm."

*   **[Anh Vương (Performance)]:** "Câu hỏi hay đấy Hùng. Để anh nói nhé: Kiểu dữ liệu giống như cái 'khuôn' - nó quyết định cái gì có thể nhét vào và cái gì sẽ ra. Nếu khuôn sai, thành phẩm sẽ méo mó hoặc không ra gì cả."

*   **[Anh Khánh]:** "Vương nói đúng. Nam, em có đang dùng máy tính Windows không? Em thử tưởng tượng khuôn là 16-bit, nhưng em nhét 32-bit vào - chuyện gì xảy ra?"

*   **[Nam (Intern)]:** "Dạ... em nghĩ là nó sẽ bị cắt bớt hoặc lỗi anh?"

*   **[Em Hải (Clean Code)]:** "Chính xác! Đó là lý do tại sao chúng ta phải hiểu rõ từng kiểu dữ liệu. Nam, em nhớ kỹ nhé: Java có 8 kiểu nguyên thủy, mỗi kiểu có kích thước và công dụng riêng."

*   **[Anh Khánh]:** "Ok, mình bắt đầu thôi. Cường, trong thực tế em thường dùng kiểu dữ liệu nào nhất?"

*   **[Cường (Intern)]:** "Dạ em thấy hay dùng int và String anh, nhưng em không biết tại sao int lại phổ biến hơn byte hay short."

*   **[Anh Đô (Senior)]:** "Câu hỏi thực tế đấy. Int vì nó phù hợp với kiến trúc của chip x86 - 32-bit. Nhưng mà... Hùng, em thử đoán xem: Nếu chỉ cần đếm từ 0 đến 100, em dùng kiểu gì?"

*   **[Hùng (Intern)]:** "Dạ... int ạ? Vì em thấy ai cũng dùng int."

*   **[Anh Đô]:** "Không sai, nhưng chưa tối ưu. Để anh giải thích chi tiết nhé."

---

## 2. Chuẩn bị (Prerequisites)

Trước khi bắt đầu, anh em cần chuẩn bị môi trường sau:

*   **JDK version:** Java 8 trở lên (khuyến nghị Java 17 LTS)
*   **IDE:** IntelliJ IDEA Community Edition hoặc VS Code với Extension Pack for Java
*   **Project structure:** Tạo project mới, package: `com.javazero.lab01`

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab01/
    ├── src/
    │   └── com/
    │       └── javazero/
    │           └── lab01/
    │               ├── DataTypesDemo.java
    │               └── OperatorsDemo.java
    └── out/ (tự động tạo bởi IDE)
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Tổng quan 8 kiểu dữ liệu nguyên thủy (Primitive Data Types)

*   **Hội ý:**

*   **[Anh Khánh]:** "Java có 8 kiểu dữ liệu nguyên thủy, chia thành 4 nhóm: số nguyên, số thập phân, ký tự, và logic."

*   **[Anh Vương (Performance)]:** "Anh em lưu ý này: Primitive types được lưu trực tiếp trên Stack Memory, còn wrapper classes (Object) được lưu trên Heap. Đây là khác biệt lớn về performance."

*   **[Em Hải (Clean Code)]:** "Và nhớ quy tắc đặt tên: kiểu nguyên thủy viết thường, wrapper classes viết hoa chữ cái đầu. Int vs Integer, boolean vs Boolean."

*   **[Anh Khánh]:** "Hùng, em nhìn vào bảng này và cho anh biết kiểu nào dùng cho số nguyên?"

*   **[Hùng (Intern)]:** "Dạ... byte, short, int, long ạ?"

*   **[Anh Khánh]:** "Đúng rồi! Còn ký tự thì sao?"

*   **[Hùng (Intern)]:** "Dạ char ạ?"

*   **[Anh Khánh]:** "Tuyệt vời. Còn số thập phân?"

*   **[Hùng (Intern)]:** "Dạ float và double ạ?"

*   **[Anh Khánh]:** "Chính xác. Còn cuối cùng là..."

*   **[Nam (Intern)]:** "Dạ boolean! Cái này em biết, true hoặc false!"

*   **[Anh Khánh]:** "Tốt lắm Nam. Giờ mình đi vào chi tiết từng kiểu."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô (Senior)]:** "Hùng, em tóm lại cho anh nghe: Java có mấy nhóm kiểu nguyên thủy, và mỗi nhóm có kiểu nào?"

*   **[Hùng (Intern)]:** "Dạ có 4 nhóm: Số nguyên (byte, short, int, long), số thập phân (float, double), ký tự (char), và logic (boolean)."

*   **[Anh Đô]:** "Chuẩn! Nam, em hỏi em câu này: byte và int khác nhau ở điểm nào quan trọng nhất?"

*   **[Nam (Intern)]:** "Dạ... kích thước? byte = 8 bit, int = 32 bit?"

*   **[Anh Đô]:** "Đúng rồi! Việt, em nghĩ tại sao byte ít được dùng trong thực tế dù nó tiết kiệm memory hơn?"

*   **[Việt (Intern)]:** "Dạ vì máy tính nó xử lý 32-bit hoặc 64-bit một lần, nên byte cũng phải convert thành int để tính toán, thành ra không tiết kiệm được gì anh?"

*   **[Anh Đô]:** "Hay! Em hiểu nhanh đấy. Cường, còn câu hỏi cuối: boolean dùng bao nhiêu bit?"

*   **[Cường (Intern)]:** "Dạ... em nghĩ là 1 bit, nhưng trong Java thực tế nó là 1 byte vì JVM không xử lý bit riêng lẻ."

*   **[Anh Đô]:** "Chuẩn! Rồi, mình đi vào từng chi tiết."

---

*   **Thực hiện:**

```java
// File: DataTypesDemo.java
// Package: com.javazero.lab01

public class DataTypesDemo {
    public static void main(String[] args) {
        // ========== NHÓM 1: SỐ NGUYÊN (Integer Types) ==========
        
        // byte: 8-bit, range: -128 to 127
        byte byteMin = -128;
        byte byteMax = 127;
        System.out.println("Byte range: " + byteMin + " to " + byteMax);
        
        // short: 16-bit, range: -32,768 to 32,767
        short shortMin = -32768;
        short shortMax = 32767;
        System.out.println("Short range: " + shortMin + " to " + shortMax);
        
        // int: 32-bit, range: -2,147,483,648 to 2,147,483,647
        int intMin = -2147483648;
        int intMax = 2147483647;
        System.out.println("Int range: " + intMin + " to " + intMax);
        
        // long: 64-bit, range: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
        long longValue = 9223372036854775807L; // Phải thêm 'L' ở cuối
        System.out.println("Long value: " + longValue);
        
        // ========== NHÓM 2: SỐ THẬP PHÂN (Floating-Point Types) ==========
        
        // float: 32-bit IEEE 754
        float floatValue = 3.14159f; // Phải thêm 'f' hoặc 'F'
        System.out.println("Float: " + floatValue);
        
        // double: 64-bit IEEE 754 (mặc định cho số thập phân)
        double doubleValue = 3.14159265358979;
        System.out.println("Double: " + doubleValue);
        
        // ========== NHÓM 3: KÝ TỰ (Character Type) ==========
        
        // char: 16-bit Unicode, range: '\u0000' to '\uffff' (0 to 65,535)
        char charA = 'A';
        char charUnicode = '\u0041'; // 'A' in Unicode
        char charAscii = 65; // 'A' in ASCII
        System.out.println("Char 'A': " + charA);
        System.out.println("Char Unicode \\u0041: " + charUnicode);
        System.out.println("Char ASCII 65: " + charAscii);
        
        // ========== NHÓM 4: LOGIC (Boolean Type) ==========
        
        // boolean: true hoặc false
        boolean isJavaFun = true;
        boolean isFishTasty = false;
        System.out.println("Is Java fun? " + isJavaFun);
        System.out.println("Is fish tasty? " + isFishTasty);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/DataTypesDemo.java
// java com.javazero.lab01.DataTypesDemo

// Output:
// Byte range: -128 to 127
// Short range: -32768 to 32767
// Int range: -2147483648 to 2147483647
// Long value: 9223372036854775807
// Float: 3.14159
// Double: 3.14159265358979
// Char 'A': A
// Char Unicode \u0041: A
// Char ASCII 65: A
// Is Java fun? true
// Is fish tasty? false
```

---

*   **Phân tích Output:**

*   **[Anh Khánh]:** "Anh em nhìn output và phân tích với anh nhé."

*   **[Hùng (Intern)]:** "Dạ em thấy byte chỉ từ -128 đến 127, ngắn quá. Sao không cho âm hoặc dương thôi mà phải chia đều vậy anh?"

*   **[Anh Đô (Senior)]:** "Câu hỏi xuất sắc! Lý do nằm ở cách máy tính lưu số âm - dùng 'Two's Complement'. Với n bit, ta có 2^n giá trị. Chia đều thành phần âm và dương, cộng thêm số 0. Nên byte: -2^7 đến 2^7-1 = -128 đến 127."

*   **[Nam (Intern)]:** "Dạ em hơi hoang mang. Tại sao lại phức tạp vậy anh? Sao không lưu từ 0 đến 255 rồi quy ước 128-255 là số âm?"

*   **[Anh Vương (Performance)]:** "Nam hỏi hay đấy. Lý do là performance! Two's Complement cho phép CPU tính toán số âm bằng cùng mạch cộng/trừ với số dương. Không cần mạch riêng cho số âm, tốc độ nhanh hơn."

*   **[Em Hải (Clean Code)]:** "Thêm một điểm nữa: Với hai số bất kỳ, so sánh lớn hơn/nhỏ hơn với Two's Complement cũng nhanh hơn. CPU chỉ cần một lệnh so sánh."

*   **[Anh Khánh]:** "Hùng, em tóm lại cho anh: Tại sao byte chỉ -128 đến 127?"

*   **[Hùng (Intern)]:** "Dạ vì 8 bit có 256 giá trị (2^8). Chia đều cho số âm (-128) và số dương (+127), cộng số 0. Hai's Complement giúp tính toán nhanh hơn."

*   **[Anh Khánh]:** "Tuyệt vời! Nam còn thắc mắc gì không?"

*   **[Nam (Intern)]:** "Dạ char là 16-bit mà không âm, trong khi short là 16-bit có âm. Sao lạ vậy anh?"

*   **[Anh Đô]:** "Char trong Java lưu Unicode, nên không cần số âm - nó chỉ đại diện cho ký tự. Còn short thì dùng cho tính toán số học, nên cần số âm."

---

### BƯỚC 2: Chi tiết về kiểu int và overflow

*   **Hội ý:**

*   **[Anh Khánh]:** "Giờ mình đi sâu vào int, kiểu dữ liệu được dùng nhiều nhất."

*   **[Anh Vương (Performance)]:** "Int là kiểu mặc định cho số nguyên trong Java. Khi em viết `byte x = 5;`, thực ra 5 là int, JVM phải implicit cast xuống byte. Nên khai báo `int x = 5;` là tối ưu nhất."

*   **[Em Hải (Clean Code)]:** "Thêm quy tắc nữa: Luôn dùng int trừ khi có lý do cụ thể để dùng byte/short/long. Code sẽ nhất quán, dễ đọc hơn."

*   **[Anh Khánh]:** "Việt, em hay dùng gì khi cần số rất lớn?"

*   **[Việt (Intern)]:** "Dạ em hay dùng int, nhưng khi vượt quá 2 tỷ thì Java nó báo lỗi. Phải đổi sang long, nhưng quên cái 'L' ở cuối."

*   **[Anh Đô]:** "Đó là lỗi phổ biến. Hùng, em thử tưởng tượng: intMax = 2147483647, cộng thêm 1 thì sao?"

*   **[Hùng (Intern)]:** "Dạ... 2147483648?"

*   **[Anh Đô]:** "Không! Em chạy thử code này nhé."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Hùng, trước khi chạy code, em đoán xem điều gì xảy ra khi intMax + 1?"

*   **[Hùng (Intern)]:** "Dạ em đoán nó sẽ thành 2147483648 anh."

*   **[Anh Đô]:** "Sai rồi! Chạy thử đi, Nam và Cường quan sát kỹ nhé."

*   **[Nam (Intern)]:** "Dạ em run đây..."

---

*   **Thực hiện - OVERFLOW DEMO:**

```java
// File: OverflowDemo.java
// Package: com.javazero.lab01

public class OverflowDemo {
    public static void main(String[] args) {
        System.out.println("=== DEMO INTEGER OVERFLOW ===");
        
        int intMax = 2147483647;
        System.out.println("intMax = " + intMax);
        
        int overflow = intMax + 1;
        System.out.println("intMax + 1 = " + overflow);
        
        // Giải thích: Số dương lớn nhất + 1 = số âm nhỏ nhất (wrap around)
        System.out.println("Lý do: Two's Complement overflow");
        System.out.println("Giá trị thực: -2147483648 (Integer.MIN_VALUE)");
        
        System.out.println("\n=== DEMO UNDERFLOW ===");
        int intMin = -2147483648;
        System.out.println("intMin = " + intMin);
        
        int underflow = intMin - 1;
        System.out.println("intMin - 1 = " + underflow);
        System.out.println("Giá trị thực: 2147483647 (Integer.MAX_VALUE)");
        
        // Thử với byte để thấy rõ hơn
        System.out.println("\n=== DEMO VỚI BYTE ===");
        byte byteMax = 127;
        byte byteOverflow = (byte) (byteMax + 1);
        System.out.println("byteMax = 127, +1 = " + byteOverflow);
        
        byte byteMin = -128;
        byte byteUnderflow = (byte) (byteMin - 1);
        System.out.println("byteMin = -128, -1 = " + byteUnderflow);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/OverflowDemo.java
// java com.javazero.lab01.OverflowDemo

// Output:
// === DEMO INTEGER OVERFLOW ===
// intMax = 2147483647
// intMax + 1 = -2147483648
// Lý do: Two's Complement overflow
// Giá trị thực: -2147483648 (Integer.MIN_VALUE)
// 
// === DEMO UNDERFLOW ===
// intMin = -2147483648
// intMin - 1 = 2147483647
// Giá trị thực: 2147483647 (Integer.MAX_VALUE)
// 
// === DEMO VỚI BYTE ===
// byteMax = 127, +1 = -128
// byteMin = -128, -1 = 127
```

---

*   **Phân tích Output - TRIPLE CHECK:**

*   **[Nam (Intern)]:** "ANH ƠI! Sao 2147483647 + 1 lại thành -2147483648 vậy?!!! Em hoảng quá!"

*   **[Anh Khánh]:** "Bình tĩnh Nam, đây gọi là overflow, không phải lỗi. JVM không ném exception cho overflow."

*   **[Việt (Intern)]:** "Chờ đã... em đọc lại output. intMin - 1 = 2147483647? Tức là nó quay vòng (wrap around)?"

*   **[Anh Vương (Performance)]:** "Đúng rồi Việt! Đây là wrap-around behavior của Two's Complement. CPU thực hiện phép cộng 32-bit, bit cao nhất bị overflow và bị bỏ qua."

*   **[Em Hải (Clean Code)]:** "Đây là lý do tại sao luôn phải validate input! Nếu user nhập số lớn hơn Integer.MAX_VALUE mà không check, chương trình sẽ cho kết quả sai mà không báo lỗi."

*   **[Anh Đô]:** "Hùng, em tóm tắt lại cho anh: Overflow là gì và xảy ra khi nào?"

*   **[Hùng (Intern)]:** "Dạ Overflow là khi giá trị vượt quá giới hạn max của kiểu dữ liệu. Khi đó nó quay về giá trị min. Còn Underflow là khi nhỏ hơn giá trị min thì quay về max."

*   **[Anh Đô]:** "Chuẩn! Cường, em có biết cách phòng tránh overflow không?"

*   **[Cường (Intern)]:** "Dạ dùng long thay vì int, hoặc kiểm tra trước khi cộng?"

*   **[Anh Đô]:** "Đúng! Và Java có Math.addExact() sẽ ném exception nếu overflow. Cách này an toàn hơn."

---

### BƯỚC 3: Chi tiết về kiểu char và Unicode

*   **Hội ý:**

*   **[Anh Khánh]:** "Giờ mình sang kiểu char - kiểu ký tự. Nhiều người nghĩ char = 1 ký tự ASCII, nhưng thực ra char trong Java là 16-bit Unicode."

*   **[Hùng (Intern)]:** "Dạ em thắc mắc: char có phải là String không anh? Vì char lưu ký tự, String cũng lưu ký tự."

*   **[Anh Đô]:** "Khác hoàn toàn! Char là primitive (1 ký tự), String là Object (nhiều ký tự). So sánh này giống như hỏi 'cái thùng' khác gì 'cả kho hàng'."

*   **[Em Hải (Clean Code)]:** "Thêm điểm: Char dùng single quotes `'A'`, String dùng double quotes `"A"`. Quên dấu này là lỗi syntax ngay."

*   **[Anh Vương (Performance)]:** "Char trong Java là UTF-16, hỗ trợ tiếng Việt, tiếng Trung, tiếng Nhật... Tất cả các ngôn ngữ trên thế giới!"

*   **[Nam (Intern)]:** "Dạ tuyệt vời! Vậy em có thể lưu tiếng Việt có dấu như 'ấ', 'ầ', 'ự'?"

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Nam, em thử lưu ký tự 'ấ' xem?"

*   **[Nam (Intern)]:** "Dạ... char c = 'ấ'; ?"

*   **[Anh Đô]:** "Chạy thử đi."

---

*   **Thực hiện - CHAR UNICODE DEMO:**

```java
// File: CharDemo.java
// Package: com.javazero.lab01

public class CharDemo {
    public static void main(String[] args) {
        System.out.println("=== DEMO CHAR VÀ UNICODE ===");
        
        // Char với ký tự đơn giản
        char letterA = 'A';
        char letterZ = 'Z';
        System.out.println("letterA = " + letterA);
        System.out.println("letterZ = " + letterZ);
        
        // Char với tiếng Việt
        char vietnameseA = 'ấ'; // tiếng Việt có dấu
        char vietnameseE = 'ê';
        char vietnameseO = 'ố';
        System.out.println("vietnameseA = " + vietnameseA);
        System.out.println("vietnameseE = " + vietnameseE);
        System.out.println("vietnameseO = " + vietnameseO);
        
        // Char với ký tự đặc biệt
        char newLine = '\n';
        char tab = '\t';
        char singleQuote = '\'';
        char backslash = '\\';
        System.out.println("Newline: A" + newLine + "B");
        System.out.println("Tab: A" + tab + "B");
        System.out.println("Single quote: " + singleQuote);
        System.out.println("Backslash: " + backslash);
        
        // Char với Unicode escape
        char unicodeA = '\u0041'; // 'A'
        char unicodeHeart = '\u2665'; // ♥
        char unicodeInfinity = '\u221E'; // ∞
        System.out.println("Unicode \\u0041 = " + unicodeA);
        System.out.println("Unicode \\u2665 = " + unicodeHeart);
        System.out.println("Unicode \\u221E = " + unicodeInfinity);
        
        // Char với số (ASCII/Unicode code)
        char asciiA = 65;
        char asciiB = 66;
        System.out.println("ASCII 65 = " + asciiA);
        System.out.println("ASCII 66 = " + asciiB);
        
        // Phép toán với char (char là số!)
        char c1 = 'A';
        char c2 = (char) (c1 + 1); // 'A' + 1 = 65 + 1 = 66 = 'B'
        System.out.println("'A' + 1 = " + c2);
        
        // Lỗi thường gặp: dùng double quotes cho char
        // char wrong = "A"; // COMPILE ERROR!
        // System.out.println(wrong);
        
        System.out.println("\n=== MINH HỌA: CHAR LÀ SỐ ===");
        System.out.println("char 'A' = " + (int) letterA);
        System.out.println("char 'Z' = " + (int) letterZ);
        System.out.println("char 'a' = " + (int) 'a');
        System.out.println("char 'z' = " + (int) 'z');
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/CharDemo.java
// java com.javazero.lab01.CharDemo

// Output:
// === DEMO CHAR VÀ UNICODE ===
// letterA = A
// letterZ = Z
// vietnameseA = ấ
// vietnameseE = ê
// vietnameseO = ố
// Newline: A
// B
// Tab: A    B
// Single quote: '
// Backslash: \
// Unicode \u0041 = A
// Unicode \u2665 = ♥
// Unicode \u221E = ∞
// ASCII 65 = A
// ASCII 66 = B
// 'A' + 1 = B
// 
// === MINH HỌA: CHAR LÀ SỐ ===
// char 'A' = 65
// char 'Z' = 90
// char 'a' = 97
// char 'z' = 122
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Ơ! Sao 'A' + 1 lại thành 'B' vậy anh? Em tưởng char là ký tự, sao lại cộng được?"

*   **[Anh Đô]:** "Việt hỏi rất hay! Char trong Java thực chất là số nguyên 16-bit không dấu. Khi em viết 'A', JVM hiểu là số 65. Nên 'A' + 1 = 65 + 1 = 66 = 'B'."

*   **[Hùng (Intern)]:** "A ha! Em hiểu rồi! Char cũng là số, nhưng không dấu (unsigned), nên từ 0 đến 65535."

*   **[Anh Vương (Performance)]:** "Đúng rồi! Đây là lý do char có thể dùng cho tính toán số học, nhưng ít khi làm vậy trong thực tế vì dễ gây confusion."

*   **[Nam (Intern)]:** "Dạ em thấy hay là Unicode escape \\u0041. Cái này viết code mà không cần keyboard có chữ A được."

*   **[Em Hải (Clean Code)]:** "Đúng! Unicode escape hữu ích khi cần ký tự đặc biệt hoặc khi làm việc với legacy systems. Nhưng trong code thường ngày, dùng trực tiếp ký tự dễ đọc hơn."

*   **[Anh Khánh]:** "Hùng, em tóm tắt: Char trong Java là gì và khác gì với String?"

*   **[Hùng (Intern)]:** "Dạ char là primitive 16-bit lưu 1 ký tự Unicode, dùng single quotes. String là Object lưu nhiều ký tự, dùng double quotes."

*   **[Anh Khánh]:** "Chuẩn! Còn câu hỏi cuối: 'A' + 1 = gì?"

*   **[Hùng (Intern)]:** "Dạ 66, tức là 'B'!"

---

### BƯỚC 4: Kiểu boolean và logic

*   **Hội ý:**

*   **[Anh Khánh]:** "Boolean - kiểu đơn giản nhất nhưng cũng dễ hiểu sai nhất."

*   **[Anh Vương (Performance)]:** "Boolean trong Java chỉ có 2 giá trị: true hoặc false. Không có '1', '0', 'yes', 'no' hay null như một số ngôn ngữ khác."

*   **[Em Hải (Clean Code)]:** "Tên biến boolean nên bắt đầu bằng is, has, can, should... để đọc là hiểu ngay. Ví dụ: isValid, hasError, canLogin."

*   **[Hùng (Intern)]:** "Dạ sao không đặt là valid thôi, phải thêm is làm gì anh?"

*   **[Anh Đô]:** "Hỏi hay! Vì khi đọc code: `if (isValid)` rất tự nhiên, còn `if (valid)` nghe hơi thiếu. Đây là convention của Java."

*   **[Việt (Intern)]:** "Em hay thấy `if (flag)` trên StackOverflow, có sao không anh?"

*   **[Em Hải]:** "Flag là bad practice! 'Flag' không nói lên ý nghĩa gì. Đặt tên như isProcessed, isCompleted, hasData..."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Việt, em thử viết code với boolean và show output?"

*   **[Việt (Intern)]:** "Dạ được!"

---

*   **Thực hiện - BOOLEAN DEMO:**

```java
// File: BooleanDemo.java
// Package: com.javazero.lab01

public class BooleanDemo {
    public static void main(String[] args) {
        System.out.println("=== DEMO BOOLEAN ===");
        
        // Khai báo boolean đúng cách
        boolean isJavaFun = true;
        boolean isFishTasty = false;
        boolean isSkyGreen = false;
        boolean isGrassBlue = false;
        
        System.out.println("Is Java fun? " + isJavaFun);
        System.out.println("Is fish tasty? " + isFishTasty);
        System.out.println("Is sky green? " + isSkyGreen);
        System.out.println("Is grass blue? " + isGrassBlue);
        
        // Boolean từ so sánh
        int myAge = 25;
        int votingAge = 18;
        boolean canVote = myAge >= votingAge;
        System.out.println("\nCan I vote? " + canVote);
        
        // Boolean từ equals
        String name1 = new String("John");
        String name2 = new String("John");
        boolean isEqual = name1 == name2; // So sánh tham chiếu
        boolean isEqualContent = name1.equals(name2); // So sánh nội dung
        System.out.println("name1 == name2: " + isEqual);
        System.out.println("name1.equals(name2): " + isEqualContent);
        
        // Boolean expressions
        int x = 10;
        int y = 20;
        boolean greater = x > y;
        boolean less = x < y;
        boolean equal = x == y;
        boolean notEqual = x != y;
        boolean greaterOrEqual = x >= y;
        boolean lessOrEqual = x <= y;
        
        System.out.println("\n=== SO SÁNH x=10, y=20 ===");
        System.out.println("x > y: " + greater);
        System.out.println("x < y: " + less);
        System.out.println("x == y: " + equal);
        System.out.println("x != y: " + notEqual);
        System.out.println("x >= y: " + greaterOrEqual);
        System.out.println("x <= y: " + lessOrEqual);
        
        // LỖI THƯỜNG GẶP
        System.out.println("\n=== LỖI THƯỜNG GẶP ===");
        // int z = 1;
        // if (z) { } // COMPILE ERROR: incompatible types
        // if (z = 2) { } // COMPILE ERROR thông minh! 
        //                  // Java không cho gán trong if
        
        boolean b1 = true;
        boolean b2 = false;
        // boolean b3 = "true"; // COMPILE ERROR: String != boolean
        
        System.out.println("Các giá trị boolean hợp lệ: true, false");
        System.out.println("int không thể dùng trong if: if (1)");
        System.out.println("String không thể dùng trong if: if (\"true\")");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/BooleanDemo.java
// java com.javazero.lab01.BooleanDemo

// Output:
// === DEMO BOOLEAN ===
// Is Java fun? true
// Is fish tasty? false
// Is sky green? false
// Is grass blue? false
// 
// Can I vote? true
// name1 == name2: false
// name1.equals(name2): true
// 
// === SO SÁNH x=10, y=20 ===
// x > y: false
// x < y: true
// x == y: false
// x != y: true
// x >= y: false
// x <= y: true
// 
// === LỖI THƯỜNG GẶP ===
// Các giá trị boolean hợp lệ: true, false
// int không thể dùng trong if: if (1)
// String không thể dùng trong if: if ("true")
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! Em thấy `name1 == name2` false mà `name1.equals(name2)` true. Sao lạ vậy?"

*   **[Anh Đô]:** "Nam hỏi câu quan trọng! Đây là khác biệt giữa 'so sánh tham chiếu' và 'so sánh nội dung'."

*   **[Hùng (Intern)]:** "Dạ sao khác được anh? Em tưởng == so sánh bằng?"

*   **[Anh Vương (Performance)]:** "Với primitives (int, char...), == so sánh giá trị. Với Objects (String...), == so sánh xem 2 biến có trỏ đến cùng một object trong memory không."

*   **[Em Hải (Clean Code)]:** "Đây là quy tắc VÀNG: Khi so sánh String, LUÔN dùng equals(). Đừng bao giờ dùng == cho String."

*   **[Cường (Intern)]:** "Dạ em hiểu rồi! `new String("John")` tạo 2 object khác nhau trong memory, nên == false. Nhưng nội dung đều là 'John', nên equals() true."

*   **[Anh Đô]:** "Chuẩn! Hùng, em tóm tắt lại: Tại sao String nên dùng equals() thay vì ==?"

*   **[Hùng (Intern)]:** "Dạ vì == so sánh địa chỉ memory, còn equals() so sánh nội dung. Với String thì mình cần so sánh nội dung."

*   **[Anh Khánh]:** "Tốt lắm! Nam còn thắc mắc gì không?"

*   **[Nam (Intern)]:** "Dạ còn chỗ `if (z = 2)` báo lỗi - sao Java biết em đang gán thay vì so sánh?"

*   **[Anh Đô]:** "Java compiler rất thông minh! Nó biết `if (condition)` cần boolean. Nếu em gán `z = 2` (int), compiler biết ngay là lỗi. Nhưng C/C++ thì khác - nó cho phép, gây ra bug!"

---

### BƯỚC 5: Toán tử số học (Arithmetic Operators)

*   **Hội ý:**

*   **[Anh Khánh]:** "Giờ mình học về toán tử. Đây là những thứ mình dùng hàng ngày: +, -, *, /, %."

*   **[Anh Vương (Performance)]:** "Anh em lưu ý: Phép chia `/` với integers sẽ bỏ phần dư. `5 / 2 = 2`, không phải 2.5!"

*   **[Hùng (Intern)]:** "Dạ em hay quên điều này! Em từng viết `int result = 5 / 2;` và tự hỏi sao ra 2."

*   **[Em Hải (Clean Code)]:** "Quy tắc: Muốn kết quả thập phân, ít nhất một operand phải là float hoặc double."

*   **[Việt (Intern)]:** "Còn % là gì anh? Em thấy hay dùng để kiểm tra số chẵn/lẻ."

*   **[Anh Đô]:** "% là modulo - lấy phần dư. 5 % 2 = 1, 10 % 2 = 0. Đúng rồi, hay dùng để kiểm tra chẵn lẻ."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Việt, em viết code demo phép chia và modulo đi?"

*   **[Việt (Intern)]:** "Dạ được!"

---

*   **Thực hiện - ARITHMETIC OPERATORS DEMO:**

```java
// File: ArithmeticDemo.java
// Package: com.javazero.lab01

public class ArithmeticDemo {
    public static void main(String[] args) {
        System.out.println("=== TOÁN TỬ SỐ HỌC ===");
        
        int a = 10;
        int b = 3;
        
        // Phép cộng
        int sum = a + b;
        System.out.println("a + b = " + sum);
        
        // Phép trừ
        int difference = a - b;
        System.out.println("a - b = " + difference);
        
        // Phép nhân
        int product = a * b;
        System.out.println("a * b = " + product);
        
        // Phép chia (integer division - bỏ phần dư)
        int quotient = a / b;
        System.out.println("a / b = " + quotient + " (bỏ phần dư)");
        
        // Phép modulo (lấy phần dư)
        int remainder = a % b;
        System.out.println("a % b = " + remainder + " (phần dư)");
        
        // Demo phép chia với số thập phân
        System.out.println("\n=== PHÉP CHIA VỚI SỐ THẬP PHÂN ===");
        double decimalResult = (double) a / b;
        System.out.println("(double) a / b = " + decimalResult);
        
        double decimalResult2 = a / (double) b;
        System.out.println("a / (double) b = " + decimalResult2);
        
        double decimalResult3 = (double) a / (double) b;
        System.out.println("(double) a / (double) b = " + decimalResult3);
        
        // Phép chia cho 0
        System.out.println("\n=== CHIA CHO 0 ===");
        // int divideByZero = 10 / 0; // ARITHMETIC EXCEPTION!
        // System.out.println(divideByZero);
        
        double doubleDivByZero = 10.0 / 0;
        System.out.println("10.0 / 0 = " + doubleDivByZero + " (Infinity)");
        
        double doubleModByZero = 10.0 % 0;
        System.out.println("10.0 % 0 = " + doubleModByZero + " (NaN)");
        
        // Toán tử tăng/giảm
        System.out.println("\n=== TOÁN TỬ TĂNG/GIẢM ===");
        int counter = 5;
        System.out.println("counter = " + counter);
        
        // Prefix: tăng rồi dùng
        System.out.println("++counter = " + (++counter));
        System.out.println("counter = " + counter);
        
        // Reset
        counter = 5;
        // Postfix: dùng rồi tăng
        System.out.println("counter++ = " + (counter++));
        System.out.println("counter = " + counter);
        
        // Tương tự với --
        int value = 10;
        System.out.println("\n--value = " + (--value));
        System.out.println("value-- = " + (value--));
        System.out.println("value = " + value);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/ArithmeticDemo.java
// java com.javazero.lab01.ArithmeticDemo

// Output:
// === TOÁN TỬ SỐ HỌC ===
// a + b = 13
// a - b = 7
// a * b = 30
// a / b = 3 (bỏ phần dư)
// a % b = 1 (phần dư)
// 
// === PHÉP CHIA VỚI SỐ THẬP PHÂN ===
// (double) a / b = 3.3333333333333335
// a / (double) b = 3.3333333333333335
// (double) a / (double) b = 3.3333333333333335
// 
// === CHIA CHO 0 ===
// 10.0 / 0 = Infinity
// 10.0 % 0 = NaN
// 
// === TOÁN TỬ TĂNG/GIẢM ===
// counter = 5
// ++counter = 6
// counter = 6
// counter++ = 5
// counter = 6
// --value = 9
// value-- = 9
// value = 8
```

---

*   **Phân tích Output - GIẢI THÍCH CHI TIẾT:**

*   **[Hùng (Intern)]:** "Anh ơi! Em thấy `a / b = 3` nhưng 10 / 3 = 3.333... Sao Java nó bỏ phần dư đi vậy?"

*   **[Anh Đô]:** "Hùng hỏi đúng rồi! Khi cả 2 operand đều là int, Java thực hiện 'integer division'. Nó chỉ lấy phần nguyên, bỏ phần thập phân. Muốn kết quả đúng, phải ép kiểu sang double."

*   **[Nam (Intern)]:** "Dạ còn chỗ `++counter` vs `counter++` khác nhau thế nào anh?"

*   **[Anh Vương (Performance)]:** "Cả hai đều tăng counter lên 1. Khác nhau ở thứ tự thực hiện. Prefix (++x): tăng trước, dùng sau. Postfix (x++): dùng trước, tăng sau."

*   **[Em Hải (Clean Code)]:** "Trong code thực tế, nên dùng riêng dòng cho ++ hoặc --. Đừng viết `result = array[i++]` vì dễ gây bug khó tìm."

*   **[Việt (Intern)]:** "Em thấy `10 / 0` bị exception, còn `10.0 / 0` lại ra Infinity. Sao kỳ vậy?"

*   **[Anh Đô]:** "Integer division by zero là MỘT TRONG NHỮNG LỖI NGUY HIỂM NHẤT trong Java, nên JVM ném ArithmeticException. Còn floating-point theo chuẩn IEEE 754, có giá trị Infinity và NaN."

*   **[Cường (Intern)]:** "Dạ vậy NaN là gì anh?"

*   **[Anh Đô]:** "NaN = Not a Number. Kết quả không phải là số. Ví dụ: 0 / 0, Infinity - Infinity, sqrt(-1)."

*   **[Anh Khánh]:** "Hùng, em tóm tắt lại: Phép chia int / int ra gì?"

*   **[Hùng (Intern)]:** "Dạ ra phần nguyên, bỏ phần dư. 10 / 3 = 3 chứ không phải 3.333..."

*   **[Anh Khánh]:** "Còn prefix vs postfix?"

*   **[Hùng (Intern)]:** "Dạ ++x tăng rồi dùng, x++ dùng rồi tăng."

*   **[Anh Khánh]:** "Tốt lắm! Việt còn câu hỏi gì không?"

*   **[Việt (Intern)]:** "Dạ còn % dùng khi nào anh?"

*   **[Anh Đô]:** "Modulo % có nhiều ứng dụng: Kiểm tra chẵn lẻ (n % 2 == 0), tạo số ngẫu nhiên trong range, xử lý vòng lặp, hash table..."

---

### BƯỚC 6: Toán tử so sánh và logic (Comparison & Logical Operators)

*   **Hội ý:**

*   **[Anh Khánh]:** "Toán tử so sánh và logic dùng để kết hợp nhiều điều kiện."

*   **[Anh Vương (Performance)]:** "Lưu ý: && và & khác nhau! && là short-circuit (dừng ngay nếu đã biết kết quả), còn & luôn kiểm tra cả hai."

*   **[Hùng (Intern)]:** "Dạ sao lại có 2 cái vậy anh? Một cái là đủ rồi mà."

*   **[Anh Đô]:** "Hùng hỏi hay! Short-circuit giúp code chạy nhanh hơn trong nhiều trường hợp, và tránh được lỗi. Ví dụ: `if (obj != null && obj.isValid())` - nếu obj null, sẽ không gọi obj.isValid() (tránh NullPointerException)."

*   **[Em Hải (Clean Code)]:** "Luôn dùng && thay vì &, || thay vì |, trừ khi có lý do cụ thể."

*   **[Nam (Intern)]:** "Dạ còn ^ (XOR)? Em ít thấy lắm."

*   **[Anh Vương]:** "XOR = exclusive OR. Chỉ true khi hai vế khác nhau. True ^ True = False, False ^ False = False. Dùng trong cryptography và một số thuật toán."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Nam, em viết code demo các toán tử so sánh và logic đi?"

*   **[Nam (Intern)]:** "Dạ em viết đây..."

---

*   **Thực hiện - COMPARISON AND_LOGIC DEMO:**

```java
// File: ComparisonDemo.java
// Package: com.javazero.lab01

public class ComparisonDemo {
    public static void main(String[] args) {
        System.out.println("=== TOÁN TỬ SO SÁNH ===");
        
        int x = 10;
        int y = 20;
        
        // So sánh bằng
        System.out.println("x == y: " + (x == y)); // false
        // So sánh khác
        System.out.println("x != y: " + (x != y)); // true
        // Lớn hơn
        System.out.println("x > y: " + (x > y)); // false
        // Nhỏ hơn
        System.out.println("x < y: " + (x < y)); // true
        // Lớn hơn hoặc bằng
        System.out.println("x >= y: " + (x >= y)); // false
        // Nhỏ hơn hoặc bằng
        System.out.println("x <= y: " + (x <= y)); // true
        
        System.out.println("\n=== TOÁN TỬ LOGIC ===");
        
        boolean p = true;
        boolean q = false;
        
        // AND: cả hai true mới true
        System.out.println("p && q: " + (p && q)); // false
        System.out.println("p & q: " + (p & q));   // false
        
        // OR: ít nhất một true là true
        System.out.println("p || q: " + (p || q)); // true
        System.out.println("p | q: " + (p | q));   // true
        
        // XOR: khác nhau mới true
        System.out.println("p ^ q: " + (p ^ q)); // true
        
        // NOT: đảo ngược
        System.out.println("!p: " + (!p)); // false
        System.out.println("!q: " + (!q)); // true
        
        System.out.println("\n=== SHORT-CIRCUIT VS NON-SHORT-CIRCUIT ===");
        
        // Demo short-circuit với &&
        int a = 5;
        boolean condition1 = (a > 10) && (a++ > 0);
        System.out.println("condition1 ((a>10) && (a++>0)): " + condition1);
        System.out.println("a sau khi check: " + a); // a = 5, vì a++ không được thực hiện
        
        // Reset a
        a = 5;
        // Demo với &
        boolean condition2 = (a > 10) & (a++ > 0);
        System.out.println("condition2 ((a>10) & (a++>0)): " + condition2);
        System.out.println("a sau khi check: " + a); // a = 6, vì a++ được thực hiện
        
        System.out.println("\n=== THỨ TỰ ƯU TIÊN (PRECEDENCE) ===");
        // Từ cao đến thấp: ! > && > || > (?:)
        int m = 5;
        int n = 10;
        boolean result = !true || false && false;
        System.out.println("!true || false && false = " + result);
        // Giải thích: !true (false) -> false || false && false
        // false && false (false) -> false || false = false
        
        // Dùng ngoặc để rõ ràng
        result = (!true) || (false && false);
        System.out.println("(!true) || (false && false) = " + result);
        
        System.out.println("\n=== ỨNG DỤNG THỰC TẾ ===");
        int age = 20;
        boolean hasLicense = true;
        
        // AND: cả hai điều kiện phải đúng
        boolean canDrive = (age >= 18) && hasLicense;
        System.out.println("Có thể lái xe: " + canDrive);
        
        // OR: ít nhất một điều kiện đúng
        boolean hasDiscount = (age < 12) || (age >= 65);
        System.out.println("Có giảm giá: " + hasDiscount);
        
        // NOT: đảo ngược điều kiện
        boolean isAdult = (age >= 18);
        boolean isMinor = !isAdult;
        System.out.println("Là người lớn: " + isAdult);
        System.out.println("Là trẻ em: " + isMinor);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/ComparisonDemo.java
// java com.javazero.lab01.ComparisonDemo

// Output:
// === TOÁN TỬ SO SÁNH ===
// x == y: false
// x != y: true
// x > y: false
// x = 10
// y = 20
// === TOÁN TỬ LOGIC ===
// p && q: false
// p & q: false
// p || q: true
// p | q: true
// p ^ q: true
// !p: false
// !q: true
// 
// === SHORT-CIRCUIT VS NON-SHORT-CIRCUIT ===
// condition1 ((a>10) && (a++>0)): false
// a sau khi check: 5
// condition2 ((a>10) & (a++>0)): false
// a sau khi check: 6
// 
// === THỨ TỰ ƯU TIÊN (PRECEDENCE) ===
// !true || false && false = false
// (!true) || (false && false) = false
// 
// === ỨNG DỤNG THỰC TẾ ===
// Có thể lái xe: true
// Có giảm giá: false
// Là người lớn: true
// Là trẻ em: false
```

---

*   **Phân tích Output - GIẢI THÍCH NGHE HIỂU:**

*   **[Cường (Intern)]:** "Anh ơi! Em thấy `a > 10 && a++ > 0` cho a=5, a vẫn là 5. Còn `a > 10 & a++ > 0` thì a thành 6. Sao lạ vậy?"

*   **[Anh Đô]:** "Cường phát hiện hay! Đây là short-circuit behavior. Với `&&`: Nếu vế trái false, JVM biết kết quả cuối cùng là false, nên KHÔNG thực hiện vế phải. Với `&`: JVM thực hiện CẢ HAI vế."

*   **[Hùng (Intern)]:** "A ha! Nên dùng && để tránh thực hiện code không cần thiết."

*   **[Anh Vương (Performance)]:** "Đúng rồi! Đây là lý do && && || là short-circuit, & và | là không. Short-circuit giúp code nhanh hơn và an toàn hơn."

*   **[Nam (Intern)]:** "Dạ em hiểu rồi! && giúp tránh NullPointerException nữa."

*   **[Anh Đô]:** "Nam nhắc đúng điểm! Ví dụ: `if (name != null && name.length() > 0)`. Nếu name null, `name.length()` không được gọi. Còn `&` thì sẽ crash."

*   **[Em Hải (Clean Code)]:** "Đây là best practice: LUÔN đặt điều kiện có khả năng fail (null check) ở BÊN TRÁI trong &&. Để tránh NullPointerException."

*   **[Việt (Intern)]:** "Dạ còn thứ tự ưu tiên anh? `!p && q || r` thì tính sao?"

*   **[Anh Đô]:** "Thứ tự: ! (NOT) trước, rồi && (AND), rồi || (OR). Nên `!p && q || r` = `(!p && q) || r`. Nhưng nên dùng ngoặc cho rõ ràng."

*   **[Anh Khánh]:** "Hùng, em tóm tắt: && khác gì với &?"

*   **[Hùng (Intern)]:** "Dạ && là short-circuit: nếu vế trái false thì bỏ qua vế phải. Còn & thực hiện cả hai. && nhanh và an toàn hơn."

*   **[Anh Khánh]:** "Còn || vs |?"

*   **[Hùng (Intern)]:** "Dạ || là short-circuit: nếu vế trái true thì bỏ qua vế phải. | thực hiện cả hai."

---

### BƯỚC 7: Toán tử bitwise và bit shift

*   **Hội ý:**

*   **[Anh Khánh]:** "Đây là phần nâng cao hơn, ít dùng trong code thường ngày, nhưng quan trọng cho interview."

*   **[Anh Vương (Performance)]:** "Bitwise operations là các phép toán trên từng bit. Rất nhanh vì CPU hỗ trợ trực tiếp."

*   **[Hùng (Intern)]:** "Dạ em nghe nói `n << 2` = `n * 4`. Đúng không anh?"

*   **[Anh Đô]:** "Đúng! Shift left n bit = nhân với 2^n. Shift right n bit = chia cho 2^n (floor)."

*   **[Em Hải (Clean Code)]:** "Nhưng trong code thực tế, đừng viết `n << 2` thay vì `n * 4`. Người đọc code sẽ không hiểu!"

*   **[Việt (Intern)]:** "Vậy khi nào nên dùng bitwise anh?"

*   **[Anh Vương]:** "Dùng khi: 1) Làm việc với flags/permissions, 2) Tối ưu performance cực kỳ cao, 3) Thuật toán mã hóa/hashing, 4) Game programming."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Việt, em viết code demo bitwise và shift operations đi?"

*   **[Việt (Intern)]:** "Dạ em viết đây..."

---

*   **Thực hiện - BITWISE AND BITSHIFT DEMO:**

```java
// File: BitwiseDemo.java
// Package: com.javazero.lab01

public class BitwiseDemo {
    public static void main(String[] args) {
        System.out.println("=== TOÁN TỬ BITWISE ===");
        
        // Binary representation
        int a = 5;   // 0101 in binary
        int b = 3;   // 0011 in binary
        
        System.out.println("a = " + a + " = " + Integer.toBinaryString(a));
        System.out.println("b = " + b + " = " + Integer.toBinaryString(b));
        
        // AND: bit = 1 chỉ khi cả hai bit = 1
        int andResult = a & b; // 0101 & 0011 = 0001 = 1
        System.out.println("a & b = " + andResult + " = " + Integer.toBinaryString(andResult));
        
        // OR: bit = 1 khi ít nhất một bit = 1
        int orResult = a | b; // 0101 | 0011 = 0111 = 7
        System.out.println("a | b = " + orResult + " = " + Integer.toBinaryString(orResult));
        
        // XOR: bit = 1 khi hai bit khác nhau
        int xorResult = a ^ b; // 0101 ^ 0011 = 0110 = 6
        System.out.println("a ^ b = " + xorResult + " = " + Integer.toBinaryString(xorResult));
        
        // NOT: đảo bit (two's complement)
        int notResult = ~a; // ~0101 = ...1010 (với 32 bits)
        System.out.println("~a = " + notResult);
        System.out.println("~a (binary) = " + Integer.toBinaryString(notResult));
        
        System.out.println("\n=== TOÁN TỬ BIT SHIFT ===");
        
        int n = 10; // 1010 in binary
        System.out.println("n = " + n + " = " + Integer.toBinaryString(n));
        
        // Shift left: <<
        int shiftLeft = n << 2; // 1010 << 2 = 101000 = 40 = 10 * 4
        System.out.println("n << 2 = " + shiftLeft + " = " + Integer.toBinaryString(shiftLeft));
        System.out.println("Giải thích: 10 * 2^2 = 10 * 4 = 40");
        
        // Shift right (signed): >>
        int shiftRight = n >> 2; // 1010 >> 2 = 0010 = 2 = 10 / 4 (floor)
        System.out.println("n >> 2 = " + shiftRight + " = " + Integer.toBinaryString(shiftRight));
        System.out.println("Giải thích: 10 / 2^2 = 10 / 4 = 2 (floor)");
        
        // Shift right (unsigned): >>>
        int unsignedRight = -10 >>> 2; // Điền bit 0 từ trái
        System.out.println("-10 >>> 2 = " + unsignedRight);
        
        // Demo shift với số âm
        int negative = -5; // ...11111011 in binary (32 bits)
        System.out.println("\n=== SHIFT VỚI SỐ ÂM ===");
        System.out.println("negative = " + negative + " = " + Integer.toBinaryString(negative));
        System.out.println("negative << 2 = " + (negative << 2) + " = " + Integer.toBinaryString(negative << 2));
        System.out.println("negative >> 2 = " + (negative >> 2) + " = " + Integer.toBinaryString(negative >> 2));
        
        System.out.println("\n=== ỨNG DỤNG: PERMISSIONS FLAGS ===");
        // Ví dụ: Permission system với bit flags
        // READ = 1 (0001), WRITE = 2 (0010), EXECUTE = 4 (0100)
        final int READ = 1;     // 0001
        final int WRITE = 2;     // 0010
        final int EXECUTE = 4;   // 0100
        
        int userPermissions = READ | WRITE; // 0001 | 0011 = 0011 (READ + WRITE)
        System.out.println("User permissions: " + userPermissions);
        
        boolean canRead = (userPermissions & READ) != 0;
        boolean canWrite = (userPermissions & WRITE) != 0;
        boolean canExecute = (userPermissions & EXECUTE) != 0;
        
        System.out.println("Can read: " + canRead);
        System.out.println("Can write: " + canWrite);
        System.out.println("Can execute: " + canExecute);
        
        // Thêm quyền EXECUTE
        userPermissions = userPermissions | EXECUTE; // 0011 | 0100 = 0111
        System.out.println("\nAfter adding EXECUTE: " + userPermissions);
        canExecute = (userPermissions & EXECUTE) != 0;
        System.out.println("Can execute now: " + canExecute);
        
        // Xóa quyền WRITE
        userPermissions = userPermissions & ~WRITE; // 0111 & ~0010 = 0101
        System.out.println("\nAfter removing WRITE: " + userPermissions);
        canWrite = (userPermissions & WRITE) != 0;
        System.out.println("Can write now: " + canWrite);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/BitwiseDemo.java
// java com.javazero.lab01.BitwiseDemo

// Output:
// === TOÁN TỬ BITWISE ===
// a = 5 = 101
// b = 3 = 11
// a & b = 1 = 1
// a | b = 7 = 111
// a ^ b = 6 = 110
// ~a = -6
// ~a (binary) = 11111111111111111111111111111010
// 
// === TOÁN TỬ BIT SHIFT ===
// n = 10 = 1010
// n << 2 = 40 = 101000
// Giải thích: 10 * 2^2 = 10 * 4 = 10
// n >> 2 = 2 = 10
// Giải thích: 10 / 2^2 = 10 / 4 = 2 (floor)
// -10 >>> 2 = 1073741821
// 
// === SHIFT VỚI SỐ ÂM ===
// negative = -5 = 11111111111111111111111111111011
// negative << 2 = -20 = 11111111111111111111111111101100
// negative >> 2 = -2 = 11111111111111111111111111111110
// 
// === ỨNG DỤNG: PERMISSIONS FLAGS ===
// User permissions: 3
// Can read: true
// Can write: true
// Can execute: false
// 
// After adding EXECUTE: 7
// Can execute now: true
// 
// After removing WRITE: 5
// Can write now: false
```

---

*   **Phân tích Output - GIẢI THÍCH CHUYÊN SÂU:**

*   **[Hùng (Intern)]:** "Anh ơi! Sao `~5 = -6` vậy? Em tưởng ~ (NOT) đảo bit thì 5 (0101) thành 1010 = 10 chứ?"

*   **[Anh Đô]:** "Hùng hỏi câu này rất hay! Java dùng 'Two's Complement' cho số âm. Bit đầu tiên là sign bit (0 = dương, 1 = âm). Khi ~5 (0101), nó thành 1010. Đây là số âm, nên phải chuyển về dạng magnitude: invert bits rồi cộng 1."

*   **[Nam (Intern)]:** "Dạ em hoang mang. Anh có thể giải thích đơn giản hơn không?"

*   **[Anh Vương]**: "Được rồi. Quy tắc: ~x = -(x + 1). ~5 = -6, ~0 = -1, ~(-1) = 0. Đừng cố hiểu sâu, cứ nhớ quy tắc này."

*   **[Việt (Intern)]:** "Dạ còn `n << 2 = n * 4` đúng không ạ?"

*   **[Anh Đô]:** "Đúng với số dương. Nhưng với số âm thì phức tạp hơn. `n << 2` dịch các bit sang trái, thêm 0 bên phải. -5 << 2 = -20 (vì shift có thể overflow)."

*   **[Cường (Intern)]:** "Dạ em thấy phần permissions flags rất hay! Sao không dùng boolean array mà phải dùng bit flags?"

*   **[Anh Vương]**: "Câu hỏi tuyệt vời! Bit flags tiết kiệm memory: 1 bit cho mỗi quyền thay vì 1 byte cho boolean. Và có thể pack nhiều flags vào một int. Dùng trong Unix/Linux permissions (chmod), Java collections..."

*   **[Em Hải]**: "Nhưng trong code thường ngày, dùng Enum hoặc Set sẽ clean hơn. Bit flags chỉ dùng khi cần performance hoặc tương thích với hệ thống cũ."

*   **[Anh Khánh]:** "Hùng, em tóm tắt: << nghĩa là gì?"

*   **[Hùng (Intern)]:** "Dạ shift left: dịch bit sang trái, thêm 0 bên phải. Tương đương nhân 2^n."

*   **[Anh Khánh]:** "Còn >>?"

*   **[Hùng (Intern)]:** "Dạ shift right (có sign): dịch bit sang phải, giữ sign bit. Tương đương chia 2^n (floor)."

*   **[Anh Khánh]:** "Còn >>>?"

*   **[Hùng (Intern)]:** "Dạ shift right (unsigned): dịch bit sang phải, luôn thêm 0 bên trái. Dùng cho số âm để không giữ sign bit."

---

### BƯỚC 8: Toán tử gán (Assignment Operators)

*   **Hội ý:**

*   **[Anh Khánh]:** "Toán tử gán thì quen thuộc rồi: =, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=, >>>="

*   **[Em Hải (Clean Code)]:** "Quy tắc vàng: Dùng = cho gán đơn giản. Dùng +=, -= khi muốn thay đổi giá trị hiện tại."

*   **[Hùng (Intern)]:** "Dạ `a += b` khác gì `a = a + b` không anh?"

*   **[Anh Đô]:** "Về kết quả thì giống nhau. Nhưng `a += b` ngắn gọn hơn, và với String thì khác biệt lớn: `str += "text"` nối chuỗi, còn `str = str + "text"` cũng nối nhưng dài hơn."

*   **[Anh Vương (Performance)]:** "Với primitives, compiler optimize nên `a += b` và `a = a + b` có performance tương đương. Nhưng `a += b` ít code hơn, dễ đọc hơn."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Hùng, em viết code demo assignment operators đi?"

*   **[Hùng (Intern)]:** "Dạ được!"

---

*   **Thực hiện - ASSIGNMENT DEMO:**

```java
// File: AssignmentDemo.java
// Package: com.javazero.lab01

public class AssignmentDemo {
    public static void main(String[] args) {
        System.out.println("=== TOÁN TỬ GÁN ===");
        
        int a = 10;
        System.out.println("a = " + a);
        
        // += : cộng rồi gán
        a += 5; // a = a + 5 = 15
        System.out.println("a += 5 => a = " + a);
        
        // -= : trừ rồi gán
        a -= 3; // a = a - 3 = 12
        System.out.println("a -= 3 => a = " + a);
        
        // *= : nhân rồi gán
        a *= 2; // a = a * 2 = 24
        System.out.println("a *= 2 => a = " + a);
        
        // /= : chia rồi gán
        a /= 4; // a = a / 4 = 6
        System.out.println("a /= 4 => a = " + a);
        
        // %= : modulo rồi gán
        a %= 5; // a = a % 5 = 1
        System.out.println("a %= 5 => a = " + a);
        
        System.out.println("\n=== BITWISE ASSIGNMENT ===");
        int flags = 0b0001; // READ
        System.out.println("flags = " + flags + " = " + Integer.toBinaryString(flags));
        
        flags |= 0b0010; // ADD WRITE: flags = flags | 0b0010
        System.out.println("flags |= 0b0010 => " + flags + " = " + Integer.toBinaryString(flags));
        
        flags &= 0b1110; // REMOVE READ: flags = flags & ~0b0001
        System.out.println("flags &= 0b1110 => " + flags + " = " + Integer.toBinaryString(flags));
        
        flags ^= 0b0010; // TOGGLE WRITE: 0 -> 1, 1 -> 0
        System.out.println("flags ^= 0b0010 => " + flags + " = " + Integer.toBinaryString(flags));
        
        System.out.println("\n=== SHIFT ASSIGNMENT ===");
        int n = 10;
        System.out.println("n = " + n);
        
        n <<= 2; // n = n << 2 = 40
        System.out.println("n <<= 2 => n = " + n);
        
        n >>= 2; // n = n >> 2 = 10
        System.out.println("n >>= 2 => n = " + n);
        
        System.out.println("\n=== STRING CONCATENATION ===");
        String str = "Hello";
        str += " "; // str = str + " "
        str += "World"; // str = str + "World"
        System.out.println("str = " + str);
        
        // Lưu ý: String += làm việc nhưng không hiệu quả trong vòng lặp
        // Nên dùng StringBuilder thay vì String += trong vòng lặp
        
        System.out.println("\n=== COMPOUND ASSIGNMENT BENEFITS ===");
        // Ví dụ: x += y ngắn gọn hơn x = x + y
        int x = 10;
        double y = 3.14;
        x += y; // x = x + y = 13 (int + double = double, rồi cast về int)
        System.out.println("x += y (x=10, y=3.14) => x = " + x);
        
        // Reset
        x = 10;
        // x = x + y; // COMPILE ERROR: possible lossy conversion from double to int
        // Nhưng x += y lại OK vì compiler tự cast
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/AssignmentDemo.java
// java com.javazero.lab01.AssignmentDemo

// Output:
// === TOÁN TỬ GÁN ===
// a = 10
// a += 5 => a = 15
// a -= 3 => a = 12
// a *= 2 => a = 24
// a /= 4 => a = 6
// a %= 5 => a = 1
// 
// === BITWISE ASSIGNMENT ===
// flags = 1 = 1
// flags |= 0b0010 => 3 = 11
// flags &= 0b1110 => 2 = 10
// flags ^= 0b0010 => 0 = 0
// 
// === SHIFT ASSIGNMENT ===
// n = 10
// n <<= 2 => n = 40
// n >>= 2 => 10
// 
// === STRING CONCATENATION ===
// str = Hello World
// 
// === COMPOUND ASSIGNMENT BENEFITS ===
// x += y (x=10, y=3.14) => x = 10
// x = x + y; // COMPILE ERROR: possible lossy conversion from double to int
// Nhưng x += y lại OK vì compiler tự cast
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! Sao `x = x + y` báo lỗi còn `x += y` lại chạy được?"

*   **[Anh Đô]:** "Việt phát hiện hay! `x = x + y` với x=int, y=double: Java báo 'possible lossy conversion' vì double có thể chứa số lớn hơn int, có thể mất thông tin. Nhưng `x += y` compiler tự thêm cast: `x = (int)(x + y)`."

*   **[Nam (Intern)]:** "Dạ vậy dùng += thay vì + = có lợi hơn?"

*   **[Anh Vương]:** "Đúng! +=, -=, *=, /= tự động cast, nên an toàn hơn. Tránh được compile error và giữ code ngắn gọn."

*   **[Cường (Intern)]:** "Dạ còn phần string += em hiểu rồi, nhưng anh nói StringBuilder là gì?"

*   **[Anh Đô]:** "StringBuilder là class dùng để nối chuỗi hiệu quả hơn. Trong vòng lặp, `str += "..."` tạo ra nhiều object trung gian, chậm và tốn memory. StringBuilder tránh được điều này."

*   **[Em Hải]:** "Trong code thực tế, nếu chỉ nối 2-3 chuỗi, dùng += hoặc + là OK. Nhưng trong vòng lặp hoặc nối nhiều lần, dùng StringBuilder."

---

### BƯỚC 9: Toán tử điều kiện (Ternary Operator)

*   **Hội ý:**

*   **[Anh Khánh]:** "Toán tử điều kiện ?: là if-else rút gọn. Dùng khi muốn gán giá trị dựa trên điều kiện."

*   **[Em Hải (Clean Code)]:** "Quy tắc: Chỉ dùng ?: khi ngắn gọn và dễ đọc. Đừng lồng nhiều ?: vào nhau - code sẽ khó đọc như spaghetti."

*   **[Hùng (Intern)]:** "Dạ ví dụ `result = (x > 0) ? "Positive" : "Non-positive"` nghĩa là gì?"

*   **[Anh Đô]:** "Nếu x > 0 thì result = "Positive", ngược lại result = "Non-positive". ? là 'nếu thỏa mãn', : là 'ngược lại'."

---

*   **Thực hiện - TERNARY DEMO:**

```java
// File: TernaryDemo.java
// Package: com.javazero.lab01

public class TernaryDemo {
    public static void main(String[] args) {
        System.out.println("=== TOÁN TỬ ĐIỀU KIỆN (TERNARY) ===");
        
        // Cú pháp: condition ? valueIfTrue : valueIfFalse
        int x = 10;
        String result = (x > 0) ? "Positive" : "Non-positive";
        System.out.println("x = " + x + " => " + result);
        
        x = -5;
        result = (x > 0) ? "Positive" : "Non-positive";
        System.out.println("x = " + x + " => " + result);
        
        System.out.println("\n=== TERNARY TRONG GÁN ===");
        int age = 18;
        String category = (age < 13) ? "Child" : 
                         (age < 20) ? "Teenager" : 
                         (age < 65) ? "Adult" : "Senior";
        System.out.println("age = " + age + " => category = " + category);
        
        System.out.println("\n=== TERNARY THAY CHO IF-ELSE ĐƠN GIẢN ===");
        int a = 10;
        int b = 20;
        int max = (a > b) ? a : b;
        System.out.println("max(10, 20) = " + max);
        
        // Dùng với method call
        int[] numbers = {1, 2, 3};
        int length = (numbers != null) ? numbers.length : 0;
        System.out.println("Array length: " + length);
        
        System.out.println("\n=== LƯU Ý: TRÁNH LỒNG NHIỀU TERNARY ===");
        // BAD PRACTICE - khó đọc:
        // String category = (age < 13) ? "Child" : (age < 20) ? "Teenager" : (age < 65) ? "Adult" : "Senior";
        
        // GOOD PRACTICE - dùng if-else:
        String category2;
        if (age < 13) {
            category2 = "Child";
        } else if (age < 20) {
            category2 = "Teenager";
        } else if (age < 65) {
            category2 = "Adult";
        } else {
            category2 = "Senior";
        }
        System.out.println("Using if-else: " + category2);
        
        System.out.println("\n=== TERNARY VỚI SIDE EFFECTS ===");
        int value = 10;
        // CẢNH BÁO: ternary có thể gọi method có side effects
        // boolean test = (value > 0) ? isPositive() : isNegative();
        // Tránh gọi method có side effects trong ternary!
        
        // Tốt hơn:
        boolean isPositive;
        if (value > 0) {
            isPositive = true;
        } else {
            isPositive = false;
        }
        System.out.println("isPositive: " + isPositive);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/TernaryDemo.java
// java com.javazero.lab01.TernaryDemo

// Output:
// === TOÁN TỬ ĐIỀU KIỆN (TERNARY) ===
// x = 10 => Positive
// x = -5 => Non-positive
// 
// === TERNARY TRONG GÁN ===
// age = 18 => category = Adult
// 
// === TERNARY THAY CHO IF-ELSE ĐƠN GIẢN ===
// max(10, 20) = 20
// 
// Array length: 3
// 
// === LƯU Ý: TRÁNH LỒNG NHIỀU TERNARY ===
// Using if-else: Adult
// 
// === TERNARY VỚI SIDE EFFECTS ===
// isPositive: true
```

---

*   **Phân tích Output:**

*   **[Hùng (Intern)]:** "Dạ em hiểu rồi! Ternary là if-else rút gọn. Nhưng sao anh khuyên không lồng nhiều?"

*   **[Anh Đô]:** "Hùng hỏi đúng! Lồng nhiều ternary: `a ? b : c ? d : e ? f : g` rất khó đọc và dễ sai. Đọc code như đọc câu đố. Nên dùng if-else khi có nhiều điều kiện."

*   **[Em Hải]:** "Quy tắc: Ternary chỉ dùng cho gán đơn giản, 1 điều kiện. Khi cần kiểm tra nhiều điều kiện, dùng if-else."

*   **[Việt (Intern)]:** "Dạ còn chỗ side effects là gì anh?"

*   **[Anh Vương]:** "Side effects là khi method thay đổi state ngoài việc trả về giá trị. Ví dụ: `printMessage()` in ra console. Gọi method có side effects trong ternary có thể gây bug khó tìm vì thứ tự thực hiện không rõ ràng."

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ mình sẽ phá để học! Việt, Nam, Hùng - mỗi người chọn 1 lỗi để thử."

*   **[Việt (Intern)]:** "Em thử truyền số quá lớn vào byte xem?"

*   **[Nam (Intern)]:** "Em thử chia cho 0!"

*   **[Hùng (Intern)]:** "Em thử dùng == với String xem sao!"

---

*   **Case 1: Integer Overflow**

```java
// File: OverflowBugDemo.java
// Package: com.javazero.lab01

public class OverflowBugDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 1: INTEGER OVERFLOW BUG ===");
        
        // Bug: Tính toán vượt giới hạn int mà không biết
        int balance = 2147483647;
        System.out.println("Current balance: " + balance);
        
        int newBalance = balance + 1000;
        System.out.println("After adding 1000: " + newBalance);
        // KẾT QUẢ SAI! Nên là 2147484647 nhưng thành -2147473649
        
        // Fix: Dùng long
        long balanceLong = 2147483647L;
        long newBalanceLong = balanceLong + 1000;
        System.out.println("\nFix with long:");
        System.out.println("Current balance: " + balanceLong);
        System.out.println("After adding 1000: " + newBalanceLong);
        
        // Fix 2: Dùng Math.addExact() - throws exception khi overflow
        System.out.println("\nFix with Math.addExact():");
        try {
            int safeBalance = Math.addExact(balance, 1000);
            System.out.println("Safe balance: " + safeBalance);
        } catch (ArithmeticException e) {
            System.out.println("ERROR: Overflow detected! " + e.getMessage());
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/OverflowBugDemo.java
// java com.javazero.lab01.OverflowBugDemo

// Output (BUG):
// === CASE 1: INTEGER OVERFLOW BUG ===
// Current balance: 2147483647
// After adding 1000: -2147473649
// 
// Fix with long:
// Current balance: 2147483647
// After adding 1000: 2147484647
// 
// Fix with Math.addExact():
// ERROR: Overflow detected: integer overflow
```

---

*   **Case 2: Division by Zero**

```java
// File: DivisionByZeroDemo.java
// Package: com.javazero.lab01

public class DivisionByZeroDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 2: DIVISION BY ZERO ===");
        
        // Bug 1: Integer division by zero
        System.out.println("Bug 1: int / 0");
        try {
            int result = 10 / 0;
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("CAUGHT: " + e.getClass().getSimpleName() + " - " + e.getMessage());
            System.out.println("Reason: Integer division by zero is undefined");
        }
        
        // Bug 2: Floating-point division by zero (không exception)
        System.out.println("\nBug 2: double / 0");
        double doubleResult = 10.0 / 0;
        System.out.println("Result: " + doubleResult); // Infinity
        
        double negativeZero = -10.0 / 0;
        System.out.println("-10.0 / 0 = " + negativeZero); // -Infinity
        
        // Bug 3: 0.0 / 0.0 = NaN
        double nanResult = 0.0 / 0.0;
        System.out.println("0.0 / 0.0 = " + nanResult); // NaN
        
        // Fix: Luôn kiểm tra trước khi chia
        System.out.println("\nFix: Check before division");
        int numerator = 10;
        int denominator = 0;
        
        if (denominator != 0) {
            int safeResult = numerator / denominator;
            System.out.println("Safe result: " + safeResult);
        } else {
            System.out.println("ERROR: Cannot divide by zero!");
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/DivisionByZeroDemo.java
// java com.javazero.lab01.DivisionByZeroDemo

// Output:
// === CASE 2: DIVISION BY ZERO ===
// Bug 1: int / 0
// CAUGHT: ArithmeticException - / by zero
// Reason: Integer division by zero is undefined
// 
// Bug 2: double / 0
// Result: Infinity
// -10.0 / 0 = -Infinity
// 
// 0.0 / 0.0 = NaN
// 
// Fix: Check before division
// ERROR: Cannot divide by zero!
```

---

*   **Case 3: String Comparison with ==**

```java
// File: StringComparisonBugDemo.java
// Package: com.javazero.lab01

public class StringComparisonBugDemo {
    public static void main(String[] args) {
        System.out.println("=== CASE 3: STRING COMPARISON WITH == (BUG) ===");
        
        // Bug: Dùng == để so sánh String
        String str1 = new String("hello");
        String str2 = new String("hello");
        
        System.out.println("str1 = new String(\"hello\")");
        System.out.println("str2 = new String(\"hello\")");
        
        // SAI: So sánh tham chiếu
        System.out.println("str1 == str2: " + (str1 == str2)); // false
        
        // ĐÚNG: So sánh nội dung
        System.out.println("str1.equals(str2): " + str1.equals(str2)); // true
        
        // Bug phổ biến: String literals
        System.out.println("\nBug with literals:");
        String str3 = "hello";
        String str4 = "hello";
        String str5 = new String("hello");
        
        System.out.println("str3 = \"hello\"");
        System.out.println("str4 = \"hello\"");
        System.out.println("str5 = new String(\"hello\")");
        
        System.out.println("str3 == str4: " + (str3 == str4)); // true (string pool!)
        System.out.println("str3 == str5: " + (str3 == str5)); // false
        
        System.out.println("str3.equals(str5): " + str3.equals(str5)); // true
        
        // Fix: LUÔN dùng equals() cho String
        System.out.println("\nFix: Always use equals()");
        String input1 = "admin";
        String input2 = "Admin";
        
        boolean isMatch = input1.equals(input2); // false (case-sensitive)
        boolean isMatchIgnoreCase = input1.equalsIgnoreCase(input2); // true
        
        System.out.println("\"admin\".equals(\"Admin\"): " + isMatch);
        System.out.println("\"admin\".equalsIgnoreCase(\"Admin\"): " + isMatchIgnoreCase);
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/StringComparisonBugDemo.java
// java com.javazero.lab01.StringComparisonBugDemo

// Output:
// === CASE 3: STRING COMPARISON WITH == (BUG) ===
// str1 = new String("hello")
// str2 = new String("hello")
// str1 == str2: false
// str1.equals(str2): true
// 
// Bug with literals:
// str3 = "hello"
// str4 = "hello"
// str5 = new String("hello")
// str3 == str4: true (string pool!)
// str3 == str5: false
// 
// str3.equals(str5): true
// 
// Fix: Always use equals()
// "admin".equals("Admin"): false
// "admin".equalsIgnoreCase("Admin"): true
```

---

### The Panic - ĐỌC STACK TRACE

*   **[Anh Khánh]:** "Giờ mình học cách đọc stack trace. Nam, em run code này và mô tả lỗi."

```java
// File: StackTraceDemo.java
// Package: com.javazero.lab01

public class StackTraceDemo {
    public static void main(String[] args) {
        System.out.println("=== DEMO: ĐỌC STACK TRACE ===");
        
        // Gây lỗi cố ý
        int[] array = new int[5];
        System.out.println("Accessing index 10 in array of size 5...");
        int value = array[10]; // ArrayIndexOutOfBoundsException
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/StackTraceDemo.java
// java com.javazero.lab01.StackTraceDemo

// IDE Console (Output):
// Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 10
//         at StackTraceDemo.main(StackTraceDemo.java:8)
// 
```

*   **[Nam (Intern)]:** "Dạ em thấy lỗi `ArrayIndexOutOfBoundsException: 10`. Nhưng em không hiểu nên làm gì với thông báo này."

*   **[Anh Đô]:** "Nam hỏi rất hay! Stack trace có 3 phần quan trọng:"

*   **Phân tích Stack Trace:**
    1. **Exception type:** `java.lang.ArrayIndexOutOfBoundsException`
       - Đây là loại lỗi: truy cập index ngoài mảng
    2. **Error message:** `10`
       - Index gây lỗi: 10
    3. **Stack trace:** `at StackTraceDemo.main(StackTraceDemo.java:8)`
       - File: StackTraceDemo.java
       - Method: main
       - Dòng: 8

*   **[Hùng (Intern)]:** "Dạ vậy em biết lỗi ở dòng 8 trong file StackTraceDemo.java, index 10!"

*   **[Anh Vương]:** "Đúng rồi! Đây là kỹ năng quan trọng: Đọc stack trace để tìm lỗi nhanh. Đừng hoảng khi thấy nhiều dòng lỗi - dòng đầu tiên thường là nơi lỗi xảy ra."

---

### The Fix - SỬA LỖI

*   **Fix cho ArrayIndexOutOfBoundsException:**

```java
// File: FixArrayIndexDemo.java
// Package: com.javazero.lab01

public class FixArrayIndexDemo {
    public static void main(String[] args) {
        System.out.println("=== FIX: ArrayIndexOutOfBoundsException ===");
        
        int[] array = new int[5];
        System.out.println("Array size: " + array.length);
        
        // Fix: Kiểm tra index trước khi truy cập
        int indexToAccess = 10;
        
        if (indexToAccess >= 0 && indexToAccess < array.length) {
            int value = array[indexToAccess];
            System.out.println("Value at index " + indexToAccess + ": " + value);
        } else {
            System.out.println("ERROR: Index " + indexToAccess + " is out of bounds!");
            System.out.println("Valid range: 0 to " + (array.length - 1));
        }
        
        // Fix 2: Dùng try-catch
        System.out.println("\nFix with try-catch:");
        try {
            int value = array[10];
            System.out.println("Value: " + value);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("CAUGHT: Index out of bounds!");
            System.out.println("Exception: " + e.getClass().getSimpleName());
            System.out.println("Message: " + e.getMessage());
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab01/FixArrayIndexDemo.java
// java com.javazero.lab01.FixArrayIndexDemo

// Output:
// === FIX: ArrayIndexOutOfBoundsException ===
// Array size: 5
// ERROR: Index 10 is out of bounds!
// Valid range: 0 to 4
// 
// Fix with try-catch:
// CAUGHT: Index out of bounds!
// Exception: ArrayIndexOutOfBoundsException
// Message: 10
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: Java có 8 kiểu nguyên thủy: byte, short, int, long, float, double, char, boolean. Mỗi kiểu có range riêng."

*   **[Nam (Intern)]:** "Dạ em sợ Integer Overflow lắm! Nên dùng Math.addExact() hoặc long khi cần số lớn."

*   **[Việt (Intern)]:** "Dạ em học được là String phải dùng equals() chứ không được dùng ==. Và && là short-circuit, nhanh hơn &."

*   **[Cường (Intern)]:** "Dạ em học được: Bit shift << = nhân 2^n, >> = chia 2^n (floor). Dùng trong performance-critical code hoặc flags."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| 8 Primitive Data Types | ☐ | ☐ |
| int range (-2^31 to 2^31-1) | ☐ | ☐ |
| char = 16-bit Unicode | ☐ | ☐ |
| boolean chỉ có true/false | ☐ | ☐ |
| Integer Overflow | ☐ | ☐ |
| Division by zero (int vs double) | ☐ | ☐ |
| Arithmetic Operators (+, -, *, /, %) | ☐ | ☐ |
| ++x vs x++ | ☐ | ☐ |
| Comparison Operators (==, !=, >, <, >=, <=) | ☐ | ☐ |
| Logical Operators (&&, ||, !, &, \|) | ☐ | ☐ |
| Short-circuit behavior | ☐ | ☐ |
| Bitwise Operators (&, \|, ^, ~) | ☐ | ☐ |
| Bit Shift Operators (<<, >>, >>>) | ☐ | ☐ |
| Assignment Operators (+=, -=, etc.) | ☐ | ☐ |
| Ternary Operator (?:) | ☐ | ☐ |
| String comparison: equals() vs == | ☐ | ☐ |
| ArrayIndexOutOfBoundsException | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Viết chương trình tính tổng các số từ 1 đến 1000, kiểm tra xem có overflow không.
2.  Tạo 1 method kiểm tra số chẵn/lẻ dùng toán tử %.
3.  Viết chương trình chuyển đổi nhiệt độ từ Celsius sang Fahrenheit (dùng double).
4.  Tạo 1 program dùng bit flags để quản lý permissions (READ, WRITE, EXECUTE).
5.  Thử gây lỗi NullPointerException và đọc stack trace.

---

## 4. BÀI TẬP THỰC HÀNH (Practice Exercises)

### Bài tập 1: Viết chương trình tính toán đơn giản
**Yêu cầu:** Tạo chương trình Java để thực hiện các phép tính cơ bản với hai số nguyên. Hiển thị kết quả và giải thích từng bước.

```java
// File: CalculatorExercise.java
// Package: com.javazero.lab01.exercises

public class CalculatorExercise {
    public static void main(String[] args) {
        int a = 15;
        int b = 4;

        System.out.println("=== BÀI TẬP: TÍNH TOÁN CƠ BẢN ===");
        System.out.println("Cho a = " + a + ", b = " + b);
        System.out.println();

        // Các phép tính
        System.out.println("Cộng: " + a + " + " + b + " = " + (a + b));
        System.out.println("Trừ: " + a + " - " + b + " = " + (a - b));
        System.out.println("Nhân: " + a + " * " + b + " = " + (a * b));
        System.out.println("Chia: " + a + " / " + b + " = " + (a / b) + " (integer division)");
        System.out.println("Modulo: " + a + " % " + b + " = " + (a % b));

        // Kiểm tra chẵn lẻ
        System.out.println();
        System.out.println("=== KIỂM TRA CHẴN LẺ ===");
        System.out.println(a + " là số: " + (a % 2 == 0 ? "chẵn" : "lẻ"));
        System.out.println(b + " là số: " + (b % 2 == 0 ? "chẵn" : "lẻ"));
    }
}
```

**Output mẫu:**
```
=== BÀI TẬP: TÍNH TOÁN CƠ BẢN ===
Cho a = 15, b = 4

Cộng: 15 + 4 = 19
Trừ: 15 - 4 = 11
Nhân: 15 * 4 = 60
Chia: 15 / 4 = 3 (integer division)
Modulo: 15 % 4 = 3

=== KIỂM TRA CHẴN LẺ ===
15 là số: lẻ
4 là số: chẵn
```

### Bài tập 2: Viết chương trình so sánh và logic
**Yêu cầu:** Tạo chương trình nhập tuổi và kiểm tra điều kiện để xem có được vay tiền hay không.

```java
// File: LoanEligibility.java
// Package: com.javazero.lab01.exercises

public class LoanEligibility {
    public static void main(String[] args) {
        int age = 25;
        int income = 50000;
        boolean hasJob = true;

        System.out.println("=== BÀI TẬP: KIỂM TRA ĐIỀU KIỆN VAY TIỀN ===");
        System.out.println("Tuổi: " + age);
        System.out.println("Thu nhập: $" + income);
        System.out.println("Có việc làm: " + hasJob);
        System.out.println();

        // Điều kiện vay
        boolean ageValid = age >= 18 && age <= 65;
        boolean incomeValid = income >= 30000;
        boolean employmentValid = hasJob;

        System.out.println("=== KIỂM TRA TỪNG ĐIỀU KIỆN ===");
        System.out.println("Tuổi hợp lệ (18-65): " + ageValid);
        System.out.println("Thu nhập đủ (>=30000): " + incomeValid);
        System.out.println("Có việc làm: " + employmentValid);
        System.out.println();

        // Kết luận
        boolean approved = ageValid && incomeValid && employmentValid;
        System.out.println("=== KẾT LUẬN ===");
        System.out.println("Đủ điều kiện vay: " + (approved ? "ĐƯỢC DUYỆT" : "KHÔNG ĐƯỢC DUYỆT"));
    }
}
```

### Bài tập 3: Viết chương trình với bitwise operations
**Yêu cầu:** Tạo chương trình quản lý quyền truy cập sử dụng bit flags.

```java
// File: PermissionSystem.java
// Package: com.javazero.lab01.exercises

public class PermissionSystem {
    // Định nghĩa permissions bằng bit flags
    public static final int READ = 1;    // 0001
    public static final int WRITE = 2;    // 0010
    public static final int DELETE = 4;   // 0100
    public static final int EXECUTE = 8;  // 1000

    public static void main(String[] args) {
        System.out.println("=== BÀI TẬP: HỆ THỐNG QUYỀN TRUY CẬP ===");
        System.out.println();

        // Tạo permissions cho user
        int userPermissions = READ | WRITE;
        System.out.println("User permissions (READ | WRITE): " + userPermissions);
        System.out.println("Binary: " + Integer.toBinaryString(userPermissions));
        System.out.println();

        // Kiểm tra permissions
        System.out.println("=== KIỂM TRA QUYỀN ===");
        System.out.println("Có quyền đọc: " + hasPermission(userPermissions, READ));
        System.out.println("Có quyền ghi: " + hasPermission(userPermissions, WRITE));
        System.out.println("Có quyền xóa: " + hasPermission(userPermissions, DELETE));
        System.out.println("Có quyền thực thi: " + hasPermission(userPermissions, EXECUTE));
        System.out.println();

        // Thêm quyền DELETE
        userPermissions |= DELETE;
        System.out.println("Sau khi thêm DELETE: " + userPermissions);
        System.out.println("Có quyền xóa: " + hasPermission(userPermissions, DELETE));
        System.out.println();

        // Xóa quyền WRITE
        userPermissions &= ~WRITE;
        System.out.println("Sau khi xóa WRITE: " + userPermissions);
        System.out.println("Có quyền ghi: " + hasPermission(userPermissions, WRITE));
    }

    // Kiểm tra permission
    public static boolean hasPermission(int permissions, int permission) {
        return (permissions & permission) != 0;
    }
}
```

### Bài tập 4: Viết chương trình với char và Unicode
**Yêu cầu:** Tạo chương trình chuyển đổi chữ hoa/thường và hiển thị Unicode.

```java
// File: CharExercise.java
// Package: com.javazero.lab01.exercises

public class CharExercise {
    public static void main(String[] args) {
        System.out.println("=== BÀI TẬP: CHAR VÀ UNICODE ===");
        System.out.println();

        // Chữ hoa và chữ thường
        char uppercase = 'A';
        char lowercase = 'a';

        System.out.println("=== MÃ ASCII ===");
        System.out.println("'A' = " + (int)uppercase);
        System.out.println("'a' = " + (int)lowercase);
        System.out.println("'A' - 'a' = " + (uppercase - lowercase));
        System.out.println();

        // Chuyển đổi hoa thường
        System.out.println("=== CHUYỂN ĐỔI ===");
        char original = 'm';
        System.out.println("Chữ gốc: '" + original + "' = " + (int)original);

        // Chuyển thành hoa
        char upperCase = (char)(original - 32);
        System.out.println("Chuyển hoa: '" + upperCase + "' = " + (int)upperCase);

        // Chuyển thành thường
        char lowerCase = (char)(upperCase + 32);
        System.out.println("Chuyển thường: '" + lowerCase + "' = " + (int)lowerCase);
        System.out.println();

        // Unicode tiếng Việt
        System.out.println("=== TIẾNG VIỆT ===");
        char vietnamese[] = {'à', 'á', 'ạ', 'ả', 'ã', 'â', 'ầ', 'ấ', 'ậ', 'ẩ', 'ẫ'};

        System.out.println("Các ký tự tiếng Việt:");
        for (char c : vietnamese) {
            System.out.println("'" + c + "' = " + (int)c);
        }
    }
}
```

### Bài tập 5: Tìm lỗi trong code (Debug Challenge)
**Yêu cầu:** Tìm và sửa các lỗi trong đoạn code sau:

```java
// File: FindTheBugs.java
// Package: com.javazero.lab01.exercises

public class FindTheBugs {
    public static void main(String[] args) {
        System.out.println("=== CHALLENGE: TÌM LỖI ===");
        System.out.println();

        // Bug 1: Overflow
        int maxInt = 2147483647;
        // int overflow = maxInt + 1; // Bug: overflow!
        long safeMaxInt = maxInt + 1L; // Fix: dùng long

        System.out.println("Bug 1: Integer overflow");
        System.out.println("maxInt + 1 = " + safeMaxInt);
        System.out.println();

        // Bug 2: Division
        int a = 7;
        int b = 2;
        // int wrongResult = a / b; // Bug: integer division
        double correctResult = (double) a / b; // Fix: ép kiểu

        System.out.println("Bug 2: Integer division");
        System.out.println("7 / 2 = " + correctResult);
        System.out.println();

        // Bug 3: Char vs String
        // char single = \"A\"; // Bug: dùng double quotes
        char single = 'A'; // Fix: dùng single quotes

        System.out.println("Bug 3: Char vs String");
        System.out.println("Char đúng: " + single);
        System.out.println();

        // Bug 4: Comparison
        String s1 = new String("Hello");
        String s2 = new String("Hello");
        // if (s1 == s2) // Bug: so sánh tham chiếu
        if (s1.equals(s2)) // Fix: so sánh nội dung
            System.out.println("Bug 4: String comparison");
            System.out.println("s1.equals(s2) = true (nội dung bằng nhau)");
        System.out.println();

        System.out.println("=== TỔNG KẾT LỖI ===");
        System.out.println("1. Integer overflow: dùng long hoặc Math.addExact()");
        System.out.println("2. Integer division: ép kiểu sang double");
        System.out.println("3. Char: dùng single quotes");
        System.out.println("4. String comparison: dùng equals()");
    }
}
```

---

## 5. CHECKLIST KIẾN THỨC (Knowledge Checklist)

Sau khi hoàn thành Lab01, hãy đảm bảo bạn trả lời được các câu hỏi sau:

### Về Kiểu Dữ liệu Nguyên thủy (Primitive Data Types)

- [ ] Tôi có thể liệt kê 8 kiểu dữ liệu nguyên thủy và phân loại chúng không?
- [ ] Tôi hiểu sự khác biệt giữa primitive types và wrapper classes không?
- [ ] Tôi biết kích thước và phạm vi của từng kiểu không?
- [ ] Tôi hiểu tại sao char trong Java là 16-bit không?
- [ ] Tôi biết khi nào nên dùng int, long, float, double không?

### Về Overflow và Underflow

- [ ] Tôi hiểu overflow là gì và khi nào nó xảy ra không?
- [ ] Tôi có thể giải thích Two's Complement không?
- [ ] Tôi biết cách phòng tránh overflow không?
- [ ] Tôi biết Math.addExact() có tác dụng gì không?

### Về Toán tử Số học (Arithmetic Operators)

- [ ] Tôi hiểu sự khác biệt giữa / và % không?
- [ ] Tôi biết integer division là gì không?
- [ ] Tôi hiểu promotion rules của Java không?
- [ ] Tôi phân biệt được ++i và i++ không?

### Về Toán tử So sánh và Logic

- [ ] Tôi biết sự khác biệt giữa == và equals() không?
- [ ] Tôi hiểu short-circuit evaluation là gì không?
- [ ] Tôi biết khi nào nên dùng && thay vì & không?
- [ ] Tôi nhớ thứ tự ưu tiên của các toán tử không?

### Về Toán tử Bitwise và Bit Shift

- [ ] Tôi có thể giải thích &, |, ^, ~ không?
- [ ] Tôi biết sự khác biệt giữa >>, >>>, << không?
- [ ] Tôi hiểu ứng dụng của bit flags không?
- [ ] Tôi biết khi nào nên dùng bitwise operations không?

### Về Kiểu Char và Unicode

- [ ] Tôi biết char trong Java là 16-bit không?
- [ ] Tôi hiểu sự khác biệt giữa 'A' và "A" không?
- [ ] Tôi có thể chuyển đổi giữa char và số không?
- [ ] Tôi biết cách sử dụng Unicode escape \uXXXX không?

---

## 6. CÂU HỎI INTERVIEW THƯỜNG GẶP (Common Interview Questions)

### Câu hỏi về Kiểu dữ liệu

**Q1: Tại sao Java có cả primitive types và wrapper classes?**
- Primitives: performance (lưu trên Stack), không thể null
- Wrappers: OOP features (lưu trên Heap), có thể null, dùng với generics

**Q2: Kích thước của char trong Java là bao nhiêu?**
- 16-bit (2 bytes), Unicode, range 0-65535

**Q3: Phạm vi của int là gì?**
- -2,147,483,648 đến 2,147,483,647 (khoảng 2.1 tỷ)

**Q4: char có phải là số nguyên không?**
- Có, char là số nguyên 16-bit không dấu (unsigned)

### Câu hỏi về Operators

**Q5: Sự khác biệt giữa == và equals()?**
- ==: so sánh tham chiếu (với Objects) hoặc giá trị (với primitives)
- equals(): so sánh nội dung (được override trong class)

**Q6: && và & khác nhau ở đâu?**
- &&: short-circuit (dừng nếu vế trái false)
- &: luôn kiểm tra cả hai vế

**Q7: ++i và i++ khác nhau thế nào?**
- ++i: tăng trước, trả về giá trị mới
- i++: trả về giá trị cũ, tăng sau

**Q8: 3 * 4 có bằng 3 << 2 không?**
- Có, vì 3 << 2 = 3 * 2^2 = 3 * 4 = 12

**Q9: Expression với byte và int được promote thành kiểu gì?**
- Luôn promote thành int

### Câu hỏi về Overflow

**Q10: Điều gì xảy ra khi intMax + 1?**
- Overflow, kết quả = Integer.MIN_VALUE

**Q11: Cách phòng tránh overflow?**
- Dùng Math.addExact() để ném exception
- Kiểm tra trước khi thực hiện phép tính
- Dùng long nếu cần giá trị lớn

---

## 7. TỔNG KẾT (Summary)

### Những điểm quan trọng cần nhớ:

1. **8 Primitive Types:** byte, short, int, long, float, double, char, boolean
2. **Int là mặc định** cho số nguyên, double là mặc định cho số thập phân
3. **Overflow không ném exception** - phải tự xử lý
4. **Integer division** bỏ phần dư - phải ép kiểu để lấy số thập phân
5. **Short-circuit operators** (&&, ||) nhanh và an toàn hơn
6. **== với String** so sánh tham chiếu - phải dùng equals()
7. **Char là 16-bit** Unicode, không phải 8-bit ASCII
8. **Bitwise operations** dùng cho flags, permissions, performance

### Các lỗi thường gặp:

1. Quên thêm 'L' khi khai báo long
2. Quên thêm 'f' khi khai báo float
3. Integer division thay vì floating-point division
4. So sánh String bằng ==
5. Overflow không được phát hiện
6. Dùng double quotes cho char

---

## 8. TÀI LIỆU THAM KHẢO (References)

- Oracle Java Documentation: https://docs.oracle.com/javase/tutorial/java/javaOO/index.html
- Java Language Specification: https://docs.oracle.com/javase/specs/jls/se17/html/
- Effective Java (Joshua Bloch) - Item 6: Avoid unnecessary objects
- Java Performance: The Definitive Guide (Scott Oaks)

---

**Chúc anh em học tốt! Hẹn gặp lại ở Lab02 - Control Flow!**