# 📘 BÁO CÁO THỰC TẬP TUẦN 1

## Thông tin

- **Chủ đề:** Java Core và Linux Fundamentals
- **Intern:** Bùi Văn Nam
- **Team:** Platform - Adtech
- **Gmail:** buivannam13032004@gmail.com
- **Leader:** Nguyễn Văn Cương

---

# 1. Mục tiêu tuần

Trong tuần đầu tiên, theo roadmap mục tiêu là củng cố nền tảng về ngôn ngữ **Java** và hệ điều hành **Linux** nhằm chuẩn bị cho việc phát triển Backend Java trong các giai đoạn tiếp theo.

Nội dung tập trung vào lập trình hướng đối tượng, các nguyên lý thiết kế phần mềm, xử lý ngoại lệ cùng các thao tác quản trị hệ thống và sử dụng dòng lệnh trên Linux.

---

# 2. Lịch học Tuần 1

| Ngày | Nội dung học | Kết quả đạt được |
|------|--------------|------------------|
| **Thứ 2** | Java OOP | Nắm vững 4 tính chất OOP; thực hành xây dựng Class và Object. |
| **Thứ 3** | SOLID, Interface, Abstract Class, Static | Hiểu 5 nguyên lý SOLID; phân biệt Interface và Abstract Class; sử dụng từ khóa `static`. |
| **Thứ 4** | Collections & Exception Handling | Hiểu Java Collections Framework, so sánh hiệu năng các Collection và Exception Handling. |
| **Thứ 5** | Linux Fundamentals | Thực hành File System, File Permission, Process Management, Text Processing, Network Utilities. |
| **Thứ 6** | Shell Script & Linux Theory | Học Shell Script, Environment Variables, Process Lifecycle, I/O Redirection và System Logs. |

---

# 3. Chi tiết nội dung đã học

## 3.1 Java Core

### a. Lập trình hướng đối tượng (OOP)

Đã tìm hiểu và nắm vững bốn tính chất cơ bản:

- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

Thông qua các ví dụ và bài thực hành, hiểu được vai trò của OOP trong việc tổ chức mã nguồn, tăng khả năng tái sử dụng và mở rộng chương trình.

---

### b. Nguyên lý SOLID

Đã nghiên cứu năm nguyên lý:

- Single Responsibility Principle
- Open/Closed Principle
- Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion Principle

Qua đó hiểu cách áp dụng SOLID để xây dựng phần mềm dễ bảo trì và mở rộng.

---

### c. Interface, Abstract Class và Static

Đã tìm hiểu sự khác nhau giữa **Interface** và **Abstract Class**, hiểu được trường hợp sử dụng của từng loại.

Đồng thời nghiên cứu:

- Static Variable
- Static Method
- Static Block

Qua đó hiểu được cách các thành phần `static` được quản lý ở cấp lớp.

---

### d. Java Collections Framework

Đã tìm hiểu:

**Các cấu trúc dữ liệu**

- List
- Set
- Map
- Queue

**Hiệu năng**

- Thêm dữ liệu
- Xóa dữ liệu
- Tìm kiếm
- Truy cập phần tử

**Thread-safe Collections**

- ConcurrentHashMap
- CopyOnWriteArrayList
- Vector
- Hashtable

Qua đó hiểu được sự khác biệt giữa Collection thông thường và Collection thread-safe.

---

### e. Exception Handling

Đã nghiên cứu:

- Checked Exception
- Unchecked Exception
- try-catch-finally
- throw
- throws
- Custom Exception

Đồng thời tìm hiểu các nguyên tắc xử lý ngoại lệ theo best practices.

---

## 3.2 Linux Fundamentals

### a. Linux File System

Đã tìm hiểu cấu trúc thư mục Linux:

| Thư mục | Chức năng |
|---------|-----------|
| `/` | Thư mục gốc |
| `/home` | Thư mục người dùng |
| `/etc` | Tệp cấu hình hệ thống |
| `/usr` | Chương trình và thư viện |
| `/var` | Log và dữ liệu hệ thống |
| `/tmp` | Tệp tạm |
| `/bin` | Các lệnh cơ bản |

---

### b. File Permissions

**Đối tượng phân quyền**

- **User:** Chủ sở hữu
- **Group:** Nhóm người dùng
- **Other:** Người dùng khác

**Quyền truy cập**

- **Read (r):** Đọc
- **Write (w):** Ghi
- **Execute (x):** Thực thi

**Các lệnh**

- `chmod` – Thay đổi quyền
- `chown` – Thay đổi chủ sở hữu
- `umask` – Thiết lập quyền mặc định

---

### c. Process Management

Đã thực hành:

| Lệnh | Chức năng |
|------|-----------|
| `ps` | Hiển thị tiến trình |
| `top` | Theo dõi tiến trình theo thời gian thực |
| `htop` | Giao diện trực quan của top |
| `kill` | Kết thúc tiến trình |
| `nohup` | Chạy tiến trình nền |
| `jobs` | Hiển thị tiến trình nền |

---

### d. Text Processing

| Lệnh | Chức năng |
|------|-----------|
| `grep` | Tìm kiếm nội dung |
| `sed` | Chỉnh sửa văn bản |
| `awk` | Xử lý dữ liệu theo cột |
| `cut` | Cắt dữ liệu |
| `sort` | Sắp xếp |
| `uniq` | Loại bỏ dòng trùng |

---

### e. Network Utilities

| Lệnh | Chức năng |
|------|-----------|
| `netstat` | Kiểm tra kết nối mạng |
| `ss` | Hiển thị socket |
| `curl` | Gửi HTTP Request |
| `wget` | Tải dữ liệu |

---

### f. System Monitoring

| Lệnh | Chức năng |
|------|-----------|
| `df` | Kiểm tra dung lượng ổ đĩa |
| `du` | Kiểm tra dung lượng thư mục |
| `free` | Kiểm tra RAM |
| `top` | Theo dõi CPU, RAM |
| `iostat` | Theo dõi I/O |

---

### g. Shell Scripting

Đã tìm hiểu:

- Khai báo biến
- Điều kiện
- Vòng lặp
- Hàm
- Tham số dòng lệnh
- Environment Variables (`PATH`, `JAVA_HOME`)

---

## 3.3 Kiến thức lý thuyết Linux

### Process Lifecycle

- `fork()`
- `exec()`
- `wait()`
- Zombie Process

---

### File Permissions

Hiểu mô hình phân quyền:

- User
- Group
- Other

---

### I/O Redirection

| Thành phần | Ý nghĩa |
|------------|----------|
| `stdin` | Đầu vào |
| `stdout` | Đầu ra |
| `stderr` | Luồng lỗi |
| `|` | Pipe |

---

### System Logs

| Thành phần | Chức năng |
|------------|-----------|
| `/var/log` | Lưu log hệ thống |
| `syslog` | Nhật ký hệ điều hành |
| `journalctl` | Xem log của systemd |

---

# 4. Kết quả đạt được

Sau tuần đầu tiên, em đã:

- ✅ Nắm vững OOP và SOLID.
- ✅ Phân biệt Interface và Abstract Class.
- ✅ Hiểu Java Collections Framework.
- ✅ Nắm được Exception Handling.
- ✅ Thành thạo các lệnh Linux cơ bản.
- ✅ Hiểu File System, Process Management và File Permissions.
- ✅ Nắm được Process Lifecycle, I/O Redirection và System Logs.
- ✅ Xây dựng nền tảng để học Spring Boot, Docker và MySQL.

---

# 5. Kế hoạch Tuần 2

## Collections

- HashMap, HashSet, ArrayList Internals
- HashCode và Equals Contract
- Concurrent Collections
- Design Patterns

## Testing

- Unit Testing
- JUnit 5
- Mocking
- Integration Testing
- Test Coverage
