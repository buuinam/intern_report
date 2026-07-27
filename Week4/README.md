# BÁO CÁO THỰC TẬP TUẦN 4

## Chủ đề: Database, Logging & I/O

**Intern:** Bùi Văn Nam  
**Team:** Platform - Adtech  
**Gmail:** buivannam13032004@gmail.com  
**Leader:** Nguyễn Văn Cương  

---

## 1. Mục tiêu tuần

Trong tuần thứ tư, theo roadmap mục tiêu là tìm hiểu các kiến thức về Database, Logging và I/O trong Java.

Nội dung học tập tập trung vào việc tìm hiểu cách cài đặt và cấu hình hệ quản trị cơ sở dữ liệu MySQL/PostgreSQL, tối ưu hóa câu lệnh SQL bằng EXPLAIN, các chiến lược Indexing và Database Normalization. Bên cạnh đó, tìm hiểu các thuộc tính ACID và các mức độ cô lập của Transaction.

Ngoài ra, đã nghiên cứu các Framework Logging phổ biến trong Java như SLF4J, Logback và Log4j2, cách sử dụng các Log Level, Structured Logging và các phương pháp quản lý Log tập trung.

Đối với I/O, đã tìm hiểu sự khác biệt giữa Blocking I/O và Non-blocking I/O, Java NIO.2, Event-driven File Processing, các mô hình High-performance I/O, Memory-mapped Files và Zero-copy Techniques.

### Lịch học Tuần 4

| Ngày | Nội dung học | Kết quả đạt được |
|---|---|---|
| Thứ 2 | Database Installation, Configuration & SQL Optimization | Hiểu cách cài đặt Database, tối ưu câu lệnh SQL và sử dụng EXPLAIN Plans. |
| Thứ 3 | Database Normalization, Indexing & Transactions | Hiểu Normalization, Indexing Strategies, ACID và Transaction Isolation Levels. |
| Thứ 4 | Logging Frameworks & Log Levels | Hiểu SLF4J, Logback, Log4j2, Log Levels và Appenders. |
| Thứ 5 | Structured Logging & Centralized Logging | Hiểu Structured Logging, JSON Format, Log Aggregation và Performance Impact. |
| Thứ 6 | Java I/O, NIO.2 & Async I/O | Hiểu Blocking/Non-blocking I/O, Event Loop, NIO Selector, Async File I/O và Zero-copy. |

---

## 2. Chi tiết nội dung đã học

## 2.1. Database

### a. MySQL/PostgreSQL Installation và Configuration

Đã tìm hiểu về việc cài đặt và cấu hình các hệ quản trị cơ sở dữ liệu MySQL và PostgreSQL.

Database Management System được sử dụng để lưu trữ, quản lý và truy xuất dữ liệu cho các ứng dụng.

Một số nội dung cấu hình cơ bản:

- Database Server.
- Database Port.
- Username và Password.
- Database Schema.
- Connection Configuration.
- Database Connection Pool.

Việc cấu hình Database phù hợp giúp ứng dụng có thể kết nối và thao tác với dữ liệu một cách ổn định.

### b. SQL Optimization và EXPLAIN Plans

Đã tìm hiểu các phương pháp tối ưu câu lệnh SQL và sử dụng `EXPLAIN` để phân tích cách Database thực thi Query.

`EXPLAIN` giúp cung cấp thông tin về Execution Plan của một câu lệnh SQL.

Thông qua Execution Plan có thể phân tích:

- Cách Database thực hiện Query.
- Bảng được truy cập.
- Index có được sử dụng hay không.
- Loại Join được sử dụng.
- Số lượng Row được quét.
- Chi phí thực thi của Query.

Việc sử dụng `EXPLAIN` giúp phát hiện các câu lệnh SQL có hiệu năng thấp và tìm ra hướng tối ưu phù hợp.

Một số phương pháp tối ưu SQL:

- Sử dụng Index phù hợp.
- Chỉ lấy các cột cần thiết thay vì sử dụng `SELECT *`.
- Tối ưu điều kiện `WHERE`.
- Hạn chế các Query không cần thiết.
- Tối ưu các câu lệnh JOIN.
- Phân tích Execution Plan trước và sau khi tối ưu.

### c. Database Normalization

Đã tìm hiểu về Database Normalization và mục đích chuẩn hóa dữ liệu trong cơ sở dữ liệu.

Normalization là quá trình tổ chức dữ liệu nhằm:

- Giảm dữ liệu trùng lặp.
- Hạn chế các vấn đề khi Insert, Update và Delete dữ liệu.
- Đảm bảo tính nhất quán của dữ liệu.
- Tổ chức các bảng và mối quan hệ một cách hợp lý.

Một số mức Normal Form phổ biến:

- **First Normal Form (1NF)**.
- **Second Normal Form (2NF)**.
- **Third Normal Form (3NF)**.

Việc chuẩn hóa Database giúp giảm sự dư thừa dữ liệu và nâng cao tính nhất quán của hệ thống.

### d. Indexing Strategies

Đã tìm hiểu về Index và các chiến lược sử dụng Index trong Database.

Index là một cấu trúc dữ liệu giúp Database tìm kiếm dữ liệu nhanh hơn mà không cần quét toàn bộ bảng.

Index thường được sử dụng cho các cột thường xuyên xuất hiện trong:

- `WHERE`.
- `JOIN`.
- `ORDER BY`.
- `GROUP BY`.

Một số lợi ích của Index:

- Tăng tốc độ truy vấn.
- Giảm số lượng dữ liệu cần quét.
- Cải thiện hiệu năng tìm kiếm.

Tuy nhiên, việc tạo quá nhiều Index cũng có thể làm tăng chi phí khi thực hiện các thao tác `INSERT`, `UPDATE` và `DELETE`.

Do đó, cần lựa chọn các cột cần Index dựa trên cách ứng dụng thực hiện truy vấn dữ liệu.

### e. ACID Properties

Đã tìm hiểu các thuộc tính ACID của Database Transaction.

ACID bao gồm:

- **Atomicity**: Transaction được thực hiện toàn bộ hoặc không thực hiện phần nào.
- **Consistency**: Dữ liệu luôn duy trì trạng thái hợp lệ trước và sau Transaction.
- **Isolation**: Các Transaction đồng thời không ảnh hưởng không mong muốn đến nhau.
- **Durability**: Dữ liệu đã Commit sẽ được đảm bảo lưu trữ kể cả khi hệ thống gặp sự cố.

Các thuộc tính ACID giúp đảm bảo tính chính xác và đáng tin cậy của dữ liệu trong các hệ thống Database.

### f. Transaction Isolation Levels

Đã tìm hiểu các mức độ cô lập của Transaction.

Transaction Isolation Level quy định mức độ mà một Transaction có thể nhìn thấy dữ liệu được thay đổi bởi các Transaction khác.

Các mức Isolation Level phổ biến:

- **Read Uncommitted**.
- **Read Committed**.
- **Repeatable Read**.
- **Serializable**.

Các vấn đề có thể xảy ra khi nhiều Transaction hoạt động đồng thời:

- **Dirty Read**: Đọc dữ liệu chưa được Commit.
- **Non-repeatable Read**: Cùng một Query nhưng trả về kết quả khác nhau trong cùng một Transaction.
- **Phantom Read**: Xuất hiện thêm các bản ghi mới khi thực hiện lại Query.

Việc lựa chọn Isolation Level phù hợp giúp cân bằng giữa tính nhất quán của dữ liệu và hiệu năng của hệ thống.

---

## 2.2. Logging

### a. Logging Frameworks

Đã tìm hiểu các Logging Framework phổ biến trong Java:

- **SLF4J**.
- **Logback**.
- **Log4j2**.

SLF4J cung cấp một Abstraction Layer cho Logging, cho phép ứng dụng sử dụng API Logging thống nhất và có thể thay đổi Implementation phía sau.

Logback và Log4j2 là các Logging Framework được sử dụng để thực hiện việc ghi Log.

Logging giúp theo dõi hoạt động của ứng dụng, phát hiện lỗi và hỗ trợ quá trình Debug cũng như Monitoring hệ thống.

### b. Log Levels

Đã tìm hiểu các Log Level và cách sử dụng phù hợp.

Các Log Level phổ biến:

- **TRACE**: Ghi lại thông tin chi tiết nhất để theo dõi quá trình xử lý.
- **DEBUG**: Sử dụng trong quá trình Debug và phát triển ứng dụng.
- **INFO**: Ghi lại các thông tin quan trọng trong quá trình hoạt động bình thường.
- **WARN**: Cảnh báo các tình huống bất thường nhưng hệ thống vẫn có thể tiếp tục hoạt động.
- **ERROR**: Ghi lại các lỗi xảy ra trong quá trình xử lý.

Việc lựa chọn Log Level phù hợp giúp giảm lượng Log không cần thiết và hỗ trợ việc theo dõi hệ thống hiệu quả hơn.

### c. Appenders

Đã tìm hiểu về Appender và vai trò của Appender trong Logging.

Appender xác định nơi mà Log được ghi tới.

Một số Appender phổ biến:

- **Console Appender**: Ghi Log ra Console.
- **File Appender**: Ghi Log vào File.
- **Rolling File Appender**: Tự động tạo File Log mới theo thời gian hoặc kích thước.
- **Async Appender**: Xử lý việc ghi Log bất đồng bộ để giảm ảnh hưởng đến Application Thread.

Việc lựa chọn Appender phụ thuộc vào mục đích sử dụng và yêu cầu của hệ thống.

### d. Log Patterns

Đã tìm hiểu về Log Pattern và cách định dạng nội dung Log.

Một Log Entry thường có thể bao gồm:

- Timestamp.
- Log Level.
- Thread Name.
- Class Name.
- Method Name.
- Message.

Ví dụ một Log Entry có thể chứa thông tin:

```text
2026-07-27 10:30:00 INFO [main] UserService - User login successfully
```

Việc chuẩn hóa Log Pattern giúp việc đọc, tìm kiếm và phân tích Log trở nên dễ dàng hơn.

### e. Structured Logging

Đã tìm hiểu về Structured Logging và cách biểu diễn Log dưới dạng các Key-Value Pair hoặc JSON Format.

Thay vì ghi Log dưới dạng một đoạn Text không có cấu trúc, Structured Logging giúp các thông tin trong Log được tổ chức rõ ràng.

Ví dụ:

```json
{
  "timestamp": "2026-07-27T10:30:00",
  "level": "INFO",
  "service": "user-service",
  "userId": "123",
  "message": "User login successfully"
}
```

Structured Logging giúp:

- Dễ dàng tìm kiếm Log.
- Dễ dàng phân tích dữ liệu.
- Hỗ trợ Log Aggregation.
- Phù hợp với các hệ thống Distributed System.

### f. Log Aggregation và Centralized Logging

Đã tìm hiểu về Log Aggregation và Centralized Logging.

Trong các hệ thống có nhiều Service, mỗi Service có thể tạo ra Log riêng. Việc lưu trữ Log phân tán gây khó khăn cho quá trình theo dõi và Debug.

Centralized Logging giúp thu thập Log từ nhiều Application hoặc Service về một hệ thống tập trung.

Các lợi ích:

- Theo dõi Log từ nhiều Service tại một nơi.
- Tìm kiếm và phân tích Log dễ dàng hơn.
- Hỗ trợ Debug các hệ thống Distributed.
- Dễ dàng xây dựng Monitoring và Alerting.

### g. Performance Impact của Logging

Đã tìm hiểu ảnh hưởng của Logging đến hiệu năng của ứng dụng.

Logging quá nhiều có thể gây:

- Tăng I/O.
- Tăng CPU Usage.
- Tăng Memory Usage.
- Tăng kích thước Log File.
- Làm giảm hiệu năng của Application.

Để hạn chế ảnh hưởng đến hiệu năng:

- Sử dụng Log Level phù hợp.
- Không ghi các thông tin không cần thiết.
- Sử dụng Async Logging khi phù hợp.
- Hạn chế việc tạo String không cần thiết khi Log Level không được bật.
- Sử dụng Log Rotation để kiểm soát kích thước Log.

---

## 2.3. I/O và Java NIO.2

### a. Blocking I/O và Non-blocking I/O

Đã tìm hiểu sự khác biệt giữa Blocking I/O và Non-blocking I/O.

**Blocking I/O** là mô hình trong đó Thread phải chờ cho đến khi thao tác I/O hoàn thành.

Ví dụ:

- Đọc File.
- Ghi File.
- Đọc dữ liệu từ Network.
- Gửi dữ liệu qua Socket.

Trong quá trình chờ, Thread có thể không thực hiện được các Task khác.

**Non-blocking I/O** cho phép Thread tiếp tục xử lý các công việc khác trong khi thao tác I/O đang được thực hiện.

So sánh:

| Đặc điểm | Blocking I/O | Non-blocking I/O |
|---|---|---|
| Thread | Phải chờ thao tác I/O hoàn thành | Có thể tiếp tục xử lý Task khác |
| Hiệu năng | Có thể giảm khi có nhiều Request | Phù hợp với nhiều kết nối đồng thời |
| Mô hình | Đơn giản hơn | Phức tạp hơn |
| Ứng dụng | Hệ thống đơn giản | Hệ thống có yêu cầu cao về Concurrency |

### b. Java NIO.2

Đã tìm hiểu Java NIO.2 và các API hỗ trợ xử lý I/O hiện đại trong Java.

Một số thành phần:

- `AsynchronousFileChannel`.
- `AsynchronousSocketChannel`.

`AsynchronousFileChannel` hỗ trợ thực hiện các thao tác đọc và ghi File bất đồng bộ.

`AsynchronousSocketChannel` hỗ trợ giao tiếp Network theo hướng bất đồng bộ.

Các API này giúp xây dựng các ứng dụng có khả năng xử lý nhiều thao tác I/O mà không cần Blocking Thread trong thời gian chờ.

### c. Event-driven File Processing

Đã tìm hiểu mô hình Event-driven File Processing.

Trong mô hình này, hệ thống thực hiện xử lý dựa trên các Event thay vì liên tục kiểm tra trạng thái của File.

Ví dụ:

```text
File Event
    ↓
Event Handler
    ↓
Process File
    ↓
Generate Result
```

Mô hình Event-driven giúp:

- Giảm việc Polling liên tục.
- Phản hồi nhanh hơn khi có Event.
- Tối ưu việc sử dụng tài nguyên.
- Phù hợp với các hệ thống xử lý dữ liệu theo Event.

### d. High-performance I/O Patterns

Đã tìm hiểu một số Pattern giúp nâng cao hiệu năng I/O.

Một số phương pháp:

- Sử dụng Non-blocking I/O.
- Xử lý bất đồng bộ.
- Sử dụng Buffer hiệu quả.
- Giảm số lần đọc và ghi dữ liệu.
- Sử dụng Batch Processing khi phù hợp.
- Tối ưu việc sử dụng Thread.
- Sử dụng Event-driven Architecture.

Mục tiêu của các Pattern này là giảm thời gian chờ và nâng cao khả năng xử lý đồng thời của hệ thống.

### e. Memory-mapped Files

Đã tìm hiểu Memory-mapped Files và cách ánh xạ File vào vùng nhớ của Process.

Memory-mapped File cho phép ứng dụng truy cập dữ liệu trong File thông qua vùng nhớ được ánh xạ.

Một số ưu điểm:

- Giảm số lần Copy dữ liệu.
- Có thể cải thiện hiệu năng khi xử lý File lớn.
- Cho phép truy cập dữ liệu giống như truy cập vùng nhớ.

Memory-mapped Files phù hợp với các ứng dụng cần xử lý lượng dữ liệu lớn hoặc truy cập File thường xuyên.

### f. Zero-copy Techniques

Đã tìm hiểu về Zero-copy và mục tiêu giảm số lần Copy dữ liệu giữa các vùng nhớ.

Trong quá trình xử lý I/O truyền thống, dữ liệu có thể phải được Copy qua nhiều vùng nhớ khác nhau trước khi đến nơi cần sử dụng.

Zero-copy giúp giảm các thao tác Copy không cần thiết.

Một ví dụ là cơ chế `sendfile()` trong hệ điều hành, cho phép truyền dữ liệu hiệu quả hơn giữa File và Network.

Lợi ích của Zero-copy:

- Giảm CPU Usage.
- Giảm số lần Copy dữ liệu.
- Giảm Memory Overhead.
- Cải thiện hiệu năng I/O.

---

## 2.4. Event Loop và Async I/O

### a. Event Loop Implementation

Đã tìm hiểu mô hình Event Loop và cách xử lý các Event.

Event Loop liên tục chờ và xử lý các Event phát sinh.

Mô hình cơ bản:

```text
Event Loop
    ↓
Wait for Event
    ↓
Receive Event
    ↓
Process Event
    ↓
Wait for Next Event
```

Event Loop có thể xử lý nhiều Event mà không cần tạo một Thread riêng cho từng Event.

Mô hình này giúp giảm chi phí tạo quá nhiều Thread và thường được sử dụng trong các hệ thống xử lý I/O bất đồng bộ.

### b. Callback Hell

Đã tìm hiểu vấn đề Callback Hell trong lập trình bất đồng bộ.

Callback Hell xảy ra khi nhiều Callback được lồng vào nhau, khiến Code:

- Khó đọc.
- Khó bảo trì.
- Khó Debug.
- Khó xử lý Error.

Một số giải pháp:

- Promises.
- `CompletableFuture`.
- Reactive Programming.

Việc sử dụng các mô hình xử lý bất đồng bộ hiện đại giúp cấu trúc Code rõ ràng và dễ quản lý hơn.

### c. Reactive Streams và Backpressure

Đã tìm hiểu Reactive Streams và khái niệm Backpressure.

Trong một hệ thống xử lý Stream, Producer có thể tạo dữ liệu nhanh hơn tốc độ Consumer xử lý.

Backpressure là cơ chế giúp Consumer thông báo khả năng xử lý của mình để kiểm soát tốc độ dữ liệu được truyền từ Producer.

Mục tiêu của Backpressure:

- Tránh Consumer bị quá tải.
- Kiểm soát tốc độ dữ liệu.
- Hạn chế Memory Overflow.
- Giúp hệ thống ổn định hơn.

### d. NIO Selector

Đã tìm hiểu `NIO Selector` và cơ chế Multiplexing nhiều Channel.

Selector cho phép một Thread theo dõi nhiều Channel và xử lý các Channel đã sẵn sàng cho các thao tác I/O.

Thay vì sử dụng một Thread cho mỗi Connection, một Thread có thể quản lý nhiều Connection.

Điều này giúp:

- Giảm số lượng Thread.
- Giảm Memory Usage.
- Tăng khả năng xử lý nhiều Connection đồng thời.

### e. Async File I/O

Đã tìm hiểu Async File I/O và cách thực hiện các thao tác File theo hướng bất đồng bộ.

Với Async File I/O, Application Thread không cần phải chờ trực tiếp cho đến khi thao tác đọc hoặc ghi File hoàn thành.

Khi thao tác hoàn thành, hệ thống có thể trả về kết quả thông qua Callback hoặc Completion Handler.

Điều này giúp cải thiện khả năng xử lý các tác vụ I/O trong các ứng dụng có yêu cầu cao về hiệu năng.

### f. Zero-copy và `sendfile()`

Đã tìm hiểu cơ chế Zero-copy và System Call `sendfile()`.

`sendfile()` cho phép truyền dữ liệu trực tiếp từ File đến Network Socket với số lần Copy dữ liệu ít hơn so với mô hình truyền thống.

Điều này giúp:

- Giảm số lần chuyển dữ liệu giữa User Space và Kernel Space.
- Giảm CPU Usage.
- Giảm Memory Copy.
- Tăng hiệu năng khi truyền File lớn.

---

## 3. Kết quả đạt được

Sau khi hoàn thành tuần học thứ tư, đã đạt được các kết quả sau:

- Hiểu cách cài đặt và cấu hình MySQL/PostgreSQL.
- Nắm được các phương pháp tối ưu SQL và sử dụng `EXPLAIN` để phân tích Execution Plan.
- Hiểu Database Normalization và mục đích giảm dữ liệu trùng lặp.
- Nắm được các Indexing Strategies và ảnh hưởng của Index đến hiệu năng Database.
- Hiểu các thuộc tính ACID của Transaction.
- Nắm được các Transaction Isolation Levels và các vấn đề Dirty Read, Non-repeatable Read và Phantom Read.
- Hiểu vai trò của Logging trong việc theo dõi và Debug Application.
- Nắm được các Logging Framework như SLF4J, Logback và Log4j2.
- Hiểu các Log Level gồm TRACE, DEBUG, INFO, WARN và ERROR.
- Nắm được các loại Appender như Console, File, Rolling File và Async.
- Hiểu Log Pattern và các thông tin thường xuất hiện trong Log.
- Nắm được Structured Logging và cách sử dụng JSON Format.
- Hiểu Log Aggregation và Centralized Logging trong các hệ thống Distributed.
- Nhận thức được ảnh hưởng của Logging đến Performance của Application.
- Hiểu sự khác biệt giữa Blocking I/O và Non-blocking I/O.
- Nắm được các thành phần cơ bản của Java NIO.2.
- Hiểu cách sử dụng AsynchronousFileChannel và AsynchronousSocketChannel.
- Nắm được khái niệm Event Loop và Event-driven Processing.
- Hiểu Callback Hell và các giải pháp như Promises, CompletableFuture và Reactive Programming.
- Nắm được khái niệm Reactive Streams và Backpressure.
- Hiểu cơ chế Multiplexing của NIO Selector.
- Nắm được Async File I/O và các High-performance I/O Patterns.
- Hiểu Memory-mapped Files và Zero-copy Techniques.
- Hiểu vai trò của `sendfile()` trong việc tối ưu truyền dữ liệu.
- Xây dựng được nền tảng về Database, Logging và High-performance I/O để tiếp tục phát triển các ứng dụng Backend có hiệu năng cao và khả năng mở rộng tốt.

---

## 4. Kế hoạch tuần 5

### Tuần 5: Spring Boot, REST API & Database Integration

#### Yêu cầu Spring Boot

- Spring Framework và Dependency Injection.
- Inversion of Control (IoC) và Application Context.
- Spring Boot Auto-configuration và Starter Dependencies.
- Spring MVC và RESTful API.
- Controller, Service, Repository và Entity.
- Spring Data JPA và Hibernate.

#### Yêu cầu REST API

- HTTP Methods và Status Codes.
- Request, Response và JSON.
- RESTful API Design.
- Exception Handling và Validation.
- Pagination và Sorting.
- API Documentation với Swagger/OpenAPI.

#### Yêu cầu Database Integration

- Kết nối Spring Boot với MySQL/PostgreSQL.
- Spring Data JPA.
- Entity Mapping.
- Repository và Query Methods.
- Transaction Management.
- Database Migration.
