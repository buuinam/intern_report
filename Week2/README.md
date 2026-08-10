# 📘 BÁO CÁO THỰC TẬP TUẦN 2

## Thông tin

* **Chủ đề:** Collections, Design Patterns & Testing
* **Intern:** Bùi Văn Nam
* **Team:** Platform - Adtech
* **Gmail:** [buivannam13032004@gmail.com](mailto:buivannam13032004@gmail.com)
* **Leader:** Nguyễn Văn Cương

---

# 1. Mục tiêu tuần

Trong tuần thứ hai, theo roadmap, mục tiêu là tìm hiểu chuyên sâu hơn về **Java Collections Framework**, một số **Design Patterns phổ biến** và các kiến thức nền tảng về **Software Testing**.

Đối với Collections, tập trung tìm hiểu cách hoạt động bên trong của `HashMap`, `HashSet`, `ArrayList`, cơ chế `hashCode()` và `equals()`, cũng như các Collection hỗ trợ môi trường đa luồng như `ConcurrentHashMap` và `BlockingQueue`.

Đối với Design Patterns, tìm hiểu các Pattern phổ biến gồm:

* Singleton.
* Factory.
* Observer.
* Strategy.

Đối với Testing, tập trung vào:

* Unit Testing.
* JUnit 5.
* Mocking.
* Integration Testing.
* Test Coverage.
* Quality Metrics.

Mục tiêu chung là hiểu không chỉ cách sử dụng các thành phần trên mà còn hiểu được **nguyên lý hoạt động, trường hợp sử dụng và ảnh hưởng đến khả năng bảo trì, hiệu năng và chất lượng của hệ thống**.

---

# 2. Lịch học Tuần 2

| Ngày      | Nội dung học                                 | Kết quả đạt được                                                                    |
| --------- | -------------------------------------------- | ----------------------------------------------------------------------------------- |
| **Thứ 2** | HashMap, HashSet, ArrayList Internals        | Hiểu cấu trúc bên trong và cách các Collection xử lý dữ liệu.                       |
| **Thứ 3** | HashCode, Equals & Concurrent Collections    | Hiểu HashCode/Equals Contract và làm quen với `ConcurrentHashMap`, `BlockingQueue`. |
| **Thứ 4** | Design Patterns                              | Hiểu Singleton, Factory, Observer và Strategy Pattern.                              |
| **Thứ 5** | Unit Testing & JUnit 5                       | Hiểu nguyên tắc Unit Testing và cách xây dựng test với JUnit 5.                     |
| **Thứ 6** | Mocking, Integration Testing & Test Coverage | Hiểu Mocking, Integration Testing và các chỉ số đánh giá chất lượng test.           |

---

# 3. Chi tiết nội dung đã học

# 3.1. Java Collections Internals

Trong tuần này, em đi sâu hơn vào cách Java Collections hoạt động bên trong thay vì chỉ sử dụng các API có sẵn.

Các Collection trọng tâm:

* `ArrayList`
* `HashMap`
* `HashSet`

---

## 3.1.1. ArrayList Internals

`ArrayList` được xây dựng dựa trên một mảng động.

Về cơ bản, ArrayList sử dụng một mảng bên trong để lưu trữ các phần tử.

Khi thêm phần tử:

```java
list.add(element);
```

Nếu mảng bên trong đã đầy, ArrayList sẽ cần mở rộng capacity và sao chép các phần tử sang vùng nhớ mới.

### Đặc điểm

* Truy cập theo index nhanh.
* Dữ liệu được lưu trữ liên tiếp trong cấu trúc mảng.
* Thêm phần tử cuối thường có độ phức tạp amortized `O(1)`.
* Chèn hoặc xóa phần tử ở giữa có thể có độ phức tạp `O(n)` do phải dịch chuyển phần tử.

### Độ phức tạp

| Operation       |     Complexity |
| --------------- | -------------: |
| `get()`         |           O(1) |
| `set()`         |           O(1) |
| `add()` cuối    | O(1) amortized |
| `add(index)`    |           O(n) |
| `remove(index)` |           O(n) |
| `contains()`    |           O(n) |

Qua nội dung này, em hiểu rằng ArrayList phù hợp với các trường hợp cần truy cập phần tử thường xuyên bằng index.

---

# 3.2. HashMap Internals

`HashMap` là một trong những Collection quan trọng nhất trong Java.

HashMap lưu dữ liệu theo dạng:

```text
Key → Value
```

Ví dụ:

```java
Map<String, Integer> scores = new HashMap<>();
```

Khi thêm dữ liệu:

```java
scores.put("Nam", 90);
```

HashMap sẽ sử dụng `hashCode()` của key để xác định vị trí bucket phù hợp.

Quá trình xử lý cơ bản:

```text
Key
 ↓
hashCode()
 ↓
Hash
 ↓
Bucket
 ↓
Entry/Node
 ↓
Value
```

---

## Bucket

HashMap sử dụng một array các bucket để lưu trữ các entry.

Mỗi entry chứa thông tin tương tự:

```text
Hash
Key
Value
Next
```

Khi nhiều key có hash dẫn đến cùng một bucket sẽ xảy ra **Collision**.

---

## Collision

Collision xảy ra khi nhiều key được ánh xạ vào cùng một bucket.

Java sử dụng cấu trúc liên kết để xử lý collision.

Trong các phiên bản Java hiện đại, khi số lượng node trong một bucket đủ lớn và thỏa mãn các điều kiện nhất định, cấu trúc có thể chuyển từ linked list sang balanced tree để cải thiện hiệu năng tìm kiếm.

Qua nội dung này, em hiểu rằng hiệu năng của HashMap phụ thuộc nhiều vào chất lượng của `hashCode()` và cách dữ liệu được phân bố trong các bucket.

---

## Độ phức tạp HashMap

Trong điều kiện thông thường:

| Operation       | Average |
| --------------- | ------: |
| `put()`         |    O(1) |
| `get()`         |    O(1) |
| `remove()`      |    O(1) |
| `containsKey()` |    O(1) |

Trong trường hợp xảy ra nhiều collision, hiệu năng có thể giảm.

---

# 3.3. HashSet Internals

`HashSet` được sử dụng để lưu tập hợp các phần tử không trùng nhau.

Một điểm quan trọng là `HashSet` được xây dựng dựa trên `HashMap`.

Có thể hình dung:

```text
HashSet
   |
   └── HashMap
          |
          ├── Key
          └── Dummy Value
```

Khi thêm một phần tử vào HashSet:

```java
set.add("Nam");
```

Phần tử được sử dụng như key của một HashMap bên trong.

Do đó, HashSet cũng phụ thuộc vào:

* `hashCode()`
* `equals()`

để xác định phần tử có tồn tại hay chưa.

### Đặc điểm

* Không cho phép duplicate.
* Không đảm bảo thứ tự.
* Các thao tác cơ bản thường có độ phức tạp trung bình `O(1)`.

Qua đó hiểu được mối quan hệ giữa `HashSet` và `HashMap`.

---

# 3.4. HashCode và Equals Contract

Đây là một nội dung quan trọng khi làm việc với:

* `HashMap`
* `HashSet`
* `Hashtable`
* Các cấu trúc dữ liệu dựa trên hashing.

## equals()

`equals()` được sử dụng để kiểm tra hai object có được xem là bằng nhau hay không.

Ví dụ:

```java
user1.equals(user2)
```

---

## hashCode()

`hashCode()` trả về giá trị hash đại diện cho object.

Hash-based Collection sử dụng hash code để xác định vị trí lưu trữ hoặc tìm kiếm object.

---

## HashCode và Equals Contract

Một số nguyên tắc quan trọng:

### Quy tắc 1

Nếu:

```java
a.equals(b) == true
```

thì:

```java
a.hashCode() == b.hashCode()
```

phải đúng.

### Quy tắc 2

Nếu:

```java
a.hashCode() == b.hashCode()
```

thì không nhất thiết:

```java
a.equals(b) == true
```

Vì có thể xảy ra hash collision.

### Quy tắc 3

Nếu override `equals()` thì thông thường cần override `hashCode()`.

Nếu không tuân thủ contract này, HashMap và HashSet có thể hoạt động không đúng như mong đợi.

---

# 3.5. Concurrent Collections

Trong môi trường Multithreading, việc sử dụng Collection thông thường có thể dẫn đến race condition hoặc các vấn đề về thread safety.

Do đó, Java cung cấp các Concurrent Collections.

Các nội dung tập trung:

* `ConcurrentHashMap`
* `BlockingQueue`

---

## ConcurrentHashMap

`ConcurrentHashMap` được thiết kế để cho phép nhiều thread truy cập và cập nhật dữ liệu đồng thời với mức độ đồng bộ hóa phù hợp.

Ví dụ:

```java
ConcurrentHashMap<String, Integer> map =
        new ConcurrentHashMap<>();
```

Một số đặc điểm:

* Thread-safe.
* Hỗ trợ concurrent read/write.
* Không cho phép `null` key hoặc `null` value.
* Phù hợp với các ứng dụng có nhiều thread cùng truy cập Map.

So với việc đồng bộ toàn bộ `HashMap`, `ConcurrentHashMap` được thiết kế để đạt concurrency tốt hơn.

---

# 3.6. BlockingQueue

`BlockingQueue` là một Queue hỗ trợ cơ chế chờ khi queue ở trạng thái:

* Đầy.
* Rỗng.

Một số implementation phổ biến:

```text
ArrayBlockingQueue
LinkedBlockingQueue
PriorityBlockingQueue
```

Ví dụ mô hình Producer - Consumer:

```text
Producer
   |
   ↓
BlockingQueue
   |
   ↓
Consumer
```

Producer thêm dữ liệu vào queue.

Consumer lấy dữ liệu từ queue.

Nếu queue rỗng, Consumer có thể chờ dữ liệu.

Nếu queue đầy, Producer có thể chờ cho đến khi có vị trí trống.

BlockingQueue rất hữu ích trong các hệ thống xử lý công việc bất đồng bộ và mô hình Producer-Consumer.

---

# 3.7. Design Patterns

Design Pattern là các giải pháp thiết kế đã được chuẩn hóa cho những vấn đề thường gặp trong phát triển phần mềm.

Trong tuần này, em tìm hiểu bốn Pattern:

* Singleton.
* Factory.
* Observer.
* Strategy.

---

# 3.8. Singleton Pattern

Singleton đảm bảo một class chỉ có một instance trong phạm vi mà Pattern quản lý và cung cấp một cách truy cập instance đó.

Mục đích thường gặp:

* Quản lý một resource dùng chung.
* Configuration.
* Một số service đặc biệt.

Cấu trúc cơ bản:

```text
Singleton
   |
   ├── private constructor
   ├── static instance
   └── getInstance()
```

Một vấn đề quan trọng khi triển khai Singleton trong môi trường Multithreading là đảm bảo quá trình khởi tạo instance an toàn.

Qua Pattern này, em hiểu thêm về:

* Object lifecycle.
* Private constructor.
* Static instance.
* Thread safety.

---

# 3.9. Factory Pattern

Factory Pattern được sử dụng để tách logic tạo object khỏi code sử dụng object.

Thay vì:

```java
new MomoPayment();
```

Code có thể sử dụng một Factory để tạo implementation phù hợp.

Mô hình:

```text
Client
   |
   ↓
Factory
   |
   ├── Product A
   ├── Product B
   └── Product C
```

Ưu điểm:

* Giảm coupling.
* Tập trung logic khởi tạo.
* Dễ mở rộng khi có thêm implementation.

Factory Pattern thường được sử dụng khi hệ thống có nhiều loại object cùng implement một Interface hoặc kế thừa cùng một base class.

---

# 3.10. Observer Pattern

Observer Pattern mô tả quan hệ:

```text
Subject
   |
   ├── Observer 1
   ├── Observer 2
   └── Observer 3
```

Khi trạng thái của Subject thay đổi, các Observer được thông báo.

Ví dụ thực tế:

```text
Order Created
     |
     ├── Send Email
     ├── Send Notification
     └── Update Statistics
```

Ưu điểm:

* Giảm coupling giữa Subject và Observer.
* Dễ thêm Observer mới.
* Phù hợp với các hệ thống Event-driven.

---

# 3.11. Strategy Pattern

Strategy Pattern cho phép định nghĩa nhiều thuật toán hoặc cách xử lý khác nhau và có thể thay đổi chúng một cách linh hoạt.

Ví dụ:

```text
PaymentStrategy
       |
       ├── CashPayment
       ├── BankPayment
       └── MomoPayment
```

Client có thể lựa chọn Strategy phù hợp tại runtime.

Ưu điểm:

* Giảm các khối `if-else` hoặc `switch` lớn.
* Dễ mở rộng.
* Dễ test từng strategy.
* Tuân thủ tốt Open/Closed Principle.

Qua Strategy Pattern, em hiểu rõ hơn cách áp dụng polymorphism để thay thế các logic điều kiện phức tạp.

---

# 3.12. Unit Testing

Unit Testing là quá trình kiểm thử từng đơn vị nhỏ của chương trình một cách độc lập.

Một Unit thường có thể là:

* Method.
* Class.
* Một đơn vị logic nghiệp vụ.

Mục tiêu:

* Phát hiện lỗi sớm.
* Đảm bảo logic hoạt động đúng.
* Giảm rủi ro khi thay đổi code.
* Hỗ trợ Refactoring.
* Cải thiện chất lượng code.

---

## Nguyên tắc Unit Testing

Một Unit Test tốt nên:

* Độc lập.
* Có kết quả xác định.
* Chạy nhanh.
* Dễ đọc.
* Dễ bảo trì.
* Không phụ thuộc vào database hoặc external service nếu không cần thiết.

Một test thường có cấu trúc:

```text
Arrange
   ↓
Act
   ↓
Assert
```

### Arrange

Chuẩn bị dữ liệu và trạng thái cần thiết.

### Act

Thực hiện hành động cần kiểm thử.

### Assert

Kiểm tra kết quả thực tế có đúng với kết quả mong đợi hay không.

---

# 3.13. JUnit 5

JUnit 5 là framework phổ biến để viết Unit Test trong Java.

Một số annotation quan trọng:

```text
@Test
@BeforeEach
@AfterEach
@BeforeAll
@AfterAll
@DisplayName
```

Các Assertion phổ biến:

```text
assertEquals()
assertNotEquals()
assertTrue()
assertFalse()
assertNull()
assertNotNull()
assertThrows()
```

Ví dụ cấu trúc:

```java
@Test
void shouldCalculateTotalCorrectly() {
    // Arrange

    // Act

    // Assert
}
```

JUnit 5 cung cấp nhiều tính năng giúp xây dựng test có cấu trúc và dễ quản lý.

---

# 3.14. Mocking

Mocking là kỹ thuật tạo ra các object giả lập để thay thế dependency thật trong quá trình Unit Testing.

Ví dụ:

```text
UserService
     |
     ↓
UserRepository
```

Khi test `UserService`, không nhất thiết phải truy cập database thật.

Có thể mock:

```text
UserRepository
```

Mục đích:

* Cô lập Unit cần test.
* Không phụ thuộc database.
* Không phụ thuộc API bên ngoài.
* Kiểm soát được dữ liệu trả về.
* Test nhanh hơn.

---

# 3.15. Mockito

Mockito là framework phổ biến trong Java để hỗ trợ Mocking.

Một số khái niệm quan trọng:

* Mock.
* Stub.
* Verify.
* Argument Matching.

Ví dụ:

```java
when(repository.findById(1L))
    .thenReturn(user);
```

Sau đó có thể kiểm tra method đã được gọi:

```java
verify(repository).findById(1L);
```

Qua Mockito, em hiểu cách cô lập một thành phần khỏi các dependency bên ngoài khi thực hiện Unit Testing.

---

# 3.16. Integration Testing

Integration Testing kiểm tra sự tương tác giữa nhiều thành phần trong hệ thống.

Ví dụ:

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Database
```

Khác với Unit Testing, Integration Testing thường kiểm tra nhiều thành phần hoạt động cùng nhau.

Một số nội dung cần quan tâm:

* Database Integration.
* REST API Integration.
* Repository Integration.
* External Service Integration.

Mục tiêu:

* Kiểm tra sự tương tác giữa các module.
* Phát hiện lỗi cấu hình.
* Phát hiện lỗi kết nối.
* Đảm bảo các thành phần hoạt động đúng khi kết hợp.

---

# 3.17. Unit Testing và Integration Testing

| Unit Testing                                   | Integration Testing                  |
| ---------------------------------------------- | ------------------------------------ |
| Kiểm tra một đơn vị nhỏ                        | Kiểm tra nhiều thành phần            |
| Thường mock dependency                         | Có thể sử dụng dependency thật       |
| Chạy nhanh                                     | Thường chậm hơn                      |
| Dễ xác định vị trí lỗi                         | Phát hiện lỗi tương tác              |
| Không cần database thật trong nhiều trường hợp | Có thể cần database/test environment |

Trong một dự án Backend thực tế, cả Unit Testing và Integration Testing đều cần thiết và bổ sung cho nhau.

---

# 3.18. Test Coverage

Test Coverage là một chỉ số thể hiện mức độ code được thực thi bởi các test.

Một số loại Coverage:

* Line Coverage.
* Branch Coverage.
* Method Coverage.
* Class Coverage.

Ví dụ:

Nếu chương trình có 100 dòng code và test chạy qua 80 dòng:

```text
Line Coverage = 80%
```

Tuy nhiên, Coverage cao không đồng nghĩa với chất lượng test cao.

Một test suite có thể đạt Coverage cao nhưng vẫn bỏ sót các trường hợp nghiệp vụ quan trọng.

Do đó cần kết hợp Coverage với:

* Chất lượng Test Case.
* Boundary Cases.
* Error Cases.
* Business Requirements.

---

# 3.19. Quality Metrics

Một số chỉ số có thể được sử dụng để đánh giá chất lượng phần mềm:

* Test Coverage.
* Test Pass Rate.
* Test Failure Rate.
* Defect Density.
* Code Complexity.
* Maintainability.
* Reliability.

Mục tiêu của Quality Metrics không chỉ là đạt một con số Coverage cao mà là đảm bảo phần mềm có:

* Tính ổn định.
* Khả năng bảo trì.
* Khả năng mở rộng.
* Khả năng phát hiện lỗi.
* Chất lượng code tốt.

---

# 4. Kết quả đạt được

Sau tuần thứ hai, em đã đạt được các kết quả:

### Collections

* Hiểu cấu trúc bên trong của `ArrayList`.
* Hiểu cách `HashMap` sử dụng hashing và bucket.
* Hiểu cơ chế xử lý Collision.
* Hiểu mối quan hệ giữa `HashSet` và `HashMap`.
* Hiểu `hashCode()` và `equals()`.
* Nắm được HashCode và Equals Contract.
* Hiểu các vấn đề cơ bản khi sử dụng Collection trong môi trường Multithreading.
* Biết mục đích sử dụng `ConcurrentHashMap`.
* Hiểu mô hình Producer-Consumer với `BlockingQueue`.

### Design Patterns

* Hiểu khái niệm Design Pattern.
* Hiểu Singleton Pattern.
* Hiểu Factory Pattern.
* Hiểu Observer Pattern.
* Hiểu Strategy Pattern.
* Biết trường hợp sử dụng và ưu nhược điểm cơ bản của từng Pattern.
* Hiểu cách Design Pattern hỗ trợ giảm coupling và tăng khả năng mở rộng.

### Testing

* Hiểu nguyên tắc Unit Testing.
* Biết cấu trúc Arrange - Act - Assert.
* Làm quen với JUnit 5.
* Biết các Assertion phổ biến.
* Hiểu Mocking và mục đích của Mock.
* Làm quen với Mockito.
* Phân biệt Unit Testing và Integration Testing.
* Hiểu các chiến lược Integration Testing cơ bản.
* Hiểu Test Coverage.
* Biết một số Quality Metrics.

Qua tuần thứ hai, em đã có nền tảng tốt hơn về cách xây dựng code có cấu trúc, có khả năng mở rộng và có thể kiểm thử.

---

# 5. Khó khăn và hướng khắc phục

Trong quá trình học tập, em gặp một số khó khăn:

* Việc hiểu cơ chế bên trong của HashMap và HashSet phức tạp hơn việc sử dụng Collection thông thường.
* HashCode, Equals và Collision cần hiểu cả về logic và cách Java triển khai.
* Các Concurrent Collection có nhiều cơ chế xử lý đồng thời khác nhau.
* Việc lựa chọn Design Pattern phù hợp phụ thuộc nhiều vào bài toán thực tế.
* Ban đầu còn nhầm lẫn giữa Unit Testing và Integration Testing.
* Mocking và Mockito yêu cầu hiểu rõ dependency giữa các class.
* Test Coverage cao không đồng nghĩa với chất lượng test cao nên cần hiểu thêm về cách xây dựng Test Case.

Để khắc phục, em tiếp tục đọc tài liệu, phân tích source code, xây dựng các ví dụ nhỏ và so sánh từng trường hợp sử dụng.

---

# 6. Kế hoạch Tuần 3

Trong tuần thứ ba, nội dung học tập sẽ tập trung vào **Concurrency và Docker**.

## 6.1. Concurrency

Các nội dung dự kiến:

* Thread Lifecycle.
* Thread Management.
* ThreadPool.
* ExecutorService.
* `synchronized`.
* Lock.
* Atomic Classes.
* CompletableFuture.
* Reactive Programming Basics.

Mục tiêu:

* Hiểu cách Java quản lý Thread.
* Biết cách sử dụng ThreadPool.
* Hiểu ExecutorService.
* Hiểu các cơ chế Synchronization.
* Biết xử lý Race Condition.
* Hiểu Atomic Classes.
* Làm quen với Asynchronous Programming.
* Tìm hiểu CompletableFuture và Reactive Programming.

---

## 6.2. Docker

Các nội dung dự kiến:

* Container Concepts.
* Docker Architecture.
* Dockerfile.
* Docker Image.
* Image Layers.
* Image Optimization.
* Container Networking.
* Docker Volumes.
* Docker Compose.
* Multi-container Applications.

Mục tiêu là hiểu Docker từ kiến trúc cơ bản đến cách xây dựng và vận hành một ứng dụng gồm nhiều container.

---

# 7. Kết luận

Tuần thứ hai giúp em đi sâu hơn vào các kiến thức Java và quy trình đảm bảo chất lượng phần mềm.

Về **Collections**, em đã tìm hiểu cách `ArrayList`, `HashMap`, `HashSet` hoạt động bên trong, đồng thời hiểu rõ hơn về Hashing, Collision, `hashCode()` và `equals()`.

Về **Design Patterns**, em đã tìm hiểu Singleton, Factory, Observer và Strategy, qua đó hiểu cách các Pattern giúp giải quyết những vấn đề thiết kế phổ biến và cải thiện khả năng mở rộng của hệ thống.

Về **Testing**, em đã nắm được các khái niệm về Unit Testing, JUnit 5, Mocking, Mockito, Integration Testing và Test Coverage.

Những kiến thức này là nền tảng quan trọng để tiếp tục học **Concurrency, Docker và các kỹ thuật phát triển Backend nâng cao** trong tuần tiếp theo.
