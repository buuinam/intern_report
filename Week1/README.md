
BÁO CÁO THỰC TẬP TUẦN 1
Chủ đề: Java Core và Linux Fundamentals
Intern: Bùi Văn Nam
Team: Platform - Adtech
Gmail: buivannam13032004@gmail.com
Leader: Nguyễn Văn Cương
1. Mục tiêu tuần
Trong tuần đầu tiên, theo roadmap mục tiêu là củng cố nền tảng về ngôn ngữ Java và hệ điều hành Linux nhằm chuẩn bị cho việc phát triển Backend Java trong các giai đoạn tiếp theo. Nội dung tập trung vào lập trình hướng đối tượng, các nguyên lý thiết kế phần mềm, xử lý ngoại lệ, cùng các thao tác quản trị hệ thống và sử dụng dòng lệnh trên Linux.
Lịch học Tuần 1 (Thứ 2 - Thứ 6)
Ngày	Nội dung học	Kết quả đạt được
Thứ 2	Java OOP	Nắm vững 4 tính chất OOP: Encapsulation, Inheritance, Polymorphism, Abstraction; thực hành xây dựng class và object.
Thứ 3	SOLID, Interface, Abstract Class, Static	Hiểu 5 nguyên lý SOLID; phân biệt Interface và Abstract Class; sử dụng từ khóa static.
Thứ 4	Collections & Exception Handling	Hiểu Java Collections Framework, so sánh hiệu năng các Collection; nắm cách xử lý Exception và các best practices.
Thứ 5	Linux Fundamentals	Thực hành File System, phân quyền (chmod, chown, umask), quản lý tiến trình, xử lý văn bản, mạng và giám sát hệ thống.
Thứ 6	Shell Script & Lý thuyết Linux	Học Shell Script cơ bản, Environment Variables; tìm hiểu Process Lifecycle, File Permissions, I/O Redirection, System Logs và ôn tập kiến thức tuần.

2. Chi tiết nội dung đã học
2.1 Java Core
a. Lập trình hướng đối tượng (OOP)
Đã tìm hiểu và nắm vững bốn tính chất cơ bản của lập trình hướng đối tượng gồm:
-	Tính đóng gói (Encapsulation) 
-	Tính kế thừa (Inheritance) 
-	Tính đa hình (Polymorphism) 
-	Tính trừu tượng (Abstraction) 
Thông qua việc nghiên cứu các ví dụ và xây dựng các chương trình Java đơn giản, đã hiểu được vai trò của từng tính chất trong việc tổ chức mã nguồn, tăng khả năng tái sử dụng và mở rộng chương trình.
b. Nguyên lý SOLID
Đã nghiên cứu năm nguyên lý SOLID trong thiết kế hướng đối tượng, bao gồm:
-	Single Responsibility Principle 
-	Open/Closed Principle 
-	Liskov Substitution Principle 
-	Interface Segregation Principle 
-	Dependency Inversion Principle 
Qua các ví dụ minh họa, đã hiểu cách áp dụng các nguyên lý này để xây dựng phần mềm dễ bảo trì, dễ mở rộng và giảm sự phụ thuộc giữa các thành phần.
c. Interface, Abstract Class và Static
Đã tìm hiểu sự khác nhau giữa Interface và Abstract Class, hiểu được trường hợp sử dụng của từng loại trong quá trình thiết kế chương trình.
Bên cạnh đó, đã nghiên cứu từ khóa static, bao gồm:
-	Static variable 
-	Static method 
-	Static block 
Qua đó hiểu được cách các thành phần static được quản lý ở cấp lớp thay vì cấp đối tượng.
d. Java Collections Framework
Đã tìm hiểu các cấu trúc dữ liệu phổ biến trong Java Collections Framework như:
-	List 
-	Set 
-	Map 
-	Queue 
Đồng thời nghiên cứu hiệu năng của từng cấu trúc dữ liệu trong các thao tác:
-	Thêm dữ liệu 
-	Xóa dữ liệu 
-	Tìm kiếm 
-	Truy cập phần tử 
Ngoài ra cũng tìm hiểu các collection hỗ trợ đa luồng như:
-	ConcurrentHashMap 
-	CopyOnWriteArrayList 
-	Vector 
-	Hashtable 
Qua đó hiểu được sự khác biệt giữa collection thông thường và collection thread-safe.
e. Exception Handling
Đã nghiên cứu cơ chế xử lý ngoại lệ trong Java, bao gồm:
-	Checked Exception 
-	Unchecked Exception 
-	try-catch-finally 
-	throw 
-	throws 
-	Custom Exception 
Đồng thời tìm hiểu các nguyên tắc xử lý ngoại lệ theo best practices nhằm giúp chương trình ổn định và dễ bảo trì.
2.2 Linux Fundamentals
a. Linux File System
Đã tìm hiểu cấu trúc thư mục của hệ điều hành Linux, hiểu được chức năng của các thư mục quan trọng như:
-	/: Thư mục gốc. 
-	/home: Thư mục người dùng. 
-	/etc: Tệp cấu hình. 
-	/usr: Chương trình và thư viện. 
-	/var: Nhật ký và dữ liệu hệ thống. 
-	/tmp: Tệp tạm. 
-	/bin: Các lệnh hệ thống cơ bản.Qua đó hiểu được cách Linux tổ chức dữ liệu và quản lý hệ thống.
b. File Permissions
Đã nghiên cứu cơ chế phân quyền trên Linux.
Nắm được:
-	User: Chủ sở hữu của tệp hoặc thư mục.
-	Group: Nhóm người dùng được cấp quyền. 
-	Other: Những người dùng còn lại. 
Hiểu ý nghĩa của các quyền:
-	Read (r): Quyền đọc nội dung. 
-	Write (w): Quyền chỉnh sửa hoặc ghi dữ liệu. 
-	Execute (x): Quyền thực thi chương trình hoặc truy cập thư mục. 
Đồng thời thực hành các lệnh:
-	Chmod: Thay đổi quyền truy cập. 
-	Chown: Thay đổi chủ sở hữu hoặc nhóm. 
-	Umask: Thiết lập quyền mặc định khi tạo tệp hoặc thư mục. 
để thay đổi quyền truy cập và chủ sở hữu của tập tin.
c. Process Management
Đã tìm hiểu cách quản lý tiến trình trên Linux.
Thực hành các lệnh:
-	ps: Hiển thị danh sách tiến trình đang chạy. 
-	top: Theo dõi tiến trình và tài nguyên hệ thống theo thời gian thực. 
-	htop: Công cụ theo dõi tiến trình với giao diện trực quan. 
-	kill: Kết thúc một tiến trình theo PID. 
-	nohup: Chạy tiến trình ở chế độ nền, vẫn hoạt động khi đóng Terminal. 
-	jobs: Hiển thị các tiến trình đang chạy nền trong phiên làm việc hiện tại.
Qua đó hiểu được cách theo dõi, quản lý và kết thúc các tiến trình đang chạy trên hệ thống.
d. Text Processing
Đã tìm hiểu các công cụ xử lý văn bản trên Linux, bao gồm:
-	grep: Tìm kiếm nội dung theo từ khóa. 
-	sed: Chỉnh sửa và thay thế nội dung văn bản. 
-	awk: Xử lý dữ liệu theo cột hoặc dòng. 
-	cut: Cắt và trích xuất dữ liệu từ văn bản. 
-	sort: Sắp xếp dữ liệu theo thứ tự. 
-	uniq: Loại bỏ hoặc thống kê các dòng trùng lặp
Hiểu được cách lọc dữ liệu, tìm kiếm nội dung và xử lý tệp văn bản thông qua dòng lệnh.
e. Network Utilities
Đã nghiên cứu các công cụ kiểm tra và kết nối mạng như:
-	netstat: Kiểm tra các kết nối mạng và cổng đang sử dụng. 
-	ss: Hiển thị thông tin socket và trạng thái kết nối mạng. 
-	curl: Gửi yêu cầu HTTP và kiểm tra phản hồi từ máy chủ. 
-	wget: Tải tệp hoặc dữ liệu từ Internet.
Qua đó hiểu cách kiểm tra cổng mạng, gửi yêu cầu HTTP và tải dữ liệu từ Internet.
f. System Monitoring
Đã tìm hiểu các công cụ giám sát tài nguyên hệ thống:
-	df: Kiểm tra dung lượng ổ đĩa. 
-	du: Kiểm tra dung lượng thư mục hoặc tệp. 
-	free: Hiển thị thông tin bộ nhớ RAM. 
-	top: Theo dõi CPU, RAM và các tiến trình đang chạy. 
-	iostat: Theo dõi hiệu năng ổ đĩa và hoạt động I/O.
Hiểu được cách kiểm tra dung lượng ổ cứng, bộ nhớ, CPU và hiệu năng của hệ thống.
g. Shell Scripting
Đã làm quen với Shell Script, hiểu cấu trúc cơ bản của một tập lệnh Bash.
Tìm hiểu:
-	Khai báo biến 
-	Điều kiện 
-	Vòng lặp 
-	Hàm 
-	Tham số dòng lệnh 
Đồng thời tìm hiểu về biến môi trường (Environment Variables) và cách thiết lập các biến như PATH và JAVA_HOME.
2.3 Kiến thức lý thuyết Linux
Trong quá trình học, đã nghiên cứu thêm các kiến thức nền tảng của hệ điều hành Linux.
Process Lifecycle
Hiểu được vòng đời của một tiến trình từ khi được tạo bởi fork(), thực thi bằng exec(), chờ kết thúc thông qua wait() cho đến khi tiến trình kết thúc.
Đồng thời tìm hiểu khái niệm Zombie Process và nguyên nhân hình thành tiến trình Zombie.
File Permissions
Hiểu rõ mô hình phân quyền User – Group – Other và cách hệ điều hành kiểm soát quyền truy cập đối với từng người dùng.
I/O Redirection
Nắm được cơ chế chuyển hướng dữ liệu trong Linux, bao gồm:
-	stdin: Luồng dữ liệu đầu vào. 
-	stdout: Luồng dữ liệu đầu ra. 
-	stderr: Luồng hiển thị thông báo lỗi. 
-	Pipe (|): Chuyển đầu ra của lệnh này thành đầu vào của lệnh khác.
Hiểu cách kết hợp nhiều lệnh để xử lý dữ liệu hiệu quả trên dòng lệnh.
System Logs
Đã tìm hiểu cơ chế ghi nhật ký của Linux.
Hiểu được vai trò của:
-	/var/log: Thư mục lưu trữ các tệp nhật ký của hệ thống. 
-	syslog: Ghi lại các sự kiện và thông báo của hệ điều hành. 
-	journalctl: Xem và tra cứu nhật ký do systemd quản lý.
trong việc theo dõi hoạt động của hệ thống và hỗ trợ xử lý lỗi.
3. Kết quả đạt được
Sau khi hoàn thành tuần học đầu tiên, đã đạt được các kết quả sau:
-	Nắm được các kiến thức nền tảng về lập trình hướng đối tượng trong Java. 
-	Hiểu và phân biệt được Interface, Abstract Class và từ khóa static. 
-	Hiểu các nguyên lý SOLID và vai trò của chúng trong thiết kế phần mềm. 
-	Nắm được cách sử dụng Java Collections và lựa chọn cấu trúc dữ liệu phù hợp theo yêu cầu bài toán. 
-	Hiểu cơ chế xử lý ngoại lệ và áp dụng các nguyên tắc xử lý ngoại lệ trong Java. 
-	Thành thạo các thao tác cơ bản trên hệ điều hành Linux như quản lý tệp, phân quyền, quản lý tiến trình, xử lý văn bản và kiểm tra tài nguyên hệ thống. 
-	Hiểu vòng đời của tiến trình, cơ chế phân quyền, chuyển hướng dữ liệu và hệ thống nhật ký của Linux. 
-	Xây dựng được nền tảng kiến thức để tiếp tục học các công nghệ Backend như Spring Boot, Docker, MySQL và các hệ thống triển khai ứng dụng trong các tuần tiếp theo.
4. Kế hoạch tuần 2
Tuần 2: Collections, Design Patterns & Testing
Yêu cầu Collections:
•	HashMap, HashSet, ArrayList internals
•	HashCode và Equals contract
•	Concurrent collections (ConcurrentHashMap, BlockingQueue)
•	Design Patterns: Singleton, Factory, Observer, Strategy
Yêu cầu Testing:
•	Unit Testing principles và JUnit 5
•	Mocking
•	Integration testing strategies
•	Test coverage và quality metrics

