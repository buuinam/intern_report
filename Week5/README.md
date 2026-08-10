# 📘 BÁO CÁO THỰC TẬP TUẦN 5

## Thông tin

* **Chủ đề:** Spring Boot & Middleware - Authentication + Rate Limiting
* **Intern:** Bùi Văn Nam
* **Team:** Platform - Adtech
* **Gmail:** [buivannam13032004@gmail.com](mailto:buivannam13032004@gmail.com)
* **Leader:** Nguyễn Văn Cương

---

# 1. Mục tiêu tuần

Trong tuần thứ năm, theo roadmap, nội dung tập trung vào **Spring Boot và Middleware**, trong đó hai nội dung trọng tâm là **Authentication** và **Rate Limiting**.

Đối với Spring Boot, em tìm hiểu kiến trúc Spring Boot, cơ chế Auto-configuration, Dependency Injection, IoC Container, Spring MVC, Request Lifecycle, RESTful API và Configuration Profiles.

Đối với Authentication, em tìm hiểu các phương thức xác thực phổ biến như Session-based Authentication, JWT, OAuth2/OIDC, API Key và mTLS. Đồng thời tìm hiểu cách Spring Security xử lý request thông qua Filter Chain, cách triển khai JWT Access Token/Refresh Token và các cơ chế Authorization như RBAC, ABAC.

Đối với Rate Limiting, em tìm hiểu các thuật toán Fixed Window, Sliding Window, Token Bucket và Leaky Bucket. Ngoài ra, em tìm hiểu cách triển khai Rate Limiting trong ứng dụng, sử dụng Redis cho môi trường nhiều instance và triển khai tại API Gateway.

Mục tiêu của tuần là xây dựng nền tảng để phát triển Backend API bằng Spring Boot có khả năng **xác thực người dùng, phân quyền và kiểm soát lưu lượng request**.

---

# 2. Lịch học Tuần 5

| Ngày      | Nội dung học                                  | Kết quả đạt được                                                                         |
| --------- | --------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Thứ 2** | Spring Boot Architecture & Auto-configuration | Hiểu kiến trúc Spring Boot và cơ chế Auto-configuration.                                 |
| **Thứ 3** | Dependency Injection, IoC & Spring MVC        | Hiểu IoC Container, DI và Request Lifecycle.                                             |
| **Thứ 4** | RESTful API & Configuration                   | Biết thiết kế REST API và quản lý Configuration/Profiles.                                |
| **Thứ 5** | Authentication & Spring Security              | Hiểu JWT, Security Filter Chain, Authorization và các chiến lược Authentication.         |
| **Thứ 6** | Rate Limiting                                 | Hiểu các thuật toán Rate Limiting và cách triển khai với Bucket4j, Redis và API Gateway. |

---

# 3. Chi tiết nội dung đã học

# 3.1. Spring Boot

Spring Boot là framework được xây dựng trên Spring Framework, giúp đơn giản hóa quá trình phát triển và triển khai ứng dụng Java Backend.

Spring Boot cung cấp:

* Auto-configuration.
* Starter Dependencies.
* Embedded Server.
* Dependency Injection.
* Spring MVC.
* Configuration Management.
* Production-ready features.

Mô hình tổng quát:

```text
Client
   |
   ↓
Spring Boot Application
   |
   ├── Controller
   |
   ├── Service
   |
   ├── Repository
   |
   └── Database
```

---

# 3.2. Spring Boot Architecture

Một ứng dụng Spring Boot thường được tổ chức thành nhiều Layer.

```text
┌─────────────────────────┐
│       Controller        │
│   HTTP Request/Response │
└────────────┬────────────┘
             ↓
┌─────────────────────────┐
│         Service         │
│     Business Logic      │
└────────────┬────────────┘
             ↓
┌─────────────────────────┐
│       Repository        │
│      Data Access        │
└────────────┬────────────┘
             ↓
┌─────────────────────────┐
│        Database         │
└─────────────────────────┘
```

Việc chia Layer giúp:

* Giảm coupling.
* Dễ bảo trì.
* Dễ testing.
* Dễ mở rộng.
* Phân tách trách nhiệm giữa các thành phần.

---

# 3.3. Auto-configuration

Một trong những tính năng quan trọng của Spring Boot là **Auto-configuration**.

Spring Boot dựa trên:

* Dependencies trong Classpath.
* Configuration.
* Beans đã tồn tại.

để tự động cấu hình các thành phần phù hợp.

Ví dụ khi thêm Spring Web dependency, Spring Boot có thể tự động cấu hình các thành phần cần thiết cho Web Application.

Điều này giúp giảm lượng Configuration thủ công.

Có thể hình dung:

```text
Dependencies
     |
     ↓
Spring Boot
     |
     ↓
Auto-configuration
     |
     ↓
Application Context
```

---

# 3.4. Dependency Injection

Dependency Injection (DI) là cơ chế Spring cung cấp Dependency cho Object thay vì Object tự tạo Dependency.

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

Trong trường hợp này, `UserService` không trực tiếp tạo `UserRepository`.

Spring Container sẽ chịu trách nhiệm tạo và inject dependency.

Lợi ích:

* Loose Coupling.
* Dễ Unit Test.
* Dễ thay đổi Implementation.
* Quản lý Object Lifecycle tập trung.

---

# 3.5. IoC Container

IoC là viết tắt của **Inversion of Control**.

Trong ứng dụng thông thường:

```text
Application
    |
    ↓
new Object()
    |
    ↓
Manage Object
```

Với Spring:

```text
Spring Container
      |
      ├── Create Bean
      ├── Configure Bean
      ├── Inject Dependency
      └── Manage Lifecycle
```

Spring IoC Container chịu trách nhiệm quản lý các Object được gọi là **Bean**.

Các Annotation thường gặp:

* `@Component`
* `@Service`
* `@Repository`
* `@Controller`
* `@RestController`

---

# 3.6. Spring MVC

Spring MVC là framework dùng để xây dựng Web Application và REST API.

Mô hình:

```text
Client
  |
  ↓
DispatcherServlet
  |
  ↓
Controller
  |
  ↓
Service
  |
  ↓
Repository
  |
  ↓
Database
```

Trong Spring MVC, `DispatcherServlet` đóng vai trò Front Controller, tiếp nhận request và điều phối request đến Controller phù hợp.

---

# 3.7. Request Lifecycle

Một HTTP Request trong Spring Boot có thể được xử lý theo flow:

```text
Client
  |
  ↓
HTTP Request
  |
  ↓
Servlet Container
  |
  ↓
Filter
  |
  ↓
DispatcherServlet
  |
  ↓
Controller
  |
  ↓
Service
  |
  ↓
Repository
  |
  ↓
Database
  |
  ↓
Response
```

Các bước chính:

1. Client gửi HTTP Request.
2. Request đi vào Servlet Container.
3. Request có thể đi qua các Filter.
4. `DispatcherServlet` tiếp nhận request.
5. Spring tìm Controller phù hợp.
6. Controller gọi Service.
7. Service xử lý Business Logic.
8. Repository tương tác Database.
9. Kết quả được trả về Controller.
10. Spring tạo HTTP Response.
11. Response được trả về Client.

---

# 3.8. RESTful API

REST là một architectural style thường được sử dụng để xây dựng Web API.

Một số HTTP Method:

| Method   | Mục đích          |
| -------- | ----------------- |
| `GET`    | Lấy dữ liệu       |
| `POST`   | Tạo dữ liệu       |
| `PUT`    | Cập nhật toàn bộ  |
| `PATCH`  | Cập nhật một phần |
| `DELETE` | Xóa dữ liệu       |

Ví dụ:

```text
GET    /api/users
GET    /api/users/{id}
POST   /api/users
PUT    /api/users/{id}
DELETE /api/users/{id}
```

---

# 3.9. REST API Best Practices

Một số nguyên tắc:

* Sử dụng HTTP Method đúng mục đích.
* URL sử dụng Resource thay vì Action.
* Sử dụng HTTP Status Code phù hợp.
* Chuẩn hóa Response.
* Validate Request.
* Xử lý Exception tập trung.
* Không trả về dữ liệu không cần thiết.
* Version API khi cần thiết.
* Sử dụng Pagination với danh sách lớn.

Một số HTTP Status Code:

```text
200 OK
201 Created
204 No Content
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
409 Conflict
429 Too Many Requests
500 Internal Server Error
```

---

# 3.10. Configuration Properties

Spring Boot hỗ trợ quản lý Configuration thông qua:

* `application.properties`
* `application.yml`
* Environment Variables.
* Command Line Arguments.

Ví dụ:

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/app
    username: root
```

Configuration nên được tách khỏi Source Code để dễ thay đổi giữa các môi trường.

---

# 3.11. Spring Profiles

Spring Profiles cho phép cấu hình ứng dụng theo từng môi trường.

Ví dụ:

```text
application.yml
application-dev.yml
application-test.yml
application-prod.yml
```

Có thể sử dụng:

```text
dev
test
prod
```

Ví dụ:

```yaml
spring:
  profiles:
    active: dev
```

Lợi ích:

* Tách Configuration giữa các môi trường.
* Không cần sửa Source Code.
* Dễ triển khai.
* Hạn chế cấu hình nhầm Production.

---

# 4. Middleware - Authentication

Authentication là quá trình xác định **người dùng là ai**.

Authorization là quá trình xác định **người dùng được phép làm gì**.

Có thể phân biệt:

```text
Authentication
      ↓
Who are you?

Authorization
      ↓
What can you do?
```

---

# 4.1. Session-based Authentication

Session-based Authentication thường sử dụng Cookie.

Flow:

```text
Client
  |
  | Login
  ↓
Server
  |
  | Create Session
  ↓
Session Store
  |
  ↓
Cookie
  |
  ↓
Client
```

Client gửi Cookie trong các request tiếp theo.

Server sử dụng Session ID để xác định user.

Ưu điểm:

* Dễ triển khai.
* Có thể dễ dàng revoke Session.
* Server kiểm soát Session.

Nhược điểm:

* Server phải quản lý Session.
* Khó scale nếu không có Shared Session Store.
* Có thể cần Redis hoặc Session Store tập trung.

---

# 4.2. Token-based Authentication

Trong Token-based Authentication, Server cấp Token cho Client sau khi Login.

Flow:

```text
Client
  |
  | Username + Password
  ↓
Server
  |
  | Generate Token
  ↓
Client
  |
  | Authorization: Bearer Token
  ↓
Server
```

JWT là một trong những Token Format phổ biến.

---

# 4.3. JWT

JWT gồm ba thành phần chính:

```text
Header.Payload.Signature
```

Ví dụ cấu trúc:

```text
xxxxx.yyyyy.zzzzz
```

Payload có thể chứa:

* `sub`
* `iat`
* `exp`
* `roles`

JWT được ký bằng Secret Key hoặc Private Key để đảm bảo tính toàn vẹn.

---

# 4.4. Access Token và Refresh Token

Một hệ thống Authentication thường sử dụng hai loại Token:

```text
Access Token
    ↓
Thời gian sống ngắn
    ↓
Dùng gọi API

Refresh Token
    ↓
Thời gian sống dài hơn
    ↓
Dùng lấy Access Token mới
```

Flow:

```text
Client
  |
  | Access Token expired
  ↓
Refresh Token
  |
  ↓
Authentication Server
  |
  ↓
New Access Token
```

Việc sử dụng Access Token có thời gian sống ngắn giúp giảm rủi ro khi Token bị lộ.

---

# 4.5. Token Revocation

JWT thường có đặc điểm Stateless nên Server không nhất thiết lưu Session.

Tuy nhiên điều này gây khó khăn khi cần revoke Token trước thời gian hết hạn.

Một số giải pháp:

* Token Blacklist.
* Short-lived Access Token.
* Refresh Token Rotation.
* Lưu trạng thái Token trong Redis.

---

# 4.6. JWT Blacklist với Redis

Redis có thể lưu những Token đã bị revoke.

Mô hình:

```text
Client
  |
  ↓
Spring Security
  |
  ↓
Check JWT
  |
  ↓
Redis
  |
  ├── Token exists → Reject
  |
  └── Token absent → Continue
```

Khi Logout hoặc Token bị revoke, Token có thể được thêm vào Redis với TTL tương ứng với thời gian còn lại của Token.

---

# 4.7. OAuth2 và OIDC

OAuth2 là framework cho Authorization.

OIDC xây dựng trên OAuth2 và bổ sung Authentication.

Có thể sử dụng với các Identity Provider bên ngoài.

Flow cơ bản:

```text
User
  |
  ↓
Client Application
  |
  ↓
Authorization Server
  |
  ↓
Authentication
  |
  ↓
Authorization Code
  |
  ↓
Access Token
```

---

# 4.8. API Key

API Key là một chuỗi định danh được cấp cho Client.

Ví dụ:

```text
X-API-Key: abc123
```

Thường được sử dụng cho:

* Internal API.
* Service-to-service communication.
* Public API.
* Developer API.

API Key đơn giản nhưng cần được bảo vệ và quản lý vòng đời.

---

# 4.9. mTLS

mTLS là Mutual TLS.

Trong HTTPS thông thường:

```text
Client → Server
Server xác thực Client
```

Với mTLS:

```text
Client ↔ Server
```

Cả Client và Server đều xác thực Certificate của nhau.

mTLS thường phù hợp với:

* Service-to-service communication.
* Internal systems.
* High-security environments.

---

# 4.10. Stateless vs Stateful Authentication

## Stateful

Server lưu trạng thái Authentication.

Ví dụ:

```text
Client
  ↓
Session ID
  ↓
Server Session Store
```

Ưu điểm:

* Dễ revoke.
* Quản lý Session tập trung.

Nhược điểm:

* Cần Session Store.
* Scale phức tạp hơn.

---

## Stateless

Server không cần lưu Session cho từng Client.

Ví dụ:

```text
Client
  ↓
JWT
  ↓
Server verifies token
```

Ưu điểm:

* Dễ scale.
* Không phụ thuộc Session Store.
* Phù hợp với Microservices.

Nhược điểm:

* Khó revoke Token.
* Token có thể chứa nhiều thông tin.
* Cần quản lý Token Expiration.

---

# 5. Spring Security

Spring Security cung cấp các cơ chế:

* Authentication.
* Authorization.
* Password Management.
* Security Filter.
* Method-level Security.
* CSRF Protection.
* OAuth2/JWT Support.

---

# 5.1. Security Filter Chain

Spring Security xử lý HTTP Request thông qua một chuỗi Filter.

```text
HTTP Request
     |
     ↓
Security Filters
     |
     ├── Authentication
     ├── Authorization
     ├── CSRF
     └── Exception Handling
     |
     ↓
Controller
```

Mỗi Filter đảm nhiệm một phần công việc liên quan đến Security.

---

# 5.2. SecurityFilterChain

Spring Security cho phép cấu hình Security bằng `SecurityFilterChain`.

Ví dụ khái quát:

```java
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http) {
    return http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/public/**").permitAll()
            .anyRequest().authenticated()
        )
        .build();
}
```

Qua đó có thể định nghĩa:

* Endpoint Public.
* Endpoint yêu cầu Authentication.
* Authorization Rules.
* Security Policies.

---

# 5.3. Authorization

Authorization xác định quyền của User sau khi Authentication thành công.

Có hai mô hình được tìm hiểu:

* RBAC.
* ABAC.

---

# 5.4. RBAC

RBAC là **Role-Based Access Control**.

Quyền được xác định dựa trên Role.

Ví dụ:

```text
USER
 ├── READ_PROFILE
 └── CREATE_ORDER

ADMIN
 ├── READ_PROFILE
 ├── CREATE_ORDER
 ├── DELETE_USER
 └── MANAGE_SYSTEM
```

Ưu điểm:

* Dễ triển khai.
* Dễ quản lý.
* Phù hợp với nhiều hệ thống.

---

# 5.5. ABAC

ABAC là **Attribute-Based Access Control**.

Quyền được xác định dựa trên nhiều Attribute:

* User.
* Resource.
* Action.
* Environment.

Ví dụ:

```text
User.department = "Finance"
AND
Resource.department = "Finance"
AND
Action = "READ"
```

ABAC linh hoạt hơn RBAC nhưng phức tạp hơn trong việc thiết kế Policy.

---

# 5.6. Method-level Security

Spring Security hỗ trợ Authorization ở Method Level.

Ví dụ:

```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) {
    // ...
}
```

Điều này giúp kiểm soát quyền trực tiếp tại Business Method.

---

# 6. Middleware - Rate Limiting

Rate Limiting là cơ chế giới hạn số lượng Request mà một Client có thể gửi trong một khoảng thời gian.

Mục tiêu:

* Chống Abuse.
* Chống Brute Force.
* Bảo vệ API.
* Bảo vệ Database.
* Kiểm soát Resource.
* Ổn định hệ thống khi Traffic tăng đột biến.

Ví dụ:

```text
100 requests / minute / user
```

Nếu vượt quá giới hạn:

```text
HTTP 429 Too Many Requests
```

---

# 6.1. Fixed Window

Fixed Window chia thời gian thành các khoảng cố định.

Ví dụ:

```text
10:00:00 ───── 10:01:00
             100 requests
```

Rule:

```text
100 requests / minute
```

Ưu điểm:

* Dễ triển khai.
* Chi phí thấp.
* Dễ hiểu.

Nhược điểm:

* Có Boundary Problem.

Ví dụ Client có thể gửi:

```text
100 requests
59 giây cuối Window A

+

100 requests
đầu Window B
```

Có thể tạo Burst lớn tại Boundary.

---

# 6.2. Sliding Window

Sliding Window xem xét một khoảng thời gian liên tục thay vì Window cố định.

Ví dụ:

```text
Current Time
     |
     ↓
<---- 60 seconds ---->
```

Có thể triển khai bằng:

* Sliding Window Log.
* Sliding Window Counter.

Ưu điểm:

* Chính xác hơn Fixed Window.
* Giảm Boundary Problem.

Nhược điểm:

* Tốn tài nguyên hơn.
* Sliding Window Log có thể cần lưu nhiều request timestamps.

---

# 6.3. Token Bucket

Token Bucket sử dụng một Bucket chứa Token.

Mỗi Request cần tiêu thụ một Token.

```text
       Token refill
            ↓
      ┌───────────┐
      │  ● ● ● ●  │
      │  ● ● ●    │
      └─────┬─────┘
            ↓
         Request
```

Nếu Bucket còn Token:

```text
Request → Allow
```

Nếu hết Token:

```text
Request → Reject / Wait
```

Ưu điểm:

* Hỗ trợ Burst.
* Kiểm soát Average Rate.
* Phù hợp với API Rate Limiting.

---

# 6.4. Leaky Bucket

Leaky Bucket có thể hình dung giống như một Bucket có tốc độ xử lý cố định.

```text
Requests
   ↓↓↓↓↓
┌─────────┐
│         │
│ Bucket  │
│         │
└────┬────┘
     ↓
 Fixed Rate
```

Request được xử lý với tốc độ tương đối ổn định.

Ưu điểm:

* Kiểm soát Output Rate.
* Giảm Burst.

Nhược điểm:

* Có thể làm tăng latency.
* Burst không được xử lý linh hoạt như Token Bucket.

---

# 6.5. So sánh các thuật toán

| Thuật toán     | Ưu điểm             | Nhược điểm          |
| -------------- | ------------------- | ------------------- |
| Fixed Window   | Đơn giản, ít memory | Boundary Problem    |
| Sliding Window | Chính xác hơn       | Tốn tài nguyên hơn  |
| Token Bucket   | Hỗ trợ Burst        | Cần quản lý Token   |
| Leaky Bucket   | Output ổn định      | Có thể tăng latency |

Việc lựa chọn thuật toán phụ thuộc vào:

* Traffic Pattern.
* Độ chính xác yêu cầu.
* Memory.
* Burst Handling.
* Số lượng Instance.

---

# 6.6. Rate Limiting bằng Bucket4j

Bucket4j là thư viện Java hỗ trợ Token Bucket Rate Limiting.

Mô hình:

```text
Request
   |
   ↓
Bucket4j
   |
   ├── Token available → Allow
   |
   └── No token → Reject
```

Phù hợp khi Rate Limiting được triển khai trực tiếp trong Application.

Ưu điểm:

* Dễ tích hợp.
* Không cần Redis cho trường hợp Single Instance.
* Hiệu năng tốt.

Nhược điểm:

* Nếu có nhiều Application Instance, mỗi Instance có Bucket riêng.
* Không đảm bảo giới hạn toàn hệ thống nếu không có Shared State.

---

# 6.7. Distributed Rate Limiting với Redis

Trong hệ thống có nhiều Instance:

```text
             Load Balancer
                  |
        ┌─────────┼─────────┐
        ↓         ↓         ↓
    Instance A Instance B Instance C
        |         |         |
        └─────────┼─────────┘
                  ↓
                Redis
```

Redis được sử dụng làm Shared State.

Ví dụ:

```text
user:123:rate_limit
```

Các Instance cùng kiểm tra và cập nhật Rate Limit tại Redis.

Ưu điểm:

* Rate Limit nhất quán giữa nhiều Instance.
* Phù hợp Microservices.
* Có thể scale Application.

Nhược điểm:

* Có thêm Network I/O.
* Phụ thuộc Redis.
* Cần xử lý Redis failure.

---

# 6.8. API Gateway Rate Limiting

Rate Limiting có thể triển khai tại API Gateway.

Mô hình:

```text
Client
  |
  ↓
API Gateway
  |
  ├── Authentication
  ├── Rate Limiting
  └── Routing
        |
        ↓
Backend Services
```

Các công cụ có thể sử dụng:

* Spring Cloud Gateway.
* Nginx.
* Kong.

Ưu điểm:

* Chặn Request trước khi vào Backend.
* Bảo vệ toàn bộ hệ thống.
* Centralized Policy.

---

# 6.9. Rate Limit theo User/IP/API Key

Có thể áp dụng Rate Limit dựa trên:

### User

```text
user:123 → 100 requests/minute
```

### IP

```text
192.168.1.10 → 100 requests/minute
```

### API Key

```text
api-key-abc → 1000 requests/hour
```

Việc lựa chọn Key phụ thuộc vào mô hình Authentication và yêu cầu của hệ thống.

---

# 6.10. HTTP 429

Khi Client vượt quá Rate Limit, Server có thể trả:

```http
HTTP/1.1 429 Too Many Requests
```

Response có thể cung cấp thêm thông tin về giới hạn.

Ví dụ:

```text
X-RateLimit-Limit
X-RateLimit-Remaining
X-RateLimit-Reset
```

Các Header này giúp Client biết:

* Giới hạn hiện tại.
* Số Request còn lại.
* Thời điểm Rate Limit được reset.

---

# 7. So sánh Authentication và Authorization

| Nội dung  | Authentication      | Authorization      |
| --------- | ------------------- | ------------------ |
| Mục đích  | Xác định User       | Xác định quyền     |
| Câu hỏi   | Who are you?        | What can you do?   |
| Ví dụ     | Login, JWT          | RBAC, ABAC         |
| Thời điểm | Trước Authorization | Sau Authentication |

Flow tổng quát:

```text
Client
   |
   ↓
Authentication
   |
   ↓
Identity
   |
   ↓
Authorization
   |
   ↓
Access Resource
```

---

# 8. So sánh Stateful và Stateless

| Tiêu chí           | Stateful     | Stateless        |
| ------------------ | ------------ | ---------------- |
| Server lưu Session | Có           | Không nhất thiết |
| Scale              | Phức tạp hơn | Dễ hơn           |
| Revoke             | Dễ           | Khó hơn          |
| Shared Store       | Thường cần   | Không nhất thiết |
| Ví dụ              | Session      | JWT              |

---

# 9. Kết quả đạt được

Sau tuần thứ năm, em đã đạt được các kết quả:

## Spring Boot

* Hiểu kiến trúc Spring Boot.
* Hiểu cơ chế Auto-configuration.
* Nắm được Dependency Injection.
* Hiểu IoC Container.
* Hiểu Spring MVC.
* Nắm được Request Lifecycle.
* Hiểu cách thiết kế RESTful API.
* Biết các HTTP Method và Status Code.
* Hiểu Configuration Properties.
* Biết sử dụng Spring Profiles.

## Authentication

* Hiểu Session-based Authentication.
* Hiểu Token-based Authentication.
* Hiểu JWT.
* Phân biệt Access Token và Refresh Token.
* Hiểu OAuth2/OIDC.
* Biết khái niệm API Key.
* Hiểu mTLS.
* Phân biệt Stateful và Stateless Authentication.
* Hiểu Spring Security Filter Chain.
* Biết cấu hình `SecurityFilterChain`.
* Hiểu Token Revocation.
* Biết cách sử dụng Redis làm Token Blacklist.
* Hiểu RBAC và ABAC.
* Biết Method-level Security với `@PreAuthorize`.

## Rate Limiting

* Hiểu mục đích của Rate Limiting.
* Nắm được Fixed Window.
* Nắm được Sliding Window.
* Hiểu Token Bucket.
* Hiểu Leaky Bucket.
* Biết so sánh ưu nhược điểm của từng thuật toán.
* Hiểu cách triển khai Bucket4j.
* Hiểu Distributed Rate Limiting với Redis.
* Hiểu Rate Limiting tại API Gateway.
* Biết Rate Limit theo User/IP/API Key.
* Hiểu HTTP 429.
* Biết vai trò của các `X-RateLimit-*` Headers.

---

# 10. Khó khăn và hướng khắc phục

Trong quá trình học tập, em gặp một số khó khăn:

* Spring Boot có nhiều cơ chế tự động nên ban đầu khó hiểu cách các Bean được tạo và quản lý.
* Dependency Injection và IoC yêu cầu thay đổi cách tư duy so với việc tự tạo Object bằng `new`.
* Request Lifecycle của Spring MVC có nhiều thành phần như Filter, DispatcherServlet, Controller và Service.
* JWT có ưu điểm Stateless nhưng việc Revoke Token và Logout cần thiết kế thêm cơ chế quản lý trạng thái.
* RBAC đơn giản nhưng không linh hoạt bằng ABAC trong các hệ thống có Policy phức tạp.
* Các thuật toán Rate Limiting có cách hoạt động và Trade-off khác nhau.
* Distributed Rate Limiting cần xử lý vấn đề đồng bộ State giữa nhiều Application Instance.
* Việc lựa chọn vị trí triển khai Rate Limiting giữa Application và API Gateway cần dựa trên yêu cầu thực tế.

Để khắc phục, em tập trung xây dựng sơ đồ Flow cho từng cơ chế, so sánh các phương pháp theo ưu nhược điểm và thực hành cấu hình từng thành phần để hiểu rõ cách chúng hoạt động.

---

# 11. Kế hoạch Tuần 6

Trong tuần thứ sáu, nội dung tiếp theo sẽ tập trung vào **ORM với JPA/Hibernate**.

## JPA/Hibernate

Các nội dung dự kiến:

* JPA Fundamentals.
* Hibernate Architecture.
* Entity Mapping.
* Entity Relationships.
* Repository Pattern.
* Entity Lifecycle.
* Lazy Loading.
* Eager Loading.
* N+1 Query Problem.
* Query Optimization.
* Caching.
* Transaction Management.

## Connection Pool

Tiếp tục tìm hiểu:

* HikariCP.
* Connection Pool Configuration.
* Pool Sizing.
* Connection Timeout.
* Idle Timeout.
* Connection Leak Detection.
* Performance Metrics.
* Deadlock Prevention.
* Connection Pool Performance Optimization.

Mục tiêu là hiểu cách ORM hoạt động bên dưới Application Layer và biết cách tối ưu việc truy cập Database trong ứng dụng Spring Boot.

---

# 12. Kết luận

Tuần thứ năm giúp em xây dựng nền tảng quan trọng về **Spring Boot, Authentication và Rate Limiting**.

Về Spring Boot, em đã hiểu kiến trúc ứng dụng, Auto-configuration, IoC, Dependency Injection, Spring MVC, Request Lifecycle và RESTful API.

Về Authentication, em đã tìm hiểu nhiều phương thức xác thực từ Session-based, JWT, OAuth2/OIDC, API Key đến mTLS. Đồng thời hiểu cách Spring Security sử dụng Filter Chain để xử lý Authentication và Authorization.

Về Rate Limiting, em đã tìm hiểu các thuật toán Fixed Window, Sliding Window, Token Bucket và Leaky Bucket. Bên cạnh đó, em hiểu cách triển khai Rate Limiting trong Application bằng Bucket4j, sử dụng Redis cho Distributed Rate Limiting và triển khai tại API Gateway.

Những kiến thức trong tuần là nền tảng quan trọng để tiếp tục tìm hiểu **JPA/Hibernate, ORM, Transaction và Connection Pool** trong tuần thứ sáu, từ đó nâng cao khả năng xây dựng và tối ưu Backend Application bằng Spring Boot.
