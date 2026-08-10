# 📘 BÁO CÁO THỰC TẬP TUẦN 3

## Thông tin

* **Chủ đề:** Concurrency và Docker
* **Intern:** Bùi Văn Nam
* **Team:** Platform - Adtech
* **Gmail:** [buivannam13032004@gmail.com](mailto:buivannam13032004@gmail.com)
* **Leader:** Nguyễn Văn Cương

---

# 1. Mục tiêu tuần

Trong tuần thứ ba, theo roadmap, mục tiêu là tìm hiểu về **Concurrency trong Java** và **Docker**.

Đối với Concurrency, tập trung tìm hiểu cách Java quản lý Thread, Thread Lifecycle, ThreadPool, ExecutorService và các cơ chế đồng bộ hóa dữ liệu trong môi trường đa luồng.

Các nội dung chính:

* Thread Lifecycle và Thread Management.
* ThreadPool và ExecutorService.
* `synchronized`.
* `Lock`.
* Atomic Classes.
* CompletableFuture.
* Reactive Programming cơ bản.

Đối với Docker, mục tiêu là hiểu các khái niệm nền tảng về Container, Docker Architecture và cách đóng gói ứng dụng thành Docker Image.

Các nội dung chính:

* Container Concepts.
* Docker Architecture.
* Dockerfile.
* Image Layers.
* Image Optimization.
* Container Networking.
* Volumes.
* Docker Compose.
* Multi-container Applications.

Ngoài ra, em tìm hiểu sâu hơn về sự khác biệt giữa **Container và Virtual Machine**, Container Lifecycle, Networking và Storage trong Docker.

---

# 2. Lịch học Tuần 3

| Ngày      | Nội dung học                                       | Kết quả đạt được                                                                           |
| --------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Thứ 2** | Thread Lifecycle & Management                      | Hiểu vòng đời Thread, trạng thái Thread và cách tạo/quản lý Thread.                        |
| **Thứ 3** | ThreadPool & ExecutorService                       | Hiểu ThreadPool, ExecutorService và cách quản lý nhiều task đồng thời.                     |
| **Thứ 4** | Synchronization                                    | Hiểu `synchronized`, `Lock`, Atomic Classes và vấn đề Race Condition.                      |
| **Thứ 5** | CompletableFuture & Docker Fundamentals            | Hiểu xử lý bất đồng bộ và các khái niệm cơ bản của Docker.                                 |
| **Thứ 6** | Docker Architecture, Networking, Storage & Compose | Hiểu Dockerfile, Image Layers, Container Lifecycle, Networking, Volumes và Docker Compose. |

---

# 3. Chi tiết nội dung đã học

# 3.1. Java Concurrency

Concurrency là khả năng hệ thống thực hiện nhiều công việc có thể tiến triển đồng thời.

Trong Java, Concurrency được sử dụng để:

* Tận dụng CPU.
* Xử lý nhiều request đồng thời.
* Thực hiện các tác vụ nền.
* Cải thiện khả năng đáp ứng của ứng dụng.
* Xử lý các tác vụ I/O bất đồng bộ.

Tuy nhiên, lập trình Concurrent cũng phát sinh các vấn đề như:

* Race Condition.
* Deadlock.
* Data Race.
* Thread Starvation.
* Resource Contention.

---

# 3.2. Thread Lifecycle

Thread trong Java có các trạng thái được mô hình hóa bởi `Thread.State`.

Các trạng thái chính:

* `NEW`
* `RUNNABLE`
* `BLOCKED`
* `WAITING`
* `TIMED_WAITING`
* `TERMINATED`

Có thể mô hình hóa vòng đời Thread:

```text
NEW
 |
 | start()
 ↓
RUNNABLE
 |
 ├── BLOCKED
 |
 ├── WAITING
 |
 ├── TIMED_WAITING
 |
 ↓
TERMINATED
```

## NEW

Thread được tạo nhưng chưa gọi `start()`.

```java
Thread thread = new Thread();
```

## RUNNABLE

Thread đã được gọi `start()` và sẵn sàng được CPU scheduler thực thi.

## BLOCKED

Thread đang chờ lock để truy cập vào synchronized section.

## WAITING

Thread chờ một Thread khác thực hiện một hành động nhất định.

Ví dụ:

```java
thread.join();
```

## TIMED_WAITING

Thread chờ trong một khoảng thời gian xác định.

Ví dụ:

```java
Thread.sleep(1000);
```

## TERMINATED

Thread đã hoàn thành execution hoặc kết thúc do Exception.

---

# 3.3. Thread Management

Có nhiều cách làm việc với Thread trong Java.

Một cách cơ bản là tạo Thread:

```java
Thread thread = new Thread(() -> {
    System.out.println("Running");
});

thread.start();
```

Các method thường gặp:

```text
start()
run()
sleep()
join()
interrupt()
isAlive()
```

### start()

Bắt đầu thực thi Thread.

### run()

Chứa logic mà Thread thực hiện.

### sleep()

Tạm dừng Thread trong một khoảng thời gian.

### join()

Cho phép một Thread chờ Thread khác hoàn thành.

### interrupt()

Gửi yêu cầu interrupt tới Thread.

Qua nội dung này, em hiểu được cách tạo và quản lý Thread trong Java.

---

# 3.4. ThreadPool

Việc tạo quá nhiều Thread trực tiếp có thể gây ra:

* Tốn memory.
* Tốn thời gian tạo Thread.
* Context switching.
* Khó quản lý lifecycle.
* Có thể gây quá tải hệ thống.

ThreadPool giải quyết vấn đề bằng cách tái sử dụng một nhóm Thread để xử lý nhiều task.

Mô hình:

```text
Task 1 ─┐
Task 2 ─┤
Task 3 ─┼──→ Thread Pool ──→ Worker Threads
Task 4 ─┤
Task 5 ─┘
```

Lợi ích:

* Reuse Thread.
* Giới hạn số lượng Thread.
* Quản lý task tốt hơn.
* Giảm overhead khi tạo Thread.
* Kiểm soát resource tốt hơn.

---

# 3.5. ExecutorService

`ExecutorService` cung cấp API để quản lý ThreadPool và thực thi các task bất đồng bộ.

Ví dụ:

```java
ExecutorService executor =
        Executors.newFixedThreadPool(4);
```

Có thể submit task:

```java
executor.submit(() -> {
    // task
});
```

Sau khi hoàn thành công việc, cần shutdown:

```java
executor.shutdown();
```

Một số loại Executor phổ biến:

* `newFixedThreadPool()`
* `newSingleThreadExecutor()`
* `newScheduledThreadPool()`

ExecutorService giúp tách việc **submit task** khỏi việc trực tiếp quản lý Thread.

---

# 3.6. Synchronization

Khi nhiều Thread cùng truy cập và thay đổi một shared resource, có thể xảy ra **Race Condition**.

Ví dụ:

```text
Thread A ─┐
          ├──→ Shared Data
Thread B ─┘
```

Nếu không có cơ chế đồng bộ phù hợp, kết quả có thể không chính xác.

Các cơ chế được tìm hiểu:

* `synchronized`
* `Lock`
* Atomic Classes

---

# 3.7. synchronized

`synchronized` đảm bảo tại một thời điểm chỉ có Thread phù hợp được truy cập vào vùng code được bảo vệ bởi cùng một monitor/lock.

Ví dụ:

```java
public synchronized void increment() {
    count++;
}
```

Hoặc:

```java
synchronized (lock) {
    count++;
}
```

Ưu điểm:

* Dễ sử dụng.
* Code đơn giản.
* Java tự quản lý việc acquire/release monitor.

Hạn chế:

* Có thể giảm concurrency nếu lock quá rộng.
* Khó kiểm soát hơn trong các tình huống synchronization phức tạp.

---

# 3.8. Lock

Java cung cấp `Lock` trong package:

```text
java.util.concurrent.locks
```

Một implementation phổ biến:

```text
ReentrantLock
```

Ví dụ:

```java
Lock lock = new ReentrantLock();

lock.lock();

try {
    // critical section
} finally {
    lock.unlock();
}
```

So với `synchronized`, Lock cung cấp nhiều khả năng kiểm soát hơn:

* `tryLock()`.
* Có thể hỗ trợ interrupt khi chờ lock.
* Có thể quản lý lock rõ ràng hơn.

Tuy nhiên, cần đảm bảo luôn release lock, thường thông qua `finally`.

---

# 3.9. Atomic Classes

Atomic Classes cung cấp các thao tác thread-safe trên một số kiểu dữ liệu mà không cần sử dụng lock theo cách truyền thống.

Các class phổ biến:

* `AtomicInteger`
* `AtomicLong`
* `AtomicBoolean`
* `AtomicReference`

Ví dụ:

```java
AtomicInteger counter = new AtomicInteger();

counter.incrementAndGet();
```

Atomic Classes thường sử dụng các cơ chế atomic của CPU và JVM để thực hiện các thao tác hiệu quả trong nhiều trường hợp.

Ưu điểm:

* Thread-safe.
* Giảm nhu cầu sử dụng explicit lock.
* Phù hợp với các counter hoặc trạng thái đơn giản.

---

# 3.10. CompletableFuture

`CompletableFuture` hỗ trợ lập trình bất đồng bộ trong Java.

Cho phép:

* Chạy task asynchronous.
* Kết hợp nhiều task.
* Xử lý kết quả.
* Xử lý Exception.
* Xây dựng chuỗi asynchronous operations.

Ví dụ mô hình:

```text
Task A
  |
  ↓
Task B
  |
  ↓
Task C
```

Một số method quan trọng:

```text
supplyAsync()
runAsync()
thenApply()
thenAccept()
thenCompose()
thenCombine()
exceptionally()
handle()
```

Ví dụ:

```java
CompletableFuture
    .supplyAsync(() -> getUser())
    .thenApply(user -> processUser(user))
    .thenAccept(result -> save(result));
```

Qua nội dung này, em hiểu được cách xây dựng các workflow bất đồng bộ bằng Java.

---

# 3.11. Reactive Programming Basics

Reactive Programming là mô hình lập trình tập trung vào việc xử lý các dòng dữ liệu và sự kiện bất đồng bộ.

Các khái niệm cơ bản:

* Publisher.
* Subscriber.
* Stream.
* Event.
* Backpressure.

Mô hình cơ bản:

```text
Publisher
    |
    ↓
Stream
    |
    ↓
Subscriber
```

Reactive Programming phù hợp với:

* High-concurrency applications.
* Event-driven systems.
* Streaming data.
* Non-blocking applications.

---

# 4. Docker

# 4.1. Container Concepts

Container là một môi trường thực thi ứng dụng được cô lập ở mức hệ điều hành.

Container chứa:

* Application.
* Dependencies.
* Libraries.
* Configuration cần thiết.

Khác với Virtual Machine, Container không cần chạy một Guest Operating System đầy đủ cho từng application.

---

# 4.2. Container vs Virtual Machine

| Container               | Virtual Machine            |
| ----------------------- | -------------------------- |
| Chia sẻ OS Kernel       | Có Guest OS riêng          |
| Nhẹ hơn                 | Nặng hơn                   |
| Khởi động nhanh         | Khởi động chậm hơn         |
| Sử dụng ít resource hơn | Sử dụng nhiều resource hơn |
| Isolation ở mức OS      | Isolation ở mức VM         |
| Phù hợp Microservices   | Phù hợp full OS isolation  |

Có thể hình dung:

```text
Virtual Machine

Hardware
   ↓
Host OS
   ↓
Hypervisor
   ↓
Guest OS
   ↓
Application
```

Trong khi Container:

```text
Hardware
   ↓
Host OS
   ↓
Container Runtime
   ↓
Container
   ↓
Application
```

Container phù hợp với việc đóng gói và triển khai ứng dụng nhất quán giữa các môi trường.

---

# 4.3. Docker Architecture

Docker sử dụng kiến trúc Client - Server.

Các thành phần chính:

* Docker Client.
* Docker Daemon.
* Docker Registry.
* Docker Images.
* Docker Containers.

Mô hình:

```text
Docker Client
      |
      ↓
Docker Daemon
      |
      ├── Images
      ├── Containers
      ├── Networks
      └── Volumes
```

Docker Client gửi command tới Docker Daemon.

Docker Daemon chịu trách nhiệm quản lý:

* Container.
* Image.
* Network.
* Volume.

Docker Registry được sử dụng để lưu trữ và phân phối Docker Image.

---

# 4.4. Docker Image

Docker Image là template bất biến được sử dụng để tạo Container.

Image có thể chứa:

* Base OS layer.
* Runtime.
* Dependencies.
* Application.
* Configuration.

Ví dụ:

```text
Docker Image
    |
    ├── Base Image
    ├── Runtime
    ├── Dependencies
    └── Application
```

Một Image có thể được sử dụng để tạo nhiều Container.

---

# 4.5. Dockerfile

Dockerfile là file chứa các instruction để xây dựng Docker Image.

Một số instruction phổ biến:

```text
FROM
WORKDIR
COPY
ADD
RUN
ENV
EXPOSE
CMD
ENTRYPOINT
```

Ví dụ:

```dockerfile
FROM eclipse-temurin:21-jdk

WORKDIR /app

COPY target/app.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

Dockerfile giúp việc build application image trở nên có thể lặp lại và nhất quán.

---

# 4.6. Dockerfile Best Practices

Một số nguyên tắc:

* Sử dụng base image phù hợp.
* Ưu tiên image nhỏ.
* Sử dụng `.dockerignore`.
* Giảm số lượng layer không cần thiết.
* Không đưa secret vào image.
* Chạy application bằng non-root user khi phù hợp.
* Tối ưu thứ tự các instruction để tận dụng cache.
* Chỉ copy những file cần thiết.
* Sử dụng multi-stage build cho ứng dụng cần build trong Docker.

Ví dụ:

```text
Build Stage
    ↓
Compile Application
    ↓
Runtime Stage
    ↓
Run Application
```

Multi-stage build giúp giảm kích thước image runtime.

---

# 4.7. Image Layers

Docker Image được xây dựng từ nhiều layer.

Ví dụ:

```text
Application Layer
       ↓
Dependency Layer
       ↓
Runtime Layer
       ↓
Base Image Layer
```

Mỗi instruction trong Dockerfile có thể tạo ra một layer hoặc đóng góp vào filesystem của image.

Lợi ích:

* Có thể tái sử dụng layer.
* Giảm thời gian build.
* Tiết kiệm bandwidth.
* Hỗ trợ image caching.

---

# 4.8. Union Filesystem

Docker sử dụng cơ chế filesystem theo layer.

Các layer có thể được kết hợp để tạo thành filesystem mà Container nhìn thấy.

Có thể hình dung:

```text
Layer 4 - Application
Layer 3 - Dependencies
Layer 2 - Runtime
Layer 1 - Base Image
---------------------
Container Filesystem
```

Các image layer thường có tính chất read-only.

Container có thêm một writable layer ở phía trên để lưu các thay đổi runtime.

---

# 4.9. Image Layer Caching

Docker có thể cache các layer đã được build trước đó.

Ví dụ:

```dockerfile
COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn package
```

Nếu chỉ thay đổi source code, các layer dependency phía trước có thể được reuse.

Do đó thứ tự Dockerfile có ảnh hưởng đến thời gian build.

---

# 4.10. Container Lifecycle

Một Container có các trạng thái/lifecycle cơ bản:

```text
Created
   ↓
Running
   ↓
Stopped
   ↓
Removed
```

Các command:

```bash
docker create
docker start
docker stop
docker restart
docker rm
```

Ngoài ra:

```bash
docker run
```

thường kết hợp quá trình tạo và khởi động Container.

---

# 4.11. Docker Networking

Docker cung cấp networking để các Container giao tiếp với nhau hoặc với bên ngoài.

Một số loại network:

* Bridge.
* Host.
* Overlay.

---

## Bridge Network

Là network phổ biến cho các Container chạy trên cùng một Docker Host.

```text
Container A
     |
     ↓
  Bridge
     ↑
     |
Container B
```

Các Container trên cùng network có thể giao tiếp với nhau theo cơ chế network của Docker.

---

## Host Network

Container sử dụng trực tiếp network namespace của Host.

Ưu điểm:

* Giảm một lớp network abstraction.

Nhược điểm:

* Isolation về network thấp hơn.
* Phụ thuộc network của Host.

---

## Overlay Network

Overlay Network được sử dụng để kết nối Container giữa nhiều Docker Host.

Phù hợp với:

* Distributed applications.
* Docker Swarm.
* Multi-host networking.

---

# 4.12. Docker Storage

Container có filesystem riêng nhưng dữ liệu trong writable layer không phù hợp để lưu trữ dữ liệu cần tồn tại lâu dài.

Docker cung cấp các cơ chế:

* Bind Mount.
* Volume.
* tmpfs.

---

## Bind Mount

Bind Mount ánh xạ trực tiếp một thư mục/file trên Host vào Container.

Mô hình:

```text
Host Directory
      |
      ↓
Container Directory
```

Phù hợp khi cần chia sẻ file giữa Host và Container.

---

## Volume

Docker Volume được Docker quản lý và lưu trữ.

Mô hình:

```text
Container
    |
    ↓
Docker Volume
```

Volume phù hợp để lưu dữ liệu persistent như:

* Database.
* Uploaded files.
* Application data.

---

## tmpfs

`tmpfs` lưu dữ liệu trong memory của Host.

Đặc điểm:

* Không lưu persistent khi Container dừng/xóa.
* Tốc độ nhanh.
* Phù hợp với dữ liệu tạm thời.

---

# 4.13. Docker Compose

Docker Compose được sử dụng để định nghĩa và quản lý các ứng dụng gồm nhiều Container.

Ví dụ một hệ thống Backend:

```text
          Docker Compose
                |
      ┌─────────┴─────────┐
      ↓                   ↓
  Backend API          MySQL
      |
      ↓
   Network
```

Một ứng dụng có thể gồm:

* Backend.
* Database.
* Redis.
* Message Broker.

Docker Compose cho phép định nghĩa các Service trong file:

```text
docker-compose.yml
```

Ví dụ:

```yaml
services:
  app:
    build: .
    ports:
      - "8080:8080"
    depends_on:
      - db

  db:
    image: mysql:8
```

Lợi ích:

* Dễ quản lý nhiều Container.
* Dễ thiết lập Network.
* Dễ cấu hình Volume.
* Dễ khởi động toàn bộ hệ thống.
* Phù hợp với môi trường Development và Testing.

---

# 5. Kết quả đạt được

Sau tuần thứ ba, em đã đạt được các kết quả:

## Concurrency

* Hiểu khái niệm Concurrency.
* Nắm được Thread Lifecycle.
* Hiểu các trạng thái của Thread.
* Biết cách tạo và quản lý Thread.
* Hiểu ThreadPool.
* Biết sử dụng ExecutorService.
* Hiểu vấn đề Race Condition.
* Nắm được cơ chế `synchronized`.
* Hiểu cách sử dụng `Lock`.
* Biết mục đích của Atomic Classes.
* Hiểu CompletableFuture.
* Nắm được những khái niệm cơ bản của Reactive Programming.

## Docker

* Hiểu Container và Container Runtime.
* Phân biệt Container và Virtual Machine.
* Hiểu Docker Architecture.
* Hiểu Docker Client và Docker Daemon.
* Hiểu Docker Image và Container.
* Biết cấu trúc Dockerfile.
* Hiểu Dockerfile Best Practices.
* Hiểu Image Layers và Layer Caching.
* Nắm được Container Lifecycle.
* Hiểu Docker Networking.
* Phân biệt Bridge, Host và Overlay Network.
* Hiểu Bind Mount, Volume và tmpfs.
* Hiểu cách Docker Compose quản lý Multi-container Application.

Qua tuần thứ ba, em đã có nền tảng về xử lý đồng thời trong Java và bước đầu hiểu được quy trình đóng gói, chạy và quản lý Backend Application bằng Docker.

---

# 6. Khó khăn và hướng khắc phục

Trong quá trình học tập, em gặp một số khó khăn:

* Thread Lifecycle có nhiều trạng thái và cần hiểu rõ điều kiện chuyển trạng thái.
* Race Condition và Synchronization khá khó hình dung nếu chỉ học lý thuyết.
* Việc lựa chọn giữa `synchronized`, `Lock` và Atomic Classes phụ thuộc vào từng bài toán.
* CompletableFuture có nhiều API nên cần thời gian để hiểu cách kết hợp các asynchronous task.
* Docker có nhiều khái niệm mới như Image, Container, Layer, Network và Volume.
* Việc phân biệt Container với Virtual Machine ban đầu chưa thực sự rõ ràng.
* Docker Networking và Storage cần kết hợp giữa kiến thức lý thuyết và thực hành.
* Docker Compose yêu cầu hiểu đồng thời Container, Network, Volume và Service.

Để khắc phục, em tiếp tục:

* Đọc tài liệu về Java Concurrency.
* Phân tích Thread Lifecycle.
* So sánh các cơ chế Synchronization.
* Tìm hiểu cách ExecutorService quản lý ThreadPool.
* Thực hành xây dựng Docker Image.
* Phân tích Dockerfile.
* Tìm hiểu cách Container giao tiếp thông qua Network.
* Tìm hiểu cách Persistent Data được quản lý bằng Volume.
* Sử dụng Docker Compose để mô hình hóa hệ thống nhiều Service.

---

# 7. Kế hoạch Tuần 4

Trong tuần thứ tư, nội dung học tập sẽ tập trung vào **Database, Logging và I/O**.

## 7.1. Database

Các nội dung dự kiến:

* MySQL/PostgreSQL Installation và Configuration.
* SQL Optimization.
* `EXPLAIN` Plans.
* Database Normalization.
* Indexing Strategies.
* ACID Properties.
* Transaction.
* Transaction Isolation Levels.

Mục tiêu:

* Hiểu cách Database lưu trữ và xử lý dữ liệu.
* Biết phân tích SQL Query.
* Hiểu Execution Plan.
* Biết cách sử dụng Index phù hợp.
* Hiểu Normalization.
* Hiểu Transaction và ACID.
* Nắm được các mức Transaction Isolation.

---

## 7.2. Logging

Các nội dung dự kiến:

* SLF4J.
* Logback.
* Log4j2.
* Log Levels.
* Structured Logging.
* JSON Logging.
* Log Aggregation.
* Centralized Logging.
* Performance Impact của Logging.

Đồng thời tìm hiểu:

* TRACE.
* DEBUG.
* INFO.
* WARN.
* ERROR.
* Console Appender.
* File Appender.
* Rolling File Appender.
* Async Appender.
* Log Pattern.

---

## 7.3. I/O

Các nội dung dự kiến:

* Blocking I/O.
* Non-blocking I/O.
* Java NIO.2.
* `AsynchronousFileChannel`.
* `AsynchronousSocketChannel`.
* Event-driven File Processing.
* High-performance I/O.
* Memory-mapped Files.
* Zero-copy Techniques.

Ngoài ra tìm hiểu:

* Event Loop.
* Callback Hell.
* CompletableFuture.
* Reactive Streams.
* Backpressure.
* NIO Selector.
* Async File I/O.
* `sendfile()`.

---

# 8. Kết luận

Tuần thứ ba giúp em mở rộng kiến thức từ Java Core sang các vấn đề quan trọng trong phát triển Backend hiện đại.

Về **Concurrency**, em đã tìm hiểu Thread Lifecycle, ThreadPool, ExecutorService, Synchronization, Lock, Atomic Classes và CompletableFuture. Qua đó hiểu được cách xử lý nhiều tác vụ đồng thời và những vấn đề cần quan tâm khi nhiều Thread cùng truy cập tài nguyên.

Về **Docker**, em đã tìm hiểu các khái niệm nền tảng về Container, Docker Architecture, Docker Image, Dockerfile, Image Layers, Container Lifecycle, Networking và Storage. Đồng thời hiểu được cách sử dụng Docker Compose để quản lý hệ thống gồm nhiều Container.

Những kiến thức này tạo nền tảng quan trọng để tiếp tục tìm hiểu về **Database, Logging và High-performance I/O** trong tuần thứ tư, đồng thời chuẩn bị cho việc triển khai các ứng dụng Backend trong môi trường thực tế.
