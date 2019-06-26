## Log

#### 1. Khái niệm về Log

- Log là một quá trình ghi lại những thông tin được thông báo, lưu lại trong quá trình hoạt động của một ứng dụng ở một nơi tập trung. Mục đích chính là để có thể xem lại các thông tin hoạt động của ứng dụng trong quá khứ như debug khi có lỗi xảy ra, check health, xem info, error, warning,…
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

#### 3. Phân loại các log ( LOG level )

Các level để phân loại log : 

- All: đây là cấp độ thấp nhất, Logger và Appender được định nghĩa với cấp độ này, mọi thông tin cần log sẽ được log.
- Debug: các thông tin dùng để debug, chúng ta có thể bật/ tắt log này dựa vào mode của application.
- Info: các thông tin mà bạn muốn ghi nhận thêm trong quá trình hoạt động của hệ thống. Ví dụ: log số lượng request, status, duration, … để biết traffic của hệ thống thế nào.
- Warning: log các thông tin cảnh báo của chương trình.
- Error: các lỗi khi chạy chương trình sẽ được log. Cố gắng log toàn bộ thông tin liên quan nhiều nhất có thể để có thể reproduce lại được mà ít tốn thời gian nhất.
- Fatal: log các lỗi nghiêm trọng xảy ra trong chương trình, có thể làm cho chương trình không sử dụng được nữa.
- Off: đây là cấp độ cao nhất, được sử dụng khi chúng ta không muốn log bất kỳ thông tin nào nữa.




#### 4. Syslog trong Linux

##### a, syslog là gì ?
Syslog là một giao thức dùng để xử lý các file log Linux. Các file log có thể được lưu tại chính máy Linux đó, hoặc có thể di chuyển và lưu tại 1 máy khác.

##### Ứng dụng của syslog :


- Phân tích nguyên nhân gốc rễ của một vấn đề
- Giúp cho việc khắc phục sự cố nhanh hơn khi hệ thống gặp vấn đề
- Giúp cho việc phát hiện, dự đoán một vấn đề có thể xảy ra đối với hệ thống

##### Đi qua hàng   ` Lịch Sử `  của syslog

Syslog được phát triển năm 1980 bởi Eric Allman, nó là một phần của dự án Sendmail, và ban đầu chỉ được sử dụng duy nhất cho Sendmail. Nó đã thể hiện giá trị của mình và các ứng dụng khác cũng bắt đầu sử dụng nó. Syslog hiện nay trở thành giải pháp khai thác log tiêu chuẩn trên Unix-Linux cũng như trên hàng loạt các hệ điều hành khác và thường được tìm thấy trong các thiết bị mạng như router Trong năm 2009, Internet Engineering Task Forec (IETF) đưa ra chuẩn syslog trong RFC 5424.

Syslog ban đầu sử dụng UDP, điều này là không đảm bảo cho việc truyền tin. Tuy nhiên sau đó IETF đã ban hành RFC 3195 (Đảm bảo tin cậy cho syslog) và RFC 6587 (Truyền tải thông báo syslog qua TCP). Điều này có nghĩa là ngoài UDP thì giờ đây syslog cũng đã sử dụng TCP để đảm bảo an toàn cho quá trình truyền tin.

##### Cách thức hoạt động của syslog

Syslog là một giao thức, và được sử dụng bới dịch vụ Rsyslog. Dịch vụ Rsyslog mới là người đưa ra các quyết định như sử dụng port nào để vận chuyển log, sau bao nhiêu lâu thì log sẽ được xoay vòng…

Hai khái niệm xoay quanh syslog :
- Syslog : Giao thức dùng để xử lý file log trong Linux.
- Rsyslog : Dịch vụ sử dụng Syslog

##### b, Phân tích cấu hình của syslog

##### File cấu hình syslog :

- Trong CENTOS, file cấu hình là /etc/rsyslog.conf . File này chứa cả các rule về log
- Trong UBUNTU file cấu hình là /etc/rsyslog.conf nhưng các rule được định nghĩa riêng trong /etc/rsyslog.d/50-defaul.conf .

> file /etc.rsyslog.conf treong CENTOS 

```
# rsyslog configuration file

# For more information see /usr/share/doc/rsyslog-*/rsyslog_conf.html
# If you experience problems, see http://www.rsyslog.com/doc/troubleshoot.html

#### MODULES ####

# The imjournal module bellow is now used as a message source instead of imuxsock.
$ModLoad imuxsock # provides support for local system logging (e.g. via logger command)
$ModLoad imjournal # provides access to the systemd journal
#$ModLoad imklog # reads kernel messages (the same are read from journald)
#$ModLoad immark  # provides --MARK-- message capability

# Provides UDP syslog reception
#$ModLoad imudp
#$UDPServerRun 514

# Provides TCP syslog reception
#$ModLoad imtcp
#$InputTCPServerRun 514


#### GLOBAL DIRECTIVES ####

# Where to place auxiliary files
$WorkDirectory /var/lib/rsyslog

# Use default timestamp format
$ActionFileDefaultTemplate RSYSLOG_TraditionalFileFormat

# File syncing capability is disabled by default. This feature is usually not required,
# not useful and an extreme performance hit
#$ActionFileEnableSync on

# Include all config files in /etc/rsyslog.d/
$IncludeConfig /etc/rsyslog.d/*.conf

# Turn off message reception via local log socket;
# local messages are retrieved through imjournal now.
$OmitLocalLogging on

# File to store the position in the journal
$IMJournalStateFile imjournal.state


#### RULES ####

# Log all kernel messages to the console.
# Logging much else clutters up the screen.
#kern.*                                                 /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none;cron.none                /var/log/messages

# The authpriv file has restricted access.
authpriv.*                                              /var/log/secure

# Log all the mail messages in one place.
mail.*                                                  -/var/log/maillog


# Log cron stuff
cron.*                                                  /var/log/cron

# Everybody gets emergency messages
*.emerg                                                 :omusrmsg:*

# Save news errors of level crit and higher in a special file.
uucp,news.crit                                          /var/log/spooler

# Save boot messages also to boot.log
local7.*                                                /var/log/boot.log


# ### begin forwarding rule ###
# The statement between the begin ... end define a SINGLE forwarding
# rule. They belong together, do NOT split them. If you create multiple
# forwarding rules, duplicate the whole block!
# Remote Logging (we use TCP for reliable delivery)
#
# An on-disk queue is created for this action. If the remote host is
# down, messages are spooled to disk and sent when it is up again.
#$ActionQueueFileName fwdRule1 # unique name prefix for spool files
#$ActionQueueMaxDiskSpace 1g   # 1gb space limit (use as much as possible)
#$ActionQueueSaveOnShutdown on # save messages to disk on shutdown
#$ActionQueueType LinkedList   # run asynchronously
#$ActionResumeRetryCount -1    # infinite retries if host is down
# remote host is: name/ip:port, e.g. 192.168.0.1:514, port optional
#*.* @@remote-host:514
# ### end of the forwarding rule ###

```

 Có thể nhận biết nơi lưu log của app qua file cấu hình của syslog ( /etc/rsyslog.conf):
 ``` 
 # Log all the mail messages in one place.
mail.*                                                  -/var/log/maillog
```

Cấu hình Syslog như hình trên được chia thành 2 trường:

- Trường 1: Trường Seletor (` mail.* ` ) :
    - Trường Seletor : Chỉ ra nguồn tạo ra log và mức cảnh bảo của log đó.
    - Trong trường seletor có 2 thành phần và được tách nhau bằng dấu “.”
- Trường 2: Trường action (`  -/var/log/maillog `)
    - Chỉ ra nơi lưu log của tiến trình đó.( Thường được lưu tại localhost )

##### Các nguồn tạo log ( Facility Level )



|Nguồn tạo log | Ý nghĩa |
|--------------|---------|
|kernel | Những log mà do kernel sinh ra |
|auth hoặc authpriv | Log do quá trình đăng nhập hoặc xác thực tài khoản |
|mail | Log của mail |
|cron | Log do tiến trình cron trong hệ thống |
|user | Log của đến từ ứng dụng của người dùng |
|lpr | Log từ hệ thống in ấn |
|deamon | Log từ các tiến trình chạy trên nền của hệ thống |
|ftp | Log từ tiến trình ftp | 
|console | 	Log cảnh báo hệ thống |
|security | Kiểm tra đăng nhập |
|local 0 -> local 7 | Log dự trữ cho sử dụng nội bộ |

##### Mức cảnh báo của log ( Severity Level )

| Code | Mức cảnh báo | Ý nghĩa |
|------|--------------|---------|
|0 |emerg | Thông báo tình trạng khẩn cấp |
|1 |alert | Hệ thống cần can thiệp ngay |
|2 |crit | Tình trạng nguy kịch |
|3 |error | Thông báo lỗi đối với hệ thống |
|4 |warn | Mức cảnh báo đối với hệ thống |
|5 |notice | Chú ý đối với hệ thống |
|6 |info | Thông tin của hệ thống |
|7 |debug | Quá trình kiểm tra hệ thống |

Ví dụ tùy chỉnh việc lưu log với từng mức cảnh báo với dịch vụ ` mail ` :
( Mức cảnh báo đi theo thứ tự từ 7 => 1 . Tức là khi bạn muốn mức độ cảnh báo là info thì mức độ cảnh báo sẽ chỉ ghi log khi có cảnh báo từ Info trở lên như notice, warn , .. )

- lưu các Log với mức độ cảnh báo là INFO (các mức cảnh báo như info, notice ,.. syslog mới thực hiện lưu log ):
` mail.info         /var/log/mail `
- mail ghi các log với mức là info
` mail.=info         /var/log/mail `
- lưu lại tất cả các mức của dịch vụ mail vào log:
` mail.*         /var/log/mail  `
- lưu lại tất cả, ngoài trừ các log INFO:
` mail.!info         /var/log/mail `







