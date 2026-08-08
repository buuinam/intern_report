# BÁO CÁO THỰC TẬP TUẦN 5

## Chủ đề: Spring Boot & Middleware (Authentication + Rate Limiting)

**Intern:** Bùi Văn Nam
**Team:** Platform - Adtech
**Gmail:** [buivannam13032004@gmail.com](mailto:buivannam13032004@gmail.com)
**Leader:** Nguyễn Văn Cương

---

## 1. Mục tiêu tuần

Trong tuần thứ năm, theo roadmap mục tiêu là tìm hiểu các kiến thức về **Spring Boot và Middleware**, tập trung vào việc xây dựng Backend Application, Authentication, Authorization và Rate Limiting.

Nội dung học tập tập trung vào kiến trúc Spring Boot, cơ chế Auto-configuration, Dependency Injection và IoC Container. Bên cạnh đó, tìm hiểu Spring MVC Pattern, Request Lifecycle, RESTful API Design và cách quản lý Configuration Properties cũng như Spring Profiles.

Đối với Middleware - Authentication, đã tìm hiểu các chiến lược Authentication phổ biến như Session-based Authentication, Token-based Authentication, JWT, OAuth2/OIDC, API Key và mTLS. Đồng thời tìm hiểu sự khác biệt giữa Stateful và Stateless Authentication và các trade-off khi triển khai trong hệ thống có nhiều instance.

Ngoài ra, đã nghiên cứu Spring Security, Security Filter Chain, `SecurityFilterChain`, JWT Access Token/Refresh Token, Token Revocation, Redis Blacklist và các mô hình Authorization như RBAC, ABAC cũng như Method-level Security với `@PreAuthorize`.

Đối với Middleware - Rate Limiting, đã tìm hiểu các thuật toán Fixed Window, Sliding Window, Token Bucket và Leaky Bucket. Bên cạnh đó, nghiên cứu cách triển khai Rate Limiting bằng Bucket4j, Redis-based Distributed Rate Limiting và API Gateway như Spring Cloud Gateway, Nginx và Kong.

### Lịch học Tuần 5

| **Ngày** | **Nội dung học**                                   | **Kết quả đạt được**                                                                         |
| -------- | -------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| Thứ 2    | Spring Boot Architecture, Auto-configuration & IoC | Hiểu kiến trúc Spring Boot, Auto-configuration, IoC Container và Dependency Injection.       |
| Thứ 3    | Spring MVC, RESTful API & Configuration            | Hiểu Request Lifecycle, RESTful API Design, Configuration Properties và Spring Profiles.     |
| Thứ 4    | Authentication, JWT & Spring Security              | Hiểu Session/Token-based Authentication, JWT, Access/Refresh Token và Security Filter Chain. |
| Thứ 5    | Authorization, Redis & Token Revocation            | Hiểu RBAC, ABAC, `@PreAuthorize`, JWT Revocation và Redis Blacklist.                         |
| Thứ 6    | Rate Limiting & Distributed Rate Limiting          | Hiểu các Rate Limiting Algorithms, Bucket4j, Redis Rate Limiting, API Gateway và HTTP 429.   |

---

## 2. Chi tiết nội dung đã học

## 2.1. Spring Boot

### a. Spring Boot Architecture và Auto-configuration

Đã tìm hiểu về kiến trúc Spring Boot và các thành phần cơ bản được sử dụng để xây dựng ứng dụng Backend.

Spring Boot được xây dựng trên nền tảng Spring Framework và cung cấp các cơ chế giúp giảm lượng Configuration cần thiết khi phát triển Application.

Một số thành phần quan trọng:

* Spring Boot Starter.
* Auto-configuration.
* Embedded Server.
* Application Context.
* IoC Container.
* Dependency Injection.
* Spring MVC.

Spring Boot sử dụng Auto-configuration để tự động cấu hình các thành phần dựa trên Dependencies có trong Project và các Configuration hiện tại.

Ví dụ, khi sử dụng `spring-boot-starter-web`, Spring Boot có thể tự động cấu hình các thành phần cần thiết cho Spring MVC và Embedded Tomcat.

Việc sử dụng Auto-configuration giúp giảm Configuration thủ công và tăng tốc quá trình phát triển Application.

### b. Dependency Injection và IoC Container

Đã tìm hiểu về Inversion of Control (IoC) và Dependency Injection (DI).

IoC là nguyên lý trong đó quyền quản lý việc tạo và kết nối các Object được chuyển từ Developer sang Spring IoC Container.

IoC Container chịu trách nhiệm:

* Tạo Bean.
* Quản lý Bean Lifecycle.
* Inject Dependency.
* Quản lý Bean Scope.
* Kết nối các thành phần trong Application.

Dependency Injection cho phép một Class nhận Dependency từ bên ngoài thay vì tự tạo Dependency.

Ví dụ:

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
}
```

Trong trường hợp trên, `UserService` phụ thuộc vào `UserRepository`. Spring Container sẽ tạo và Inject `UserRepository` vào `UserService`.

Constructor Injection được ưu tiên vì:

* Dependency được khai báo rõ ràng.
* Có thể sử dụng `final`.
* Dễ Unit Test.
* Giảm sự phụ thuộc trực tiếp giữa các Class.

### c. Spring MVC và Request Lifecycle

Đã tìm hiểu Spring MVC Pattern và vòng đời xử lý HTTP Request trong Spring Boot.

Một Request thường được xử lý theo mô hình:

```text
Client
   |
   v
Filter
   |
   v
DispatcherServlet
   |
   v
Controller
   |
   v
Service
   |
   v
Repository
   |
   v
Database
```

Các bước xử lý:

* Client gửi HTTP Request.
* Request đi qua các Filter.
* `DispatcherServlet` tiếp nhận Request.
* DispatcherServlet xác định Controller phù hợp.
* Controller gọi Service.
* Service thực hiện Business Logic.
* Repository thực hiện thao tác với Database.
* Kết quả được trả về Controller.
* Spring chuyển kết quả thành HTTP Response.

Việc hiểu Request Lifecycle giúp xác định được vai trò của từng thành phần trong Spring MVC và vị trí phù hợp để xử lý các logic như Authentication, Logging và Validation.

### d. RESTful API Design

Đã tìm hiểu các nguyên tắc thiết kế RESTful API trong Spring Boot.

Các HTTP Method phổ biến:

* `GET`: Lấy dữ liệu.
* `POST`: Tạo dữ liệu.
* `PUT`: Cập nhật toàn bộ Resource.
* `PATCH`: Cập nhật một phần Resource.
* `DELETE`: Xóa Resource.

Ví dụ:

```text
GET    /api/users
GET    /api/users/{id}
POST   /api/users
PUT    /api/users/{id}
PATCH  /api/users/{id}
DELETE /api/users/{id}
```

Một số HTTP Status Code thường sử dụng:

* `200 OK`.
* `201 Created`.
* `204 No Content`.
* `400 Bad Request`.
* `401 Unauthorized`.
* `403 Forbidden`.
* `404 Not Found`.
* `409 Conflict`.
* `429 Too Many Requests`.
* `500 Internal Server Error`.

Một số nguyên tắc khi thiết kế REST API:

* Sử dụng HTTP Method đúng mục đích.
* URL biểu diễn Resource.
* Sử dụng Status Code phù hợp.
* Response có cấu trúc thống nhất.
* API nên Stateless.
* Có Authentication và Authorization phù hợp.
* Validate dữ liệu đầu vào.

### e. Configuration Properties và Profiles

Đã tìm hiểu cách quản lý Configuration trong Spring Boot thông qua `application.properties` và `application.yml`.

Ví dụ:

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/demo
    username: root
    password: password
```

Configuration giúp quản lý các thông tin như:

* Server Port.
* Database Connection.
* Application Settings.
* External Service Configuration.
* Security Configuration.

Đã tìm hiểu Spring Profiles để sử dụng Configuration khác nhau cho từng Environment.

Ví dụ:

```text
application.yml
application-dev.yml
application-test.yml
application-prod.yml
```

Việc sử dụng Profiles giúp Application có thể sử dụng Configuration phù hợp với từng môi trường Development, Testing và Production.

Các thông tin nhạy cảm như Password, API Key và JWT Secret không nên Hard-code trực tiếp trong Source Code mà nên sử dụng Environment Variables hoặc Secret Management.

---

## 2.2. Middleware - Authentication

### a. Authentication Strategies

Đã tìm hiểu các chiến lược Authentication phổ biến trong Backend System.

Các phương pháp gồm:

* Session-based Authentication.
* Token-based Authentication.
* JWT.
* OAuth2/OIDC.
* API Key.
* mTLS.

Authentication là quá trình xác định danh tính của User hoặc Client khi truy cập vào hệ thống.

### b. Session-based Authentication

Session-based Authentication lưu trạng thái đăng nhập của User trên Server.

Flow cơ bản:

```text
Client
   |
   | Login
   v
Server
   |
   v
Session Store
```

Sau khi đăng nhập thành công, Server tạo Session và Client lưu Session ID, thường thông qua Cookie.

Ưu điểm:

* Dễ quản lý Session.
* Dễ Revoke Session.
* Phù hợp với các ứng dụng truyền thống.

Nhược điểm:

* Server phải lưu trạng thái Session.
* Khi chạy nhiều Instance cần Shared Session Store.
* Tăng độ phức tạp khi Scale hệ thống.

### c. Token-based Authentication

Token-based Authentication sử dụng Token để xác thực Request.

Sau khi Login thành công:

```text
Client
   |
   | Login
   v
Server
   |
   v
Access Token
```

Client gửi Token trong các Request tiếp theo:

```http
Authorization: Bearer <access_token>
```

Ưu điểm:

* Có thể triển khai Stateless.
* Dễ Scale nhiều Instance.
* Phù hợp với REST API và Distributed System.

Nhược điểm:

* Cần quản lý Token.
* Việc Revoke Token phức tạp hơn Session.
* Cần đảm bảo Token được bảo vệ an toàn.

### d. Stateful và Stateless Authentication

Đã tìm hiểu sự khác biệt giữa Stateful và Stateless Authentication.

**Stateful Authentication** yêu cầu Server lưu trạng thái Authentication.

```text
Client
  |
  v
Server
  |
  v
Session Store
```

**Stateless Authentication** không yêu cầu Server lưu Session State. Thông tin Authentication được chứa trong Token.

```text
Client
  |
  | JWT
  v
Server
```

So sánh:

| Đặc điểm           | Stateful | Stateless |
| ------------------ | -------- | --------- |
| Server lưu Session | Có       | Không     |
| Scalability        | Khó hơn  | Dễ hơn    |
| Revoke             | Dễ       | Khó hơn   |
| Shared State       | Cần      | Không cần |
| Ví dụ              | Session  | JWT       |

Stateless Authentication phù hợp với các hệ thống cần Scale nhiều Instance, trong khi Stateful Authentication có lợi thế trong việc quản lý và Revoke Session.

### e. JWT

Đã tìm hiểu JSON Web Token (JWT) và cách sử dụng JWT trong Authentication.

JWT có cấu trúc:

```text
Header.Payload.Signature
```

JWT Payload có thể chứa các thông tin như:

```json
{
  "sub": "123",
  "role": "USER",
  "exp": 1780000000
}
```

Trong đó:

* `sub`: Subject/User ID.
* `role`: Role của User.
* `exp`: Expiration Time.

JWT thường được sử dụng để Server xác thực Request mà không cần lưu Session.

### f. Access Token và Refresh Token

Đã tìm hiểu mô hình sử dụng Access Token và Refresh Token.

```text
Login
  |
  v
Access Token + Refresh Token
  |
  +----> Access Token ----> API
  |
  +----> Refresh Token ---> New Access Token
```

**Access Token:**

* Có thời gian sống ngắn.
* Được sử dụng để truy cập API.

**Refresh Token:**

* Có thời gian sống dài hơn.
* Dùng để lấy Access Token mới khi Access Token hết hạn.

Việc sử dụng Access Token có thời gian sống ngắn giúp giảm thời gian sử dụng của Token nếu Token bị lộ.

### g. Spring Security và Security Filter Chain

Đã tìm hiểu Spring Security và Security Filter Chain.

Spring Security cung cấp các cơ chế:

* Authentication.
* Authorization.
* Password Encoding.
* Security Filter.
* JWT Authentication.
* Method-level Security.

Request khi đi vào Application có thể được xử lý qua Security Filter Chain trước khi đến Controller.

```text
HTTP Request
     |
     v
Security Filter Chain
     |
     +---- Authentication
     |
     +---- Authorization
     |
     v
Controller
```

Security Filter Chain giúp kiểm tra Security của Request trước khi Request được xử lý bởi Business Logic.

---

## 2.3. Authorization

### a. Authentication và Authorization

Đã tìm hiểu sự khác biệt giữa Authentication và Authorization.

**Authentication** trả lời câu hỏi:

> Người dùng là ai?

**Authorization** trả lời câu hỏi:

> Người dùng được phép làm gì?

Ví dụ:

```text
Authentication
      |
      v
User = Nam
      |
      v
Authorization
      |
      +---- USER  → READ
      |
      +---- ADMIN → READ / WRITE / DELETE
```

### b. RBAC

Đã tìm hiểu Role-Based Access Control (RBAC).

RBAC phân quyền dựa trên Role của User.

Ví dụ:

```text
ADMIN
 ├── CREATE
 ├── READ
 ├── UPDATE
 └── DELETE

USER
 └── READ
```

Ưu điểm:

* Dễ triển khai.
* Dễ quản lý.
* Phù hợp với các hệ thống có Role rõ ràng.

### c. ABAC

Đã tìm hiểu Attribute-Based Access Control (ABAC).

ABAC sử dụng các Attribute của User, Resource và Action để đưa ra quyết định Authorization.

Ví dụ:

```text
User:
  role = MANAGER
  department = IT

Resource:
  department = IT

Action:
  UPDATE
```

ABAC có tính linh hoạt cao hơn RBAC nhưng Logic Authorization phức tạp hơn.

### d. Method-level Security

Spring Security hỗ trợ phân quyền trực tiếp trên Method.

Ví dụ:

```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) {
    // Delete user
}
```

Chỉ User có Role `ADMIN` mới có thể thực hiện Method này.

Method-level Security giúp kiểm soát quyền truy cập gần với Business Logic của Application.

### e. Token Revocation và Redis Blacklist

Đã tìm hiểu vấn đề Revoke JWT Token trước khi Token hết hạn.

Do JWT thường được xử lý theo Stateless Model nên Server không lưu trạng thái của Token. Khi cần Logout hoặc Revoke Token, có thể sử dụng Redis để lưu các Token đã bị Blacklist.

Flow:

```text
Logout
   |
   v
JWT Token
   |
   v
Redis Blacklist
```

Khi Request mới được gửi:

```text
Request
   |
   v
Validate JWT
   |
   v
Check Redis
   |
   +---- Blacklisted → Reject
   |
   +---- Valid       → Allow
```

Redis phù hợp với trường hợp này nhờ khả năng truy cập nhanh và hỗ trợ TTL.

---

## 2.4. Middleware - Rate Limiting

### a. Rate Limiting

Đã tìm hiểu Rate Limiting và vai trò của Rate Limiting trong việc kiểm soát Traffic.

Rate Limiting giới hạn số lượng Request mà một User, IP hoặc API Key có thể gửi trong một khoảng thời gian.

Ví dụ:

```text
100 requests / minute / user
```

Khi Client vượt quá giới hạn:

```http
HTTP/1.1 429 Too Many Requests
```

Rate Limiting giúp:

* Chống API Abuse.
* Kiểm soát Traffic.
* Bảo vệ Backend.
* Bảo vệ Database.
* Hạn chế việc một Client gửi quá nhiều Request.

### b. Fixed Window

Fixed Window chia thời gian thành các khoảng cố định.

Ví dụ:

```text
10:00:00 → 10:00:59
10:01:00 → 10:01:59
10:02:00 → 10:02:59
```

Nếu giới hạn là:

```text
100 requests / minute
```

thì mỗi Window có một Counter riêng.

Ưu điểm:

* Dễ triển khai.
* Ít tốn Memory.
* Hiệu năng tốt.

Nhược điểm:

* Có thể xảy ra Burst ở ranh giới giữa hai Window.

Ví dụ Client có thể gửi nhiều Request gần cuối Window và tiếp tục gửi nhiều Request ngay đầu Window tiếp theo.

### c. Sliding Window

Sliding Window sử dụng một khoảng thời gian trượt để tính số lượng Request.

Ví dụ:

```text
100 requests / 60 seconds
```

Có thể triển khai bằng:

* Sliding Window Log.
* Sliding Window Counter.

Ưu điểm:

* Chính xác hơn Fixed Window.
* Hạn chế Burst tại Boundary.

Nhược điểm:

* Có thể tốn nhiều Memory hơn.
* Implementation phức tạp hơn.

### d. Token Bucket

Token Bucket sử dụng một Bucket chứa Token.

Ví dụ:

```text
Capacity = 100 tokens
Refill = 10 tokens/second
```

Mỗi Request cần sử dụng một Token.

```text
        Refill
          ↓
   +-------------+
   | Token Token |
   | Token Token |
   +-------------+
          |
          v
       Request
```

Nếu Bucket còn Token:

```text
Request → Allow
```

Nếu Bucket hết Token:

```text
Request → Rate Limited
```

Ưu điểm:

* Hỗ trợ Burst tốt.
* Có thể kiểm soát tốc độ Request.
* Phù hợp với API Rate Limiting.

### e. Leaky Bucket

Leaky Bucket xử lý Request với tốc độ tương đối ổn định.

```text
Requests
    |
    v
+---------+
| Bucket  |
+---------+
    |
    | Fixed Rate
    v
Processing
```

Ưu điểm:

* Giữ tốc độ xử lý ổn định.
* Hạn chế Burst.

Nhược điểm:

* Khả năng xử lý Burst kém linh hoạt hơn Token Bucket.

### f. So sánh các Rate Limiting Algorithms

| Algorithm      | Độ chính xác | Memory         | Burst Handling | Độ phức tạp |
| -------------- | ------------ | -------------- | -------------- | ----------- |
| Fixed Window   | Thấp         | Thấp           | Kém            | Thấp        |
| Sliding Window | Cao          | Trung bình/Cao | Tốt            | Trung bình  |
| Token Bucket   | Cao          | Thấp           | Tốt            | Trung bình  |
| Leaky Bucket   | Cao          | Thấp           | Hạn chế        | Trung bình  |

Việc lựa chọn Algorithm phụ thuộc vào yêu cầu về Accuracy, Memory, Performance và khả năng xử lý Burst của hệ thống.

---

## 2.5. Triển khai Rate Limiting

### a. Bucket4j

Đã tìm hiểu Bucket4j, một thư viện Java hỗ trợ triển khai Token Bucket Rate Limiting.

Ví dụ:

```java
Bandwidth limit = Bandwidth.builder()
        .capacity(100)
        .refillGreedy(100, Duration.ofMinutes(1))
        .build();

Bucket bucket = Bucket.builder()
        .addLimit(limit)
        .build();
```

Kiểm tra Request:

```java
if (bucket.tryConsume(1)) {
    // Allow request
} else {
    // Reject request
}
```

Bucket4j phù hợp với Rate Limiting được triển khai trực tiếp trong Application.

### b. Redis-based Distributed Rate Limiting

Trong hệ thống có nhiều Application Instance:

```text
             Load Balancer
                  |
        +---------+---------+
        |         |         |
      App 1     App 2     App 3
        |         |         |
        +---------+---------+
                  |
                Redis
```

Nếu mỗi Instance tự quản lý Counter riêng, Rate Limit có thể không chính xác.

Redis có thể được sử dụng làm Shared Storage:

```text
App 1 ─┐
App 2 ─┼──> Redis
App 3 ─┘
```

Ưu điểm:

* Shared State giữa các Instance.
* Tốc độ truy cập cao.
* Hỗ trợ Atomic Operations.
* Hỗ trợ TTL.
* Phù hợp với Distributed System.

### c. API Gateway-level Rate Limiting

Rate Limiting có thể được triển khai tại API Gateway thay vì trực tiếp trong từng Backend Service.

```text
Client
  |
  v
API Gateway
  |
  | Rate Limiting
  |
  v
Backend Services
```

Một số giải pháp:

* Spring Cloud Gateway.
* Nginx.
* Kong.

Ưu điểm:

* Chặn Request trước khi vào Backend.
* Giảm tải cho Backend.
* Quản lý Policy tập trung.
* Phù hợp với Microservices Architecture.

### d. Rate Limit theo User / IP / API Key

Rate Limit có thể được áp dụng theo nhiều Identifier.

**Theo IP:**

```text
IP: 192.168.1.10
Limit: 100 requests/minute
```

**Theo User:**

```text
User ID: 123
Limit: 1000 requests/minute
```

**Theo API Key:**

```text
API Key A
Limit: 10000 requests/hour
```

Việc lựa chọn Identifier phụ thuộc vào loại API và yêu cầu của hệ thống.

### e. HTTP 429 và Rate Limit Headers

Khi Client vượt quá Rate Limit, Server có thể trả về:

```http
HTTP/1.1 429 Too Many Requests
```

Có thể cung cấp thêm các Header:

```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1780000000
```

Ý nghĩa:

* `X-RateLimit-Limit`: Giới hạn Request tối đa.
* `X-RateLimit-Remaining`: Số Request còn lại.
* `X-RateLimit-Reset`: Thời điểm Rate Limit được Reset.

Các thông tin này giúp Client biết trạng thái Rate Limit và điều chỉnh tốc độ gửi Request.

---

## 3. Kết quả đạt được

Sau khi hoàn thành tuần học thứ năm, đã đạt được các kết quả sau:

* Hiểu kiến trúc cơ bản của Spring Boot.
* Hiểu cơ chế Auto-configuration.
* Nắm được IoC Container và Dependency Injection.
* Hiểu Spring MVC và Request Lifecycle.
* Nắm được cách thiết kế RESTful API.
* Hiểu HTTP Methods và HTTP Status Codes.
* Nắm được Configuration Properties và Spring Profiles.
* Hiểu các chiến lược Session-based và Token-based Authentication.
* Phân biệt Stateful và Stateless Authentication.
* Hiểu cấu trúc và cơ chế hoạt động của JWT.
* Nắm được Access Token và Refresh Token.
* Hiểu OAuth2/OIDC, API Key và mTLS.
* Hiểu Spring Security và Security Filter Chain.
* Nắm được `SecurityFilterChain`.
* Phân biệt Authentication và Authorization.
* Hiểu RBAC và ABAC.
* Nắm được Method-level Security với `@PreAuthorize`.
* Hiểu Token Revocation và Redis Blacklist.
* Hiểu khái niệm Rate Limiting và mục đích sử dụng.
* Nắm được Fixed Window và Sliding Window.
* Hiểu Token Bucket và Leaky Bucket.
* Biết các Trade-off giữa Accuracy, Memory và Burst Handling.
* Hiểu cách triển khai Rate Limiting với Bucket4j.
* Hiểu Distributed Rate Limiting sử dụng Redis.
* Hiểu Rate Limiting tại API Gateway.
* Nắm được Rate Limit theo User, IP và API Key.
* Hiểu HTTP `429 Too Many Requests`.
* Nắm được các `X-RateLimit-*` Response Headers.
* Xây dựng được nền tảng về Spring Boot, Authentication, Authorization và Rate Limiting để tiếp tục phát triển các Backend Application có tính bảo mật, khả năng mở rộng và kiểm soát Traffic tốt.

---

## 4. Kế hoạch tuần 6

###Yêu cầu ORM:###

- JPA/Hibernate fundamentals
- Entity mapping và relationships
- Repository pattern implementation
- Query optimization và performance tuning

###Lý thuyết về ORM:###

- **Hibernate Architecture**: SessionFactory, Session, Transaction
- **Entity Lifecycle**: Transient, Persistent, Detached, Removed
- **Lazy vs Eager Loading**: Performance implications và strategies
- **N+1 Query Problem**: Detection và solutions (batch fetching, join fetching)
- **Caching**: First-level, Second-level, Query cache
- **Connection Pool Integration**: Hibernate + HikariCP configuration
- **Transaction Management**: @Transactional, propagation, isolation

###Lý thuyết về Connection Pool:###

- **HikariCP Configuration**: Pool sizing, connection timeout, idle timeout
- **Pool Monitoring**: Connection leaks, performance metrics
- **Deadlock Prevention**: `pool_size = Tn × (Cm - 1) + 1`
    - Tn = Maximum threads
    - Cm = Max connections per thread
    - Formula ensures minimum pool size to avoid deadlock
- **Performance Optimization**: `(core_count * 2) + effective_spindle_count`
