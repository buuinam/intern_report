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
**5. Thực hành

Trong tuần này, em vừa đọc lý thuyết vừa thực hành một số nội dung để trực tiếp quan sát cách kiến thức hoạt động trong thực tế, thay vì chỉ học qua tài liệu.

Java OOP: Em xây dựng một chương trình quản lý nhân viên đơn giản để áp dụng 4 tính chất OOP. Em tạo class Employee, sử dụng private cho các thuộc tính để thực hành Encapsulation, sau đó tạo các class Developer và Tester kế thừa từ Employee để quan sát Inheritance. Em override phương thức work() ở các class con và gọi thông qua kiểu dữ liệu của class cha để hiểu rõ hơn về Polymorphism. Ngoài ra, em cũng thử sử dụng Abstract Class và Abstract Method để thấy cách Abstraction được áp dụng trong chương trình.

SOLID: Em thử xây dựng một chương trình có chức năng quản lý nhân viên, trong đó ban đầu một class đảm nhiệm nhiều công việc như quản lý thông tin, tính lương và lưu dữ liệu. Sau đó em tách các chức năng này thành những class riêng để áp dụng Single Responsibility Principle. Em cũng thử sử dụng Interface và Dependency Injection đơn giản để giảm sự phụ thuộc trực tiếp giữa các thành phần. Qua thực hành, em hiểu rõ hơn lý do SOLID giúp code dễ thay đổi và bảo trì hơn.

Interface, Abstract Class và Static: Em tạo một ví dụ về các phương thức thanh toán, trong đó Payment là Interface và có các implementation như thanh toán bằng tiền mặt và chuyển khoản. Em gọi các implementation thông qua kiểu Interface để quan sát Polymorphism. Đồng thời em thử tạo static variable, static method và static block để hiểu cách các thành phần static thuộc về class thay vì từng object.

Java Collections: Em tạo danh sách nhân viên và thử quản lý dữ liệu bằng ArrayList, HashSet và HashMap. Em thực hiện các thao tác thêm, xóa, tìm kiếm và kiểm tra dữ liệu để quan sát sự khác nhau giữa các cấu trúc dữ liệu. Em cũng thử dùng HashMap để tìm nhân viên theo ID và HashSet để loại bỏ dữ liệu trùng lặp. Ngoài ra, em tìm hiểu và chạy thử ConcurrentHashMap trong trường hợp nhiều thread cùng truy cập dữ liệu để thấy sự khác biệt giữa Collection thông thường và Thread-safe Collection.

Exception Handling: Em tạo một số tình huống có thể phát sinh lỗi như chia cho 0, nhập sai kiểu dữ liệu hoặc truyền dữ liệu không hợp lệ. Em sử dụng try-catch-finally để bắt và xử lý lỗi thay vì để chương trình dừng đột ngột. Em cũng thử tạo một Custom Exception cho trường hợp dữ liệu không hợp lệ để hiểu cách xây dựng exception phục vụ cho nghiệp vụ riêng của ứng dụng.

Linux File System & Permissions: Em thực hành tạo thư mục, file và di chuyển giữa các thư mục để làm quen với Linux File System. Sau đó em sử dụng ls -l để quan sát quyền truy cập của file và thử thay đổi quyền bằng chmod. Em thay đổi các quyền read, write, execute cho User, Group và Other để trực tiếp thấy sự thay đổi trong quyền truy cập. Em cũng tìm hiểu cách chown và umask ảnh hưởng đến quyền sở hữu và quyền mặc định của file.

Process Management: Em chạy một số chương trình trên Linux rồi sử dụng ps, top và htop để quan sát process đang hoạt động. Em thử chạy một chương trình ở background bằng &, kiểm tra bằng jobs và lấy PID của process. Sau đó em sử dụng kill để kết thúc process và quan sát trạng thái của nó trước và sau khi bị dừng. Em cũng thử nohup để chạy một chương trình trong background và thấy process vẫn tiếp tục hoạt động ngay cả khi terminal kết thúc.

Text Processing: Em tạo một file log mẫu chứa các dòng INFO, WARNING và ERROR, sau đó dùng grep để tìm các dòng lỗi. Em kết hợp grep, sort, uniq và pipe | để lọc và xử lý dữ liệu từ file. Em cũng thử cut và awk trên dữ liệu dạng cột để hiểu cách Linux có thể xử lý log và dữ liệu văn bản trực tiếp từ command line.

Network Utilities: Em sử dụng ss để quan sát các port và socket đang hoạt động trên máy. Em dùng curl để gửi HTTP request đến một website và thử sử dụng option -I để chỉ lấy HTTP headers. Em cũng thử wget để tải một file từ Internet. Qua đó em hiểu rõ hơn cách kiểm tra kết nối và tương tác với HTTP service từ command line.

System Monitoring: Em thực hành sử dụng df -h để kiểm tra dung lượng ổ đĩa và du để xem dung lượng của từng thư mục. Em dùng free để quan sát RAM và top để theo dõi CPU, RAM cũng như các process đang chạy. Qua đó em hiểu được các command cơ bản có thể sử dụng khi cần kiểm tra tình trạng tài nguyên của một server Linux.

Shell Script: Em viết một shell script đơn giản để lấy thông tin hệ thống như username, thư mục hiện tại, dung lượng ổ đĩa và bộ nhớ RAM. Em thực hành khai báo biến, sử dụng câu điều kiện và vòng lặp, đồng thời truyền tham số từ command line vào script. Em cũng thử sử dụng các environment variable như PATH và tìm hiểu vai trò của JAVA_HOME trong môi trường Java.

Process Lifecycle: Em tìm hiểu và quan sát mối quan hệ giữa process cha và process con thông qua các khái niệm fork(), exec() và wait(). Em đặc biệt chú ý đến Zombie Process để hiểu trường hợp process con đã kết thúc nhưng process cha chưa thu hồi trạng thái của nó. Qua phần thực hành và quan sát process bằng các command Linux, em hiểu rõ hơn vòng đời của một process thay vì chỉ ghi nhớ các khái niệm.

I/O Redirection: Em thực hành redirect output của command vào file bằng >, nối thêm dữ liệu bằng >> và redirect lỗi bằng 2>. Em sử dụng pipe | để đưa output của command này làm input cho command khác, ví dụ kết hợp ps và grep để tìm các process Java đang chạy. Qua đó em hiểu rõ hơn vai trò của stdin, stdout, stderr và cách các command Linux có thể kết hợp thành một pipeline.

System Logs: Em tìm hiểu thư mục /var/log và quan sát các file log hệ thống. Trên hệ thống sử dụng systemd, em thử dùng journalctl để xem log và journalctl -f để theo dõi log theo thời gian thực. Qua thực hành, em hiểu được log là nguồn thông tin quan trọng để kiểm tra hoạt động và xác định lỗi của hệ thống.

Thông qua các bài thực hành trên, em đã có cơ hội kiểm chứng lại các kiến thức lý thuyết bằng những tình huống cụ thể. Đặc biệt, việc kết hợp Java với các công cụ Linux giúp em bước đầu hình dung được môi trường làm việc thực tế của một Backend Developer, nơi không chỉ cần viết code mà còn phải biết chạy, theo dõi process, kiểm tra log và xử lý các vấn đề cơ bản trên hệ thống.

# 6. Kế hoạch Tuần 2

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
