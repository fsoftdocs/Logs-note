## Log

#### 1. Khái niệm về Log

- Log giống như là hộp đen lưu lại những thông báo về hoạt động của hệ thống hoặc dịch vụ một cách cụ thể .
- Log file thường là các file văn bản thông thường dưới dạng “clear text” tức là bạn có thể dễ dàng đọc được nó, vì thế có thể sử dụng các trình soạn thảo văn bản (vi, vim, nano...) hoặc các trình xem văn bản thông thường (cat, tailf, head...) là có thể xem được file log.
- Các log được lưu lại tại ` /var/log ` .
  
 ==> Log giúp bạn theo dõi và giải quyết vấn đề về hệ thống của bạn .

 #### 2. Cau truc cua dong log

 ` Jun 25 04:32:33 localhost systemd-logind: New session 203 of user root. `

 - ` Jun 25 04:32:33 ` : Thoi gian ma log ghi lai .
 - ` localhost ` : (du doan) log duoc ghi tren may ` localhost ` 
 - ` systemd-logind ` : (du doan) la process name .
 - `  New session 203 of user root. `: la noi dung cua log .
  

  ##### NOTE : cac log cua process khac nhau hay cua cac app khac nhau se co cu phap ghi log rieng va duoc dat o tung muc cua app trong  ` /var/log  ` .
    
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

#### 3. Cac level trong log 


##### -- To be continute --
