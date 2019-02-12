## 					File Managerment 

Trong Unix, có ba loại tệp cơ bản 
+ **Tệp thông thường** - Một tệp thông thường là một tệp trên hệ thống chứa dữ liệu, văn bản hoặc hướng dẫn chương trình. 
+ **Thư mục** - Thư mục lưu trữ cả các tập tin đặc biệt và thông thường. Đối với người dùng quen thuộc với Windows hoặc Mac OS, các thư mục Unix tương đương với các thư mục.
+ **Tệp đặc biệt** - Một số tệp đặc biệt cung cấp quyền truy cập vào phần cứng như ổ cứng, ổ đĩa CD-ROM, modem và bộ điều hợp Ethernet.  

### 1. Tạo, xóa file, thư mục
- Tạo 1 thư mục

Cú pháp: 
```
$ mkdir <filename>
```

- Tạo file

Cú pháp:
``` 
$ touch <filename>
``` 
Tùy chọn -t cho phép bạn đặt dấu ngày và thời gian của tệp. Để đặt dấu thời gian thành thời gian cụ thể:
VD: 
```
$ touch –t 02122019 file1
```
-	Xóa file
Sử dụng lệnh rm .  
Cú pháp:
```
$ rm filename
```
 `rm –r “filename”`  : Hỏi trước khi xóa
 
 `rm –rf “filename”` Xóa không hỏi trước.

### 2. Copy, di chuyển , đổi tên
- Sao chép tệp tin

Sử dụng lệnh cp . 
Cú pháp:
```
$ cp source_file destination_file
```

- Đổi tên tập tin

Sử dụng lệnh mv . 
```
$ mv old_file new_file
```
- So sánh các tệp tin
Sử dụng lệnh diff

Cú pháp: 
```
$ diff filename1 filename2
```
`diff –c` : so sánh cả ngày giờ

`diff –i` : so sánh theo từng lỗi.
### 3. Các lệnh đọc file

#### 3.1. Cat 
Đọc toàn bộ nội dung file 

Cú pháp: 
```
$ cat filename
```
Bạn có thể hiển thị số dòng bằng cách sử dụng tùy chọn -b 
```
$ cat -b filename
```

Bạn có thể sử dụng lệnh wc để lấy tổng số dòng, từ và ký tự có trong một tệp. Sau đây là một ví dụ đơn giản để xem thông tin về tệp được tạo ở trên -
```
$ wc filename
2  19 103 filename
```

+ **Cột đầu tiên** - Tổng số dòng trong tệp.
+ **Cột thứ hai** - Tổng số từ trong tệp.
+ **Cột thứ ba** - Tổng số byte trong tệp. Đây là kích thước thực tế của tập tin.
+ **Cột thứ tư** - Thể hiện tên tệp.

Vì lệnh `cat` đọc toàn bộ nên nếu flie quá lớn thì phải cuộn lên để 
đọc. Để tiện hơn dùng lệnh more
#### 3.2.	More
Lệnh `more` xem từng đoạn một. 
Nếu muốn đọc các đoạn tiếp theo ấn **Space**

Lệnh More có 1 điểm yếu là không xem lại được đoạn trước đó
#### 3.3. Less

Rất ưu việt. Có thể tùy ý đọc file cần xem. 
Sử dụng mũi tên xuống và lên, **pgdn**, **pgup**. 
Di chuyển đến cuối văn bản gõ **shift+g**. Quay về đầu văn bản gõ **g**. 

Gõ **q** để thoát. 
#### 3.4.	Head 
Hiện ra 10 dòng nội dung dầu tiên.

Muốn hiện n dòng dầu tiên : head –n n /etc/passwd 
Ví dụ: 
```
$ head -n 5 /etc/passwd
```
#### 3.5.	Tail

Hiện phần cuối của file etc
VD : tail /etc/passwd 

