# BÁO CÁO THỰC TẬP TUẦN 4

## Chủ đề: Database, Logging & I/O

**Intern:** Bùi Văn Nam  
**Team:** Platform - Adtech  
**Gmail:** buivannam13032004@gmail.com  
**Leader:** Nguyễn Văn Cương  

---

## 1. Mục tiêu tuần

Trong tuần thứ tư, theo roadmap mục tiêu là tìm hiểu các kiến thức về Database, Logging và I/O trong Java.

Nội dung học tập tập trung vào việc hiểu cách cài đặt và cấu hình MySQL/PostgreSQL, tối ưu hóa truy vấn SQL với EXPLAIN plans, các chiến lược Normalization và Indexing, cũng như các đặc tính ACID và Transaction Isolation Levels trong Database.

Bên cạnh đó, đã tìm hiểu các Logging Frameworks phổ biến trong Java như SLF4J, Logback và Log4j2, cách sử dụng Log Levels, Structured Logging và Log Aggregation.

Về I/O, đã tìm hiểu sự khác biệt giữa Blocking và Non-blocking I/O, Java NIO.2 API, Event-driven file processing và các kỹ thuật High-performance I/O như Memory-mapped files và Zero-copy.

---

### Lịch học Tuần 4

| Ngày | Nội dung học | Kết quả đạt được |
|---|---|---|
| Thứ 2 | Database Installation, Configuration & SQL Optimization | Hiểu cách cài đặt MySQL/PostgreSQL, cấu hình cơ bản và tối ưu truy vấn với EXPLAIN plans. |
| Thứ 3 | Database Normalization, Indexing & ACID Properties | Nắm được các chiến lược Normalization, Indexing, ACID properties và Transaction Isolation Levels. |
| Thứ 4 | Logging Frameworks (SLF4J, Logback, Log4j2) | Hiểu các Logging Frameworks, Log Levels, Structured Logging và Log Aggregation. |
| Thứ 5 | I/O Concepts: Blocking vs Non-blocking, Java NIO.2 | Hiểu sự khác biệt giữa Blocking và Non-blocking I/O, và cách sử dụng Java NIO.2. |
| Thứ 6 | Advanced I/O: Memory-mapped files, Zero-copy & Event Loop | Nắm được các kỹ thuật High-performance I/O và Event Loop Implementation. |

---

## 2. Chi tiết nội dung đã học

### 2.1. Database

#### a. MySQL/PostgreSQL Installation và Configuration

Đã tìm hiểu cách cài đặt và cấu hình MySQL và PostgreSQL trên môi trường Local và Docker.

**MySQL Installation (via Docker):**


docker run --name mysql-db -e MYSQL_ROOT_PASSWORD=root123 -p 3306:3306 -d mysql:8.0
PostgreSQL Installation (via Docker):

bash
docker run --name postgres-db -e POSTGRES_PASSWORD=root123 -p 5432:5432 -d postgres:15
Cấu hình cơ bản:

Thiết lập max_connections phù hợp với nhu cầu ứng dụng

Cấu hình innodb_buffer_pool_size (MySQL) hoặc shared_buffers (PostgreSQL) để tối ưu performance

Enable Query Logging để debug và phân tích truy vấn chậm

b. SQL Optimization với EXPLAIN Plans
Đã tìm hiểu cách sử dụng EXPLAIN để phân tích và tối ưu truy vấn SQL.

Ví dụ sử dụng EXPLAIN trong MySQL:

sql
EXPLAIN SELECT * FROM users WHERE email = 'example@gmail.com';
Các thông tin quan trọng trong EXPLAIN Plan:

Column	Ý nghĩa
id	Identifier của truy vấn
select_type	Loại truy vấn (SIMPLE, PRIMARY, SUBQUERY, ...)
table	Tên bảng được truy cập
type	Loại Join (ALL, index, range, ref, eq_ref, const, system)
possible_keys	Các Index có thể được sử dụng
key	Index thực tế được sử dụng
key_len	Độ dài của Index
ref	Cột hoặc hằng số được so sánh với Index
rows	Số lượng dòng được ước tính phải scan
Extra	Thông tin bổ sung (Using index, Using where, Using filesort, ...)
Một số kỹ thuật tối ưu truy vấn:

Sử dụng Index đúng cách để giảm số lượng rows scan

Tránh SELECT *, chỉ lấy các cột cần thiết

Sử dụng LIMIT để giới hạn số lượng kết quả

Tránh sử dụng hàm trên cột được Index trong mệnh đề WHERE

Sử dụng JOIN thay vì Subquery khi có thể

c. Database Normalization và Indexing Strategies
Đã tìm hiểu các cấp độ Normalization và chiến lược Indexing để tối ưu hiệu suất Database.

Normalization Forms:

1NF (First Normal Form): Mỗi cột chỉ chứa một giá trị atomic, không có repeating groups

2NF (Second Normal Form): Đạt 1NF và loại bỏ partial dependency

3NF (Third Normal Form): Đạt 2NF và loại bỏ transitive dependency

BCNF (Boyce-Codd Normal Form): Phiên bản mạnh hơn của 3NF

Chiến lược Indexing:

B-Tree Index: Index mặc định, phù hợp cho các truy vấn so sánh và range queries

Hash Index: Phù hợp cho truy vấn tìm kiếm chính xác (=)

Composite Index: Index trên nhiều cột, cần chú ý thứ tự các cột

Covering Index: Index chứa tất cả các cột cần thiết cho truy vấn, giúp tránh đọc dữ liệu từ bảng

Nguyên tắc tạo Index:

Index trên các cột thường xuất hiện trong WHERE, JOIN, ORDER BY, GROUP BY

Hạn chế số lượng Index để tránh ảnh hưởng đến Insert/Update/Delete

Sử dụng Composite Index khi truy vấn có nhiều điều kiện

d. ACID Properties và Transaction Isolation Levels
Đã tìm hiểu các đặc tính ACID của Database và các mức Isolation Level.

ACID Properties:

Property	Mô tả
Atomicity	Transaction được thực hiện toàn bộ hoặc không thực hiện gì cả
Consistency	Transaction đưa Database từ trạng thái hợp lệ này sang trạng thái hợp lệ khác
Isolation	Các Transaction thực thi độc lập với nhau
Durability	Dữ liệu được lưu vĩnh viễn sau khi Transaction commit
Transaction Isolation Levels:

Isolation Level	Dirty Read	Non-repeatable Read	Phantom Read
READ UNCOMMITTED	✅ Có thể xảy ra	✅ Có thể xảy ra	✅ Có thể xảy ra
READ COMMITTED	❌ Không xảy ra	✅ Có thể xảy ra	✅ Có thể xảy ra
REPEATABLE READ	❌ Không xảy ra	❌ Không xảy ra	✅ Có thể xảy ra (MySQL)
SERIALIZABLE	❌ Không xảy ra	❌ Không xảy ra	❌ Không xảy ra
Ví dụ thiết lập Isolation Level trong Spring:

java
@Transactional(isolation = Isolation.READ_COMMITTED)
public void processOrder(Order order) {
    // Business logic
}
2.2. Logging
a. Logging Frameworks: SLF4J, Logback, Log4j2
Đã tìm hiểu các Logging Framework phổ biến trong hệ sinh thái Java.

SLF4J (Simple Logging Facade for Java):

Là một Facade pattern, cung cấp API thống nhất cho các logging frameworks khác nhau

Cho phép thay đổi logging framework mà không cần thay đổi code

Logback:

Framework logging phổ biến, được xem là kế thừa của Log4j

Có hiệu suất tốt và hỗ trợ nhiều tính năng nâng cao

Cấu hình qua file logback.xml hoặc logback-spring.xml

Log4j2:

Phiên bản cải tiến của Log4j với nhiều tính năng mới

Hỗ trợ Async Logging với hiệu suất cao

Cấu hình qua file log4j2.xml hoặc log4j2.properties

Ví dụ sử dụng SLF4J với Logback:

java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class UserService {
    private static final Logger logger = LoggerFactory.getLogger(UserService.class);
    
    public User findUserById(Long id) {
        logger.info("Finding user with id: {}", id);
        // Business logic
        return user;
    }
}
b. Log Levels và Appropriate Usage
Đã tìm hiểu các Log Levels và cách sử dụng chúng một cách phù hợp trong ứng dụng.

Level	Khi nào sử dụng	Ví dụ
TRACE	Debugging chi tiết nhất, theo dõi luồng thực thi	logger.trace("Entering method processOrder()")
DEBUG	Debugging, thông tin chi tiết dành cho developers	logger.debug("User session: {}", sessionId)
INFO	Thông tin vận hành bình thường của ứng dụng	logger.info("Order created: {}", orderId)
WARN	Cảnh báo, tình huống bất thường nhưng không gây lỗi	logger.warn("Low inventory for product: {}", productId)
ERROR	Lỗi nghiêm trọng, cần được xử lý	logger.error("Failed to process payment", exception)
Nguyên tắc sử dụng Log Levels:

Sử dụng đúng mức độ log để tránh quá tải logging

Không log thông tin nhạy cảm (password, credit card, ...)

Log có cấu trúc để dễ dàng query và phân tích

c. Structured Logging (JSON Format)
Đã tìm hiểu về Structured Logging và cách triển khai log dưới dạng JSON.

Lợi ích của Structured Logging:

Dễ dàng query và filter log

Tích hợp tốt với các công cụ log aggregation (ELK Stack, Splunk, ...)

Cho phép thêm metadata vào log

Ví dụ cấu hình Logback cho JSON format:

xml
<configuration>
    <appender name="JSON" class="ch.qos.logback.core.ConsoleAppender">
        <encoder class="ch.qos.logback.classic.encoder.JsonEncoder"/>
    </appender>
    
    <root level="INFO">
        <appender-ref ref="JSON"/>
    </root>
</configuration>
Ví dụ Structured Log với MDC (Mapped Diagnostic Context):

java
import org.slf4j.MDC;

public class OrderService {
    public void processOrder(Order order) {
        MDC.put("orderId", order.getId().toString());
        MDC.put("userId", order.getUserId().toString());
        MDC.put("requestId", UUID.randomUUID().toString());
        
        try {
            logger.info("Processing order");
            // Business logic
        } finally {
            MDC.clear();
        }
    }
}
Output JSON:

json
{
    "timestamp": "2026-07-27T10:30:45.123Z",
    "level": "INFO",
    "logger": "com.example.OrderService",
    "message": "Processing order",
    "orderId": "12345",
    "userId": "67890",
    "requestId": "abc-def-ghi"
}
d. Log Aggregation và Centralized Logging
Đã tìm hiểu về các giải pháp Log Aggregation và Centralized Logging.

ELK Stack:

Elasticsearch: Lưu trữ và index log

Logstash: Thu thập, xử lý và chuyển đổi log

Kibana: Hiển thị và phân tích log

Loki Stack:

Loki: Lưu trữ log với chi phí thấp

Promtail: Thu thập log

Grafana: Hiển thị log

Lợi ích của Centralized Logging:

Tập trung log từ nhiều service

Dễ dàng troubleshooting và debugging

Monitoring và alerting

Phân tích xu hướng và pattern

e. Performance Impact của Logging
Đã tìm hiểu về ảnh hưởng hiệu suất của logging và cách tối ưu.

Các vấn đề về performance:

I/O overhead khi ghi log

Blocking khi log sync

Context switching khi log nhiều

Storage và network I/O

Các kỹ thuật tối ưu:

Kỹ thuật	Mô tả	Lợi ích
Async Logging	Ghi log không đồng bộ	Giảm blocking, tăng throughput
Batch Logging	Ghi log theo batch	Giảm I/O calls
Conditional Logging	Chỉ log khi cần	Giảm logging overhead
Log Level Filtering	Lọc theo level ở appender	Giảm xử lý không cần thiết
Ví dụ cấu hình Async Appender trong Logback:

xml
<configuration>
    <appender name="ASYNC" class="ch.qos.logback.classic.AsyncAppender">
        <queueSize>512</queueSize>
        <discardingThreshold>0</discardingThreshold>
        <appender-ref ref="FILE"/>
    </appender>
    
    <root level="INFO">
        <appender-ref ref="ASYNC"/>
    </root>
</configuration>
2.3. I/O (Input/Output)
a. Blocking I/O vs Non-blocking I/O Concepts
Đã tìm hiểu sự khác biệt giữa Blocking và Non-blocking I/O.

Blocking I/O (BIO):

Thread bị block cho đến khi I/O operation hoàn thành

Mỗi kết nối cần một thread riêng

Phù hợp với ứng dụng có số lượng kết nối thấp

Non-blocking I/O (NIO):

Thread không bị block khi thực hiện I/O

Một thread có thể xử lý nhiều kết nối

Phù hợp với ứng dụng có số lượng kết nối cao

So sánh:

Đặc điểm	Blocking I/O	Non-blocking I/O
Thread model	1 thread per connection	1 thread xử lý nhiều connection
CPU usage	Cao khi nhiều kết nối	Thấp hơn
Memory usage	Cao (mỗi thread có stack riêng)	Thấp hơn
Complexity	Đơn giản	Phức tạp hơn
Use case	Số lượng connection thấp	Số lượng connection cao
b. Java NIO.2 (AsynchronousFileChannel, AsynchronousSocketChannel)
Đã tìm hiểu về Java NIO.2 API và cách sử dụng cho I/O bất đồng bộ.

AsynchronousFileChannel:

java
import java.nio.channels.AsynchronousFileChannel;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.ByteBuffer;
import java.nio.file.StandardOpenOption;
import java.util.concurrent.Future;

public class AsyncFileReader {
    public void readFileAsync() throws Exception {
        Path file = Paths.get("data.txt");
        AsynchronousFileChannel channel = AsynchronousFileChannel.open(file, StandardOpenOption.READ);
        
        ByteBuffer buffer = ByteBuffer.allocate(1024);
        Future<Integer> future = channel.read(buffer, 0);
        
        // Do other work while reading
        System.out.println("Reading file in background...");
        
        // Wait for result
        int bytesRead = future.get();
        System.out.println("Bytes read: " + bytesRead);
    }
}
AsynchronousSocketChannel:

java
import java.nio.channels.AsynchronousSocketChannel;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;

public class AsyncSocketClient {
    public void connectAsync() throws Exception {
        AsynchronousSocketChannel client = AsynchronousSocketChannel.open();
        
        client.connect(new InetSocketAddress("localhost", 8080), null, 
            new CompletionHandler<Void, Void>() {
                @Override
                public void completed(Void result, Void attachment) {
                    System.out.println("Connected to server");
                    ByteBuffer buffer = ByteBuffer.wrap("Hello Server".getBytes());
                    client.write(buffer, null, new CompletionHandler<Integer, Void>() {
                        @Override
                        public void completed(Integer result, Void attachment) {
                            System.out.println("Sent: " + result + " bytes");
                        }
                        @Override
                        public void failed(Throwable exc, Void attachment) {
                            System.err.println("Write failed: " + exc.getMessage());
                        }
                    });
                }
                
                @Override
                public void failed(Throwable exc, Void attachment) {
                    System.err.println("Connect failed: " + exc.getMessage());
                }
            }
        );
        
        // Wait a bit to see results
        Thread.sleep(2000);
    }
}
c. Event-driven File Processing
Đã tìm hiểu về Event-driven File Processing và cách xử lý sự kiện file.

Sử dụng WatchService để monitor file system:

java
import java.nio.file.*;

public class FileWatchService {
    public void watchDirectory(String dirPath) throws Exception {
        Path path = Paths.get(dirPath);
        WatchService watchService = FileSystems.getDefault().newWatchService();
        
        path.register(watchService,
                StandardWatchEventKinds.ENTRY_CREATE,
                StandardWatchEventKinds.ENTRY_MODIFY,
                StandardWatchEventKinds.ENTRY_DELETE);
        
        System.out.println("Watching directory: " + dirPath);
        
        while (true) {
            WatchKey key = watchService.take();
            
            for (WatchEvent<?> event : key.pollEvents()) {
                WatchEvent.Kind<?> kind = event.kind();
                Path fileName = (Path) event.context();
                
                if (kind == StandardWatchEventKinds.ENTRY_CREATE) {
                    System.out.println("File created: " + fileName);
                    processNewFile(fileName);
                } else if (kind == StandardWatchEventKinds.ENTRY_MODIFY) {
                    System.out.println("File modified: " + fileName);
                    processModifiedFile(fileName);
                } else if (kind == StandardWatchEventKinds.ENTRY_DELETE) {
                    System.out.println("File deleted: " + fileName);
                }
            }
            
            key.reset();
        }
    }
    
    private void processNewFile(Path fileName) {
        // Process new file
    }
    
    private void processModifiedFile(Path fileName) {
        // Process modified file
    }
}
d. High-performance I/O Patterns
Đã tìm hiểu các pattern I/O hiệu suất cao.

Producer-Consumer Pattern:

text
[Producer] -> [Queue] -> [Consumer]
Reactor Pattern (Event-driven):

text
[Event Demultiplexer] -> [Event Handler] -> [Application]
Proactor Pattern (Async I/O):

text
[Async Operation] -> [Completion Handler] -> [Application]
Ví dụ Reactor Pattern với Selector:

java
import java.nio.channels.*;
import java.nio.ByteBuffer;
import java.net.ServerSocketChannel;
import java.net.InetSocketAddress;
import java.util.Iterator;
import java.util.Set;

public class ReactorServer {
    public void startServer(int port) throws Exception {
        Selector selector = Selector.open();
        ServerSocketChannel serverChannel = ServerSocketChannel.open();
        serverChannel.bind(new InetSocketAddress(port));
        serverChannel.configureBlocking(false);
        serverChannel.register(selector, SelectionKey.OP_ACCEPT);
        
        System.out.println("Server started on port: " + port);
        
        while (true) {
            selector.select();
            Set<SelectionKey> selectedKeys = selector.selectedKeys();
            Iterator<SelectionKey> iterator = selectedKeys.iterator();
            
            while (iterator.hasNext()) {
                SelectionKey key = iterator.next();
                iterator.remove();
                
                if (key.isAcceptable()) {
                    // Handle new connection
                    ServerSocketChannel server = (ServerSocketChannel) key.channel();
                    SocketChannel client = server.accept();
                    client.configureBlocking(false);
                    client.register(selector, SelectionKey.OP_READ);
                    System.out.println("New connection accepted");
                } else if (key.isReadable()) {
                    // Handle read
                    SocketChannel client = (SocketChannel) key.channel();
                    ByteBuffer buffer = ByteBuffer.allocate(1024);
                    int bytesRead = client.read(buffer);
                    
                    if (bytesRead > 0) {
                        buffer.flip();
                        String message = new String(buffer.array(), 0, bytesRead);
                        System.out.println("Received: " + message);
                        
                        // Echo back
                        client.write(ByteBuffer.wrap(("Echo: " + message).getBytes()));
                    } else if (bytesRead == -1) {
                        client.close();
                    }
                }
            }
        }
    }
}
e. Memory-mapped Files và Zero-copy Techniques
Đã tìm hiểu về Memory-mapped files và Zero-copy techniques trong Java.

Memory-mapped Files:

Cho phép mapping file vào memory, giúp truy xuất dữ liệu nhanh hơn I/O truyền thống.

java
import java.nio.MappedByteBuffer;
import java.nio.channels.FileChannel;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.nio.charset.StandardCharsets;

public class MemoryMappedFileExample {
    
    public void readMappedFile() throws Exception {
        Path path = Paths.get("large-file.dat");
        
        try (FileChannel channel = FileChannel.open(path, StandardOpenOption.READ)) {
            long fileSize = channel.size();
            MappedByteBuffer buffer = channel.map(
                    FileChannel.MapMode.READ_ONLY, 
                    0, 
                    fileSize
            );
            
            // Read data directly from memory
            while (buffer.hasRemaining()) {
                byte b = buffer.get();
                // Process byte
            }
        }
    }
    
    public void writeMappedFile() throws Exception {
        Path path = Paths.get("output.dat");
        
        try (FileChannel channel = FileChannel.open(path, 
                StandardOpenOption.READ, 
                StandardOpenOption.WRITE, 
                StandardOpenOption.CREATE)) {
            
            MappedByteBuffer buffer = channel.map(
                    FileChannel.MapMode.READ_WRITE, 
                    0, 
                    1024
            );
            
            String data = "Hello Memory-mapped file!";
            buffer.put(data.getBytes(StandardCharsets.UTF_8));
        }
    }
}
Zero-copy Techniques:

Giảm số lần copy dữ liệu giữa user space và kernel space.

java
import java.nio.channels.FileChannel;
import java.nio.channels.SocketChannel;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;

public class ZeroCopyExample {
    public void transferFile(String sourcePath, SocketChannel target) throws Exception {
        Path path = Paths.get(sourcePath);
        
        try (FileChannel source = FileChannel.open(path, StandardOpenOption.READ)) {
            long position = 0;
            long size = source.size();
            
            // transferTo uses zero-copy when possible
            long transferred = source.transferTo(position, size, target);
            System.out.println("Transferred: " + transferred + " bytes");
        }
    }
}
So sánh I/O Techniques:

Technique	Use Case	Performance
Blocking I/O	File I/O, small number of connections	Low
Non-blocking I/O	Network I/O, many connections	Medium
Memory-mapped files	Large files, random access	High
Zero-copy	Transfer between channels	Very High
Async I/O	I/O with callback	High
2.4. Event Loop & Async I/O
a. Event Loop Implementation
Đã tìm hiểu về Event Loop và cách triển khai trong ứng dụng.

Event Loop là gì?

Event Loop là một vòng lặp liên tục lắng nghe các sự kiện và xử lý chúng theo thứ tự.

Simple Event Loop Implementation:

java
import java.util.concurrent.*;

public class EventLoop {
    private final BlockingQueue<Runnable> taskQueue = new LinkedBlockingQueue<>();
    private volatile boolean running = true;
    private Thread worker;
    
    public void start() {
        worker = new Thread(() -> {
            while (running) {
                try {
                    Runnable task = taskQueue.take();
                    task.run();
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    break;
                }
            }
        });
        worker.start();
    }
    
    public void submit(Runnable task) {
        if (!running) {
            throw new IllegalStateException("EventLoop is not running");
        }
        taskQueue.offer(task);
    }
    
    public void stop() {
        running = false;
        worker.interrupt();
        try {
            worker.join(5000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
b. Callback Hell và Solutions
Đã tìm hiểu về vấn đề "Callback Hell" và các giải pháp khắc phục.

Callback Hell Example:

java
asyncOperation1(new Callback() {
    @Override
    public void onSuccess(Result result1) {
        asyncOperation2(result1, new Callback() {
            @Override
            public void onSuccess(Result result2) {
                asyncOperation3(result2, new Callback() {
                    @Override
                    public void onSuccess(Result result3) {
                        // Process result3
                    }
                    @Override
                    public void onError(Throwable error) {
                        // Handle error
                    }
                });
            }
            @Override
            public void onError(Throwable error) {
                // Handle error
            }
        });
    }
    @Override
    public void onError(Throwable error) {
        // Handle error
    }
});
Giải pháp 1: CompletableFuture

java
CompletableFuture.supplyAsync(() -> asyncOperation1())
    .thenApply(result1 -> asyncOperation2(result1))
    .thenApply(result2 -> asyncOperation3(result2))
    .thenAccept(result3 -> {
        // Process result3
    })
    .exceptionally(error -> {
        // Handle error
        return null;
    });
Giải pháp 2: Reactive Programming

java
Mono.fromCallable(() -> asyncOperation1())
    .flatMap(result1 -> Mono.fromCallable(() -> asyncOperation2(result1)))
    .flatMap(result2 -> Mono.fromCallable(() -> asyncOperation3(result2)))
    .doOnSuccess(result3 -> {
        // Process result3
    })
    .doOnError(error -> {
        // Handle error
    })
    .subscribe();
c. Reactive Streams và Backpressure
Đã tìm hiểu về Reactive Streams và cơ chế Backpressure.

Reactive Streams Components:

Component	Mô tả
Publisher	Nơi tạo ra dữ liệu
Subscriber	Nơi nhận dữ liệu
Subscription	Kết nối giữa Publisher và Subscriber
Processor	Vừa là Subscriber vừa là Publisher
Backpressure Implementation:

java
import org.reactivestreams.*;

public class BackpressureExample {
    public void demonstrateBackpressure() {
        Publisher<String> publisher = subscriber -> {
            Subscription subscription = new Subscription() {
                private boolean cancelled = false;
                private int count = 0;
                private long requested = 0;
                
                @Override
                public void request(long n) {
                    if (n <= 0) {
                        subscriber.onError(new IllegalArgumentException("n <= 0"));
                        return;
                    }
                    
                    requested += n;
                    // Send data up to requested amount
                    for (int i = 0; i < n && count < 100; i++) {
                        if (cancelled) break;
                        subscriber.onNext("Data-" + count++);
                    }
                    
                    if (count >= 100) {
                        subscriber.onComplete();
                    }
                }
                
                @Override
                public void cancel() {
                    cancelled = true;
                }
            };
            subscriber.onSubscribe(subscription);
        };
        
        Subscriber<String> subscriber = new Subscriber<>() {
            private Subscription subscription;
            
            @Override
            public void onSubscribe(Subscription s) {
                this.subscription = s;
                // Request first batch
                s.request(10);
            }
            
            @Override
            public void onNext(String data) {
                System.out.println("Received: " + data);
                // Request more when ready
                subscription.request(5);
            }
            
            @Override
            public void onError(Throwable t) {
                System.err.println("Error: " + t.getMessage());
            }
            
            @Override
            public void onComplete() {
                System.out.println("Complete!");
            }
        };
        
        publisher.subscribe(subscriber);
    }
}
d. NIO Selector và Multiplexing
Đã tìm hiểu về NIO Selector và cơ chế Multiplexing.

Selector Operations:

java
import java.nio.channels.Selector;
import java.nio.channels.SelectionKey;
import java.nio.channels.SocketChannel;
import java.nio.channels.ServerSocketChannel;
import java.nio.ByteBuffer;
import java.net.InetSocketAddress;
import java.util.Iterator;

public class NIOMultiplexingExample {
    public void multiplexingExample() throws Exception {
        Selector selector = Selector.open();
        
        // Setup server
        ServerSocketChannel server = ServerSocketChannel.open();
        server.bind(new InetSocketAddress(8080));
        server.configureBlocking(false);
        server.register(selector, SelectionKey.OP_ACCEPT);
        
        System.out.println("Server listening on port 8080");
        
        while (true) {
            selector.select(); // Block until events available
            
            Iterator<SelectionKey> iterator = selector.selectedKeys().iterator();
            
            while (iterator.hasNext()) {
                SelectionKey key = iterator.next();
                iterator.remove();
                
                if (key.isAcceptable()) {
                    // Accept new connection
                    ServerSocketChannel serverChannel = (ServerSocketChannel) key.channel();
                    SocketChannel client = serverChannel.accept();
                    client.configureBlocking(false);
                    client.register(selector, SelectionKey.OP_READ);
                    System.out.println("New connection");
                } else if (key.isReadable()) {
                    // Read data
                    SocketChannel client = (SocketChannel) key.channel();
                    ByteBuffer buffer = ByteBuffer.allocate(1024);
                    int bytesRead = client.read(buffer);
                    
                    if (bytesRead > 0) {
                        buffer.flip();
                        byte[] data = new byte[bytesRead];
                        buffer.get(data);
                        String message = new String(data);
                        System.out.println("Received: " + message);
                        
                        // Write response
                        String response = "ACK: " + message;
                        client.write(ByteBuffer.wrap(response.getBytes()));
                    } else if (bytesRead == -1) {
                        key.cancel();
                        client.close();
                        System.out.println("Connection closed");
                    }
                }
            }
        }
    }
}
e. Async File I/O
Đã tìm hiểu về Async File I/O và cách sử dụng trong Java.

Ví dụ Async File Operations:

java
import java.nio.file.*;
import java.nio.ByteBuffer;
import java.nio.channels.AsynchronousFileChannel;
import java.util.concurrent.CompletableFuture;

public class AsyncFileIOExample {
    
    public CompletableFuture<String> readFileAsync(String filePath) {
        Path path = Paths.get(filePath);
        CompletableFuture<String> future = new CompletableFuture<>();
        
        try {
            AsynchronousFileChannel channel = AsynchronousFileChannel.open(
                path, StandardOpenOption.READ);
            
            ByteBuffer buffer = ByteBuffer.allocate(1024 * 1024);
            
            channel.read(buffer, 0, channel, 
                new java.nio.channels.CompletionHandler<Integer, AsynchronousFileChannel>() {
                    @Override
                    public void completed(Integer bytesRead, AsynchronousFileChannel attachment) {
                        if (bytesRead > 0) {
                            buffer.flip();
                            byte[] data = new byte[bytesRead];
                            buffer.get(data);
                            future.complete(new String(data));
                        } else {
                            future.complete("");
                        }
                        try {
                            attachment.close();
                        } catch (Exception e) {
                            future.completeExceptionally(e);
                        }
                    }
                    
                    @Override
                    public void failed(Throwable exc, AsynchronousFileChannel attachment) {
                        future.completeExceptionally(exc);
                        try {
                            attachment.close();
                        } catch (Exception e) {
                            // Log error
                        }
                    }
                }
            );
        } catch (Exception e) {
            future.completeExceptionally(e);
        }
        
        return future;
    }
}
f. Zero-Copy và sendfile() System Call
Đã tìm hiểu về Zero-copy và cách sử dụng sendfile() system call.

Zero-copy với FileChannel:

java
import java.nio.channels.FileChannel;
import java.nio.channels.SocketChannel;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;

public class ZeroCopyServer {
    public void serveFile(SocketChannel client, String filePath) throws Exception {
        Path path = Paths.get(filePath);
        
        try (FileChannel fileChannel = FileChannel.open(path, StandardOpenOption.READ)) {
            long size = fileChannel.size();
            long position = 0;
            long transferred = 0;
            
            // Zero-copy transfer using sendfile()
            while (transferred < size) {
                long bytes = fileChannel.transferTo(position, size - position, client);
                position += bytes;
                transferred += bytes;
            }
            
            System.out.println("File sent: " + filePath + " (" + transferred + " bytes)");
        }
    }
}
Lợi ích của Zero-copy:

Giảm CPU usage (ít copy hơn)

Giảm memory usage

Tăng throughput

Phù hợp cho file serving và data transfer

3. Kết quả đạt được
Sau khi hoàn thành tuần học thứ tư, đã đạt được các kết quả sau:

Database
Hiểu cách cài đặt và cấu hình MySQL/PostgreSQL trên Docker

Nắm được cách sử dụng EXPLAIN để phân tích và tối ưu truy vấn SQL

Hiểu các cấp độ Normalization (1NF, 2NF, 3NF, BCNF)

Nắm được các chiến lược Indexing (B-Tree, Hash, Composite, Covering)

Hiểu các đặc tính ACID và Transaction Isolation Levels

Biết cách thiết lập Isolation Level trong Spring

Logging
Hiểu các Logging Frameworks: SLF4J, Logback, Log4j2

Nắm được cách sử dụng Log Levels phù hợp

Biết cách triển khai Structured Logging với JSON format

Hiểu về Log Aggregation và Centralized Logging (ELK Stack, Loki Stack)

Nắm được các kỹ thuật tối ưu performance logging

I/O
Hiểu sự khác biệt giữa Blocking I/O và Non-blocking I/O

Nắm được cách sử dụng Java NIO.2 (AsynchronousFileChannel, AsynchronousSocketChannel)

Biết cách triển khai Event-driven File Processing với WatchService

Hiểu các High-performance I/O Patterns (Reactor, Proactor)

Nắm được kỹ thuật Memory-mapped Files và Zero-copy

Hiểu về Event Loop, Callback Hell và Reactive Streams


```bash
