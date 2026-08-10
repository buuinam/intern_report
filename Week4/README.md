# 📘 BÁO CÁO THỰC TẬP TUẦN 4

## Thông tin

* **Chủ đề:** Database, Logging & I/O
* **Intern:** Bùi Văn Nam
* **Team:** Platform - Adtech
* **Gmail:** [buivannam13032004@gmail.com](mailto:buivannam13032004@gmail.com)
* **Leader:** Nguyễn Văn Cương

---

# 1. Mục tiêu tuần

Trong tuần thứ tư, theo roadmap, mục tiêu là tìm hiểu ba nhóm kiến thức quan trọng trong phát triển Backend gồm **Database, Logging và I/O**.

Đối với Database, tập trung tìm hiểu cách cài đặt và cấu hình MySQL/PostgreSQL, tối ưu câu lệnh SQL, phân tích Execution Plan bằng `EXPLAIN`, Database Normalization, Indexing và Transaction.

Đối với Logging, tìm hiểu các Logging Framework phổ biến trong Java như:

* SLF4J.
* Logback.
* Log4j2.

Đồng thời tìm hiểu cách phân loại Log Level, cấu hình Appender, Structured Logging, Log Aggregation và ảnh hưởng của Logging đến Performance.

Đối với I/O, tập trung tìm hiểu sự khác nhau giữa Blocking I/O và Non-blocking I/O, Java NIO.2, Asynchronous I/O, Event Loop, Reactive Streams, NIO Selector, Memory-mapped Files và Zero-copy.

Mục tiêu chung của tuần là hiểu cách Backend Application giao tiếp với Database, ghi nhận và quản lý Log, đồng thời xử lý I/O hiệu quả trong các hệ thống có yêu cầu cao về hiệu năng.

---

# 2. Lịch học Tuần 4

| Ngày      | Nội dung học                             | Kết quả đạt được                                                                       |
| --------- | ---------------------------------------- | -------------------------------------------------------------------------------------- |
| **Thứ 2** | MySQL/PostgreSQL & Database Fundamentals | Hiểu cách cài đặt, cấu hình Database và các khái niệm cơ bản.                          |
| **Thứ 3** | SQL Optimization, EXPLAIN & Indexing     | Hiểu Execution Plan, Index và các kỹ thuật tối ưu SQL.                                 |
| **Thứ 4** | Normalization, ACID & Transactions       | Hiểu Normalization, Transaction và Isolation Levels.                                   |
| **Thứ 5** | Logging Frameworks & Structured Logging  | Hiểu SLF4J, Logback, Log4j2, Log Levels, Appenders và JSON Logging.                    |
| **Thứ 6** | I/O, Event Loop & Async I/O              | Phân biệt Blocking/Non-blocking I/O, tìm hiểu NIO.2, Selector, Async I/O và Zero-copy. |

---

# 3. Chi tiết nội dung đã học

# 3.1. Database

Database là thành phần quan trọng trong Backend Application, chịu trách nhiệm lưu trữ và quản lý dữ liệu.

Trong tuần này, em tập trung tìm hiểu:

* MySQL.
* PostgreSQL.
* SQL Optimization.
* EXPLAIN.
* Normalization.
* Indexing.
* Transaction.
* ACID.
* Transaction Isolation.

---

# 3.2. MySQL và PostgreSQL

MySQL và PostgreSQL đều là các hệ quản trị cơ sở dữ liệu quan hệ phổ biến.

Database sử dụng:

* Table.
* Row.
* Column.
* Primary Key.
* Foreign Key.
* Constraint.
* Index.

Mô hình cơ bản:

```text
Database
   |
   ├── Table
   │     ├── Row
   │     └── Column
   |
   ├── Index
   |
   └── Constraint
```

---

## MySQL

MySQL là hệ quản trị cơ sở dữ liệu quan hệ phổ biến, thường được sử dụng trong các ứng dụng Web và Backend.

Các nội dung tìm hiểu:

* Cài đặt Database Server.
* Tạo Database.
* Tạo User.
* Phân quyền.
* Tạo Table.
* Thực hiện CRUD.
* Kết nối Application với Database.

---

## PostgreSQL

PostgreSQL là hệ quản trị cơ sở dữ liệu quan hệ có nhiều tính năng mạnh về:

* SQL.
* Transaction.
* Data Integrity.
* Extensibility.
* Complex Queries.

Trong quá trình học, em tìm hiểu cách cài đặt, cấu hình và kết nối PostgreSQL với ứng dụng Backend.

---

# 3.3. SQL Optimization

Khi dữ liệu trong Database tăng lên, các câu SQL đơn giản có thể trở nên chậm nếu không được thiết kế và tối ưu đúng cách.

Một số nguyên nhân:

* Query không sử dụng Index.
* Quét quá nhiều dữ liệu.
* JOIN không tối ưu.
* SELECT quá nhiều Column.
* Sử dụng điều kiện không phù hợp.
* Index không phù hợp.
* Thiết kế Database chưa tối ưu.

Một số nguyên tắc:

* Chỉ SELECT các column cần thiết.
* Sử dụng WHERE phù hợp.
* Tối ưu JOIN.
* Sử dụng Index đúng trường hợp.
* Phân tích Execution Plan.
* Tránh truy vấn dữ liệu không cần thiết.

---

# 3.4. EXPLAIN Plans

`EXPLAIN` được sử dụng để phân tích cách Database thực hiện một câu SQL.

Ví dụ:

```sql
EXPLAIN
SELECT *
FROM users
WHERE email = 'user@example.com';
```

Execution Plan có thể cung cấp thông tin về:

* Access Type.
* Index được sử dụng.
* Số dòng dự kiến được scan.
* Join strategy.
* Estimated cost.

Có thể sử dụng Execution Plan để xác định các vấn đề như:

* Full Table Scan.
* Index không được sử dụng.
* Join không hiệu quả.
* Quét quá nhiều dữ liệu.

Qua đó, em hiểu rằng tối ưu SQL không chỉ dựa vào việc viết câu lệnh ngắn mà cần phân tích cách Database thực thi câu lệnh.

---

# 3.5. Database Indexing

Index là cấu trúc dữ liệu giúp Database tìm kiếm dữ liệu nhanh hơn.

Không có Index:

```text
Query
  ↓
Scan Table
  ↓
Check từng Row
```

Có Index:

```text
Query
  ↓
Index
  ↓
Find vị trí dữ liệu
  ↓
Table
```

Một số loại Index phổ biến:

* B-Tree Index.
* Composite Index.
* Unique Index.

Index đặc biệt hữu ích đối với các Column thường xuyên xuất hiện trong:

* WHERE.
* JOIN.
* ORDER BY.
* GROUP BY.

---

## Trade-off của Index

Index giúp tăng tốc đọc dữ liệu nhưng cũng có chi phí:

* Tốn Storage.
* Tăng thời gian INSERT.
* Tăng thời gian UPDATE.
* Tăng thời gian DELETE.
* Database phải duy trì Index khi dữ liệu thay đổi.

Do đó không nên tạo Index một cách tùy tiện.

---

# 3.6. Database Normalization

Normalization là quá trình tổ chức dữ liệu nhằm:

* Giảm Duplicate Data.
* Tránh Data Anomaly.
* Cải thiện Data Integrity.

Một số Normal Form quan trọng:

* 1NF.
* 2NF.
* 3NF.

---

## First Normal Form - 1NF

Dữ liệu phải có:

* Giá trị Atomic.
* Không chứa nhóm dữ liệu lặp trong một field.
* Mỗi row có thể xác định rõ.

---

## Second Normal Form - 2NF

Database cần thỏa mãn 1NF và các thuộc tính không khóa phải phụ thuộc đầy đủ vào toàn bộ khóa chính.

---

## Third Normal Form - 3NF

Database cần thỏa mãn 2NF và các thuộc tính không khóa không được phụ thuộc bắc cầu vào khóa chính.

---

## Lợi ích của Normalization

* Giảm dữ liệu trùng lặp.
* Dễ duy trì dữ liệu.
* Giảm các Data Anomaly.
* Cải thiện tính nhất quán.

Tuy nhiên, trong một số hệ thống yêu cầu hiệu năng đọc cao, có thể sử dụng Denormalization có kiểm soát.

---

# 3.7. Transaction

Transaction là một nhóm các thao tác Database được thực hiện như một đơn vị logic.

Ví dụ chuyển tiền:

```text
Transaction
   |
   ├── Trừ tiền tài khoản A
   |
   └── Cộng tiền tài khoản B
```

Hai thao tác cần được xử lý nhất quán.

Nếu một bước thất bại, transaction có thể được Rollback.

Các thao tác cơ bản:

```text
BEGIN
COMMIT
ROLLBACK
```

---

# 3.8. ACID Properties

ACID gồm:

* Atomicity.
* Consistency.
* Isolation.
* Durability.

---

## Atomicity

Transaction được thực hiện toàn bộ hoặc không thực hiện.

```text
All
 ↓
Commit

Hoặc

None
 ↓
Rollback
```

---

## Consistency

Database phải chuyển từ một trạng thái hợp lệ sang một trạng thái hợp lệ khác.

---

## Isolation

Các transaction đồng thời không được gây ra kết quả không hợp lệ do nhìn thấy trạng thái trung gian của nhau.

---

## Durability

Sau khi transaction được Commit, dữ liệu phải được đảm bảo tồn tại ngay cả khi hệ thống gặp sự cố.

---

# 3.9. Transaction Isolation Levels

Isolation Level quy định mức độ một transaction có thể nhìn thấy thay đổi của transaction khác.

Các mức phổ biến:

* READ UNCOMMITTED.
* READ COMMITTED.
* REPEATABLE READ.
* SERIALIZABLE.

Các vấn đề liên quan:

### Dirty Read

Một transaction đọc dữ liệu chưa được transaction khác commit.

### Non-repeatable Read

Cùng một query trong một transaction nhưng trả về kết quả khác nhau do transaction khác đã commit thay đổi.

### Phantom Read

Một query được thực hiện nhiều lần và xuất hiện thêm hoặc mất các row do transaction khác thay đổi dữ liệu.

Có thể hình dung:

```text
READ UNCOMMITTED
       ↓
READ COMMITTED
       ↓
REPEATABLE READ
       ↓
SERIALIZABLE
```

Mức Isolation càng cao thường càng tăng tính nhất quán nhưng có thể làm giảm concurrency.

---

# 4. Logging

Logging là quá trình ghi lại các thông tin về hoạt động của ứng dụng.

Logging giúp:

* Debug.
* Monitoring.
* Troubleshooting.
* Audit.
* Phân tích lỗi.
* Theo dõi hệ thống Production.

---

# 4.1. SLF4J

SLF4J là abstraction layer cho Java Logging.

Có thể hình dung:

```text
Application
     |
     ↓
   SLF4J
     |
     ├── Logback
     └── Log4j2
```

Application sử dụng API của SLF4J thay vì phụ thuộc trực tiếp vào một Logging Implementation cụ thể.

Điều này giúp giảm coupling và dễ thay đổi Logging Framework.

---

# 4.2. Logback

Logback là một Logging Framework phổ biến trong Java.

Các thành phần quan trọng:

* Logger.
* Appender.
* Encoder.
* Pattern.
* Level.

Logback thường được sử dụng cùng SLF4J trong các ứng dụng Java/Spring Boot.

---

# 4.3. Log4j2

Log4j2 cũng là một Logging Framework phổ biến trong hệ sinh thái Java.

Một số đặc điểm:

* Hiệu năng tốt.
* Có nhiều cấu hình.
* Hỗ trợ Async Logging.
* Hỗ trợ nhiều Appender.
* Hỗ trợ Structured Logging.

---

# 4.4. Log Levels

Các Log Level được tìm hiểu:

```text
TRACE
  ↓
DEBUG
  ↓
INFO
  ↓
WARN
  ↓
ERROR
```

---

## TRACE

Mức chi tiết rất cao.

Thường sử dụng khi cần theo dõi flow rất chi tiết trong quá trình debug.

---

## DEBUG

Thông tin phục vụ Debug và phân tích behavior của ứng dụng.

---

## INFO

Thông tin về hoạt động bình thường của hệ thống.

Ví dụ:

```text
Application started
User logged in
Order created
```

---

## WARN

Thông báo về tình huống bất thường nhưng hệ thống vẫn có thể tiếp tục hoạt động.

---

## ERROR

Thông báo lỗi nghiêm trọng hoặc Exception xảy ra.

---

# 4.5. Appropriate Log Level

Việc chọn Log Level phù hợp rất quan trọng.

Không nên:

* Ghi mọi thứ ở ERROR.
* Ghi dữ liệu nhạy cảm.
* Ghi quá nhiều thông tin ở INFO.
* Sử dụng DEBUG/TRACE không kiểm soát trong Production.

Nên sử dụng:

```text
TRACE → Chi tiết cực cao
DEBUG → Debug
INFO  → Hoạt động bình thường
WARN  → Bất thường
ERROR → Lỗi
```

---

# 4.6. Appenders

Appender xác định Log được ghi đi đâu.

Các loại:

* Console.
* File.
* Rolling File.
* Async.

---

## Console Appender

Ghi Log ra Console.

Phù hợp:

* Development.
* Container environment.

---

## File Appender

Ghi Log vào File.

Phù hợp khi cần lưu trữ Log trên filesystem.

---

## Rolling File Appender

Cho phép tạo File Log mới dựa trên:

* Kích thước.
* Thời gian.

Ví dụ:

```text
application.log
application.2026-08-01.log
application.2026-08-02.log
```

Giúp tránh một Log File phát triển không giới hạn.

---

## Async Appender

Logging được thực hiện bất đồng bộ.

Mục tiêu:

* Giảm ảnh hưởng của Logging lên thread xử lý request.
* Cải thiện performance trong hệ thống có lượng Log lớn.

---

# 4.7. Log Patterns

Log Pattern quy định format của Log.

Một Log có thể chứa:

```text
Timestamp
Thread
Log Level
Class
Message
Exception
```

Ví dụ:

```text
2026-08-10 10:20:30
[http-nio-8080-exec-1]
INFO
UserService
User created successfully
```

Các thông tin này giúp xác định:

* Khi nào xảy ra lỗi.
* Thread nào xử lý.
* Class nào tạo Log.
* Nội dung sự kiện.

---

# 4.8. Structured Logging

Structured Logging lưu Log dưới dạng dữ liệu có cấu trúc thay vì chỉ là text tự do.

Ví dụ JSON:

```json
{
  "timestamp": "2026-08-10T10:20:30Z",
  "level": "INFO",
  "service": "user-service",
  "userId": "123",
  "event": "user_created"
}
```

Ưu điểm:

* Dễ parse.
* Dễ tìm kiếm.
* Dễ filter.
* Phù hợp với Log Aggregation.
* Phù hợp với hệ thống phân tán.

---

# 4.9. Key-Value Logging

Structured Logging thường sử dụng các cặp:

```text
key = value
```

Ví dụ:

```text
service=user-service
userId=123
action=create
status=success
```

Các trường dữ liệu có cấu trúc giúp hệ thống Logging dễ dàng:

* Search.
* Filter.
* Aggregate.
* Analyze.

---

# 4.10. Log Aggregation

Trong hệ thống có nhiều Server/Container, việc đọc Log từ từng máy sẽ rất khó khăn.

Mô hình:

```text
Application A ─┐
Application B ─┼──→ Log Aggregation
Application C ─┘          |
                           ↓
                    Centralized Storage
                           |
                           ↓
                       Monitoring
```

Log Aggregation giúp tập trung Log từ nhiều Application/Server vào một hệ thống chung.

Lợi ích:

* Search Log tập trung.
* Phân tích lỗi.
* Monitoring.
* Correlation giữa các Service.

---

# 4.11. Centralized Logging

Centralized Logging đặc biệt quan trọng trong Microservices.

Ví dụ:

```text
Service A ─┐
Service B ─┼──→ Central Logging
Service C ─┘
```

Thay vì phải truy cập từng Service để kiểm tra Log, Developer có thể tìm kiếm Log tại một hệ thống tập trung.

---

# 4.12. Performance Impact của Logging

Logging cũng tiêu tốn tài nguyên.

Các chi phí:

* CPU.
* Memory.
* Disk I/O.
* Network I/O.
* Serialization.

Nếu Logging quá nhiều có thể ảnh hưởng Performance của Application.

Do đó cần:

* Chọn Log Level phù hợp.
* Không Log dữ liệu không cần thiết.
* Sử dụng Async Logging khi phù hợp.
* Sử dụng Structured Logging.
* Quản lý Log Rotation.
* Không ghi thông tin nhạy cảm.

---

# 5. I/O

I/O là hoạt động trao đổi dữ liệu giữa Application và các resource bên ngoài như:

* File.
* Network.
* Database.
* Socket.

Trong Backend, I/O thường là một trong những yếu tố ảnh hưởng đáng kể đến Performance.

---

# 5.1. Blocking I/O

Trong Blocking I/O, Thread sẽ chờ cho đến khi thao tác I/O hoàn thành.

Mô hình:

```text
Thread
  |
  ↓
I/O Operation
  |
  | waiting
  ↓
Result
```

Trong thời gian chờ, Thread không thể thực hiện công việc khác theo flow đó.

Ưu điểm:

* Dễ hiểu.
* Dễ lập trình.

Nhược điểm:

* Tốn Thread khi có nhiều I/O.
* Khả năng scale có thể hạn chế.

---

# 5.2. Non-blocking I/O

Non-blocking I/O cho phép Thread tiếp tục xử lý công việc khác trong khi I/O chưa hoàn thành.

Mô hình:

```text
Thread
  |
  ├── Start I/O
  |
  ├── Process Task B
  |
  ├── Process Task C
  |
  └── Handle I/O Result
```

Ưu điểm:

* Sử dụng Thread hiệu quả hơn.
* Phù hợp với lượng lớn I/O operations.
* Hỗ trợ high concurrency.

Nhược điểm:

* Kiến trúc phức tạp hơn.
* Khó debug hơn.
* Cần quản lý asynchronous flow.

---

# 5.3. Java NIO.2

Java NIO.2 cung cấp API cho các thao tác I/O hiện đại hơn.

Các thành phần:

* `Path`
* `Files`
* `AsynchronousFileChannel`
* `AsynchronousSocketChannel`

NIO.2 hỗ trợ:

* File I/O.
* Network I/O.
* Asynchronous Operations.

---

# 5.4. AsynchronousFileChannel

`AsynchronousFileChannel` cho phép thực hiện các thao tác đọc/ghi File bất đồng bộ.

Thay vì:

```text
Thread
 ↓
Read File
 ↓
Wait
 ↓
Result
```

Có thể:

```text
Thread
 ↓
Start Read
 ↓
Continue Other Work
 ↓
Callback / Completion
```

Điều này phù hợp với các ứng dụng cần xử lý nhiều File I/O.

---

# 5.5. AsynchronousSocketChannel

`AsynchronousSocketChannel` hỗ trợ thao tác Socket bất đồng bộ.

Có thể sử dụng cho các ứng dụng cần:

* Network Communication.
* High Concurrency.
* Asynchronous Request Processing.

---

# 5.6. Event-driven File Processing

Event-driven processing là mô hình xử lý dựa trên sự kiện.

Ví dụ:

```text
File Created
     ↓
Event
     ↓
File Processor
     ↓
Read Data
     ↓
Process
     ↓
Save Result
```

Thay vì liên tục kiểm tra filesystem, application có thể phản ứng khi có event phù hợp.

---

# 5.7. Event Loop

Event Loop là mô hình xử lý các Event trong một vòng lặp.

Mô hình:

```text
        ┌───────────────┐
        ↓               |
   Event Queue          |
        ↓               |
   Event Loop ──────────┘
        |
        ↓
   Process Event
```

Một Event Loop có thể xử lý nhiều Event trên một Thread hoặc một nhóm Thread nhỏ.

Đặc điểm quan trọng:

* Event được đưa vào Queue.
* Event Loop lấy Event.
* Xử lý Event.
* Tiếp tục lấy Event tiếp theo.

Mô hình này đặc biệt hữu ích trong hệ thống Event-driven và Non-blocking I/O.

---

# 5.8. Single-threaded Event Processing

Trong mô hình Single-threaded Event Loop, một Thread chịu trách nhiệm xử lý tuần tự các Event.

Ưu điểm:

* Đơn giản hóa một số vấn đề concurrency.
* Không cần lock cho mọi thao tác trong cùng Event Loop.

Nhược điểm:

* Một task blocking có thể làm toàn bộ Event Loop bị chậm.
* Task CPU-intensive cần được xử lý cẩn thận.

Do đó Event Loop thường cần kết hợp với Non-blocking I/O.

---

# 5.9. Callback Hell

Khi các asynchronous operation được lồng vào nhau quá nhiều callback, code có thể trở nên khó đọc.

Ví dụ mô hình:

```text
Callback A
   |
   └── Callback B
          |
          └── Callback C
                 |
                 └── Callback D
```

Đây được gọi là Callback Hell.

Một số giải pháp:

* Promise/Future.
* CompletableFuture.
* Reactive Programming.
* Async/Await ở các ngôn ngữ hỗ trợ.

Trong Java, `CompletableFuture` có thể giúp xây dựng asynchronous flow dễ đọc hơn so với callback lồng nhau.

---

# 5.10. Reactive Streams

Reactive Streams là mô hình xử lý asynchronous stream dữ liệu.

Các khái niệm:

* Publisher.
* Subscriber.
* Subscription.
* Processor.
* Backpressure.

Mô hình:

```text
Publisher
    |
    ↓
Subscription
    |
    ↓
Subscriber
```

---

# 5.11. Backpressure

Backpressure xảy ra khi Producer tạo dữ liệu nhanh hơn Consumer có thể xử lý.

Ví dụ:

```text
Producer
  |
  | 1000 events/s
  ↓
Queue
  |
  | 100 events/s
  ↓
Consumer
```

Nếu không có cơ chế kiểm soát, Queue có thể tăng kích thước và dẫn đến:

* Memory pressure.
* Latency tăng.
* Out of Memory.

Backpressure giúp Consumer kiểm soát tốc độ dữ liệu được gửi đến.

---

# 5.12. NIO Selector

`Selector` cho phép một Thread theo dõi nhiều Channel.

Mô hình:

```text
              ┌── Channel A
              |
Selector ─────┼── Channel B
              |
              ├── Channel C
              |
              └── Channel D
```

Thay vì mỗi Connection cần một Thread riêng, một Thread có thể multiplex nhiều Channel.

Đây là nền tảng quan trọng của nhiều mô hình Non-blocking Network I/O.

---

# 5.13. Multiplexing

Multiplexing cho phép một Thread theo dõi nhiều I/O Channel.

Thay vì:

```text
Thread A → Channel A
Thread B → Channel B
Thread C → Channel C
Thread D → Channel D
```

Có thể:

```text
              ┌→ Channel A
              ├→ Channel B
Event Loop ───┼→ Channel C
              └→ Channel D
```

Điều này giúp giảm số lượng Thread cần thiết trong các hệ thống có nhiều connection.

---

# 5.14. Memory-Mapped Files

Memory-mapped File cho phép map nội dung File vào vùng nhớ của Process.

Có thể hình dung:

```text
File
  |
  ↓
Memory Mapping
  |
  ↓
Process Memory Address Space
```

Application có thể truy cập dữ liệu thông qua memory mapping thay vì thực hiện các thao tác read/write truyền thống theo cách thông thường.

Phù hợp với:

* File lớn.
* Random Access.
* High-performance File Processing.

---

# 5.15. Zero-Copy

Zero-copy là kỹ thuật giảm việc sao chép dữ liệu không cần thiết giữa các vùng memory trong quá trình truyền dữ liệu.

Trong mô hình truyền thống có thể xảy ra nhiều bước:

```text
Disk
 ↓
Kernel Buffer
 ↓
User Space
 ↓
Kernel Buffer
 ↓
Network
```

Zero-copy cố gắng giảm các lần copy không cần thiết.

Một cơ chế nổi tiếng trên Linux là:

```text
sendfile()
```

Mục tiêu:

* Giảm CPU overhead.
* Giảm Memory Copy.
* Tăng Throughput.
* Cải thiện hiệu năng truyền File.

Zero-copy thường hữu ích trong:

* File Server.
* Web Server.
* Network Applications.
* High-throughput Systems.

---

# 6. Kết quả đạt được

Sau tuần thứ tư, em đã đạt được các kết quả:

## Database

* Hiểu các khái niệm cơ bản của MySQL và PostgreSQL.
* Biết cách cài đặt và cấu hình Database.
* Hiểu SQL Optimization.
* Biết sử dụng `EXPLAIN` để phân tích Query Plan.
* Hiểu Database Index.
* Biết các chiến lược Indexing cơ bản.
* Hiểu Database Normalization.
* Nắm được 1NF, 2NF và 3NF.
* Hiểu Transaction.
* Nắm được ACID Properties.
* Hiểu Transaction Isolation Levels.
* Biết các vấn đề Dirty Read, Non-repeatable Read và Phantom Read.

## Logging

* Hiểu vai trò của Logging trong Backend.
* Hiểu SLF4J.
* Hiểu Logback.
* Hiểu Log4j2.
* Nắm được các Log Level.
* Biết cách lựa chọn Log Level phù hợp.
* Hiểu Console, File, Rolling File và Async Appender.
* Hiểu Log Pattern.
* Hiểu Structured Logging.
* Biết cách biểu diễn Log dưới dạng JSON.
* Hiểu Log Aggregation và Centralized Logging.
* Nhận thức được ảnh hưởng của Logging đến Performance.

## I/O

* Phân biệt Blocking I/O và Non-blocking I/O.
* Hiểu Java NIO.2.
* Biết vai trò của `AsynchronousFileChannel`.
* Hiểu `AsynchronousSocketChannel`.
* Hiểu Event-driven Processing.
* Nắm được Event Loop.
* Hiểu Callback Hell.
* Biết vai trò của CompletableFuture trong Async Programming.
* Hiểu Reactive Streams và Backpressure.
* Hiểu NIO Selector và Multiplexing.
* Biết khái niệm Memory-mapped Files.
* Hiểu Zero-copy và `sendfile()`.

Qua tuần thứ tư, em đã có nền tảng tốt hơn về Database, Logging và các cơ chế I/O hiệu năng cao, đây là những kiến thức quan trọng đối với Backend Developer.

---

# 7. Khó khăn và hướng khắc phục

Trong quá trình học tập, em gặp một số khó khăn:

* Execution Plan của Database có nhiều thông tin và cần thời gian để hiểu.
* Việc lựa chọn Index phù hợp cần cân nhắc giữa tốc độ đọc và chi phí ghi dữ liệu.
* Transaction Isolation có nhiều mức và các vấn đề như Dirty Read, Phantom Read khá khó phân biệt.
* Logging Framework có nhiều thành phần như Logger, Appender, Pattern và Encoder.
* Structured Logging và Centralized Logging cần kết hợp nhiều thành phần của hệ thống.
* Non-blocking I/O có flow phức tạp hơn Blocking I/O.
* Event Loop, Selector và Reactive Streams yêu cầu hiểu cả Concurrency và Asynchronous Programming.
* Zero-copy và Memory-mapped Files liên quan đến cách hệ điều hành quản lý Memory và I/O nên cần nghiên cứu thêm.

Để khắc phục, em tiếp tục đọc tài liệu, phân tích Execution Plan, tìm hiểu các mô hình I/O và so sánh giữa các phương pháp xử lý để hiểu rõ ưu nhược điểm của từng kỹ thuật.

---

# 8. Kế hoạch Tuần 5

Trong tuần thứ năm, nội dung học tập sẽ tập trung vào **Spring Boot và Middleware**, đặc biệt là **Authentication và Rate Limiting**.

## 8.1. Spring Boot

Các nội dung dự kiến:

* Spring Boot Architecture.
* Auto-configuration.
* Dependency Injection.
* IoC Container.
* Spring MVC.
* Request Lifecycle.
* RESTful API Design.
* Configuration Properties.
* Profiles.

Mục tiêu:

* Hiểu kiến trúc Spring Boot.
* Hiểu IoC và Dependency Injection.
* Nắm được Request Lifecycle.
* Biết xây dựng RESTful API.
* Biết quản lý Configuration.
* Hiểu cách sử dụng Profiles cho các môi trường khác nhau.

---

## 8.2. Authentication

Các nội dung dự kiến:

* Session-based Authentication.
* Cookie-based Authentication.
* Token-based Authentication.
* JWT.
* OAuth2.
* OIDC.
* API Key.
* mTLS.
* Stateless vs Stateful Authentication.
* Spring Security Filter Chain.
* `SecurityFilterChain`.
* Access Token.
* Refresh Token.
* Token Revocation.
* Redis Blacklist.
* RBAC.
* ABAC.
* `@PreAuthorize`.

---

## 8.3. Rate Limiting

Các nội dung dự kiến:

* Fixed Window.
* Sliding Window.
* Token Bucket.
* Leaky Bucket.
* Bucket4j.
* Redis-based Distributed Rate Limiting.
* API Gateway Rate Limiting.
* Spring Cloud Gateway.
* Nginx.
* Kong.
* Rate Limiting theo User/IP/API Key.
* HTTP `429 Too Many Requests`.
* `X-RateLimit-*` Headers.

Mục tiêu là hiểu cách bảo vệ Backend API trước quá nhiều request, đồng thời đảm bảo hệ thống có khả năng scale trong môi trường nhiều instance.

---

# 9. Kết luận

Tuần thứ tư giúp em hiểu sâu hơn về ba thành phần quan trọng trong Backend là **Database, Logging và I/O**.

Về **Database**, em đã tìm hiểu cách cấu hình MySQL/PostgreSQL, tối ưu SQL bằng `EXPLAIN`, Indexing, Normalization, Transaction và ACID.

Về **Logging**, em đã tìm hiểu SLF4J, Logback, Log4j2, Log Levels, Appenders, Log Patterns và Structured Logging. Đồng thời hiểu vai trò của Log Aggregation và Centralized Logging trong các hệ thống phân tán.

Về **I/O**, em đã phân biệt Blocking và Non-blocking I/O, tìm hiểu Java NIO.2, Asynchronous I/O, Event Loop, Reactive Streams, Backpressure, NIO Selector, Memory-mapped Files và Zero-copy.

Những kiến thức này là nền tảng quan trọng để bước sang tuần thứ năm, tập trung vào **Spring Boot, Spring Security, Authentication và Rate Limiting**, từ đó áp dụng các kiến thức đã học vào xây dựng Backend API có khả năng bảo mật và chịu tải tốt hơn.
