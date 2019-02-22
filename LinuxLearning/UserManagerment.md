##       User Managerment 


**User** là người có thể truy cập đến hệ thống. **Group** là tập hợp 
nhiều **user**. Mỗi **user** luôn là thành viên của **group**. Khi một user được
tạo ra mặc định một group được tạo ra. 

Mỗi **user** và **group** có một định danh duy nhất **uid** và **gid**. 
### 1. File quản lý người dùng và nhóm

+ File người dùng và mật khẩu được lưu trên file: /etc/passwd
```
$ tail /etc/passwd
root:x:0:0:root:/root:/bin/bash
deamon:x:1:1:deamon:/usr/sbin:/usr/sbin/nologin
.....
nguoidung:x:1001:1001::/home/nguoidung:
```
Mỗi dòng khai báo 1 người dùng trên linux. 
Với 1 tài khoản thì gồm 7 trường : 

Ví dụ dòng dầu tiên:
++ Tên nguồi dùng là root
++ Dấu : là dấu phân tách cột
++ Cột t2: Mật khẩu shadow đã được mã hóa.
++ Cột t3: UserID Trong trường hợp này người dùng có Id là 0
++ Cột t4: nhóm người dùng có ground ID là 0
++ Cột t5: Tên người dùng là root
++ Cột 6: Thư mục của người dùng
++ Cột 7: Người dùng này có thế sử dụng shell trên linux

Tài khoản bin: tường tự. Cột cuối cùng ghi /sbin/nologin: Túc là người dùng bin ko thể đăng nhập trên hệ thống

UserID là 0 là người dùng có quyền hạn cao nhất trên hệ thống linux.

+ Thông tin group đc lưu trong file /etc/group
```
$ /etc/group
```
+ `$/etc/shadow`
Lưu mật khẩu đã được mã hóa và chỉ có user root mới được quyền đọc.

Mỗi dòng mô tả 1 user

Cột 1: Tên người dùng

Cột 2: Mật khẩu. Dấu * tức là không đặt mật khẩu
### 2. User

+ Tạo user : Truy cập bằng quyền root
Cú pháp:
```
$ useradd <username>
```
Ví dụ: 
```
$ useradd nguoidung1
```
Ktra lại:
```
$tail -n1 /etc/paswd
```
+ Đặt mật khẩu cho user
Cú pháp
```
$ passwd <username>
```
+ Xem user thuộc group nào
```
groups <username>
```
+ Khóa/Mở khóa người dùng
Khóa: 
```
$ passwd -l <username> 
```
Mở: 
```
$ passwd -u <username> 
```
+ Xem uid của người dùng
```
$ id
```
+ Xóa người dùng
```
$userdel <username> 
```

### 3. Group
+ Tạo group 
```
$groupadd <groupname>
```
+ Xóa group
```
$ groupdel <groupname>
```
+ Xem các user thuộc group 
```
$ members <groupname>
```

#### Tài liệu tham khảo: https://help.ubuntu.com/lts/serverguide/user-management.html.en
