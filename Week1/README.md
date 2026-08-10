# 📘 BÁO CÁO THỰC TẬP TUẦN 1

## Thông tin

* **Chủ đề:** Java Core và Linux Fundamentals
* **Intern:** Bùi Văn Nam
* **Team:** Platform - Adtech
* **Gmail:** [buivannam13032004@gmail.com](mailto:buivannam13032004@gmail.com)
* **Leader:** Nguyễn Văn Cương

---

# 1. Mục tiêu tuần

Trong tuần đầu tiên, theo roadmap, mục tiêu chính là củng cố kiến thức nền tảng về **Java Core** và **Linux Fundamentals**, chuẩn bị cho quá trình phát triển Backend Java trong các giai đoạn tiếp theo.

Nội dung tập trung vào:

* Lập trình hướng đối tượng OOP.
* Các nguyên lý thiết kế phần mềm SOLID.
* Interface, Abstract Class và Static.
* Java Collections Framework.
* Exception Handling.
* Linux File System và File Permissions.
* Process Management.
* Text Processing.
* Network Utilities.
* System Monitoring.
* Shell Scripting.
* Process Lifecycle.
* I/O Redirection.
* System Logs.

---

# 2. Lịch học Tuần 1

| Ngày      | Nội dung học                             | Kết quả đạt được                                                                                        |
| --------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Thứ 2** | Java OOP                                 | Nắm vững 4 tính chất OOP; hiểu Class, Object, Constructor và Method.                                    |
| **Thứ 3** | SOLID, Interface, Abstract Class, Static | Hiểu 5 nguyên lý SOLID; phân biệt Interface và Abstract Class; hiểu cách sử dụng `static`.              |
| **Thứ 4** | Collections & Exception Handling         | Hiểu Java Collections Framework, đặc điểm và hiệu năng của các Collection; nắm được Exception Handling. |
| **Thứ 5** | Linux Fundamentals                       | Tìm hiểu File System, File Permission, Process Management, Text Processing và Network Utilities.        |
| **Thứ 6** | Shell Script & Linux Theory              | Tìm hiểu Shell Script, Environment Variables, Process Lifecycle, I/O Redirection và System Logs.        |

---

# 3. Chi tiết nội dung đã học

## 3.1. Java Core

### a. Lập trình hướng đối tượng (OOP)

Đã tìm hiểu và nắm vững bốn tính chất cơ bản của lập trình hướng đối tượng:

* **Encapsulation** - Đóng gói
* **Inheritance** - Kế thừa
* **Polymorphism** - Đa hình
* **Abstraction** - Trừu tượng

### Encapsulation

Đóng gói là cơ chế che giấu dữ liệu bên trong đối tượng và kiểm soát cách dữ liệu được truy cập hoặc thay đổi.

Trong Java, Encapsulation thường được thực hiện thông qua:

* Access Modifier như `private`.
* Getter và Setter.
* Các method kiểm soát việc thay đổi dữ liệu.

Lợi ích:

* Bảo vệ dữ liệu.
* Kiểm soát quyền truy cập.
* Giảm sự phụ thuộc giữa các thành phần.
* Dễ bảo trì và mở rộng.

### Inheritance

Inheritance cho phép class con kế thừa thuộc tính và phương thức của class cha.

Từ khóa thường sử dụng:

```java
extends
```

Lợi ích:

* Tái sử dụng code.
* Giảm code trùng lặp.
* Xây dựng mối quan hệ giữa các class.

### Polymorphism

Polymorphism cho phép cùng một method hoặc interface nhưng có thể có nhiều cách triển khai khác nhau.

Hai hình thức phổ biến:

* Method Overloading.
* Method Overriding.

Trong Java, Runtime Polymorphism thường được thực hiện thông qua Method Overriding.

### Abstraction

Abstraction là việc che giấu chi tiết triển khai và chỉ cung cấp những hành vi cần thiết.

Java hỗ trợ abstraction thông qua:

* Abstract Class.
* Interface.

Qua việc tìm hiểu OOP, em hiểu được cách tổ chức chương trình theo hướng đối tượng, tăng khả năng tái sử dụng và mở rộng mã nguồn.

---

## 3.2. Nguyên lý SOLID

Đã nghiên cứu năm nguyên lý SOLID:

### S - Single Responsibility Principle

Một class chỉ nên có một trách nhiệm chính và một lý do chính để thay đổi.

Việc chia nhỏ trách nhiệm giúp:

* Code dễ đọc.
* Dễ kiểm thử.
* Dễ bảo trì.
* Hạn chế ảnh hưởng khi thay đổi một chức năng.

### O - Open/Closed Principle

Software entities nên:

* Mở cho việc mở rộng.
* Đóng cho việc sửa đổi.

Khi cần thêm chức năng mới, nên ưu tiên mở rộng hệ thống thay vì sửa đổi trực tiếp những logic đã ổn định.

### L - Liskov Substitution Principle

Object của class con phải có thể thay thế object của class cha mà không làm thay đổi tính đúng đắn của chương trình.

Nguyên tắc này giúp đảm bảo class con tuân thủ đúng contract của class cha.

### I - Interface Segregation Principle

Không nên ép một class phải implement những phương thức mà class đó không sử dụng.

Nên chia Interface lớn thành các Interface nhỏ hơn, tập trung vào từng nhóm chức năng.

### D - Dependency Inversion Principle

Các module cấp cao không nên phụ thuộc trực tiếp vào module cấp thấp.

Cả hai nên phụ thuộc vào abstraction.

Nguyên lý này giúp giảm coupling và là nền tảng quan trọng cho Dependency Injection trong các Framework như Spring.

---

## 3.3. Interface, Abstract Class và Static

### Interface

Interface được sử dụng để định nghĩa contract mà các class triển khai phải tuân theo.

Đặc điểm:

* Một class có thể implement nhiều Interface.
* Phù hợp để định nghĩa hành vi chung.
* Giúp giảm sự phụ thuộc giữa các thành phần.
* Có thể chứa abstract method, default method và static method.

### Abstract Class

Abstract Class được sử dụng làm class cơ sở cho các class con.

Có thể chứa:

* Attributes.
* Constructor.
* Abstract methods.
* Concrete methods.

### So sánh Interface và Abstract Class

| Interface                                    | Abstract Class                                |
| -------------------------------------------- | --------------------------------------------- |
| Định nghĩa contract                          | Cung cấp base implementation                  |
| Một class có thể implement nhiều Interface   | Một class chỉ extends một class               |
| Phù hợp cho abstraction                      | Phù hợp khi các class có state/behavior chung |
| Không sử dụng constructor để khởi tạo object | Có constructor                                |
| Hỗ trợ default/static methods                | Có thể chứa method thông thường               |

### Static

`static` biểu thị thành phần thuộc về **class** thay vì từng object.

Đã tìm hiểu:

* Static Variable.
* Static Method.
* Static Block.
* Static Nested Class.

Static Variable được dùng chung giữa các object thuộc cùng một class.

---

# 3.4. Java Collections Framework

Đã tìm hiểu Java Collections Framework và các cấu trúc dữ liệu phổ biến:

* List.
* Set.
* Map.
* Queue.
* Deque.

## ArrayList

`ArrayList` được triển khai dựa trên dynamic array.

Đặc điểm:

* Truy cập phần tử theo index nhanh.
* Thêm phần tử vào cuối thường có hiệu năng tốt.
* Chèn hoặc xóa phần tử ở giữa có thể tốn chi phí do phải dịch chuyển phần tử.

Độ phức tạp phổ biến:

```text
get()      → O(1)
set()      → O(1)
add()      → O(1) amortized
remove()   → O(n)
search()   → O(n)
```

---

## LinkedList

`LinkedList` được triển khai dựa trên cấu trúc linked list.

Đặc điểm:

* Truy cập theo index chậm hơn ArrayList.
* Tìm kiếm có độ phức tạp O(n).
* Thao tác thêm/xóa tại vị trí đã có reference đến node có thể hiệu quả.

---

## HashSet

`HashSet` sử dụng cơ chế hashing để lưu trữ phần tử.

Đặc điểm:

* Không cho phép phần tử trùng nhau.
* Không đảm bảo thứ tự phần tử.
* Các thao tác thêm, xóa, tìm kiếm thường có độ phức tạp trung bình O(1).

---

## HashMap

`HashMap` lưu dữ liệu theo dạng:

```text
Key → Value
```

Ví dụ:

```text
User ID → User
Product ID → Product
```

Các thao tác `put()` và `get()` thường có hiệu năng trung bình O(1).

Đã tìm hiểu các khái niệm liên quan:

* Hashing.
* Hash Function.
* Bucket.
* Collision.
* Key.
* Value.

---

## TreeMap

`TreeMap` lưu trữ các key theo thứ tự.

Các thao tác cơ bản thường có độ phức tạp:

```text
put()    → O(log n)
get()    → O(log n)
remove() → O(log n)
```

Phù hợp khi cần dữ liệu được sắp xếp theo key.

---

## So sánh Collections

| Collection | Đặc điểm chính       |   Search |   Insert |
| ---------- | -------------------- | -------: | -------: |
| ArrayList  | Truy cập index nhanh |     O(n) |    O(1)* |
| LinkedList | Linked list          |     O(n) |   O(1)** |
| HashSet    | Không trùng dữ liệu  |    O(1)* |    O(1)* |
| HashMap    | Key-Value            |    O(1)* |    O(1)* |
| TreeMap    | Key được sắp xếp     | O(log n) | O(log n) |

> `*` Độ phức tạp trung bình/amortized trong điều kiện thông thường.
> `**` Hiệu quả khi đã có reference tới vị trí cần thao tác.

---

## Thread-safe Collections

Đã tìm hiểu các Collection có khả năng hỗ trợ môi trường đa luồng:

* `ConcurrentHashMap`
* `CopyOnWriteArrayList`
* `Vector`
* `Hashtable`

Trong đó:

### ConcurrentHashMap

Phù hợp khi nhiều thread cùng đọc và ghi dữ liệu.

### CopyOnWriteArrayList

Phù hợp với trường hợp đọc nhiều và ghi ít.

### Vector

Collection cũ có các method synchronized, tuy nhiên trong nhiều trường hợp hiện đại có thể ưu tiên các Collection concurrent phù hợp hơn.

### Hashtable

Collection cũ hỗ trợ synchronized, nhưng thường được thay thế bởi `ConcurrentHashMap` trong các ứng dụng hiện đại.

Qua nội dung này, em hiểu được vấn đề Thread Safety và tầm quan trọng của việc lựa chọn Collection phù hợp trong môi trường Multithreading.

---

# 3.5. Exception Handling

Đã nghiên cứu cơ chế xử lý Exception trong Java.

Các nội dung chính:

* Checked Exception.
* Unchecked Exception.
* `try`.
* `catch`.
* `finally`.
* `throw`.
* `throws`.
* Custom Exception.

## Checked Exception

Là các Exception được compiler kiểm tra tại compile time.

Ví dụ:

```text
IOException
SQLException
```

## Unchecked Exception

Thường kế thừa từ `RuntimeException` và xảy ra trong quá trình runtime.

Ví dụ:

```text
NullPointerException
ArithmeticException
IllegalArgumentException
IndexOutOfBoundsException
```

## Try-Catch-Finally

Được sử dụng để bắt và xử lý Exception.

```java
try {
    // code
} catch (Exception e) {
    // handle exception
} finally {
    // cleanup
}
```

## throw và throws

`throw` được sử dụng để chủ động ném một Exception.

`throws` được sử dụng để khai báo Exception mà method có thể phát sinh.

## Custom Exception

Custom Exception cho phép tạo các loại Exception riêng phục vụ cho nghiệp vụ của ứng dụng.

Qua đó hiểu được cách xử lý lỗi có kiểm soát và tránh làm chương trình dừng đột ngột khi xảy ra Exception.

---

# 3.6. Linux Fundamentals

## a. Linux File System

Đã tìm hiểu cấu trúc File System của Linux:

| Thư mục | Chức năng                |
| ------- | ------------------------ |
| `/`     | Thư mục gốc              |
| `/home` | Thư mục người dùng       |
| `/etc`  | File cấu hình hệ thống   |
| `/usr`  | Chương trình và thư viện |
| `/var`  | Log và dữ liệu hệ thống  |
| `/tmp`  | File tạm                 |
| `/bin`  | Các lệnh cơ bản          |

Một số command cơ bản:

```bash
pwd
ls
ls -la
cd
mkdir
touch
cp
mv
rm
```

---

# 3.7. File Permissions

Linux sử dụng mô hình phân quyền gồm:

* **User** - Chủ sở hữu.
* **Group** - Nhóm người dùng.
* **Other** - Người dùng khác.

Ba quyền cơ bản:

| Quyền   | Ký hiệu | Giá trị |
| ------- | ------- | ------: |
| Read    | `r`     |       4 |
| Write   | `w`     |       2 |
| Execute | `x`     |       1 |

Ví dụ:

```text
-rwxr-xr--
```

Có thể phân tích:

```text
User  → rwx
Group → r-x
Other → r--
```

Các command quan trọng:

```bash
chmod
chown
umask
```

### chmod

Dùng để thay đổi quyền:

```bash
chmod 755 script.sh
```

### chown

Dùng để thay đổi owner/group:

```bash
chown user:user file.txt
```

### umask

Dùng để xác định các quyền mặc định bị loại bỏ khi tạo file hoặc directory mới.

---

# 3.8. Process Management

Process là một chương trình đang được thực thi.

Các command đã tìm hiểu:

| Command  | Chức năng                               |
| -------- | --------------------------------------- |
| `ps`     | Hiển thị process                        |
| `ps aux` | Hiển thị chi tiết các process           |
| `top`    | Theo dõi process và tài nguyên realtime |
| `htop`   | Giao diện trực quan để quản lý process  |
| `kill`   | Gửi signal đến process                  |
| `nohup`  | Chạy process không phụ thuộc terminal   |
| `jobs`   | Quản lý background jobs                 |
| `fg`     | Đưa job về foreground                   |
| `bg`     | Chạy job ở background                   |

Mỗi process được xác định bởi một **PID (Process ID)**.

Qua nội dung này, em hiểu được cách kiểm tra, theo dõi và quản lý process trong Linux.

---

# 3.9. Text Processing

Linux cung cấp nhiều command mạnh để xử lý dữ liệu dạng text.

| Command | Chức năng               |
| ------- | ----------------------- |
| `grep`  | Tìm kiếm nội dung       |
| `sed`   | Chỉnh sửa và xử lý text |
| `awk`   | Xử lý dữ liệu theo cột  |
| `cut`   | Trích xuất dữ liệu      |
| `sort`  | Sắp xếp dữ liệu         |
| `uniq`  | Loại bỏ dữ liệu trùng   |
| `wc`    | Đếm dòng, từ và ký tự   |

Ví dụ:

```bash
grep "ERROR" application.log
```

Tìm kiếm các dòng chứa `ERROR`.

Kết hợp nhiều command:

```bash
cat application.log | grep ERROR | sort | uniq
```

Qua đó hiểu được cách sử dụng Pipe để kết hợp nhiều command thành một chuỗi xử lý dữ liệu.

---

# 3.10. Network Utilities

Đã tìm hiểu các command network cơ bản:

| Command   | Chức năng                    |
| --------- | ---------------------------- |
| `netstat` | Kiểm tra network connections |
| `ss`      | Kiểm tra socket và port      |
| `curl`    | Gửi HTTP request             |
| `wget`    | Download dữ liệu             |

Ví dụ:

```bash
ss -tuln
```

Dùng để xem các port đang listen.

```bash
curl http://localhost:8080
```

Dùng để gửi HTTP request tới server.

Các công cụ này rất hữu ích khi kiểm tra Backend Service, API và network connectivity.

---

# 3.11. System Monitoring

Đã tìm hiểu các công cụ theo dõi tài nguyên hệ thống:

| Command  | Chức năng                          |
| -------- | ---------------------------------- |
| `df`     | Kiểm tra dung lượng filesystem     |
| `du`     | Kiểm tra dung lượng file/directory |
| `free`   | Kiểm tra RAM                       |
| `top`    | Theo dõi CPU và process            |
| `iostat` | Theo dõi CPU và I/O                |

Ví dụ:

```bash
df -h
```

Kiểm tra dung lượng ổ đĩa.

```bash
free -h
```

Kiểm tra RAM.

```bash
top
```

Theo dõi CPU, RAM và process theo thời gian thực.

Qua nội dung này, em hiểu được các chỉ số cơ bản cần theo dõi khi vận hành một hệ thống Backend.

---

# 3.12. Shell Scripting

Đã tìm hiểu những kiến thức cơ bản về Shell Script:

* Khai báo biến.
* Kiểu dữ liệu cơ bản.
* Điều kiện `if/else`.
* Vòng lặp `for`, `while`.
* Function.
* Tham số dòng lệnh.
* Environment Variables.
* Exit Code.

Ví dụ:

```bash
#!/bin/bash

name="Nam"

echo "Hello $name"
```

Tìm hiểu các Environment Variables quan trọng:

```bash
echo $PATH
echo $JAVA_HOME
```

Trong đó:

* `PATH`: Danh sách các thư mục được hệ thống sử dụng để tìm executable.
* `JAVA_HOME`: Thường được sử dụng để xác định vị trí cài đặt JDK.

Shell Script giúp tự động hóa các công việc lặp lại trong quá trình phát triển và vận hành hệ thống.

---

# 4. Kiến thức lý thuyết Linux

## 4.1. Process Lifecycle

Đã tìm hiểu vòng đời cơ bản của một process:

```text
Parent Process
      |
    fork()
      |
 Child Process
      |
    exec()
      |
   Running
      |
    exit()
      |
    wait()
      |
 Terminated
```

### fork()

Tạo process con từ process hiện tại.

### exec()

Thay thế chương trình hiện tại bằng một chương trình mới.

### wait()

Process cha chờ process con kết thúc và thu nhận trạng thái của process con.

### Zombie Process

Zombie Process là process con đã kết thúc nhưng process cha chưa gọi `wait()` để thu nhận trạng thái kết thúc.

---

## 4.2. I/O Redirection

Linux có ba standard streams:

| Stream   | File Descriptor | Ý nghĩa |
| -------- | --------------: | ------- |
| `stdin`  |               0 | Input   |
| `stdout` |               1 | Output  |
| `stderr` |               2 | Error   |

### Redirect stdout

```bash
command > output.txt
```

### Append stdout

```bash
command >> output.txt
```

### Redirect stderr

```bash
command 2> error.log
```

### Pipe

```bash
command1 | command2
```

Pipe cho phép truyền output của command trước thành input của command sau.

---

## 4.3. System Logs

Linux lưu trữ nhiều loại log trong:

```text
/var/log
```

Một số hệ thống sử dụng `systemd` và quản lý log thông qua `journalctl`.

Các command:

```bash
journalctl
```

Xem log gần đây:

```bash
journalctl -n 50
```

Theo dõi log realtime:

```bash
journalctl -f
```

System Logs có vai trò quan trọng trong:

* Debug ứng dụng.
* Phân tích lỗi.
* Theo dõi service.
* Kiểm tra hoạt động hệ thống.
* Phân tích sự cố.

---

# 5. Kết quả đạt được

Sau tuần đầu tiên, em đã đạt được các kết quả:

### Java

* Nắm vững 4 tính chất OOP.
* Hiểu và bước đầu áp dụng 5 nguyên lý SOLID.
* Phân biệt được Interface và Abstract Class.
* Hiểu cách hoạt động của `static`.
* Nắm được Java Collections Framework.
* Hiểu đặc điểm và hiệu năng của các Collection phổ biến.
* Biết một số Thread-safe Collection.
* Hiểu Hashing, HashMap và các khái niệm liên quan.
* Nắm được Checked Exception và Unchecked Exception.
* Biết sử dụng `try-catch-finally`, `throw`, `throws`.
* Biết xây dựng Custom Exception.

### Linux

* Hiểu cấu trúc Linux File System.
* Nắm được Linux File Permissions.
* Biết sử dụng `chmod`, `chown`, `umask`.
* Biết quản lý process bằng `ps`, `top`, `htop`, `kill`, `nohup`, `jobs`.
* Biết sử dụng các command xử lý text như `grep`, `sed`, `awk`, `cut`, `sort`, `uniq`.
* Biết sử dụng `ss`, `netstat`, `curl`, `wget`.
* Biết kiểm tra CPU, RAM, Disk và I/O.
* Hiểu Process Lifecycle.
* Hiểu stdin, stdout, stderr và Pipe.
* Biết viết Shell Script cơ bản.
* Hiểu Environment Variables.
* Biết xem và theo dõi System Logs.

Qua tuần học đầu tiên, em đã xây dựng được nền tảng cần thiết để tiếp tục tiếp cận các công nghệ Backend Java và môi trường triển khai ứng dụng.

---

# 6. Khó khăn và hướng khắc phục

Trong quá trình học tập, em gặp một số khó khăn:

* Chưa phân biệt rõ Interface và Abstract Class trong một số trường hợp.
* Chưa hiểu sâu ngay về cách HashMap xử lý dữ liệu bên trong.
* Việc lựa chọn Collection phù hợp dựa trên performance cần thêm thời gian thực hành.
* Chưa quen với nhiều command và option trong Linux.
* Process Lifecycle và cơ chế `fork()`, `exec()`, `wait()` khá trừu tượng.
* Cú pháp Shell Script có nhiều điểm khác với Java.

Để khắc phục, em chủ động:

* Đọc thêm tài liệu về Java Core và Linux.
* Thực hành lại các ví dụ trên môi trường thực tế.
* So sánh các trường hợp sử dụng khác nhau.
* Ghi chú các command thường sử dụng.
* Kết hợp nhiều command Linux để hiểu rõ cơ chế Pipe và Redirection.

---

# 7. Kế hoạch Tuần 2

Trong tuần thứ hai, nội dung học tập sẽ tập trung vào **Collections, Design Patterns và Testing**.

## 7.1. Collections

Các nội dung dự kiến:

* HashMap Internals.
* HashSet Internals.
* ArrayList Internals.
* Hashing.
* HashCode.
* Equals Contract.
* Collision.
* Concurrent Collections.
* Thread Safety.
* So sánh hiệu năng các Collection.

Mục tiêu là hiểu không chỉ cách sử dụng Collection mà còn hiểu được cách chúng hoạt động bên trong và lựa chọn Collection phù hợp với từng bài toán.

---

## 7.2. Design Patterns

Tìm hiểu các Design Pattern phổ biến:

* Singleton Pattern.
* Factory Pattern.
* Builder Pattern.
* Strategy Pattern.
* Observer Pattern.

Mục tiêu:

* Hiểu vấn đề mà từng Pattern giải quyết.
* Hiểu cấu trúc của từng Pattern.
* Biết khi nào nên sử dụng.
* Biết ưu điểm và hạn chế.
* Áp dụng Pattern vào các bài toán Java thực tế.

---

## 7.3. Testing

Tìm hiểu các nội dung:

* Unit Testing.
* JUnit 5.
* Test Case.
* Assertion.
* Test Lifecycle.
* Mocking.
* Mockito.
* Integration Testing.
* Test Coverage.

Mục tiêu là hình thành thói quen viết code có khả năng kiểm thử, phát hiện lỗi sớm và đảm bảo các chức năng hoạt động đúng theo yêu cầu.

---

# 8. Kết luận

Tuần đầu tiên giúp em củng cố nền tảng quan trọng về **Java Core và Linux Fundamentals**.

Đối với Java, em đã nắm được OOP, SOLID, Interface, Abstract Class, Static, Collections và Exception Handling. Đối với Linux, em đã làm quen với File System, Permissions, Process Management, Text Processing, Network Utilities, System Monitoring, Shell Script, Process Lifecycle, I/O Redirection và System Logs.

Đây là những kiến thức nền tảng cần thiết cho quá trình phát triển Backend. Trong tuần tiếp theo, em sẽ tiếp tục đi sâu vào **Java Collections, Design Patterns và Testing**, đồng thời áp dụng các kiến thức đã học vào các bài thực hành cụ thể.
