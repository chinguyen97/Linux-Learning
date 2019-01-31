## Command Line

### 1. Giới thiệu dấu nhắc:

```
root@chichi:/#
```
root: user

chichi: computer name

#: user toàn quyền

$: user có quyền giới hạn

### 2. Biến PS1

Bạn có thể thay đổi dòng nhắc lệnh trong biến PS1
 
Ví dụ
```
chichi@chichi:/$PS1='=>'
=>
=>
=>
```

Dòng nhắc có thể trở thành `=>`. 

Để thiết lập giá trị của PS1 để nó chỉ thư mục làm việc, sử dụng lệnh sau:
```
=>PS1="[\u@\h \w]$"
[chichi@chichi/]$
[chichi@chichi/]$
```
Kết quả của lệnh này là dòng nhắc lệnh hiển thị tên người dùng hiện tại, 
tên hostname, và thư mục làm việc.

Có một vài dãy thoát (escape) được sử dụng làm tham số giá trị cho PS1

|Dãy escape	|Mô tả|
|\t	|Thời gian hiện tại, diễn tả ở dạng HH:MM:SS|
|\d	|Ngày hiện tại, diễn tả ở dạng Ngày trong tuần Tháng Ngày|
|\n	|Dòng mới|
|\s	|Môi trường Shell hiện tại|
|\W	|Thư mục làm việc|
|\w	|Đường Path đầy đủ của thư mục làm việc|
|\h	|Hostname của thiết bị hiện tại|
|#	|Số lượng lệnh của lệnh hiện tại. Tăng mỗi khi có một lệnh mới được nhập|
|$	|Nếu UID hiệu quả là 0 (đó là, nếu bạn được đăng nhập như là root), kết thúc dòng nhắc với ký tự #; nếu không thì, sử dụng $.|

Bạn có thể tạo sự thay đổi bởi chính bạn mỗi khi bạn đăng nhập vào, 
hoặc bạn có thể có thay đổi được tạo một cách tự động trong PS1 bằng cách 
thêm nó tới file .profile.
### 3. Biến PS2

Khi thực hiện 1 câu lệnh chưa hoàn thiện, Shell sẽ hiển thị một dòng nhắc 
lệnh thứ hai và đợi bạn hoàn thiện lệnh đó và nhập lại.

Dòng nhắc lệnh mặc định thứ hai là ký hiệu lớn hơn `>`, nhưng có thể được 
thay đổi bằng cách định nghĩa lại biến PS2.

Định nghĩa lại PS2 với một dòng nhắc được tùy chỉnh theo ý ban:
```
$ PS2=" ->"
```