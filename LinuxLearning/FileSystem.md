
Linux quản lý hệ thống trên một hệ thống tệp tin, bắt đầu từ thư mục `root (/)`
 đây là thư mục được cấp quyền cao nhất.
 
Cấu trúc cơ bản của hệ thống Linux như sau:

![caythumuc](https://st.quantrimang.com/photos/image/122011/05/tree.jpg)
### 1. / -root: là thư mục root, 

+ Chỉ có Root user mới có quyền truy cập, quyền viết dưới thư mục này.
+ Lưu ý rằng **/root** là thư mục gốc của Root user.

### 2. /bin: User Binaries
+ Chứa các tập tin thực thi nhị phân (binary executables). 
Và các chương trình khởi động của hệ thống.
+ Lệnh Linux phổ biến sử dụng ở chế độ Singer-user mode nằm trong thư mục này.
+ Tất cả user trên hệ thống nằm tại thư mục này đều có thể sử dụng lệnh.
+ Ví dụ: ps, ls, ping, grep, cp.

### 3. - /sbin (System Binaries)  Chương trình hệ thống
Giống như /bin, /sbin cũng chứa các chương trình thực thi, 
nhưng chúng là những chương trình của admin, dành cho việc bảo trì hệ thống 
=> dành cho người dùng admin quản trị hệ thống - người dùng root hoặc superuser. 

Ví dụ như: reboot, fdisk, iptables, shutdown, 

### 4. /boot: boot loader file 
Chứa các file khởi động và cả nhân kernel là vmlinuz.

### 5. /etc Configuration Files
+ Chứa cấu hình các tập tin cấu hình của hệ thống, các tập tin lệnh để khởi động các dịch vụ của hệ thống…
+ Ngoài ra /etc còn chứa shell scripts startup và shutdown, sử dụng để chạy/ngừng các chương trình cá nhân.
+ Ví dụ: /etc/resolv.conf, /etc/logrotate.conf.

### 6. /media: Chứa thư mục dùng để mount cho các thiết bị có thể gỡ bỏ, 
di chuyển khỏi hệ thống được như CDROM, floppy, ...
### 7. /home: thư mục chứa các file cá nhân của từng user.

### 8. /dev: chứa Các file thiết bị - nơi lưu trữ các phân vùng ổ cứng, 
thiết bị ngoại vi như usb, ổ đĩa cắm ngoài hay bất cứ thiết bị nào được 
gán vào hệ thống.
Ví dụ: 
+ /dev/sdb1 là tên của USB bạn vừa cắm vào máy, 
để mở được USB này bạn cần sử dụng lệnh mount với quyền root: # mount /dev/sdb1 /tmp
+ Hard drive thường được mount tại thư mục /dev/sda , usb mount trong /dev/sde ; các phân vùng trên ổ địa được phân ra /dev/sda1, /dev/sda2...

### 9. /lib : Thư mục này chứa các file thư viện. 
Mỗi khi cài đặt phần mềm trên Linux, các thư viện cũng tự động được download. 
Thư mục này tương tự như thư mục SYSTEM32 của Windows

### 10. /mnt: Chứa các thư mục dùng để system admin thực hiện quá trình 
mount. Đây chính nơi tạo ra các thư mục để mount các phân vùng ổ đĩa cứng 
cũng như các thiết bị khác vào

### 11. /root : Thư mục ng dùng root. 

### 12. /tmp: Temporary Files 
+ Thư mục chứa các tập tin tạm thời được tạo bởi hệ thống và user.
+ Các tập tin tạo thư mục này được xóa khi hệ thống được khởi động lại (reboot).

### 13. /var: Variable Files
 Chứa đựng các file có sự thay đổi trong quá trình hoạt động của 
 hệ điều hành cũng như các ứng dụng. 

Ví dụ: hệ thống tập tin log (/var/log), các gói và các file dữ liệu 
(/var/lib), email (/var/mail), print queues (/var/spool); 
lock files (/var/lock); các file tạm thời cần khi reboot (/var/tmp).

### 14. /swap sử dụng các file swap 

### 15. /usr: Chương trình của người dùng

Chứa các thư viện, file thực thi, tài liệu hướng dẫn 

+ /usr/bin chứa file binary cho các chương trình của user. 
Nếu như một user trong quá trình thực thi một lệnh ban đầu sẽ tìm kiếm 
trong /bin, nếu như không có thì sẽ tiếp tục nhìn vào /usr/bin. 

Ví dụ một số lệnh như at. awk, cc...
+ /usr/sbin chứa các file binary cho system administrator. 
Nếu như ta không tìm thấy các file system binary bên dưới /sbin thì 
ta có thể tìm ở trong /usr/sbin. 
Ví dụ một số lệnh như cron, sshd, useradd, userdel
+ /usr/lib chứa các file libraries cho /usr/bin và /usr/sbin
+ /usr/local dùng để chứa chương trình của các user, các chương trình này được cài đặt từ source. Ví dụ khi ta install apache từ source thì nó sẽ nằm ở vị trí là /usr/local/apache2
+ /usr/src: Thư mục chứa mã nguồn kể cả mã nguồn của Linux.
+ /usr/man: Chứa tài liệu hướng dẫn (manual).

### 16. /opt: Optional add-on Applications 
/opt chứa các ứng dụng thêm vào từ các nhà cung cấp độc lập khác. 
Các ứng dụng này có thể được cài ở /opt hoặc một thư mục con của /opt.

### 17. /proc: Process Information 
Chứa đựng thông tin về quá trình xử lý của hệ thống.

### 18. /srv
Chứa dữ liệu liên quan đến các dịch vụ máy chủ như /srv/svs, 
chứa các dữ liệu liên quan đến CVS.

### **Tài liệu tham khảo:** https://quantrimang.com/cau-truc-cay-thu-muc-trong-linux-84056

