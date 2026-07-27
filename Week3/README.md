# Week 3: Concurrency & Docker

## 1. Concurrency trong Java

### 1.1 Thread Lifecycle và Thread Management

Đã tìm hiểu về Thread và vòng đời của một Thread trong Java. Qua đó hiểu được các trạng thái khác nhau của Thread và cách quản lý Thread trong quá trình thực thi.

Các trạng thái chính của Thread:

- **NEW**: Thread được tạo nhưng chưa được bắt đầu.
- **RUNNABLE**: Thread đã sẵn sàng để được CPU thực thi.
- **BLOCKED**: Thread đang chờ lấy Lock.
- **WAITING**: Thread đang chờ một Thread khác thực hiện một hành động.
- **TIMED_WAITING**: Thread tạm dừng trong một khoảng thời gian xác định.
- **TERMINATED**: Thread đã hoàn thành quá trình thực thi.

Một số phương thức quản lý Thread:

- `start()`: Bắt đầu một Thread mới.
- `sleep()`: Tạm dừng Thread trong một khoảng thời gian.
- `join()`: Chờ một Thread khác hoàn thành.
- `interrupt()`: Gửi tín hiệu yêu cầu Thread dừng hoặc xử lý việc bị gián đoạn.

---

### 1.2 ThreadPool và ExecutorService

Đã tìm hiểu về ThreadPool và ExecutorService trong Java. Qua đó hiểu được cách tái sử dụng Thread thay vì liên tục tạo mới Thread cho từng tác vụ.

ThreadPool giúp:

- Giảm chi phí tạo và hủy Thread.
- Hạn chế số lượng Thread được tạo trong hệ thống.
- Tăng hiệu năng của ứng dụng.
- Quản lý việc thực thi các Task hiệu quả hơn.

Một số loại ThreadPool phổ biến:

- **FixedThreadPool**: Sử dụng số lượng Thread cố định.
- **CachedThreadPool**: Tự động tạo và tái sử dụng Thread tùy theo nhu cầu.
- **ScheduledThreadPool**: Thực thi Task theo lịch hoặc sau một khoảng thời gian nhất định.

Một số phương thức của `ExecutorService`:

- `execute()`: Thực thi một Task nhưng không trả về kết quả.
- `submit()`: Gửi Task và có thể nhận kết quả thông qua `Future`.
- `shutdown()`: Dừng việc nhận các Task mới và thực hiện quá trình tắt ThreadPool.

---

### 1.3 Synchronization và Thread Safety

Đã tìm hiểu các vấn đề phát sinh khi nhiều Thread cùng truy cập và thay đổi dữ liệu dùng chung.

Khi nhiều Thread cùng thao tác trên một dữ liệu, có thể xảy ra **Race Condition**. Đây là tình trạng kết quả của chương trình phụ thuộc vào thứ tự thực thi của các Thread.

Các phương pháp đồng bộ hóa:

- **synchronized**: Đảm bảo tại một thời điểm chỉ một Thread được truy cập vào vùng mã hoặc dữ liệu được bảo vệ.
- **Lock**: Cung cấp khả năng kiểm soát việc khóa và mở khóa linh hoạt hơn `synchronized`.
- **Atomic Classes**: Cung cấp các thao tác Thread-Safe trên dữ liệu mà không cần khóa toàn bộ vùng mã.

Một số Atomic Class phổ biến:

- `AtomicInteger`
- `AtomicLong`
- `AtomicBoolean`
- `AtomicReference`

Việc sử dụng đúng cơ chế Synchronization giúp đảm bảo tính nhất quán của dữ liệu trong môi trường đa luồng.

---

## 2. CompletableFuture và Reactive Programming

### 2.1 CompletableFuture

Đã tìm hiểu `CompletableFuture` và cách xử lý các tác vụ bất đồng bộ trong Java.

`CompletableFuture` là một API hỗ trợ lập trình bất đồng bộ trong Java. Nó cho phép thực hiện các Task mà không cần chặn Thread hiện tại và có thể xử lý kết quả sau khi Task hoàn thành.

Một số phương thức thường sử dụng:

- `supplyAsync()`: Thực hiện một tác vụ bất đồng bộ và trả về kết quả.
- `runAsync()`: Thực hiện một tác vụ bất đồng bộ nhưng không trả về kết quả.
- `thenApply()`: Xử lý và biến đổi kết quả của Task trước đó.
- `thenAccept()`: Nhận kết quả nhưng không trả về kết quả mới.
- `thenCombine()`: Kết hợp kết quả của hai `CompletableFuture`.

`CompletableFuture` giúp xây dựng các luồng xử lý bất đồng bộ, giảm việc phải quản lý Thread thủ công và hỗ trợ kết hợp nhiều tác vụ hiệu quả.

---

### 2.2 Reactive Programming Basics

Đã tìm hiểu các khái niệm cơ bản của Reactive Programming và cách xử lý dữ liệu theo hướng bất đồng bộ, không chặn.

Reactive Programming là mô hình lập trình tập trung vào việc xử lý các luồng dữ liệu và các sự kiện bất đồng bộ.

Một số đặc điểm:

- Xử lý dữ liệu theo dạng Stream.
- Hỗ trợ xử lý bất đồng bộ.
- Có khả năng xử lý nhiều sự kiện liên tục.
- Hạn chế việc Blocking Thread.

Reactive Programming thường được sử dụng trong các hệ thống có lượng lớn Request hoặc dữ liệu liên tục như API, hệ thống Streaming và các ứng dụng có yêu cầu cao về khả năng mở rộng.

---

# 3. Docker

## 3.1 Container Concepts và Docker Architecture

Đã tìm hiểu các khái niệm cơ bản của Docker, bao gồm Container, Image, Docker Engine và Docker Architecture.

Docker là nền tảng giúp đóng gói ứng dụng cùng với các thư viện, Dependency và môi trường cần thiết để ứng dụng có thể chạy ổn định trên nhiều môi trường khác nhau.

### Docker Image

Docker Image là một bản mẫu chứa các thành phần cần thiết để tạo ra Container.

### Docker Container

Container là một Instance được tạo ra từ Docker Image và cung cấp môi trường cô lập để chạy ứng dụng.

### Docker Architecture

Kiến trúc Docker bao gồm:

- **Docker Client**: Nhận lệnh từ người dùng.
- **Docker Daemon**: Quản lý Image, Container, Network và Volume.
- **Docker Registry**: Lưu trữ và phân phối Docker Image.

---

## 3.2 Container vs Virtual Machine

### Virtual Machine

Virtual Machine thường phải chạy một hệ điều hành Guest riêng nên tiêu tốn nhiều tài nguyên hơn.

### Container

Container sử dụng chung Kernel với hệ điều hành Host nên có các ưu điểm:

- Khởi động nhanh hơn.
- Sử dụng ít tài nguyên hơn.
- Kích thước nhỏ hơn.

| Đặc điểm | Virtual Machine | Container |
|---|---|---|
| Kích thước | Lớn | Nhỏ hơn |
| Khởi động | Chậm hơn | Nhanh hơn |
| Tài nguyên | Tốn nhiều | Tiết kiệm hơn |
| Hệ điều hành | Có Guest OS riêng | Chia sẻ Kernel với Host |
| Isolation | Mạnh hơn | Nhẹ hơn |

---

## 3.3 Dockerfile và Best Practices

Đã tìm hiểu Dockerfile và cách sử dụng Dockerfile để xây dựng Docker Image.

Dockerfile là một file chứa các hướng dẫn để Docker xây dựng Image.

Một số Instruction thường sử dụng:

- `FROM`: Chọn Base Image.
- `WORKDIR`: Thiết lập thư mục làm việc.
- `COPY`: Sao chép file vào Image.
- `RUN`: Thực thi lệnh trong quá trình Build Image.
- `CMD`: Xác định lệnh mặc định khi Container chạy.
- `EXPOSE`: Khai báo Port mà ứng dụng sử dụng.

Một số Best Practices:

- Sử dụng Base Image có kích thước nhỏ khi phù hợp.
- Sử dụng file `.dockerignore` để loại bỏ các file không cần thiết.
- Sắp xếp các Instruction hợp lý để tận dụng Docker Layer Cache.
- Sử dụng Multi-stage Build để giảm kích thước Docker Image.
- Chỉ cài đặt các Dependency thực sự cần thiết.

Việc tối ưu Dockerfile giúp giảm thời gian Build và giảm kích thước Docker Image.

---

## 3.4 Image Layers và Optimization

Docker Image được cấu tạo từ nhiều Layer khác nhau. Mỗi Instruction trong Dockerfile có thể tạo ra một Layer mới.

Ví dụ:

```text
Base Image
    ↓
Cài đặt Dependencies
    ↓
Copy Source Code
    ↓
Build Application
