# BÁO CÁO THỰC TẬP TUẦN 6

## Chủ đề: ORM & Connection Pool

**Intern:** Bùi Văn Nam
**Team:** Platform - Adtech
**Gmail:** [buivannam13032004@gmail.com](mailto:buivannam13032004@gmail.com)
**Leader:** Nguyễn Văn Cương

---

## 1. Mục tiêu tuần

Trong tuần thứ sáu, theo roadmap mục tiêu là tìm hiểu các kiến thức về **ORM (Object-Relational Mapping)** và **Connection Pool** trong Java Backend.

Nội dung học tập tập trung vào JPA/Hibernate Fundamentals, Entity Mapping và Relationships, Repository Pattern và các phương pháp Query Optimization, Performance Tuning.

Đối với ORM, đã tìm hiểu kiến trúc Hibernate với các thành phần SessionFactory, Session và Transaction. Bên cạnh đó, nghiên cứu Entity Lifecycle gồm Transient, Persistent, Detached và Removed, cũng như sự khác biệt giữa Lazy Loading và Eager Loading.

Ngoài ra, đã tìm hiểu vấn đề **N+1 Query Problem**, các phương pháp phát hiện và xử lý như Batch Fetching và Join Fetching. Đồng thời tìm hiểu các cơ chế Caching trong Hibernate gồm First-level Cache, Second-level Cache và Query Cache.

Đối với Connection Pool, đã tìm hiểu cách Hibernate tích hợp với HikariCP, các cấu hình Pool Size, Connection Timeout và Idle Timeout. Bên cạnh đó, nghiên cứu Connection Leak, Pool Monitoring, Deadlock Prevention và các công thức lựa chọn Connection Pool Size phù hợp với hệ thống.

### Lịch học Tuần 6

| **Ngày** | **Nội dung học**                                    | **Kết quả đạt được**                                                                             |
| -------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Thứ 2    | JPA/Hibernate Fundamentals & Hibernate Architecture | Hiểu ORM, JPA/Hibernate và kiến trúc SessionFactory, Session, Transaction.                       |
| Thứ 3    | Entity Mapping, Relationships & Entity Lifecycle    | Hiểu Entity Mapping, các Relationship và vòng đời Entity.                                        |
| Thứ 4    | Lazy/Eager Loading, N+1 Query & Query Optimization  | Hiểu Loading Strategies, N+1 Query Problem và các phương pháp tối ưu Query.                      |
| Thứ 5    | Hibernate Caching & Transaction Management          | Hiểu First-level, Second-level, Query Cache và `@Transactional`.                                 |
| Thứ 6    | HikariCP & Connection Pool Optimization             | Hiểu Connection Pool Configuration, Monitoring, Deadlock Prevention và Performance Optimization. |

---

## 2. Chi tiết nội dung đã học

## 2.1. ORM và JPA/Hibernate

### a. ORM Fundamentals

Đã tìm hiểu về ORM (Object-Relational Mapping) và vai trò của ORM trong các ứng dụng Java Backend.

ORM là kỹ thuật ánh xạ các Object trong Application với các Table trong Relational Database.

Thay vì trực tiếp thực hiện SQL cho từng thao tác Database, Developer có thể thao tác thông qua các Java Object và ORM Framework.

Mô hình cơ bản:

```text
Java Object
    |
    | ORM
    v
Database Table
```

Ví dụ:

```text
User Object
    |
    v
users Table

User.id       → users.id
User.name     → users.name
User.email    → users.email
```

Một số lợi ích của ORM:

* Giảm lượng SQL phải viết thủ công.
* Mapping Object với Database.
* Hỗ trợ quản lý Relationship giữa các Entity.
* Hỗ trợ Transaction Management.
* Hỗ trợ Caching.
* Tăng khả năng tái sử dụng Code.

### b. JPA và Hibernate

Đã tìm hiểu sự khác biệt giữa JPA và Hibernate.

**JPA (Jakarta Persistence API)** là Specification cung cấp các chuẩn để thực hiện ORM trong Java.

**Hibernate** là một ORM Framework triển khai JPA và cung cấp thêm nhiều tính năng mở rộng.

Mối quan hệ:

```text
JPA
 |
 | Specification
 v
Hibernate
 |
 | Implementation
 v
Database
```

Một số Annotation thường sử dụng:

* `@Entity`
* `@Table`
* `@Id`
* `@GeneratedValue`
* `@Column`
* `@OneToOne`
* `@OneToMany`
* `@ManyToOne`
* `@ManyToMany`

---

## 2.2. Hibernate Architecture

### a. SessionFactory

Đã tìm hiểu về `SessionFactory` trong Hibernate Architecture.

`SessionFactory` là thành phần được sử dụng để tạo và quản lý các `Session`.

Đặc điểm:

* Thường được tạo một lần trong Application.
* Thread-safe.
* Có thể được sử dụng bởi nhiều Thread.
* Quản lý Metadata và Configuration của Hibernate.

Mô hình:

```text
Application
     |
     v
SessionFactory
     |
     +---- Session
     |
     +---- Session
     |
     +---- Session
```

### b. Session

`Session` đại diện cho một phiên làm việc giữa Application và Database.

Session được sử dụng để:

* Load Entity.
* Save Entity.
* Update Entity.
* Delete Entity.
* Execute Query.

Thông thường mỗi Database Operation hoặc Transaction sẽ sử dụng một Session phù hợp với Lifecycle của Operation.

### c. Transaction

Transaction đảm bảo một nhóm các Database Operation được thực hiện theo một đơn vị logic.

Ví dụ:

```text
Transaction
   |
   +---- Insert Order
   |
   +---- Insert Order Detail
   |
   +---- Update Product Stock
   |
   v
Commit
```

Nếu xảy ra lỗi:

```text
Transaction
   |
   +---- Operation 1
   +---- Operation 2
   +---- Error
          |
          v
       Rollback
```

Transaction giúp đảm bảo tính nhất quán của dữ liệu.

---

## 2.3. Entity Mapping

### a. Entity

Đã tìm hiểu cách Mapping Java Class với Database Table thông qua `@Entity`.

Ví dụ:

```java id="h6r1zw"
@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    private String email;
}
```

Trong ví dụ trên:

* `User` là Entity.
* `users` là Database Table.
* `id` là Primary Key.
* Các Field được Mapping với các Column tương ứng.

### b. Relationships

Đã tìm hiểu các Relationship phổ biến trong JPA/Hibernate:

* One-to-One.
* One-to-Many.
* Many-to-One.
* Many-to-Many.

Ví dụ:

```text
User
 |
 | 1
 |
 | *
 v
Order
```

Một User có thể có nhiều Order.

Trong JPA có thể Mapping:

```java id="apx7c1"
@OneToMany(mappedBy = "user")
private List<Order> orders;
```

Relationship Mapping giúp Hibernate quản lý mối quan hệ giữa các Entity và Database Table.

### c. Repository Pattern

Đã tìm hiểu Repository Pattern và cách sử dụng Repository trong Spring Data JPA.

Repository chịu trách nhiệm giao tiếp với Database và tách Database Access Logic khỏi Business Logic.

Mô hình:

```text
Controller
    |
    v
Service
    |
    v
Repository
    |
    v
Hibernate
    |
    v
Database
```

Ví dụ:

```java id="j8f7os"
@Repository
public interface UserRepository
        extends JpaRepository<User, Long> {

    Optional<User> findByEmail(String email);
}
```

Spring Data JPA có thể tự động tạo implementation cho các Repository Interface.

---

## 2.4. Entity Lifecycle

Đã tìm hiểu Entity Lifecycle trong Hibernate.

Một Entity có thể trải qua các trạng thái:

```text
Transient
    |
    v
Persistent
    |
    v
Detached
    |
    v
Removed
```

### a. Transient

Entity vừa được tạo bằng `new` nhưng chưa được Hibernate quản lý.

```java id="0e7y7k"
User user = new User();
user.setName("Nam");
```

Entity lúc này chưa được liên kết với Persistence Context.

### b. Persistent

Entity được Hibernate quản lý bởi Persistence Context.

Ví dụ sau khi Entity được `persist` hoặc được Load từ Database, Entity có thể ở trạng thái Persistent.

```text id="r0w7q3"
Persistence Context
        |
        v
     Entity
```

Các thay đổi trên Persistent Entity có thể được Hibernate theo dõi và đồng bộ xuống Database.

### c. Detached

Entity đã từng được quản lý bởi Persistence Context nhưng không còn được quản lý nữa.

```text id="bq7y1j"
Persistent
    |
    | Session closed
    v
Detached
```

### d. Removed

Entity được đánh dấu để xóa khỏi Database.

```text id="b9z1fu"
Persistent
    |
    | remove()
    v
Removed
```

Entity sẽ được xóa khi Transaction được Flush/Commit phù hợp.

---

## 2.5. Lazy Loading và Eager Loading

### a. Lazy Loading

Lazy Loading chỉ tải dữ liệu Relationship khi dữ liệu thực sự được truy cập.

Ví dụ:

```text id="m3x0ms"
Load User
    |
    v
User loaded
    |
    | Access orders
    v
Load Orders
```

Ưu điểm:

* Giảm dữ liệu được Load ban đầu.
* Giảm thời gian Query ban đầu.
* Tiết kiệm Memory.

Nhược điểm:

* Có thể phát sinh nhiều Query.
* Có thể dẫn đến N+1 Query Problem.
* Có thể gặp lỗi khi truy cập Lazy Relationship ngoài Persistence Context.

### b. Eager Loading

Eager Loading tải Relationship ngay khi Entity được Load.

```text id="k9x8cn"
Load User
    |
    +---- Load User
    |
    +---- Load Orders
```

Ưu điểm:

* Dữ liệu Relationship có sẵn ngay.
* Tránh một số vấn đề liên quan đến Lazy Loading.

Nhược điểm:

* Có thể Load nhiều dữ liệu không cần thiết.
* Tăng thời gian Query.
* Tăng Memory Usage.

### c. So sánh

| Đặc điểm        | Lazy Loading           | Eager Loading                  |
| --------------- | ---------------------- | ------------------------------ |
| Load dữ liệu    | Khi cần                | Ngay lập tức                   |
| Initial Query   | Nhẹ hơn                | Nặng hơn                       |
| Memory          | Thấp hơn               | Cao hơn                        |
| Query phát sinh | Có thể nhiều           | Thường ít hơn                  |
| Performance     | Tốt nếu sử dụng hợp lý | Có thể giảm nếu Load quá nhiều |

Việc lựa chọn Lazy hoặc Eager Loading cần dựa trên Use Case và cách Application truy cập dữ liệu.

---

## 2.6. N+1 Query Problem

### a. Khái niệm

Đã tìm hiểu N+1 Query Problem, một vấn đề phổ biến khi sử dụng ORM.

N+1 xảy ra khi Application thực hiện:

* 1 Query để lấy danh sách Entity.
* N Query tiếp theo để lấy Relationship của từng Entity.

Ví dụ:

```text
1 Query:
SELECT * FROM users;

N Query:
SELECT * FROM orders WHERE user_id = 1;
SELECT * FROM orders WHERE user_id = 2;
SELECT * FROM orders WHERE user_id = 3;
...
```

Nếu có 100 User:

```text
1 + 100 = 101 Queries
```

Điều này có thể làm giảm Performance đáng kể.

### b. Detection

Có thể phát hiện N+1 Query thông qua:

* SQL Logs.
* Hibernate Statistics.
* Application Monitoring.
* Database Monitoring.
* Kiểm tra số lượng Query được thực hiện trong một Request.

Ví dụ:

```text
Expected:
1 - 2 Queries

Actual:
101 Queries
```

### c. Join Fetching

Một phương pháp xử lý N+1 là sử dụng Join Fetch.

Ví dụ:

```java id="5ob1es"
@Query("""
    SELECT u
    FROM User u
    JOIN FETCH u.orders
""")
List<User> findUsersWithOrders();
```

Thay vì thực hiện nhiều Query, Hibernate có thể lấy User và Orders trong cùng một Query phù hợp.

```text
User + Orders
      |
      v
   JOIN FETCH
      |
      v
  Database
```

### d. Batch Fetching

Một phương pháp khác là sử dụng Batch Fetching để giảm số lượng Query.

Thay vì:

```text
User 1 → Query
User 2 → Query
User 3 → Query
User 4 → Query
```

có thể gom nhiều Entity vào Batch:

```text
Batch
 |
 +---- User 1
 +---- User 2
 +---- User 3
 +---- User 4
```

Batch Fetching giúp giảm số lượng Database Round-trip và cải thiện Performance.

---

## 2.7. Hibernate Caching

Đã tìm hiểu các cơ chế Caching trong Hibernate.

Các loại Cache chính:

* First-level Cache.
* Second-level Cache.
* Query Cache.

### a. First-level Cache

First-level Cache nằm trong Persistence Context của một `Session`.

```text
Session
   |
   +---- First-level Cache
   |
   +---- Entity
```

First-level Cache được bật mặc định trong Hibernate.

Nếu cùng một Entity được truy cập nhiều lần trong cùng Session, Hibernate có thể sử dụng Entity đã được Cache thay vì thực hiện lại Query Database.

### b. Second-level Cache

Second-level Cache được chia sẻ giữa nhiều Session.

```text
        Session 1
           |
           |
        Session 2
           |
           v
   Second-level Cache
```

Second-level Cache có thể giúp giảm số lượng Database Query khi nhiều Session truy cập cùng dữ liệu.

Tuy nhiên cần cân nhắc:

* Cache Invalidation.
* Memory Usage.
* Dữ liệu thay đổi thường xuyên.
* Cache Consistency.

### c. Query Cache

Query Cache lưu kết quả của Query để có thể sử dụng lại trong các trường hợp phù hợp.

Query Cache cần được sử dụng cẩn thận vì dữ liệu Query có thể thay đổi và cần đảm bảo Cache được Invalidate đúng cách.

---

## 2.8. Transaction Management

### a. `@Transactional`

Đã tìm hiểu cách sử dụng `@Transactional` trong Spring để quản lý Transaction.

Ví dụ:

```java id="r5f0te"
@Transactional
public void createOrder(Order order) {

    orderRepository.save(order);

    productService.updateStock(order);
}
```

Các thao tác trong Method có thể được thực hiện trong cùng một Transaction.

Nếu xảy ra lỗi phù hợp với Transaction Policy:

```text
Operation 1
    |
Operation 2
    |
  Error
    |
    v
Rollback
```

### b. Transaction Propagation

Đã tìm hiểu Transaction Propagation, quy định cách một Method tham gia vào Transaction hiện tại.

Một số Propagation phổ biến:

* `REQUIRED`.
* `REQUIRES_NEW`.
* `SUPPORTS`.
* `MANDATORY`.
* `NOT_SUPPORTED`.
* `NEVER`.
* `NESTED`.

Trong đó `REQUIRED` thường được sử dụng để:

* Tham gia Transaction hiện tại nếu tồn tại.
* Tạo Transaction mới nếu chưa có.

### c. Transaction Isolation

Đã tìm hiểu Transaction Isolation và cách kiểm soát việc các Transaction đồng thời nhìn thấy dữ liệu của nhau.

Các Isolation Level phổ biến:

* Read Uncommitted.
* Read Committed.
* Repeatable Read.
* Serializable.

Việc lựa chọn Isolation Level cần cân bằng giữa:

* Data Consistency.
* Concurrency.
* Database Performance.

---

# 3. Connection Pool

## 3.1. Connection Pool Fundamentals

Đã tìm hiểu Connection Pool và vai trò của Connection Pool trong ứng dụng Backend.

Thay vì mỗi Request tạo một Database Connection mới:

```text
Request
   |
   v
Create Connection
   |
   v
Database
   |
   v
Close Connection
```

Connection Pool duy trì một tập hợp Connection có thể tái sử dụng:

```text
          Application
               |
               v
        +--------------+
        | Connection   |
        |    Pool      |
        +--------------+
         |  |  |  |  |
         v  v  v  v  v
        DB Connections
```

Khi Application cần Database Connection:

```text
Pool
 |
 | Borrow
 v
Connection
 |
 | Use
 v
Database
 |
 | Return
 v
Pool
```

Connection Pool giúp giảm chi phí tạo và đóng Connection liên tục.

---

## 3.2. HikariCP

Đã tìm hiểu HikariCP, một Connection Pool phổ biến trong các ứng dụng Spring Boot.

HikariCP quản lý các Database Connection và cung cấp Connection cho Application khi cần.

Một số Configuration quan trọng:

* `maximumPoolSize`.
* `minimumIdle`.
* `connectionTimeout`.
* `idleTimeout`.
* `maxLifetime`.

Ví dụ:

```yaml id="4v8xbi"
spring:
  datasource:
    hikari:
      maximum-pool-size: 10
      minimum-idle: 5
      connection-timeout: 30000
      idle-timeout: 600000
      max-lifetime: 1800000
```

---

## 3.3. HikariCP Pool Sizing

Đã tìm hiểu cách lựa chọn Pool Size phù hợp.

Nếu Pool Size quá nhỏ:

```text
Many Requests
      |
      v
Small Pool
      |
      v
Waiting for Connection
```

Có thể dẫn đến:

* Connection Wait Time tăng.
* Request Latency tăng.
* Throughput giảm.

Nếu Pool Size quá lớn:

```text
Large Pool
    |
    v
Too many DB Connections
    |
    v
Database Overload
```

Có thể gây:

* Database quá tải.
* Tăng Memory Usage.
* Tăng Context Switching.
* Giảm Performance.

Do đó cần lựa chọn Pool Size phù hợp với Application và Database.

---

## 3.4. Connection Timeout và Idle Timeout

### Connection Timeout

`connectionTimeout` xác định thời gian tối đa mà Application chờ để lấy Connection từ Pool.

Nếu không có Connection khả dụng trong khoảng thời gian này, Request có thể nhận Timeout Exception.

```text
Request
   |
   v
Connection Pool
   |
   | Waiting
   |
   +---- Connection available → Continue
   |
   +---- Timeout → Error
```

### Idle Timeout

`idleTimeout` xác định thời gian một Connection không được sử dụng trước khi có thể bị loại khỏi Pool, tùy theo cấu hình Pool.

Việc cấu hình hợp lý giúp cân bằng giữa:

* Resource Usage.
* Connection Availability.
* Performance.

---

## 3.5. Connection Pool Monitoring

Đã tìm hiểu việc Monitoring Connection Pool để phát hiện các vấn đề về Database Connection.

Một số Metrics cần theo dõi:

* Active Connections.
* Idle Connections.
* Total Connections.
* Pending Threads.
* Connection Acquisition Time.
* Connection Timeout.
* Connection Leak.

Mô hình:

```text
Application
    |
    v
HikariCP
    |
    +---- Active Connections
    |
    +---- Idle Connections
    |
    +---- Waiting Threads
    |
    +---- Timeout
    |
    v
Database
```

Monitoring giúp phát hiện các vấn đề về Pool Size, Connection Leak và Database Performance.

---

## 3.6. Connection Leak

Connection Leak xảy ra khi Application lấy Connection từ Pool nhưng không trả lại Connection sau khi sử dụng.

Ví dụ:

```text
Pool
 |
 | Borrow
 v
Connection
 |
 | Application Error
 |
 X
 |
Connection không được Return
```

Nếu xảy ra nhiều lần:

```text
Connection Pool
      |
      v
Connections bị giữ
      |
      v
Pool cạn Connection
      |
      v
Requests phải chờ
      |
      v
Timeout
```

Connection Leak có thể gây ảnh hưởng nghiêm trọng đến Performance và Availability của Application.

Do đó cần Monitoring và đảm bảo Connection/Resource được quản lý đúng Lifecycle.

---

## 3.7. Deadlock Prevention

Đã tìm hiểu công thức lựa chọn Connection Pool Size để tránh Deadlock trong một số trường hợp:

```text
pool_size = Tn × (Cm - 1) + 1
```

Trong đó:

* `Tn`: Maximum Threads.
* `Cm`: Maximum Connections per Thread.

Công thức đảm bảo Pool có số lượng Connection tối thiểu để tránh trường hợp các Thread đều giữ Connection và chờ thêm Connection mới.

Ví dụ:

```text
Tn = 10
Cm = 2

pool_size = 10 × (2 - 1) + 1
          = 11
```

Pool Size tối thiểu trong trường hợp này là `11`.

Mục tiêu của công thức là đảm bảo ít nhất một Connection có thể được cấp phát để tránh tình trạng các Thread chờ lẫn nhau.

---

## 3.8. Connection Pool Performance Optimization

Đã tìm hiểu một công thức tham khảo để tối ưu số lượng Connection:

```text
pool_size = (core_count × 2) + effective_spindle_count
```

Trong đó:

* `core_count`: Số CPU Core.
* `effective_spindle_count`: Số lượng Disk Spindle hiệu dụng.

Công thức được sử dụng như một điểm bắt đầu để ước lượng Connection Pool Size.

Tuy nhiên Pool Size thực tế cần được điều chỉnh dựa trên:

* CPU.
* Database Capacity.
* Query Performance.
* Number of Application Threads.
* Request Throughput.
* Transaction Duration.
* Connection Usage.
* Monitoring Metrics.

Do đó không nên chỉ dựa vào một công thức mà cần kiểm tra Performance thực tế của hệ thống.

---

## 4. Kết quả đạt được

Sau khi hoàn thành tuần học thứ sáu, đã đạt được các kết quả sau:

* Hiểu khái niệm ORM và vai trò của ORM trong Java Backend.
* Phân biệt JPA Specification và Hibernate Implementation.
* Hiểu kiến trúc Hibernate.
* Nắm được vai trò của `SessionFactory`, `Session` và Transaction.
* Hiểu Entity Mapping giữa Java Object và Database Table.
* Nắm được các Relationship One-to-One, One-to-Many, Many-to-One và Many-to-Many.
* Hiểu Repository Pattern và Spring Data JPA.
* Nắm được Entity Lifecycle gồm Transient, Persistent, Detached và Removed.
* Hiểu sự khác biệt giữa Lazy Loading và Eager Loading.
* Hiểu Performance Implications của các Loading Strategies.
* Nắm được N+1 Query Problem.
* Biết cách phát hiện N+1 thông qua SQL Logs và Monitoring.
* Hiểu các giải pháp xử lý N+1 như Join Fetching và Batch Fetching.
* Hiểu First-level Cache.
* Nắm được Second-level Cache và Query Cache.
* Hiểu Transaction Management với `@Transactional`.
* Nắm được Transaction Propagation.
* Hiểu Transaction Isolation Levels.
* Hiểu vai trò của Connection Pool trong Backend Application.
* Nắm được cách Hibernate tích hợp với HikariCP.
* Hiểu các HikariCP Configuration như Pool Size, Connection Timeout và Idle Timeout.
* Hiểu ảnh hưởng của Pool Size đến Application và Database Performance.
* Nắm được các Metrics cần Monitoring trong Connection Pool.
* Hiểu Connection Leak và ảnh hưởng của Connection Leak.
* Nắm được công thức Deadlock Prevention `pool_size = Tn × (Cm - 1) + 1`.
* Hiểu công thức tham khảo `(core_count × 2) + effective_spindle_count` trong Connection Pool Optimization.
* Xây dựng được nền tảng về ORM, Hibernate và Connection Pool để tiếp tục tối ưu Database Access và Performance cho các Backend Application.

---


