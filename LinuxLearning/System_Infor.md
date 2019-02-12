##  System Infor 
Là một quản trị viên hệ thống Linux cần biết được các thông tin hệ thống sau:

### 1. Hostname
```
$ cat /etc/hostname
```
- Để thay đổi host name
```
$ hostname newname 
```
### 2. Linux release
```
$ cat /etc/*release 
```
### 3. Kernel version
Sử dụng lệnh
```
$uname -r
```
Hoặc xem file
```
$cat /proc/version 
```
Ví dụ:
```
$ uname -r
4.13.0-36-generic 
```
+ Update kernel version 
B1: Kiểm tra version hiện tại
```
$ uname –r
```
B2: Cập nhật, download những phiên bản mới nhất
```
$ apt –get update
```
+ Upgrade kernel version

`$ apt –get upgrade` : Nâng cấp, thay thế gói cũ bàng gói mới, không xóa gói cũ

Hoặc:

`$ apt –get dist –upgrade` : Năng cấp, thêm gói tin mới, xóa gói cũ
### 4. Thông tin bộ nhớ
```
$ head /proc/meminfo
```
### 5. Hệ thống tệp tin
```
$ df -h
```
### 6. Đếm số lượng CPU
```
cat /proc/cpuinfo | grep model | uniq -c
```

