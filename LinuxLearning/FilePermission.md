## File Fermission 
### 1. Quyền sử hữu file
Quyền sở hữu file cung cấp phương thức bảo mật để lưu giữ file. 
Mọi file trong Unix có các thuộc tính sau để thể hiện quyền hạn truy cập tới nó (File Permission)

Các quyền sở hữu file:
+ **Quyền hạn truy cập của người sở hữu**: Quyền hạn truy cập của chủ nhân quyết định những hành động gì mà người sở hữu có thể thực hiện trên file.
+ **Quyền hạn truy cập nhóm**: Quyền hạn truy cập của nhóm quyết định hành động gì mà người sử dụng, thành viên của nhóm
có thể thực hiện trên file.
+ **Các quyền hạn truy cập khác**: Chỉ hành động nào mà tất cả những người sử dụng có thể thực hiện trên file.


Có 3 quyền cơ bản của file: 
+ **read (r)**: Cho phép đọc nội dung của file.
+ **write (w)**: Cho phép chỉnh sửa hoặc gỡ bỏ nội dung của file.
+ **execute(x)**: Người sử dụng với quyền hạn truy cập thực thi có thể chạy một file như là một chương trình.

Một file đc sở hữu bởi 3 đối tượng:
+ User owner -> u
+ Group owner -> g
+ Others-> o

Ví dụ: 
```
$ ls –l file1
-rwxr-xr-- chichi chichi 0 Th01 9 14:52 file1
```

- Các ký tự đầu tiên từ 1 đến 3 (2-4 trong dãy kể cả dấu -) quyền hạn người sử hữu file. 
- Nhóm 3 ký tự tiếp theo từ 5-7 quyền của nhóm
- Nhóm 3 ký tự cuối cùng từ 8-10 quyền hạn truy cập khác. 

Trong ví dụ trên người sở hữu có cho phép đọc (r), ghi (w), và chạy chương trình (x). 
Nhóm có cho phép đọc (r) và thực thi (x), nhưng không cho phép ghi (w). Người dùng khác cho phép đọc (r).

Để thay đổi quyền hạn truy cập của file hoặc thư mục, bạn sử dụng lệnh chmod (change mode). 

Có hai cách để sử dụng chmod là: chế độ tượng trưng (Symbolic Mode) và chế độ tuyệt đối (Absolute Mode).

## 1.1 Sử dụng chmode trong chế độ tượng trưng
Với chế độ này bạn có thể thêm, xóa hoặc xác định tập hợp các cho phép mà bạn muốn bằng cách sử dụng các toán tử sau:

|Toán tử chmod|Miêu tả|
|-------|------|
|+|Thêm quyền hạn truy cập được chỉ định tới một file hoặc tệp|
|-|Gỡ bỏ quyền hạn truy cập đã được chỉ định từ một file hoặc thư mục|
|=|Thiết lập các quyền hạn truy cập được chỉ định|

Ví dụ: file1 có quyền truy cập như sau:
```
$ ll file1
-rwxrw-r—chichi chichi 0 Th01 9 14:52 file1
```
Bạn có thể thay đổi quyền sử hữu của file1 bằng cách sử dụng lệnh chmod
```
$chmod o+w file1
$ ll file1
-rwxrw-rw- chichi chichi 0 Th01 9 14:52 file1
$chmod u-x file1
$ ll file1
-rw-rw-rw- chichi chichi 0 Th01 9 14:52 file1
```
Bạn có thể kết nối những lệnh này trên một dòng đơn:
```
$chmod o+w,u-x file1
$ ll file1
-rw-rw-rw- chichi chichi 0 Th01 9 14:52 file1
```

## 1.2 Sử dụng chmod với quyền hạn truy cập tuyệt đối trong Unix/Linux

Cách thứ hai để chỉnh sửa quyền hạn truy cập với lệnh chmod là sử dụng số để xác định các quyền hạn truy cập cho file.

|Số|Đại diện cho quyền hạn truy cập trong hệ cơ số 8|Tham chiếu|
|-----|-----|-----|
|0|Không cho phép|---|
|1|	Cho phép thực thi|--x|
|2|Cho phép ghi|-w-|
|3|Cho phép thực thi và ghi: 1 (thực thi) + 2 (ghi) = 3|-wx|
|4|Cho phép đọc|r--|
|5|Cho phép đọc và thực thi: 4(đọc) + 1 (thực thi) = 5|r-x|
|6|Cho phép đọc và ghi: 4 (đọc) + 2 (ghi) = 6|rw-|
|7|Cho phép tất cả: 4 (đọc) + 2 (ghi) + 1 (thực thi) = 7|rwx|

Ví dụ file1: 
```
$ ll file1
-rwxrw-r—chichi chichi 0 Th01 9 14:52 file1
$chmod 755 file1
$ ll file1
-rwxr-xr-xchichi chichi 0 Th01 9 14:52 file1
```
 ***Thư mục được phân quyền mặc định là 777 là initrd.img và vmlinuz***

## 2. Thay đổi người sở hữu và nhóm trong Unix/Linux

+ **chown**: Thay đổi sở hữu cá nhân (change owner).
+ **chgrp**: Thay đổi sở hữu nhóm (change group).
### 2.1 Thay đổi người sở hữu trong Unix/Linux
Lệnh chown thay đổi quyền sở hữu của một file. 

Cú pháp cơ bản là:
```
$ chown user filelist
```
Giá trị của `user` có thể là tên hoặc ID của người sử dụng trên hệ thống. Ví dụ:
Ví dụ:
```
$ chown nguoidung file1
$
```
Thay đổi người sở hữu của file1 thành `nguoidung`.

### 2.2 Thay đổi quyền sở hữu nhóm trong Unix/Linux
Lệnh `chrgp` thay đổi sở hữu nhóm của file. Cú pháp đơn giản là:
```
$ chgrp group filelist
```
Giá trị của group có thể là tên hoặc ID của nhóm trên hệ thống. 

Ví dụ:
```
$ chgrp group1 file1
$
```
Kết quả: File1 đã được thay nhóm sử hữu là group1



