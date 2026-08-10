# 📘 BÁO CÁO THỰC TẬP TUẦN 6

## Thông tin

* **Chủ đề:** ORM - JPA, Hibernate & Connection Pool
* **Intern:** Bùi Văn Nam
* **Team:** Platform - Adtech
* **Gmail:** [buivannam13032004@gmail.com](mailto:buivannam13032004@gmail.com)
* **Leader:** Nguyễn Văn Cương

---

# 1. Mục tiêu tuần

Trong tuần thứ sáu, theo roadmap, nội dung tập trung vào **ORM (Object-Relational Mapping)** với hai công nghệ chính là **JPA và Hibernate**.

Mục tiêu là hiểu cách ánh xạ các Object trong Java với dữ liệu được lưu trữ trong Database, cách xây dựng Entity, Mapping Relationships và sử dụng Repository Pattern trong ứng dụng Backend.

Bên cạnh đó, em tìm hiểu sâu hơn về kiến trúc Hibernate, Entity Lifecycle, Lazy Loading và Eager Loading, vấn đề N+1 Query, Caching, Transaction Management và tối ưu hóa Query.

Một nội dung quan trọng khác trong tuần là **Connection Pool**, tập trung tìm hiểu HikariCP - Connection Pool phổ biến trong các ứng dụng Spring Boot.

Các nội dung chính:

* JPA/Hibernate Fundamentals.
* Entity Mapping.
* Entity Relationships.
* Repository Pattern.
* Hibernate Architecture.
* Entity Lifecycle.
* Lazy Loading và Eager Loading.
* N+1 Query Problem.
* Query Optimization.
* First-level và Second-level Cache.
* Transaction Management.
* HikariCP.
* Connection Pool Sizing.
* Connection Leak.
* Deadlock Prevention.
* Connection Pool Performance.

Mục tiêu chung là hiểu được quá trình từ **Java Object → ORM → SQL → Database** và biết cách tối ưu việc truy cập Database trong ứng dụng Backend.

---

# 2. Lịch học Tuần 6

| Ngày      | Nội dung học                         | Kết quả đạt được                                                               |
| --------- | ------------------------------------ | ------------------------------------------------------------------------------ |
| **Thứ 2** | JPA & Hibernate Fundamentals         | Hiểu ORM, JPA và vai trò của Hibernate.                                        |
| **Thứ 3** | Entity Mapping & Relationships       | Hiểu Entity và các quan hệ One-to-One, One-to-Many, Many-to-One, Many-to-Many. |
| **Thứ 4** | Entity Lifecycle & Repository        | Hiểu Lifecycle của Entity và Repository Pattern.                               |
| **Thứ 5** | Query Optimization, Lazy/Eager & N+1 | Biết các vấn đề Performance khi sử dụng ORM và cách tối ưu Query.              |
| **Thứ 6** | Caching, Transaction & HikariCP      | Hiểu Cache, Transaction Management và Connection Pool.                         |

---

# 3. Tổng quan về ORM

## 3.1. ORM là gì?

ORM là viết tắt của **Object-Relational Mapping**, là kỹ thuật ánh xạ giữa Object trong ứng dụng và dữ liệu trong Relational Database.

Trong Java:

```text
Java Object
     |
     ↓
    ORM
     |
     ↓
Relational Database
```

Ví dụ một Java Class:

```java
public class User {
    private Long id;
    private String name;
    private String email;
}
```

Có thể được ánh xạ với Database Table:

```text
users
--------------------------------
id | name | email
--------------------------------
1  | Nam  | nam@example.com
```

ORM giúp Developer thao tác với Database thông qua Object thay vì phải viết SQL cho mọi thao tác CRUD.

---

# 3.2. Lợi ích của ORM

Một số lợi ích:

* Giảm lượng SQL phải viết thủ công.
* Mapping Object với Database.
* Hỗ trợ CRUD.
* Quản lý Relationship giữa các Entity.
* Hỗ trợ Transaction.
* Hỗ trợ Caching.
* Tăng khả năng tái sử dụng code.
* Tích hợp tốt với Spring Boot.

Tuy nhiên, ORM không có nghĩa là Developer không cần biết SQL.

Việc hiểu SQL vẫn rất quan trọng để:

* Phân tích Query.
* Tối ưu Performance.
* Phát hiện N+1 Query.
* Kiểm tra Index.
* Phân tích Execution Plan.

---

# 4. JPA

## 4.1. JPA là gì?

JPA là viết tắt của **Jakarta Persistence API**.

JPA là một Specification định nghĩa cách Java Application tương tác với Relational Database thông qua ORM.

JPA cung cấp các khái niệm:

* Entity.
* EntityManager.
* Persistence Context.
* Relationship Mapping.
* JPQL.
* Transaction.

JPA không phải là một ORM Implementation cụ thể.

Một số Implementation:

* Hibernate.
* EclipseLink.
* OpenJPA.

Trong Spring Boot, Hibernate thường được sử dụng làm JPA Provider.

---

# 4.2. Hibernate

Hibernate là một ORM Framework phổ biến trong Java và là một JPA Implementation.

Mô hình:

```text
Application
     |
     ↓
Spring Data JPA
     |
     ↓
JPA
     |
     ↓
Hibernate
     |
     ↓
JDBC
     |
     ↓
Database
```

Hibernate chịu trách nhiệm chuyển đổi các thao tác trên Java Object thành SQL tương ứng.

---

# 5. Hibernate Architecture

Kiến trúc Hibernate có thể hình dung:

```text
┌──────────────────────────┐
│      Java Application    │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│         JPA API          │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│        Hibernate         │
│      ORM Framework       │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│           JDBC           │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│         Database         │
└──────────────────────────┘
```

Các thành phần quan trọng:

* SessionFactory.
* Session.
* Transaction.
* Persistence Context.
* Entity.

---

# 5.1. SessionFactory

`SessionFactory` là đối tượng chịu trách nhiệm tạo Hibernate Session.

Đặc điểm:

* Được tạo một lần trong Application.
* Thread-safe.
* Có chi phí khởi tạo tương đối cao.
* Được sử dụng xuyên suốt vòng đời Application.

Mô hình:

```text
Application
     |
     ↓
SessionFactory
     |
     ├── Session
     ├── Session
     └── Session
```

Trong Spring Boot, phần lớn việc quản lý các thành phần này được Framework thực hiện tự động.

---

# 5.2. Session

`Session` đại diện cho một đơn vị làm việc với Database trong Hibernate.

Session được sử dụng để:

* Load Entity.
* Save Entity.
* Update Entity.
* Delete Entity.
* Execute Query.

Có thể hình dung:

```text
Session
   |
   ├── Load
   ├── Save
   ├── Update
   └── Delete
```

Session không nên được dùng chung tùy tiện giữa nhiều Thread.

---

# 5.3. Transaction

Transaction đảm bảo một nhóm thao tác Database được thực hiện như một đơn vị logic.

Ví dụ:

```text
Transfer Money
      |
      ├── Debit Account A
      |
      └── Credit Account B
```

Nếu một thao tác thất bại:

```text
ROLLBACK
```

Nếu tất cả thành công:

```text
COMMIT
```

Trong Spring có thể sử dụng:

```java
@Transactional
```

để quản lý Transaction.

---

# 6. Entity

Entity là Java Object được ánh xạ với Database Table.

Ví dụ:

```java
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

Trong đó:

* `@Entity`: Đánh dấu Class là Entity.
* `@Table`: Xác định Table.
* `@Id`: Xác định Primary Key.
* `@GeneratedValue`: Cấu hình cách tạo ID.

---

# 6.1. Entity Mapping

Một Entity có thể ánh xạ:

```text
Java Class
     ↓
Database Table

Java Field
     ↓
Database Column
```

Ví dụ:

```text
User.id
    ↓
users.id

User.name
    ↓
users.name

User.email
    ↓
users.email
```

Có thể sử dụng:

* `@Column`
* `@Id`
* `@GeneratedValue`
* `@Enumerated`
* `@Temporal` hoặc các kiểu Date/Time phù hợp.

---

# 7. Entity Relationships

Database thường chứa nhiều Table có quan hệ với nhau.

Các loại Relationship:

* One-to-One.
* One-to-Many.
* Many-to-One.
* Many-to-Many.

---

# 7.1. One-to-One

Một Entity liên kết với một Entity khác.

Ví dụ:

```text
User
  |
  | 1 - 1
  |
Profile
```

Một User có một Profile.

Trong JPA:

```java
@OneToOne
private Profile profile;
```

---

# 7.2. One-to-Many

Một Entity có nhiều Entity khác.

Ví dụ:

```text
Customer
   |
   ├── Order
   ├── Order
   └── Order
```

Một Customer có nhiều Order.

```java
@OneToMany
private List<Order> orders;
```

---

# 7.3. Many-to-One

Nhiều Entity cùng thuộc về một Entity khác.

Ví dụ:

```text
Order ─────┐
Order ─────┼──→ Customer
Order ─────┘
```

Trong JPA:

```java
@ManyToOne
private Customer customer;
```

Trong thực tế, `ManyToOne` thường được sử dụng cùng với Foreign Key.

---

# 7.4. Many-to-Many

Một Entity có thể liên kết với nhiều Entity khác và ngược lại.

Ví dụ:

```text
Student
  ↕
Course
```

Một Student học nhiều Course và một Course có nhiều Student.

JPA:

```java
@ManyToMany
private Set<Course> courses;
```

Quan hệ Many-to-Many thường được triển khai thông qua một Join Table.

Ví dụ:

```text
student_course
---------------------
student_id
course_id
```

---

# 8. Repository Pattern

Repository Pattern tạo ra một lớp abstraction giữa Business Logic và Data Access Layer.

Mô hình:

```text
Controller
    |
    ↓
Service
    |
    ↓
Repository
    |
    ↓
Hibernate
    |
    ↓
Database
```

Trong Spring Data JPA có thể tạo:

```java
public interface UserRepository
        extends JpaRepository<User, Long> {
}
```

Spring Data JPA có thể tự cung cấp các thao tác:

* `save()`
* `findById()`
* `findAll()`
* `deleteById()`
* `existsById()`

Điều này giúp giảm Boilerplate Code.

---

# 9. Entity Lifecycle

Entity trong Hibernate có các trạng thái chính:

```text
Transient
    ↓
Persistent
    ↓
Detached
    ↓
Removed
```

---

# 9.1. Transient

Object vừa được tạo bằng `new` nhưng chưa được Hibernate quản lý.

```java
User user = new User();
```

Lúc này:

```text
Java Object
    ↓
Transient
```

Entity chưa thuộc Persistence Context.

---

# 9.2. Persistent

Entity được Hibernate quản lý bởi Persistence Context.

Ví dụ sau khi Entity được Persist:

```text
Entity
  ↓
Persistence Context
  ↓
Persistent
```

Hibernate có thể theo dõi thay đổi của Entity.

---

# 9.3. Detached

Entity từng được quản lý bởi Persistence Context nhưng hiện tại không còn được quản lý.

Ví dụ khi Persistence Context kết thúc:

```text
Persistent
    ↓
Session closed
    ↓
Detached
```

Các thay đổi trên Detached Entity không tự động được đồng bộ với Database.

---

# 9.4. Removed

Entity được đánh dấu để xóa khỏi Database.

```text
Persistent
    ↓
remove()
    ↓
Removed
    ↓
DELETE
```

---

# 10. Persistence Context

Persistence Context là vùng quản lý các Entity đang được Hibernate theo dõi.

Có thể hình dung:

```text
Persistence Context
┌──────────────────────┐
│ User #1              │
│ User #2              │
│ Order #10            │
│ Order #11            │
└──────────────────────┘
```

Hibernate có thể biết Entity nào đang được quản lý và phát hiện thay đổi.

Ví dụ:

```java
user.setName("Nam");
```

Nếu `user` đang Persistent, Hibernate có thể phát hiện thay đổi và tạo SQL `UPDATE` khi Transaction Commit.

Cơ chế này được gọi là **Dirty Checking**.

---

# 11. Lazy Loading và Eager Loading

Một vấn đề quan trọng trong ORM là thời điểm Load Relationship.

Có hai chiến lược:

* Lazy Loading.
* Eager Loading.

---

# 11.1. Lazy Loading

Lazy Loading chỉ tải Relationship khi dữ liệu thực sự được truy cập.

Ví dụ:

```text
User
  |
  └── orders
```

Khi load User:

```text
SELECT user
```

Chưa nhất thiết load Orders.

Khi gọi:

```java
user.getOrders();
```

Hibernate mới thực hiện Query lấy Orders.

Ưu điểm:

* Giảm dữ liệu load không cần thiết.
* Giảm số lượng dữ liệu ban đầu.

Nhược điểm:

* Có thể phát sinh nhiều Query.
* Có thể gây N+1 Query.
* Có thể gặp LazyInitializationException nếu truy cập ngoài Persistence Context phù hợp.

---

# 11.2. Eager Loading

Eager Loading tải Relationship ngay khi Entity được load.

Ví dụ:

```text
SELECT User
+
SELECT Orders
```

Ưu điểm:

* Dữ liệu Relationship có sẵn.
* Tránh một số vấn đề Lazy Loading.

Nhược điểm:

* Có thể load dữ liệu không cần thiết.
* Tăng Memory Usage.
* Query có thể phức tạp.
* Có thể gây Performance Problem.

Do đó không nên sử dụng Eager Loading một cách tùy tiện.

---

# 12. N+1 Query Problem

N+1 Query là một trong những vấn đề Performance phổ biến khi sử dụng ORM.

Ví dụ có:

```text
1 Query lấy Users

+

N Query lấy Orders của từng User
```

Tổng cộng:

```text
1 + N Queries
```

Ví dụ:

```text
SELECT * FROM users;

SELECT * FROM orders WHERE user_id = 1;
SELECT * FROM orders WHERE user_id = 2;
SELECT * FROM orders WHERE user_id = 3;
...
```

Nếu có 100 User:

```text
1 + 100 = 101 Queries
```

Điều này có thể gây Performance Problem nghiêm trọng.

---

# 12.1. Phát hiện N+1

Có thể phát hiện thông qua:

* SQL Logs.
* Hibernate Statistics.
* Monitoring.
* Database Performance Tools.
* Profiling.

Ví dụ Log:

```text
SELECT users...
SELECT orders WHERE user_id = 1
SELECT orders WHERE user_id = 2
SELECT orders WHERE user_id = 3
...
```

Nếu thấy nhiều Query tương tự nhau được thực hiện lặp lại, cần kiểm tra khả năng N+1.

---

# 12.2. Giải pháp N+1

Một số giải pháp:

* Join Fetch.
* Entity Graph.
* Batch Fetching.
* DTO Projection.
* Query tối ưu.

---

## Join Fetch

JPQL có thể sử dụng:

```sql
SELECT u
FROM User u
JOIN FETCH u.orders
```

Mục tiêu là lấy User và Relationship trong một Query phù hợp.

---

## Batch Fetching

Hibernate có thể nhóm các Entity cần load thành Batch thay vì Query từng Entity.

Ví dụ:

```text
Load Order 1
Load Order 2
Load Order 3
...
```

Có thể được tối ưu thành:

```text
WHERE user_id IN (1, 2, 3, ...)
```

Giảm số lượng Query.

---

# 13. Query Optimization

ORM giúp giảm lượng SQL thủ công nhưng không đảm bảo Query luôn tối ưu.

Một số nguyên tắc:

* Tránh N+1.
* Chỉ lấy Column cần thiết.
* Sử dụng Pagination.
* Sử dụng Index phù hợp.
* Tối ưu JOIN.
* Sử dụng DTO Projection khi phù hợp.
* Kiểm tra SQL được Hibernate sinh ra.
* Sử dụng `EXPLAIN` để phân tích Query.
* Tránh Fetch quá nhiều Relationship cùng lúc.

---

# 13.1. Pagination

Khi có hàng triệu bản ghi, không nên load toàn bộ dữ liệu.

Thay vào đó sử dụng Pagination:

```text
Page 1 → 20 records
Page 2 → 20 records
Page 3 → 20 records
```

Trong Spring Data JPA:

```java
Page<User> findAll(Pageable pageable);
```

Pagination giúp:

* Giảm Memory.
* Giảm Database Load.
* Giảm Network Traffic.
* Tăng Response Performance.

---

# 14. Caching

Caching giúp giảm số lần truy cập Database bằng cách lưu dữ liệu thường xuyên sử dụng ở một vùng nhớ nhanh hơn.

Hibernate có nhiều tầng Cache.

---

# 14.1. First-level Cache

First-level Cache được gắn với Persistence Context/Session.

Mặc định Hibernate sử dụng First-level Cache.

Ví dụ:

```text
Session
  |
  ├── User #1
  └── User #2
```

Nếu cùng một Entity được truy cập nhiều lần trong cùng Persistence Context, Hibernate có thể sử dụng Object đã có thay vì thực hiện Query mới trong một số trường hợp phù hợp.

Đặc điểm:

* Mặc định được bật.
* Scope thường gắn với Persistence Context.
* Không dùng chung giữa các Session.

---

# 14.2. Second-level Cache

Second-level Cache có Scope lớn hơn First-level Cache.

Mô hình:

```text
Session A ─┐
Session B ─┼──→ Second-level Cache
Session C ─┘
```

Second-level Cache có thể được chia sẻ giữa nhiều Session.

Một số Cache Provider có thể sử dụng:

* Ehcache.
* Infinispan.
* Redis thông qua các giải pháp phù hợp.

Mục tiêu:

* Giảm Database Query.
* Tăng Read Performance.

Tuy nhiên Cache cần được sử dụng cẩn thận để tránh:

* Stale Data.
* Cache Invalidation Problem.
* Memory Overhead.

---

# 14.3. Query Cache

Query Cache lưu kết quả của Query.

Có thể giúp giảm Database Access với các Query được thực hiện thường xuyên và dữ liệu thay đổi ít.

Tuy nhiên Query Cache cần được cân nhắc vì:

* Tốn Memory.
* Cần Invalidation.
* Không phải Query nào cũng phù hợp để Cache.

---

# 15. Transaction Management

Transaction Management đảm bảo các thao tác Database được thực hiện nhất quán.

Trong Spring Boot có thể sử dụng:

```java
@Transactional
```

Ví dụ:

```java
@Transactional
public void transferMoney(
        Long fromId,
        Long toId,
        BigDecimal amount) {

    // debit account

    // credit account
}
```

Nếu có Exception khiến Transaction Rollback theo cấu hình và quy tắc của Spring, các thay đổi trong Transaction có thể được hoàn tác.

---

# 15.1. Transaction Propagation

Propagation xác định cách một Transaction Method tham gia vào Transaction hiện tại.

Một số loại:

* `REQUIRED`
* `REQUIRES_NEW`
* `SUPPORTS`
* `NOT_SUPPORTED`
* `MANDATORY`
* `NEVER`
* `NESTED`

Trong đó `REQUIRED` là lựa chọn phổ biến.

Ý nghĩa:

```text
Nếu có Transaction
        ↓
Tham gia Transaction hiện tại

Nếu chưa có
        ↓
Tạo Transaction mới
```

---

# 15.2. Transaction Isolation

Isolation kiểm soát mức độ các Transaction nhìn thấy thay đổi của nhau.

Các mức phổ biến:

* READ UNCOMMITTED.
* READ COMMITTED.
* REPEATABLE READ.
* SERIALIZABLE.

Mục tiêu là cân bằng:

```text
Consistency
     ↕
Concurrency
     ↕
Performance
```

Isolation càng cao thường tăng mức độ kiểm soát nhưng có thể ảnh hưởng đến Concurrency và Performance.

---

# 16. Connection Pool

Mỗi khi Application cần truy cập Database, việc tạo một Database Connection mới có thể tốn tài nguyên.

Connection Pool giải quyết vấn đề này bằng cách duy trì một Pool gồm các Connection có thể tái sử dụng.

Không sử dụng Pool:

```text
Request
  ↓
Create Connection
  ↓
Execute Query
  ↓
Close Connection
```

Sử dụng Pool:

```text
             ┌── Connection 1
             ├── Connection 2
Application ─┼── Connection 3
             ├── Connection 4
             └── Connection 5
```

Application lấy Connection từ Pool, sử dụng xong trả lại Pool.

---

# 16.1. HikariCP

HikariCP là một Connection Pool phổ biến và thường được sử dụng mặc định trong Spring Boot.

Flow:

```text
Application
    |
    ↓
HikariCP
    |
    ├── Connection 1
    ├── Connection 2
    ├── Connection 3
    └── Connection N
    |
    ↓
Database
```

Lợi ích:

* Connection Reuse.
* Giảm Connection Creation Overhead.
* Cải thiện Performance.
* Quản lý Connection tập trung.

---

# 16.2. HikariCP Pool Size

Pool Size xác định số lượng Connection tối đa mà Pool có thể quản lý.

Ví dụ:

```text
maximumPoolSize = 10
```

Có nghĩa Application có thể sử dụng tối đa số Connection theo cấu hình Pool trong phạm vi đó.

Không nên đặt Pool Size quá lớn vì Database cũng có giới hạn Connection.

---

# 16.3. Connection Timeout

Connection Timeout xác định thời gian Application chờ để lấy được Connection từ Pool.

Ví dụ:

```text
Request
   |
   ↓
Get Connection
   |
   ↓
Pool hết Connection
   |
   ↓
Wait
   |
   ├── Connection available → Continue
   |
   └── Timeout → Error
```

Nếu Timeout quá thấp, Request có thể thất bại sớm.

Nếu quá cao, Thread có thể phải chờ lâu.

---

# 16.4. Idle Timeout

Idle Timeout liên quan đến thời gian Connection không được sử dụng trước khi có thể bị loại khỏi Pool theo cấu hình.

Mục tiêu:

* Không duy trì quá nhiều Connection không cần thiết.
* Cân bằng Resource Usage.

---

# 16.5. Connection Leak

Connection Leak xảy ra khi Application lấy Connection nhưng không trả lại Pool đúng cách.

Ví dụ:

```text
Get Connection
      ↓
Execute Query
      ↓
Exception
      ↓
Không Release
```

Nếu tình trạng này xảy ra nhiều lần:

```text
Pool
 ↓
Connection giảm dần
 ↓
Pool exhausted
 ↓
Request phải chờ
```

Connection Leak có thể gây:

* Timeout.
* Request chậm.
* Database Connection Exhaustion.
* Application Failure.

Trong Spring/JPA, việc sử dụng đúng Transaction và Resource Management giúp hạn chế vấn đề này.

---

# 16.6. Pool Monitoring

Cần theo dõi các Metrics:

* Active Connections.
* Idle Connections.
* Total Connections.
* Pending Threads.
* Connection Timeout.
* Connection Acquisition Time.

Mục tiêu:

```text
Monitor
   ↓
Detect Bottleneck
   ↓
Tune Pool
   ↓
Improve Performance
```

---

# 17. Deadlock Prevention và Connection Pool

Khi sử dụng Connection Pool, việc xác định Pool Size cần dựa trên:

* Số lượng Thread.
* Số Connection tối đa mà mỗi Thread có thể cần.
* Cách Transaction hoạt động.

Một công thức được tìm hiểu:

```text
pool_size = Tn × (Cm - 1) + 1
```

Trong đó:

* `Tn`: Maximum Threads.
* `Cm`: Maximum Connections per Thread.

Công thức giúp xác định mức Pool Size tối thiểu trong một mô hình nhất định để tránh một số tình huống Connection Pool Deadlock.

Ví dụ:

```text
Tn = 10
Cm = 2

pool_size
= 10 × (2 - 1) + 1
= 11
```

Công thức này cần được áp dụng dựa trên mô hình truy cập Connection thực tế, không nên sử dụng máy móc cho mọi hệ thống.

---

# 18. Performance Optimization

Một công thức thường được tham khảo khi ước lượng Connection Pool Size:

```text
(core_count * 2) + effective_spindle_count
```

Trong đó:

* `core_count`: Số CPU Core.
* `effective_spindle_count`: Số lượng Storage Disk có khả năng xử lý I/O đồng thời.

Mục đích là đưa ra một điểm bắt đầu để tuning Connection Pool.

Tuy nhiên Pool Size tối ưu phụ thuộc vào:

* CPU.
* Database.
* Query.
* Transaction Duration.
* Disk I/O.
* Network.
* Application Concurrency.
* Database Connection Limit.

Do đó cần kết hợp Monitoring và Load Testing thay vì chỉ dựa vào một công thức cố định.

---

# 19. Các vấn đề Performance thường gặp trong ORM

Một số vấn đề quan trọng:

### 1. N+1 Query

```text
1 + N Queries
```

Giải pháp:

* Join Fetch.
* Entity Graph.
* Batch Fetching.

### 2. Eager Loading quá mức

Load quá nhiều Relationship không cần thiết.

Giải pháp:

* Ưu tiên Lazy Loading phù hợp.
* Chỉ Fetch dữ liệu cần thiết.

### 3. Query quá lớn

Load quá nhiều dữ liệu cùng lúc.

Giải pháp:

* Pagination.
* DTO Projection.
* Filtering.

### 4. Thiếu Index

Query phải Scan nhiều dữ liệu.

Giải pháp:

* Phân tích `EXPLAIN`.
* Tạo Index phù hợp.

### 5. Connection Pool không phù hợp

Pool quá nhỏ:

```text
Threads
   ↓
Waiting for Connection
```

Pool quá lớn:

```text
Too many Connections
   ↓
Database overload
```

Cần tìm mức cân bằng dựa trên Monitoring và Load Testing.

---

# 20. Kết quả đạt được

Sau tuần thứ sáu, em đã đạt được các kết quả:

## JPA/Hibernate

* Hiểu khái niệm ORM.
* Hiểu vai trò của JPA.
* Hiểu Hibernate là một JPA Implementation.
* Nắm được kiến trúc Hibernate.
* Hiểu SessionFactory.
* Hiểu Session.
* Hiểu Transaction.
* Hiểu Persistence Context.
* Biết cách xây dựng Entity.
* Hiểu Entity Mapping.
* Biết Mapping các Relationship.
* Hiểu One-to-One.
* Hiểu One-to-Many.
* Hiểu Many-to-One.
* Hiểu Many-to-Many.

## Entity Lifecycle

* Hiểu Transient.
* Hiểu Persistent.
* Hiểu Detached.
* Hiểu Removed.
* Hiểu Dirty Checking.

## Query Performance

* Hiểu Lazy Loading.
* Hiểu Eager Loading.
* Nhận biết N+1 Query Problem.
* Biết cách phát hiện N+1.
* Biết Join Fetch.
* Hiểu Batch Fetching.
* Biết sử dụng Pagination.
* Hiểu DTO Projection.
* Biết kết hợp ORM với SQL Optimization.

## Caching

* Hiểu First-level Cache.
* Hiểu Second-level Cache.
* Hiểu Query Cache.
* Hiểu ưu nhược điểm của Caching.
* Nhận thức được vấn đề Cache Invalidation.

## Transaction

* Hiểu `@Transactional`.
* Hiểu Transaction Propagation.
* Hiểu Transaction Isolation.
* Biết vai trò của Transaction trong việc đảm bảo Data Consistency.

## Connection Pool

* Hiểu Connection Pool.
* Hiểu HikariCP.
* Hiểu Pool Size.
* Hiểu Connection Timeout.
* Hiểu Idle Timeout.
* Hiểu Connection Leak.
* Biết các Metrics cần theo dõi.
* Hiểu vấn đề Connection Pool Exhaustion.
* Biết công thức Deadlock Prevention.
* Hiểu các yếu tố ảnh hưởng đến Connection Pool Performance.

---

# 21. Khó khăn và hướng khắc phục

Trong quá trình học ORM, em gặp một số khó khăn:

* Ban đầu khó phân biệt JPA và Hibernate.
* Entity Lifecycle có nhiều trạng thái và cần hiểu rõ Persistence Context.
* Lazy Loading và Eager Loading có ảnh hưởng trực tiếp đến Performance nên cần hiểu cách Hibernate thực hiện Query.
* N+1 Query có thể không dễ phát hiện nếu chỉ nhìn vào Source Code.
* Caching có nhiều tầng và cần hiểu Scope của từng loại Cache.
* Transaction Propagation và Isolation có nhiều trường hợp sử dụng.
* Connection Pool Size không có một giá trị cố định phù hợp với mọi Application.
* Connection Pool Performance phụ thuộc đồng thời vào Application, Database, CPU, I/O và Network.

Để khắc phục, em tập trung phân tích Flow từ Application đến Database, theo dõi SQL do Hibernate sinh ra và tìm hiểu cách các thao tác trên Entity được chuyển thành SQL.

Đồng thời, em tìm hiểu các trường hợp Performance Problem như N+1 Query, Connection Pool Exhaustion và Query quá lớn để hiểu cách phát hiện và tối ưu.

---

# 22. Kế hoạch giai đoạn tiếp theo

Sau khi hoàn thành giai đoạn kiến thức cơ bản trong 6 tuần đầu, em sẽ tiếp tục áp dụng các kiến thức đã học vào các nội dung Backend nâng cao.

Các kiến thức đã tích lũy gồm:

```text
Java Core
    ↓
Collections
    ↓
Concurrency
    ↓
Docker
    ↓
Database
    ↓
Logging & I/O
    ↓
Spring Boot
    ↓
Authentication
    ↓
Rate Limiting
    ↓
JPA / Hibernate
    ↓
Connection Pool
```

Các nội dung này tạo nền tảng để tiếp tục tìm hiểu sâu hơn về:

* Backend Architecture.
* Spring Boot Advanced.
* Microservices.
* Distributed Systems.
* Performance Optimization.
* Monitoring.
* Deployment.
* System Design.

---

# 23. Kết luận

Tuần thứ sáu giúp em hiểu sâu hơn về **ORM, JPA, Hibernate và Connection Pool**, là những thành phần quan trọng trong quá trình xây dựng Backend Application sử dụng Spring Boot.

Về ORM, em đã hiểu cách ánh xạ Java Object với Database thông qua Entity, Relationship và Repository Pattern. Em cũng hiểu kiến trúc Hibernate gồm SessionFactory, Session, Persistence Context và Transaction.

Bên cạnh đó, em tìm hiểu Entity Lifecycle gồm Transient, Persistent, Detached và Removed, đồng thời hiểu cơ chế Dirty Checking của Hibernate.

Về Performance, em đã tìm hiểu Lazy Loading, Eager Loading và đặc biệt là **N+1 Query Problem**. Em biết một số phương pháp xử lý như Join Fetch, Batch Fetching, Pagination và DTO Projection.

Về Caching, em đã phân biệt First-level Cache, Second-level Cache và Query Cache, đồng thời hiểu được lợi ích cũng như các vấn đề cần cân nhắc khi sử dụng Cache.

Về Transaction, em đã hiểu `@Transactional`, Transaction Propagation và Isolation, qua đó hiểu rõ hơn cách đảm bảo tính nhất quán của dữ liệu trong các thao tác Database.

Cuối cùng, em tìm hiểu **HikariCP Connection Pool**, Pool Sizing, Connection Timeout, Idle Timeout, Connection Leak, Pool Monitoring và các yếu tố ảnh hưởng đến Performance.

Qua tuần thứ sáu, em đã hoàn thành giai đoạn kiến thức cơ bản trong roadmap và có nền tảng cần thiết để tiếp tục áp dụng Java, Spring Boot, Database, ORM, Concurrency và Docker vào các bài toán Backend thực tế.
