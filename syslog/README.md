# Syslog

## [1. Syslog ](#syslog)
### [a, syslog là gì ? ](#syslog-lagi)
### [b, Cách đọc log cơ bản ](#syslog-ues)
### [c, Phân tích cấu hình của log ](#syslog-analyst)
### [d, Log server ](#logserver)

<a name="syslog"></a>
### 1. Syslog trong Linux
<a name="syslog-lagi"></a>
#### a, syslog là gì ?
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
<a name="syslog-use"></a>
#### b, Các cách đọc log cơ bản 


|Câu lệnh | Cú pháp |Ý nghĩa | Ghi chú thêm |
|---------|---------|--------|--------------|
|more | more [file] | Dùng xem toàn bộ nội dung của thư muc | Đối với câu lênh này nôi dung được xem theo từng trang. Bạn dung dấu "cách" để chuyển  trang |
|tail | tail [file] | In ra 10 dòng cuối cùng nội dung của file | thêm tùy chọn -n [số dòng] sẽ in ra số dòng theo yêu cầu , các log mới sinh ra cũng sẽ tự động hiện trên màn hình cho đến khi bạn dừng lại |
|head | head [file] | In ra 10 dòng đầu tiên của nôi dụng file |
|tail -f | tail -f [file] | Dùng để xem ngay lâp tức khi có log đến | Đây là câu lệnh dùng phổ biến nhất nó giúp ta có thể xem ngay lập tức log mới đến, và nó sẽ in ra 10 dong cuối cùng trong nội dung file đó |
| cat | cat [file] | dùng để xem tất cả các log được lưu trong một file | Có thể dùng thêm với grep để tìm kiếm theo ý muốn ( giả sử như muốn tìm log liên quan đến user : root)|

##### Thực hành đọc một vài file log cơ bản .



##### b,1 : Dùng tail -f để cem file log  realtime ( các log sẽ hiện trực tiếp lên màn hình )

> tail -f /var/log/messages

```
[root@localhost ~]# tail -f /var/log/messages
Jun 27 09:48:19 localhost systemd: Started Session 255 of user root.
Jun 27 09:48:19 localhost systemd-logind: New session 255 of user root.
Jun 27 09:48:19 localhost systemd: Started Session 256 of user root.
Jun 27 09:48:19 localhost systemd-logind: New session 256 of user root.
Jun 27 09:51:00 localhost systemd-logind: Removed session 255.
Jun 27 09:51:01 localhost systemd-logind: Removed session 256.
Jun 27 09:52:15 localhost systemd: Started Session 257 of user root.
Jun 27 09:52:15 localhost systemd-logind: New session 257 of user root.
Jun 27 09:52:16 localhost systemd: Started Session 258 of user root.
Jun 27 09:52:16 localhost systemd-logind: New session 258 of user root.
Jun 27 09:53:01 localhost systemd: Started Session 259 of user root.
Jun 27 09:53:01 localhost systemd-logind: New session 259 of user root.
Jun 27 09:53:32 localhost systemd: Stopping LSB: Bring up/down networking...
Jun 27 09:53:32 localhost NetworkManager[2765]: <info>  [1561604012.7022] device (eth0): state change: activated -> deactivating (reason 'user-requested', sys-iface-state: 'managed')
Jun 27 09:53:32 localhost NetworkManager[2765]: <info>  [1561604012.7027] manager: NetworkManager state is now DISCONNECTING
Jun 27 09:53:32 localhost NetworkManager[2765]: <info>  [1561604012.7335] audit: op="device-disconnect" interface="eth0" ifindex=2 pid=2520 uid=0 result="success"
Jun 27 09:53:32 localhost systemd: Starting Network Manager Script Dispatcher Service...
Jun 27 09:53:32 localhost NetworkManager[2765]: <info>  [1561604012.7336] device (eth0): state change: deactivating -> disconnected (reason 'user-requested', sys-iface-state: 'managed')
Jun 27 09:53:32 localhost dbus[2694]: [system] Activating via systemd: service name='org.freedesktop.nm_dispatcher' unit='dbus-org.freedesktop.nm-dispatcher.service'
Jun 27 09:53:32 localhost NetworkManager[2765]: <info>  [1561604012.7702] dhcp4 (eth0): canceled DHCP transaction, DHCP client pid 3063
Jun 27 09:53:32 localhost NetworkManager[2765]: <info>  [1561604012.7703] dhcp4 (eth0): state changed bound -> done
Jun 27 09:53:32 localhost dbus[2694]: [system] Successfully activated service 'org.freedesktop.nm_dispatcher'
Jun 27 09:53:32 localhost systemd: Started Network Manager Script Dispatcher Service.
Jun 27 09:53:32 localhost nm-dispatcher: req:1 'connectivity-change': new request (3 scripts)
Jun 27 09:53:32 localhost nm-dispatcher: req:1 'connectivity-change': start running ordered scripts...
Jun 27 09:53:32 localhost NetworkManager[2765]: <info>  [1561604012.8000] manager: NetworkManager state is now DISCONNECTED
Jun 27 09:53:32 localhost nm-dispatcher: req:2 'down' [eth0]: new request (3 scripts)
Jun 27 09:53:32 localhost network: Shutting down interface eth0:  Device 'eth0' successfully disconnected.
Jun 27 09:53:32 localhost network: [  OK  ]
Jun 27 09:53:32 localhost chronyd[2700]: Source 10.16.164.13 offline
Jun 27 09:53:32 localhost chronyd[2700]: Source 10.16.164.14 offline
Jun 27 09:53:32 localhost chronyd[2700]: Source 10.16.34.13 offline
Jun 27 09:53:32 localhost chronyd[2700]: Source 10.16.34.14 offline
Jun 27 09:53:32 localhost chronyd[2700]: Source 103.97.125.133 offline
Jun 27 09:53:32 localhost chronyd[2700]: Source 113.161.84.122 offline
Jun 27 09:53:32 localhost chronyd[2700]: Source 210.245.100.39 offline
Jun 27 09:53:32 localhost chronyd[2700]: Source 113.161.227.40 offline
Jun 27 09:53:32 localhost chronyd[2700]: Can't synchronise: no selectable sources
Jun 27 09:53:32 localhost nm-dispatcher: req:2 'down' [eth0]: start running ordered scripts...
Jun 27 09:53:32 localhost network: Shutting down loopback interface:  [  OK  ]
Jun 27 09:53:33 localhost systemd: Stopped LSB: Bring up/down networking.
Jun 27 09:53:33 localhost systemd: Starting LSB: Bring up/down networking...
Jun 27 09:53:33 localhost NetworkManager[2765]: <info>  [1561604013.1530] device (lo): carrier: link connected
Jun 27 09:53:33 localhost network: Bringing up loopback interface:  [  OK  ]


```
##### Phân tích cơ bản vài dòng log ( khi thực hiện tail mình đồng thời thực hiện restart network và cũng có xem được  vài dòng log cơ bản ):

- **1** . Các Interface bị shutdown

`Jun 27 09:53:32 localhost network: Shutting down interface eth0:  Device 'eth0' successfully disconnected.`

- **2** . Dịch vụ networking bị tắt đi.

`Jun 27 09:53:33 localhost systemd: Stopped LSB: Bring up/down networking.`

- **3** . Dịch vụ networking được bật lên .

`Jun 27 09:53:33 localhost systemd: Stopped LSB: Bring up/down networking.`

##### b.2 : Đọc log về login -logout (file /var/log/wtmp)

File ` wtmp ` là file log ghi lại lịch sử đăng nhập và đăng suất của hệ thống nhưng do cấu hình file đăng biệt nên k để đọc theo các câu lệnh bình thường nên ở đây mình dùng cách khác để đọc đó là dùng ` utmpdump ` 


>  utmpdump /var/log/wtmp

```
[7] [02339] [ts/0] [root    ] [pts/0       ] [10.17.58.228        ] [10.17.58.228   ] [Thu Jun 27 09:48:20 2019 +07]
[8] [02322] [    ] [        ] [pts/0       ] [                    ] [0.0.0.0        ] [Thu Jun 27 09:51:00 2019 +07]
[7] [02437] [ts/0] [root    ] [pts/0       ] [10.17.58.228        ] [10.17.58.228   ] [Thu Jun 27 09:52:16 2019 +07]
[7] [02459] [ts/1] [root    ] [pts/1       ] [172.27.100.15       ] [172.27.100.15  ] [Thu Jun 27 09:53:01 2019 +07]

```

có hai định dang log khác nhau ở  chuỗi log bên trên cụ thể là 

` [8] [02322] [    ] [        ] [pts/0       ] [                    ] [0.0.0.0        ] [Thu Jun 27 09:51:00 2019 +07] `
là định dạng của việc logout khỏi hệ thống .

`[7] [02459] [ts/1] [root    ] [pts/1       ] [172.27.100.15       ] [172.27.100.15  ] [Thu Jun 27 09:53:01 2019 +07] ` là định dạng có người dùng  `root `login vào hệ thống  dưới ip : `172.27.100.15 ` ( còn một vài thông tin  khác do hiểu biết hạn hẹp nên chưa kịp thời xác định được cụ thể )



<a name="syslog-analyst"></a>
#### c, Phân tích cấu hình của syslog

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


<a name="logserver"></a>
#### d, Log tập trung ( Log server )

##### log tập trung là gì?
 Giống như tên gọi ` log tập trung ` là nơi lưu trữ các file log mà nguồn của các file nằm ở  nhiều nơi khác nhau ` (  giả sử như Mail Server hay Web server mỗi chương trình đều sinh ra log mà mặc định log sẽ được lưu ở máy local nhưng khi sử dụng log tập trung thì các file log sẽ được gửi lên một server chỉ để dành riêng để lưu trữ log mà thôi ) `

##### Tại sao lại cần đến log tập trung ?

- Do có nhiều nguồn sinh log

    - Có nhiều nguồn sinh ra log, log nằm trên nhiều máy chủ khác nhau nên khó quản lý.
    - Nội dung log không đồng nhất (Giả sử log từ nguồn 1 có có ghi thông tin về ip mà không ghi thông tin về user name đăng nhập mà log từ nguồn 2 lại có) -> khó khăn trong việc kết hợp các log với nhau để xử lý vấn đề gặp phải.
    - Định dạng log cũng không đồng nhất -> khó khăn trong việc chuẩn hóa
    - Đảm bảo tính toàn vẹn, bí mật, sẵn sàng của log.
- Do có nhiều các rootkit được thiết kế để xóa bỏ logs.
- Do log mới được ghi đè lên log cũ -> Log phải được lưu trữ ở một nơi an toàn và phải có kênh truyền đủ đảm bảo tính an toàn và sẵn sàng sử dụng để phân tích hệ thống.


##### Tác dụng của log tập trung :

- Giúp quản trị viên có cái nhìn chi tiết về hệ thống -> có định hướng tốt hơn về hướng giải quyết
- Mọi hoạt động của hệ thống được ghi lại và lưu trữ ở một nơi an toàn (log server) -> đảm bảo tính toàn vẹn phục vụ cho quá trình phân tích điều tra các cuộc tấn công vào hệ thống
- Log tập trung kết hợp với các ứng dụng thu thập và phân tích log khác nữa giúp cho việc phân tích log trở nên thuận lợi hơn -> giảm thiểu nguồn nhân lực.

###### Thực hành trên syslog server 

Phía máy syslog-server cần chỉnh sửa cấu hình để nhận bản tin log từ các client gửi về :

- Chỉnh sửa nôi dung ở file /etc/rsyslog.conf:


```
# Provides UDP syslog reception
#$ModLoad imudp
#$UDPServerRun 514

# Provides TCP syslog reception
#$ModLoad imtcp
#$InputTCPServerRun 514

```

chúng ta có thể tùy chọn giao thức TCP hay UDP và gói tin sẽ được nhận ở cổng 514 . Ở đây mình sẽ sử dụng UDP nên sẽ bỏ comment ở hai dòng sau :

```
$ModLoad imudp
$UDPServerRun 514
```

Nếu các máy cứ gửi log lên server thì người quản lý sẽ không biết là log ở nào gửi lên vì thế cần tạo cho các máy client thư mục lưu trữ log riêng và cài đặt trong file cấu hình :

```
$template TmplAuth,"/var/log/%HOSTNAME%/%PROGRAMNAME%.log"
*.*     ?TmplAuth
```
Các dòng code trên nên được đặt ở trên GLOBAL DIRECTIVES ( cho sau ai mà có lạc vào file này còn hiểu là các modules không là họ thấy lạ lạ không cần thiết nên xóa đi đó )


Và cần thêm restart service nữa là hoàn thành những việc cần làm bên server rồi 

```
systemctl restart rsyslog
```
Bây giờ là thực hiện trên syslog client 

chúng ta cũng sẽ thêm chút mắm muối vào file /etc/rsyslog.conf chút thôi :


Thêm dòng code sau dưới mục RULES là được :
```
*.*             @Syslog_server_IP:514
```

và đừng quên restart rsyslog nhé 


##### Kiểm tra lại trên syslog server 

trong thư mục /var/log/ sẽ xuất hiện thêm một thư mục log của client (với tên là hostname của client nhé )

BEFORE
```
[root@localhost ~]# cd /var/log/
[root@localhost log]# ls
anaconda  boot.log-20190610  btmp    cron-20190614  dmesg      grubby_prune_debug  localhost         maillog-20190621  messages-20190614  rhsm             secure-20190621  spooler-20190614  tallylog  yum.log
audit     boot.log-20190613  chrony  cron-20190621  dmesg.old  jenkins             maillog           maillog-20190623  messages-20190621  secure           secure-20190623  spooler-20190621  tuned
boot.log  boot.log-20190619  cron    cron-20190623  firewalld  lastlog             maillog-20190614  messages          messages-20190623  secure-20190614  spooler          spooler-20190623  wtmp

```

AFTER

```
[root@localhost log]# ls
agent3    boot.log-20190610  chrony         cron-20190623  grubby_prune_debug  maillog           messages           rhsm             secure-20190623   spooler-20190623  yum.log
anaconda  boot.log-20190613  cron           dmesg          jenkins             maillog-20190614  messages-20190614  secure           spooler           tallylog
audit     boot.log-20190619  cron-20190614  dmesg.old      lastlog             maillog-20190621  messages-20190621  secure-20190614  spooler-20190614  tuned
boot.log  btmp               cron-20190621  firewalld      localhost           maillog-20190623  messages-20190623  secure-20190621  spooler-20190621  wtmp

```

` hostname ` ở máy client mình có tên là ` agent3 ` nên ở file /var/log đã có thêm file agent3 rồi (như thế là thành công rồi ) 


[Source](https://blog.cloud365.vn/search/?q=Tr%E1%BB%9D+th%C3%A0nh+cao+th%E1%BB%A7+logging)

--- THE END ---
