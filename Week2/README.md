# 📘 BÁO CÁO THỰC TẬP TUẦN 2

## Thông tin

- **Chủ đề:** Collections, Design Patterns & Testing
- **Intern:** Bùi Văn Nam
- **Team:** Platform - Adtech
- **Gmail:** buivannam13032004@gmail.com
- **Leader:** Nguyễn Văn Cương

---

# 1. Mục tiêu tuần

Trong tuần thứ hai, mục tiêu là tìm hiểu chuyên sâu về **Java Collections Framework**, các **Design Pattern** phổ biến và kiến thức cơ bản về **Testing**.

Nội dung tập trung vào việc hiểu cơ chế hoạt động của các cấu trúc dữ liệu trong Java, áp dụng các mẫu thiết kế để xây dựng phần mềm dễ mở rộng, dễ bảo trì và làm quen với các phương pháp kiểm thử nhằm nâng cao chất lượng mã nguồn.

---

# 2. Lịch học Tuần 2

| Ngày | Nội dung học | Kết quả đạt được |
|------|--------------|------------------|
| **Thứ 2** | HashMap, HashSet, ArrayList Internals | Hiểu cơ chế hoạt động, cách lưu trữ dữ liệu và hiệu năng của từng cấu trúc. |
| **Thứ 3** | HashCode, Equals & Concurrent Collections | Hiểu mối quan hệ giữa `hashCode()` và `equals()`; tìm hiểu Concurrent Collections. |
| **Thứ 4** | Design Patterns | Nắm được Singleton, Factory, Observer và Strategy Pattern. |
| **Thứ 5** | Unit Testing & Mocking | Tìm hiểu Unit Testing, JUnit 5 và Mocking. |
| **Thứ 6** | Integration Testing & Test Coverage | Hiểu Integration Testing, Test Coverage và ôn tập kiến thức tuần. |

---

# 3. Chi tiết nội dung đã học

## 3.1 Java Collections

### a. HashMap, HashSet và ArrayList Internals

Đã tìm hiểu cơ chế hoạt động của:

- HashMap
- HashSet
- ArrayList

**Kiến thức đạt được**

- Hiểu cách lưu trữ dữ liệu trong bộ nhớ.
- Hiểu cơ chế Resize của ArrayList và HashMap.
- Hiểu Collision và cách HashMap xử lý va chạm.
- Biết ưu, nhược điểm và hiệu năng của từng cấu trúc dữ liệu.

**Lý thuyết**

| Collection | Đặc điểm |
|------------|----------|
| ArrayList | Mảng động, truy cập nhanh, thêm/xóa giữa danh sách chậm. |
| HashMap | Lưu theo cặp Key-Value, tìm kiếm trung bình O(1). |
| HashSet | Dựa trên HashMap, không cho phép phần tử trùng lặp. |

---

### b. HashCode và Equals Contract

Đã nghiên cứu nguyên tắc hoạt động của:

- `hashCode()`
- `equals()`

**Kiến thức đạt được**

- Hiểu mối quan hệ giữa `hashCode()` và `equals()`.
- Biết cách Override đúng quy tắc.
- Hiểu vai trò của hai phương thức khi sử dụng HashMap và HashSet.

**Lý thuyết**

- `equals()` dùng để so sánh nội dung của hai đối tượng.
- `hashCode()` trả về giá trị băm của đối tượng.
- Hai đối tượng bằng nhau theo `equals()` phải có cùng `hashCode()`.

---

### c. Concurrent Collections

Đã tìm hiểu:

- ConcurrentHashMap
- BlockingQueue

**Kiến thức đạt được**

- Hiểu Collection thread-safe.
- Phân biệt Collection thông thường và Concurrent Collection.

**Lý thuyết**

Concurrent Collections cho phép nhiều luồng truy cập đồng thời nhưng vẫn đảm bảo tính nhất quán dữ liệu và có hiệu năng tốt hơn Hashtable hoặc Vector.

---

# 3.2 Design Patterns

### a. Singleton Pattern

**Kiến thức đạt được**

- Hiểu cách đảm bảo chỉ tồn tại một đối tượng duy nhất.

**Lý thuyết**

Thường sử dụng cho Logger, Configuration hoặc Database Connection Manager.

---

### b. Factory Pattern

**Kiến thức đạt được**

- Hiểu cách tạo đối tượng thông qua Factory.

**Lý thuyết**

Giúp giảm sự phụ thuộc giữa các lớp và dễ mở rộng hệ thống.

---

### c. Observer Pattern

**Kiến thức đạt được**

- Hiểu cơ chế Subject và Observer.

**Lý thuyết**

Khi Subject thay đổi trạng thái, các Observer sẽ tự động được thông báo và cập nhật.

---

### d. Strategy Pattern

**Kiến thức đạt được**

- Hiểu cách thay đổi thuật toán linh hoạt.

**Lý thuyết**

Đóng gói các thuật toán thành các lớp riêng biệt và lựa chọn thuật toán phù hợp trong quá trình chạy chương trình.

---

# 3.3 Testing

### a. Unit Testing

**Kiến thức đạt được**

- Hiểu nguyên tắc Unit Testing.
- Làm quen với JUnit 5.

**Lý thuyết**

Unit Testing kiểm thử từng đơn vị nhỏ nhất của chương trình nhằm phát hiện lỗi sớm.

---

### b. Mocking

**Kiến thức đạt được**

- Hiểu vai trò của Mock Object.

**Lý thuyết**

Mocking tạo đối tượng giả lập để thay thế Database, API hoặc các thành phần phụ thuộc khi kiểm thử.

---

### c. Integration Testing

**Kiến thức đạt được**

- Hiểu các chiến lược kiểm thử tích hợp.

**Lý thuyết**

Integration Testing kiểm tra sự tương tác giữa nhiều module sau khi Unit Test hoàn thành.

---

### d. Test Coverage và Quality Metrics

**Kiến thức đạt được**

- Hiểu các chỉ số đánh giá chất lượng kiểm thử.

**Lý thuyết**

| Chỉ số | Ý nghĩa |
|--------|---------|
| Test Coverage | Tỷ lệ mã nguồn được kiểm thử. |
| Code Coverage | Mức độ bao phủ câu lệnh, nhánh và điều kiện. |
| Quality Metrics | Chỉ số đánh giá chất lượng và khả năng bảo trì mã nguồn. |

---

# 4. Kết quả đạt được

Sau khi hoàn thành tuần học thứ hai, em đã:

- ✅ Hiểu cơ chế hoạt động của HashMap, HashSet và ArrayList.
- ✅ Nắm được nguyên tắc sử dụng `hashCode()` và `equals()`.
- ✅ Hiểu Concurrent Collections và lập trình đa luồng cơ bản.
- ✅ Nắm được mục đích và cách áp dụng Singleton, Factory, Observer và Strategy Pattern.
- ✅ Biết cách viết Unit Test cơ bản bằng JUnit 5.
- ✅ Hiểu vai trò của Mocking trong kiểm thử.
- ✅ Nắm được Integration Testing và Test Coverage.
- ✅ Xây dựng nền tảng về thiết kế phần mềm và kiểm thử để chuẩn bị học Spring Boot và các dự án Backend thực tế.

---

# 5. Kế hoạch Tuần 3

## Concurrency

- Thread Lifecycle và Management
- ThreadPool và ExecutorService
- Synchronization (`synchronized`, `Lock`, `Atomic`)
- CompletableFuture
- Reactive Programming Basics

## Docker

- Container Concepts và Docker Architecture
- Dockerfile Best Practices
- Image Layering và Optimization
- Container Networking và Volumes
- Docker Compose cho Multi-container Applications

### Lý thuyết Docker

- Container vs Virtual Machine (VM)
- Image Layers và Layer Caching
- Container Lifecycle
- Docker Networking
- Docker Storage (Bind Mounts, Volumes, tmpfs)
