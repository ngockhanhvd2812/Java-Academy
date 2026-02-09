# LAB 10 - MULTI-THREADING (ĐA LUỒNG) TRONG JAVA

## 1. Mở bài (The Huddle)

*   **[Anh Khánh]:** "Chào anh em, hôm nay chúng ta sẽ học về Multi-threading - một trong những chủ đề NÂNG CAO và KHÓ NHẤT trong Java. Đây là kỹ năng quan trọng cho ứng dụng hiện đại."

*   **[Hùng (Intern)]:** "Dạ anh ơi, 'thread' là gì vậy anh? Em nghe nói Java có thể chạy nhiều thứ cùng lúc."

*   **[Anh Đô (Senior)]:** "Hùng hỏi nền tảng quá! Thread là 'luồng thực thi' - một đơn vị nhỏ nhất của code có thể chạy độc lập. Một chương trình có thể có nhiều threads chạy song song."

*   **[Nam (Intern)]:** "Dạ em sợ multi-threading lắm! Em nghe nói có race condition, deadlock..."

*   **[Anh Vương (Performance)]:** "Nam sợ đúng rồi! Multi-threading mạnh nhưng nguy hiểm. Thread safety là ưu tiên hàng đầu. Nếu không hiểu kỹ, sẽ gây bug khó debug."

*   **[Em Hải (Clean Code)]:** "Multi-threading giúp tận dụng CPU multi-core, tăng throughput. Nhưng cần cẩn thận với shared resources và synchronization."

*   **[Việt (Intern)]:** "Dạ Thread và Runnable khác nhau thế nào anh?"

*   **[Anh Khánh]:** "Việt hỏi câu phỏng vấn kinh điển! Sẽ giải thích chi tiết: Thread là class, Runnable là interface. Java chỉ cho phép extends một class, nên implement Runnable phổ biến hơn."

---

## 2. Chuẩn bị (Prerequisites)

*   **JDK version:** Java 8 trở lên
*   **IDE:** IntelliJ IDEA hoặc VS Code
*   **Package:** com.javazero.lab10

**Cấu trúc thư mục:**
```text
JavaProjects/
└── Lab10/
    └── src/
        └── com/
            └── javazero/
                └── lab10/
                    ├── ThreadDemo.java
                    ├── RunnableDemo.java
                    ├── SynchronizedDemo.java
                    ├── ThreadCommunicationDemo.java
                    └── ThreadPoolDemo.java
```

---

## 3. Hành trình khám phá (Deep-Dive Walkthrough)

### BƯỚC 1: Thread Lifecycle và Thread States

*   **Hội ý:**

*   **[Anh Khánh]:** "Thread có lifecycle với các states: NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED."

*   **[Anh Đô]:** "Thread States Diagram:"

```java
NEW → RUNNABLE → [RUNNING]
                ↑
                | (yield)
        WAITING ← TIMED_WAITING
                ↑ (notify)
            BLOCKED ←
```

*   **[Em Hải (Clean Code)]:** "Hiểu thread states giúp debug threading issues. Khi thread 'BLOCKED', nó đợi lock. Khi 'WAITING', nó đợi notification."

*   **[Hùng (Intern)]:** "Dạ NEW nghĩa là gì?"

*   **[Anh Vương]:** "NEW = thread vừa tạo, chưa start(). RUNNABLE = sẵn sàng chạy. RUNNING = đang chạy trên CPU."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Việt, em viết code demo Thread states đi?"

*   **[Việt (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: ThreadStatesDemo.java
// Package: com.javazero.lab10

public class ThreadStatesDemo {
    
    public static void main(String[] args) throws InterruptedException {
        System.out.println("=== THREAD STATES DEMO ===");
        
        // ========== THREAD STATES ==========
        System.out.println("\n--- Thread States ---");
        
        // NEW
        Thread thread = new Thread(() -> {
            System.out.println("Thread is RUNNING");
        });
        
        System.out.println("State after create: " + thread.getState()); // NEW
        
        // START
        thread.start();
        System.out.println("State after start: " + thread.getState()); // RUNNABLE/RUNNING
        
        thread.join(); // Đợi thread kết thúc
        System.out.println("State after join: " + thread.getState()); // TERMINATED
        
        // ========== TIMED_WAITING ==========
        System.out.println("\n--- Timed Waiting ---");
        Thread sleepingThread = new Thread(() -> {
            try {
                Thread.sleep(1000); // TIMED_WAITING
            } catch (InterruptedException e) {
                System.out.println("Thread interrupted");
            }
        });
        
        sleepingThread.start();
        Thread.sleep(100); // Đợi một chút
        System.out.println("Sleeping thread state: " + sleepingThread.getState()); // TIMED_WAITING
        sleepingThread.join();
        
        // ========== WAITING ==========
        System.out.println("\n--- Waiting ---");
        Object lock = new Object();
        
        Thread waitingThread = new Thread(() -> {
            synchronized (lock) {
                try {
                    lock.wait(); // WAITING
                } catch (InterruptedException e) {
                    System.out.println("Interrupted");
                }
            }
        });
        
        waitingThread.start();
        Thread.sleep(100);
        System.out.println("Waiting thread state: " + waitingThread.getState()); // WAITING
        
        synchronized (lock) {
            lock.notify(); // Wake up waiting thread
        }
        
        waitingThread.join();
        
        // ========== THREAD STATES REFERENCE ==========
        System.out.println("\n--- Thread States Reference ---");
        System.out.println("NEW: Thread vừa tạo, chưa start()");
        System.out.println("RUNNABLE: Sẵn sàng chạy");
        System.out.println("RUNNING: Đang chạy trên CPU");
        System.out.println("BLOCKED: Đợi lock");
        System.out.println("WAITING: Đợi vô thời hạn (notify)");
        System.out.println("TIMED_WAITING: Đợi có thời hạn (sleep, wait with timeout)");
        System.out.println("TERMINATED: Đã hoàn thành");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab10/ThreadStatesDemo.java
// java com.javazero.lab10.ThreadStatesDemo

// Output:
// === THREAD STATES DEMO ===
// 
// --- Thread States ---
// State after create: NEW
// Thread is RUNNING
// State after start: RUNNABLE
// State after join: TERMINATED
// 
// --- Timed Waiting ---
// Sleeping thread state: TIMED_WAITING
// 
// --- Waiting ---
// Waiting thread state: WAITING
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! getState() trả về Thread.State enum!"

*   **[Anh Đô]:** "Đúng rồi Nam! Thread.State có 6 values: NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED."

*   **[Hùng (Intern)]:** "Dạ sleep(1000) là TIMED_WAITING, còn wait() là WAITING?"

*   **[Em Hải]:** "Đúng rồi! sleep() có timeout, nên là TIMED_WAITING. wait() không timeout, là WAITING."

---

### BƯỚC 2: Thread Creation

*   **Hội ý:**

*   **[Anh Khánh]:** "Có 2 cách tạo Thread trong Java: 1) Extends Thread class, 2) Implements Runnable interface."

*   **[Anh Vương (Performance)]:** "Implement Runnable phổ biến hơn vì: 1) Java chỉ extends một class, 2) Tách runnable logic khỏi thread control."

*   **[Em Hải (Clean Code)**: "Từ Java 8+, có thể dùng Lambda với Runnable: new Thread(() -> { // code }). Rất ngắn gọn."

*   **[Hùng (Intern)]:** "Dạ Thread và Runnable khác nhau gì?"

*   **[Anh Đô]:** "Thread extends: run() là method của Thread. Runnable implements: run() là method của Runnable. Thread.start() KHỞI TẠO thread mới. Runnable.run() chỉ gọi method trên thread hiện tại."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo 2 cách tạo Thread đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: ThreadCreationDemo.java
// Package: com.javazero.lab10

// ========== METHOD 1: EXTENDS THREAD ==========
class MyThread extends Thread {
    private String name;
    
    public MyThread(String name) {
        this.name = name;
    }
    
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(name + " - Count: " + i);
            try {
                Thread.sleep(100); // Pause
            } catch (InterruptedException e) {
                System.out.println(name + " interrupted");
            }
        }
    }
}

// ========== METHOD 2: IMPLEMENTS RUNNABLE ==========
class MyRunnable implements Runnable {
    private String name;
    
    public MyRunnable(String name) {
        this.name = name;
    }
    
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(name + " - Count: " + i);
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                System.out.println(name + " interrupted");
            }
        }
    }
}

// ========== METHOD 3: LAMBDA (Java 8+) ==========
class LambdaThreadDemo {
    public static void main(String[] args) {
        System.out.println("=== THREAD CREATION DEMO ===");
        
        // ========== METHOD 1: EXTENDS THREAD ==========
        System.out.println("\n--- Method 1: extends Thread ---");
        MyThread thread1 = new MyThread("Thread-1");
        MyThread thread2 = new MyThread("Thread-2");
        
        thread1.start(); // KHÔNG gọi run()!
        thread2.start();
        
        // ========== METHOD 2: IMPLEMENTS RUNNABLE ==========
        System.out.println("\n--- Method 2: implements Runnable ---");
        Thread runnableThread1 = new Thread(new MyRunnable("Runnable-1"));
        Thread runnableThread2 = new Thread(new MyRunnable("Runnable-2"));
        
        runnableThread1.start();
        runnableThread2.start();
        
        // ========== METHOD 3: LAMBDA (Java 8+) ==========
        System.out.println("\n--- Method 3: Lambda Runnable ---");
        Runnable lambdaTask = () -> {
            for (int i = 1; i <= 3; i++) {
                System.out.println("Lambda Thread - Count: " + i);
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    System.out.println("Lambda interrupted");
                }
            }
        };
        
        Thread lambdaThread = new Thread(lambdaTask);
        lambdaThread.start();
        
        // ========== JOIN THREADS ==========
        System.out.println("\n--- Main Thread waiting for others ---");
        try {
            thread1.join(); // Main thread đợi thread1
            thread2.join(); // Main thread đợi thread2
            runnableThread1.join();
            runnableThread2.join();
            lambdaThread.join();
        } catch (InterruptedException e) {
            System.out.println("Main thread interrupted");
        }
        
        System.out.println("\n--- All threads completed! ---");
        
        // ========== START VS RUN ==========
        System.out.println("\n--- start() vs run() ---");
        System.out.println("main: Creating threads...");
        
        Thread t = new Thread(() -> {
            System.out.println("run(): This runs in CALLER's thread");
        });
        
        System.out.println("Calling run():");
        t.run(); // Chỉ gọi method, KHÔNG tạo thread mới!
        
        System.out.println("Calling start():");
        t.start(); // Tạo thread mới!
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab10/ThreadCreationDemo.java
// java com.javazero.lab10.LambdaThreadDemo

// Output:
// === THREAD CREATION DEMO ===
// 
// --- Method 1: extends Thread ---
// Thread-1 - Count: 1
// Thread-2 - Count: 1
// Thread-1 - Count: 2
// Thread-2 - Count: 2
// ...
// 
// --- Method 2: implements Runnable ---
// Runnable-1 - Count: 1
// Runnable-2 - Count: 1
// ...
// 
// --- Method 3: Lambda Runnable ---
// Lambda Thread - Count: 1
// Lambda Thread - Count: 2
// ...
// 
// --- start() vs run() ---
// main: Creating threads...
// run(): This runs in CALLER's thread
// Calling start():
// [Thread-0] run(): This runs in NEW thread
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "Anh ơi! start() và run() khác nhau rõ rệt! run() chỉ gọi method, start() tạo thread mới!"

*   **[Anh Đô]:** "Việt hiểu đúng rồi! Đây là lỗi phổ biến: gọi run() thay vì start() - thread không chạy song song."

*   **[Nam (Intern)]:** "Dạ join() dùng để làm gì?"

*   **[Em Hải]:** "join() = main thread đợi thread khác kết thúc. Đảm bảo thread hoàn thành trước khi main tiếp tục."

*   **[Hùng (Intern)]:** "Dạ Thread.sleep(100) là gì?"

*   **[Anh Vương]:** "sleep() = tạm dừng thread hiện tại trong 100 milliseconds. Dùng để simulate work và tránh CPU 100%."

---

### BƯỚC 3: Synchronization

*   **Hội ý:**

*   **[Anh Khánh]:** "Synchronization giúp tránh race condition khi nhiều threads truy cập shared resource cùng lúc."

*   **[Anh Đô]:** "Race condition xảy ra khi kết quả phụ thuộc vào thứ tự thực thi của threads. Dẫn đến kết quả không đoán trước được."

*   **[Em Hải (Clean Code)]:** "Synchronized methods: synchronized void method() { } - lock trên object instance. Synchronized blocks: synchronized(obj) { } - lock trên object cụ thể."

*   **[Hùng (Intern)]:** "Dạ lock là gì anh?"

*   **[Anh Vương]:** "Lock = 'cổng vào'. Khi một thread synchronized, nó giữ lock. Thread khác phải đợi lock được release."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Nam, em viết code demo race condition và synchronization đi?"

*   **[Nam (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: SynchronizedDemo.java
// Package: com.javazero.lab10

// ========== RACE CONDITION DEMO ==========
class CounterWithoutSync {
    private int count = 0;
    
    public void increment() {
        count++; // RACE CONDITION!
    }
    
    public int getCount() {
        return count;
    }
}

// ========== SYNCHRONIZED METHOD ==========
class CounterWithSync {
    private int count = 0;
    
    public synchronized void increment() {
        count++;
    }
    
    public synchronized int getCount() {
        return count;
    }
}

// ========== SYNCHRONIZED BLOCK ==========
class CounterWithSyncBlock {
    private int count = 0;
    private Object lock = new Object(); // Lock object riêng
    
    public void increment() {
        synchronized (lock) { // Synchronized block
            count++;
        }
    }
    
    public int getCount() {
        synchronized (lock) {
            return count;
        }
    }
}

// ========== STATIC SYNCHRONIZED ==========
class StaticCounter {
    private static int count = 0;
    
    public static synchronized void increment() {
        count++;
    }
    
    public static synchronized int getCount() {
        return count;
    }
}

public class SynchronizedDemo {
    public static void main(String[] args) throws InterruptedException {
        System.out.println("=== SYNCHRONIZATION DEMO ===");
        
        // ========== WITHOUT SYNCHRONIZATION ==========
        System.out.println("\n--- Without Synchronization (Race Condition) ---");
        CounterWithoutSync counter1 = new CounterWithoutSync();
        
        Thread[] threads1 = new Thread[10];
        for (int i = 0; i < 10; i++) {
            threads1[i] = new Thread(() -> {
                for (int j = 0; j < 1000; j++) {
                    counter1.increment();
                }
            });
            threads1[i].start();
        }
        
        for (Thread t : threads1) {
            t.join();
        }
        
        System.out.println("Expected: 10000, Actual: " + counter1.getCount()); // Có thể < 10000!
        
        // ========== WITH SYNCHRONIZED METHOD ==========
        System.out.println("\n--- With Synchronized Method ---");
        CounterWithSync counter2 = new CounterWithSync();
        
        Thread[] threads2 = new Thread[10];
        for (int i = 0; i < 10; i++) {
            threads2[i] = new Thread(() -> {
                for (int j = 0; j < 1000; j++) {
                    counter2.increment();
                }
            });
            threads2[i].start();
        }
        
        for (Thread t : threads2) {
            t.join();
        }
        
        System.out.println("Expected: 10000, Actual: " + counter2.getCount()); // LUÔN = 10000
        
        // ========== SYNCHRONIZED BLOCK ==========
        System.out.println("\n--- With Synchronized Block ---");
        CounterWithSyncBlock counter3 = new CounterWithSyncBlock();
        
        Thread[] threads3 = new Thread[10];
        for (int i = 0; i < 10; i++) {
            threads3[i] = new Thread(() -> {
                for (int j = 0; j < 1000; j++) {
                    counter3.increment();
                }
            });
            threads3[i].start();
        }
        
        for (Thread t : threads3) {
            t.join();
        }
        
        System.out.println("Expected: 10000, Actual: " + counter3.getCount()); // LUÔN = 10000
        
        // ========== STATIC SYNCHRONIZED ==========
        System.out.println("\n--- With Static Synchronized ---");
        Thread[] threads4 = new Thread[10];
        for (int i = 0; i < 10; i++) {
            threads4[i] = new Thread(() -> {
                for (int j = 0; j < 1000; j++) {
                    StaticCounter.increment();
                }
            });
            threads4[i].start();
        }
        
        for (Thread t : threads4) {
            t.join();
        }
        
        System.out.println("Expected: 10000, Actual: " + StaticCounter.getCount()); // LUÔN = 10000
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab10/SynchronizedDemo.java
// java com.javazero.lab10.SynchronizedDemo

// Output:
// === SYNCHRONIZATION DEMO ===
// 
// --- Without Synchronization (Race Condition) ---
// Expected: 10000, Actual: 9876  // CÓ THỂ KHÁC 10000!
// 
// --- With Synchronized Method ---
// Expected: 10000, Actual: 10000  // LUÔN = 10000
// 
// --- With Synchronized Block ---
// Expected: 10000, Actual: 10000  // LUÔN = 10000
// 
// --- With Static Synchronized ---
// Expected: 10000, Actual: 10000  // LUÔN = 10000
```

---

*   **Phân tích Output:**

*   **[Việt (Intern)]:** "ANH ƠI! Without synchronization: 9876, không phải 10000!"

*   **[Anh Đô]:** "Việt hiểu race condition rồi! count++看似简单，但有3步: đọc, tăng, ghi. Nhiều threads đọc cùng giá trị trước khi ghi."

*   **[Hùng (Intern)]:** "Dạ synchronized đảm bảo chỉ một thread thực thi tại một thời điểm!"

*   **[Em Hải]:** "Đúng rồi! synchronized = mutual exclusion. Lock được giữ trong thời gian method/block thực thi."

---

### BƯỚC 4: Thread Communication

*   **Hội ý:**

*   **[Anh Khánh]:** "wait(), notify(), notifyAll() là methods của Object class, dùng để threads giao tiếp với nhau."

*   **[Anh Vương (Performance)]:** "wait() = thread release lock và CHỜ. notify() = wake up một thread đang chờ. notifyAll() = wake up TẤT CẢ threads đang chờ."

*   **[Em Hải (Clean Code)**: "Luôn dùng wait() trong while loop, không phải if. Vì có thể spurious wakeup - thread wake up mà không có notify."

*   **[Hùng (Intern)]:** "Dạ tại sao wait() và notify() là methods của Object?"

*   **[Anh Đô]:** "Vì lock là trên object. Thread phải có lock mới có thể gọi wait/notify. Đây là design pattern của Java."

---

*   **VERIFY UNDERSTANDING:**

*   **[Anh Đô]:** "Cường, em viết code demo producer-consumer với wait/notify đi?"

*   **[Cường (Intern)]:** "Dạ được anh!"

---

*   **Thực hiện:**

```java
// File: ProducerConsumerDemo.java
// Package: com.javazero.lab10

import java.util.LinkedList;
import java.util.Queue;

// ========== SHARED QUEUE ==========
class SharedQueue {
    private static final int CAPACITY = 5;
    private Queue<Integer> queue = new LinkedList<>();
    
    public synchronized void produce(int value) throws InterruptedException {
        while (queue.size() >= CAPACITY) {
            System.out.println("Queue full. Producer waiting...");
            wait(); // Release lock, đợi
        }
        
        queue.offer(value);
        System.out.println("Produced: " + value);
        notifyAll(); // Wake up consumers
    }
    
    public synchronized int consume() throws InterruptedException {
        while (queue.isEmpty()) {
            System.out.println("Queue empty. Consumer waiting...");
            wait(); // Release lock, đợi
        }
        
        int value = queue.poll();
        System.out.println("Consumed: " + value);
        notifyAll(); // Wake up producers
        return value;
    }
}

// ========== PRODUCER THREAD ==========
class Producer implements Runnable {
    private SharedQueue queue;
    
    Producer(SharedQueue queue) {
        this.queue = queue;
    }
    
    @Override
    public void run() {
        for (int i = 1; i <= 10; i++) {
            try {
                queue.produce(i);
                Thread.sleep(100);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                break;
            }
        }
    }
}

// ========== CONSUMER THREAD ==========
class Consumer implements Runnable {
    private SharedQueue queue;
    
    Consumer(SharedQueue queue) {
        this.queue = queue;
    }
    
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            try {
                queue.consume();
                Thread.sleep(200);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                break;
            }
        }
    }
}

public class ProducerConsumerDemo {
    public static void main(String[] args) {
        System.out.println("=== PRODUCER-CONSUMER DEMO ===");
        
        SharedQueue queue = new SharedQueue();
        
        Thread producer = new Thread(new Producer(queue), "Producer");
        Thread consumer = new Thread(new Consumer(queue), "Consumer");
        
        producer.start();
        consumer.start();
        
        try {
            producer.join();
            consumer.join();
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        
        System.out.println("\n--- Producer-Consumer completed! ---");
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab10/ProducerConsumerDemo.java
// java com.javazero.lab10.ProducerConsumerDemo

// Output:
// === PRODUCER-CONSUMER DEMO ===
// Produced: 1
// Consumed: 1
// Produced: 2
// Produced: 3
// Queue full. Producer waiting...
// Consumed: 2
// Produced: 4
// Produced: 5
// Produced: 6
// Produced: 7
// Produced: 8
// Produced: 9
// Produced: 10
// Consumed: 3
// Consumed: 4
// Consumed: 5
// Consumed: 6
// Consumed: 7
// Consumed: 8
// Consumed: 9
// Consumed: 10
```

---

*   **Phân tích Output:**

*   **[Nam (Intern)]:** "Anh ơi! Producer đợi khi queue đầy, Consumer đợi khi queue rỗng!"

*   **[Anh Đô]:** "Nam hiểu đúng rồi! wait() và notifyAll() giúp threads phối hợp. Producer-Consumer là pattern kinh điển."

*   **[Việt (Intern)]:** "Dạ tại sao dùng while chứ không phải if?"

*   **[Em Hải]:** "Spurious wakeup! Thread có thể wake up mà không có notify. While loop kiểm tra lại điều kiện."

*   **[Hùng (Intern)]:** "Dạ notify() và notifyAll() khác nhau?"

*   **[Anh Vương]:** "notify() = wake up MỘT thread đang chờ (JVM chọn). notifyAll() = wake up TẤT CẢ. notifyAll() an toàn hơn."

---

### BƯỚC 5: Thread Pool

*   **Hội ý:**

*   **[Anh Khánh]:** "Thread Pool quản lý và tái sử dụng threads. Thay vì tạo/xóa threads liên tục, dùng pool có sẵn threads."

*   **[Anh Vương (Performance)]:** "Tạo thread tốn resources. Thread pool giảm overhead: tránh tạo/xóa liên tục, giới hạn số threads đang chạy."

*   **[Em Hải (Clean Code)]:** "Executors class cung cấp factory methods: newFixedThreadPool(), newCachedThreadPool(), newSingleThreadExecutor(), newScheduledThreadPool()."

*   **[Hùng (Intern)]:** "Dạ ExecutorService là gì?"

*   **[Anh Đô]:** "ExecutorService là interface quản lý thread pool. submit() gửi task, shutdown() dừng pool."

---

*   **Thực hiện:**

```java
// File: ThreadPoolDemo.java
// Package: com.javazero.lab10

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ThreadPoolDemo {
    
    public static void main(String[] args) {
        System.out.println("=== THREAD POOL DEMO ===");
        
        // ========== FIXED THREAD POOL ==========
        System.out.println("\n--- Fixed Thread Pool (3 threads) ---");
        ExecutorService executor1 = Executors.newFixedThreadPool(3);
        
        for (int i = 1; i <= 5; i++) {
            final int taskId = i;
            executor1.execute(() -> {
                System.out.println("Task " + taskId + " executing in " + 
                    Thread.currentThread().getName());
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            });
        }
        
        executor1.shutdown(); // Không nhận task mới
        
        // ========== CACHED THREAD POOL ==========
        System.out.println("\n--- Cached Thread Pool (tự mở rộng) ---");
        ExecutorService executor2 = Executors.newCachedThreadPool();
        
        for (int i = 1; i <= 5; i++) {
            final int taskId = i;
            executor2.execute(() -> {
                System.out.println("Task " + taskId + " executing in " + 
                    Thread.currentThread().getName());
            });
        }
        
        executor2.shutdown();
        
        // ========== SINGLE THREAD EXECUTOR ==========
        System.out.println("\n--- Single Thread Executor (1 thread) ---");
        ExecutorService executor3 = Executors.newSingleThreadExecutor();
        
        for (int i = 1; i <= 3; i++) {
            final int taskId = i;
            executor3.execute(() -> {
                System.out.println("Task " + taskId + " executing in " + 
                    Thread.currentThread().getName());
            });
        }
        
        executor3.shutdown();
        
        // ========== SCHEDULED THREAD POOL ==========
        System.out.println("\n--- Scheduled Thread Pool ---");
        ExecutorService executor4 = Executors.newScheduledThreadPool(2);
        
        Runnable task = () -> System.out.println("Scheduled task executing at " + 
            System.currentTimeMillis());
        
        // Schedule task to run after 2 seconds
        executor4.schedule(task, 2, TimeUnit.SECONDS);
        
        // Schedule task to run every 1 second (starting after 1 second)
        executor4.scheduleAtFixedRate(task, 1, 1, TimeUnit.SECONDS);
        
        // ========== AWAIT TERMINATION ==========
        System.out.println("\n--- Await Termination ---");
        ExecutorService executor5 = Executors.newFixedThreadPool(2);
        executor5.execute(() -> {
            try {
                Thread.sleep(1000);
                System.out.println("Task completed");
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        });
        
        try {
            System.out.println("Shutting down executor...");
            executor5.shutdown();
            boolean terminated = executor5.awaitTermination(5, TimeUnit.SECONDS);
            System.out.println("Terminated: " + terminated);
        } catch (InterruptedException e) {
            executor5.shutdownNow();
        }
    }
}
```

```java
// Compile & Run:
// javac com/javazero/lab10/ThreadPoolDemo.java
// java com.javazero.lab10.ThreadPoolDemo

// Output:
// === THREAD POOL DEMO ===
// 
// --- Fixed Thread Pool (3 threads) ---
// Task 1 executing in pool-1-thread-1
// Task 2 executing in pool-1-thread-2
// Task 3 executing in pool-1-thread-3
// Task 4 executing in pool-1-thread-1
// Task 5 executing in pool-1-thread-2
// 
// --- Cached Thread Pool ---
// Task 1 executing in pool-2-thread-1
// Task 2 executing in pool-2-thread-2
// Task 3 executing in pool-2-thread-3
// Task 4 executing in pool-2-thread-4
// Task 5 executing in pool-2-thread-5
// 
// --- Single Thread Executor ---
// Task 1 executing in pool-3-thread-1
// Task 2 executing in pool-3-thread-2
// Task 3 executing in pool-3-thread-3
// 
// --- Scheduled Thread Pool ---
// Scheduled task executing at 1234567890
// [Repeating tasks]
// 
// --- Await Termination ---
// Task completed
// Shutting down executor...
// Terminated: true
```

---

## 4. Chuyên mục "Debug & Troubleshoot" (Chaos & Troubleshooting)

### The Sabotage - GÂY LỖI CỐ Ý

*   **[Anh Khánh]:** "Giờ phá multi-threading! Mỗi người gây 1 bug kinh điển."

---

*   **Case 1: Deadlock**

```java
// File: DeadlockDemo.java
// Package: com.javazero.lab10

public class DeadlockDemo {
    
    public static void main(String[] args) throws InterruptedException {
        System.out.println("=== CASE 1: DEADLOCK (NGUY HIỂM!) ===");
        
        final Object lock1 = new Object();
        final Object lock2 = new Object();
        
        Thread thread1 = new Thread(() -> {
            synchronized (lock1) {
                System.out.println("Thread 1: Holding lock1...");
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {}
                System.out.println("Thread 1: Waiting for lock2...");
                synchronized (lock2) {
                    System.out.println("Thread 1: Holding lock2...");
                }
            }
        });
        
        Thread thread2 = new Thread(() -> {
            synchronized (lock2) {
                System.out.println("Thread 2: Holding lock2...");
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {}
                System.out.println("Thread 2: Waiting for lock1...");
                synchronized (lock1) {
                    System.out.println("Thread 2: Holding lock1...");
                }
            }
        });
        
        thread1.start();
        thread2.start();
        
        thread1.join();
        thread2.join();
        
        System.out.println("→ Code sẽ KHÔNG BAO GIỜ chạy xong!");
        System.out.println("→ DEADLOCK: 2 threads đợi nhau mãi mãi!");
    }
}
```

---

*   **Case 2: Race Condition**

```java
// File: RaceConditionDemo.java
// Package: com.javazero.lab10

public class RaceConditionDemo {
    
    static class BankAccount {
        private double balance = 1000;
        
        // SAI: Không synchronized!
        public void withdraw(double amount) {
            if (balance >= amount) {
                // Race condition: Thread có thể bị interrupt ở đây!
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {}
                balance -= amount;
                System.out.println("Withdrew: " + amount + ", Balance: " + balance);
            } else {
                System.out.println("Insufficient funds!");
            }
        }
    }
    
    public static void main(String[] args) throws InterruptedException {
        System.out.println("=== CASE 2: RACE CONDITION (BANK ACCOUNT) ===");
        
        BankAccount account = new BankAccount();
        
        Thread t1 = new Thread(() -> account.withdraw(500));
        Thread t2 = new Thread(() -> account.withdraw(500));
        
        t1.start();
        t2.start();
        
        t1.join();
        t2.join();
        
        System.out.println("Final balance: " + account.balance);
        System.out.println("→ Expected: 0, Có thể: -500 (RACE CONDITION!)");
    }
}
```

---

## 5. Tổng kết & Bài học (Debrief)

### **[Anh Khánh]:** "Bài học hôm nay?"

*   **[Hùng (Intern)]:** "Dạ em học được: Thread = luồng thực thi. Có 2 cách tạo: extends Thread, implements Runnable."

*   **[Nam (Intern)]:** "Dạ em học được: synchronized ngăn race condition. wait() = đợi, notify() = wake up."

*   **[Việt (Intern)]:** "Dạ em học được: Thread Pool tái sử dụng threads, tăng performance."

*   **[Cường (Intern)]:** "Dạ em học được: Deadlock = threads đợi nhau mãi mãi. Tránh bằng cách lock theo thứ tự."

---

### Bảng Checklist - Kiến thức cần nắm vững:

| Concept | Hiểu chưa? | Thực hành chưa? |
|---------|------------|-----------------|
| Thread lifecycle | ☐ | ☐ |
| Thread creation (Thread vs Runnable) | ☐ | ☐ |
| start() vs run() | ☐ | ☐ |
| Race condition | ☐ | ☐ |
| synchronized methods | ☐ | ☐ |
| synchronized blocks | ☐ | ☐ |
| wait(), notify(), notifyAll() | ☐ | ☐ |
| Thread Pool | ☐ | ☐ |
| Deadlock | ☐ | ☐ |
| Thread safety | ☐ | ☐ |

---

### Bài tập về nhà:

1.  Tạo Timer với Thread.sleep().
2.  Implement Producer-Consumer với ArrayBlockingQueue.
3.  Tạo thread-safe Counter.
4.  Viết Callable và Future example.
5.  Sử dụng CompletableFuture (Java 8+).

---

### Tài liệu tham khảo:

*   Oracle Java Tutorials: Concurrency
*   Effective Java: Item 78-80 (Concurrency)

---

**Chúc anh em đã hoàn thành Java Zero-To-Hero! Bây giờ anh em đã có nền tảng vững chắc để tiếp tục học Java Frameworks và thực hành dự án thực tế!**
