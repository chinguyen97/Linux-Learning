## Hard and Symbolic Links

### 1. Hard Link 
Sử dụng lệnh **ln** để tạo Hard Link.
Ví dụ:
```
$ ls 
Command file1
$ ln file1 file2
$ ls -l
1061255 -rw-rw-r-- 1 chichi chichi 12 Th01  9 20:21 Command
1054114 -rw-rw-r-- 2 chichi chichi 13 Th01 14 14:57 File1
1054114 -rw-rw-r-- 2 chichi chichi 13 Th01 14 14:57 File2
$ ln file1 file3
$ ls-l
1061255 -rw-rw-r-- 1 chichi chichi 12 Th01  9 20:21 Command
1054114 -rw-rw-r-- 3 chichi chichi 13 Th01 14 14:57 File1
1054114 -rw-rw-r-- 3 chichi chichi 13 Th01 14 14:57 File2
1054114 -rw-rw-r-- 3 chichi chichi 13 Th01 14 14:57 File3
```
Đặc điểm: 
+ File gốc phải tồn tại
+ inode của các tập tin giống nhau
+ Số link count tăng lên 1 sau mỗi lần tạo lket
+ Khi xóa file gốc, file liên kết ko hề bị mất đi mà chỉ xóa đi số link count 
+ Chú ý ta không thể tạo hard-link trên hai partition khác nhau. Tức là file gốc và file trỏ tới file gốc phải cùng 1 partition.
+ Khi thay đổi nội dung file gốc or file liên kết thfi file kia cũng đc cập nhật nội dung

### 2. Symbolic Link .
Sử dụng lệnh **ln –s** đẻ tạo Symbolic Link
```
$ ln -s file1 file4
$ ls -l
1061255 -rw-rw-r-- 1 chichi chichi 12 Th01  9 20:21 Command
1054114 -rw-rw-r-- 3 chichi chichi 13 Th01 14 14:57 File1
1054114 -rw-rw-r-- 3 chichi chichi 13 Th01 14 14:57 File2
1054114 -rw-rw-r-- 3 chichi chichi 13 Th01 14 14:57 File3
1054118 lrwxrwxrwx 1 chichi chichi  5 Th01 14 15:00 File4 ->file1
```
Đặc điểm:
+ File gốc phải tồn tại
+ inode của các tập tin khác nhau
+ Khi xóa file gốc, nội dung file liên kết ko hiển thị đc vì file liên kết
 chỉ đến 1 tệp tin khác mà tệp tin đó ko tồn tại.
+ Khi thay đổi nội dung file gốc or file liên kết thì file kia cũng đc cập nhật nội dung
+ Đầu tiên có chữ “l” để nhận dạng liên kết. 
