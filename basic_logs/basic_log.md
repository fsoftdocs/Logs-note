## Log

[1. Khái niệm về Log ](h#khainiem-log)

[2. Cấu trúc Log ](#cautruc-log)


[3. Các level trong Log ](#level-log)






<a name="khainiem-log"></a>
### 1. Khái niệm về Log

- Log là một quá trình ghi lại những thông tin được thông báo, lưu lại trong quá trình hoạt động của một ứng dụng ở một nơi tập trung. Mục đích chính là để có thể xem lại các thông tin hoạt động của ứng dụng trong quá khứ như debug khi có lỗi xảy ra, check health, xem info, error, warning,…
- Log file thường là các file văn bản thông thường dưới dạng “clear text” tức là bạn có thể dễ dàng đọc được nó, vì thế có thể sử dụng các trình soạn thảo văn bản (vi, vim, nano...) hoặc các trình xem văn bản thông thường (cat, tailf, head...) là có thể xem được file log.
- Các log được lưu lại tại ` /var/log ` .
  
 ==> Log giúp bạn theo dõi và giải quyết vấn đề về hệ thống của bạn .
<a name="cautruc-log"></a>
 ### 2. Cau truc cua dong log

 ` Jun 25 04:32:33 localhost systemd-logind: New session 203 of user root. `

 - ` Jun 25 04:32:33 ` : Thoi gian ma log ghi lai .
 - ` localhost ` : (du doan) log duoc ghi tren may ` localhost ` 
 - ` systemd-logind ` : (du doan) la process name .
 - `  New session 203 of user root. `: la noi dung cua log .
  

  **NOTE**: Các log process khác nhau hay các app khác nhau sẽ có cú pháp ghi log riêng và được đặt ở từng mục của app trong ` /var/log `
   
 ##### Cac name file log chinh :

- /var/log/auth.log: Lưu các log về xác thực

- /var/log/boot.log : Log các hoạt động trong quá trình khởi động hệ thống

- /var/log/cron: Log lưu các lịch hoạt động tự động

- /var/log/dmesg : Giống log message bên dưới nhưng chủ yếu là log bộ đệm

- /var/log/message: Log lưu thông tin chung của hệ thống

- /var/log/httpd/: Thư mục chứa log của dịch vụ Apache

- /var/log/maillog: Các log hoạt động mail trên máy chủ

- /var/log/secure: Log bảo mật

- /var/log/wtmp  : Ghi log đăng nhập

- /var/log/yum.log: Các log của Yum
<a name="phanloai-log"></a>
### 3. Phân loại các log ( LOG level )

Các level để phân loại log : 

- All: đây là cấp độ thấp nhất, Logger và Appender được định nghĩa với cấp độ này, mọi thông tin cần log sẽ được log.
- Debug: các thông tin dùng để debug, chúng ta có thể bật/ tắt log này dựa vào mode của application.
- Info: các thông tin mà bạn muốn ghi nhận thêm trong quá trình hoạt động của hệ thống. Ví dụ: log số lượng request, status, duration, … để biết traffic của hệ thống thế nào.
- Warning: log các thông tin cảnh báo của chương trình.
- Error: các lỗi khi chạy chương trình sẽ được log. Cố gắng log toàn bộ thông tin liên quan nhiều nhất có thể để có thể reproduce lại được mà ít tốn thời gian nhất.
- Fatal: log các lỗi nghiêm trọng xảy ra trong chương trình, có thể làm cho chương trình không sử dụng được nữa.
- Off: đây là cấp độ cao nhất, được sử dụng khi chúng ta không muốn log bất kỳ thông tin nào nữa.


