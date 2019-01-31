## Text Command 
### 1.	Hiển thị nội dung 
-	`Cat` Hiển thị nội dung file
-	`Tac`  Hiển thị theo thứ tự ngược lại
-	`Echo` 

### 2.	Edit Content 
-	Sed 
-	Awk: Awk thường được sử dụng cho việc tìm kiếm và xử lý text. 
nó xem 1 file text giống như bảng dữ liệu, bao gồm các bản ghi và các trường. Nó sẽ tìm kiếm một hoặc nhiều file để xem xem trong các file đó có dòng nào bao gồm những pattern (khuôn mẫu) cho trước hay không, sau đó thực hiện những action (hành động) tương ứng.

Cú pháp cơ bản của câu lệnh được viết với Awk sẽ như sau:
```
awk '/search pattern 1/ {Actions}
        /search pattern 2/ {Actions}' file
```
Giải thích:	
•	search pattern là một biểu thức chính quy
•	Actions là những câu lệnh sẽ được thực hiện
•	file: file đầu vào Awk 

Theo mặc định, chương trình được viết với Awk sẽ in ra từng dòng của file đầu vào:
```
$ awk '{print}' name
1 Hoang Anh 6.7
2 Hoang Hanh 8.9
3 Ngoc Linh 7.8
4 Van Hoa 5.2
```
Trong ví dụ này, không có sự xuất hiện của phần pattern, do đó lệnh print được áp dụng cho toàn bộ các dòng.

In ra những dòng có chứa xâu mẫu
```
$ awk '/Hoang /’ name
1 Hoang Anh 6.7
2 Hoang Hanh 8.9
```

Theo mặc định awk chia bản ghi này ra thành từng trường ngăn cách nhau bởi 
các khoảng trắng và lưu trong các biến có dạng $n. Nếu một dòng có 4 từ, 
các từ ấy sẽ được lưu trong các biến $1, $2, $3 và $4. $0 đại diện cho 
toàn bộ dòng. NF là biến dựng sẵn lưu giữ giá trị tổng số trường của một 
bản ghi.
```
$ awk '{print $3, $4;}' name 
Anh 6.7
Hanh 8.9
Linh 7.8
Hoa 5.2
```

```
~ awk '{print $3, $NF;}' name
Anh 6.7
Hanh 8.9
Linh 7.8
Hoa 5.2
```
**Phép so sánh**
```
$awk '$4 > 7.5' name 
2 Hoang Hanh 8.9
3 Ngoc Linh 7.8
```
**Cú pháp điều kiện**

Giả sử chúng ta muốn in ra danh sách những sinh viên họ Hoàng
 
```
awk '$2 ~ /Hoang/' name 
1 Hoang Anh 6.7
2 Hoang Hanh 8.9
```

Toán tử ~ (thuật ngữ tiếng Anh tương ứng là tilde) được dùng để so sánh 
giá trị của một trường với một biểu thức chính quy. Nếu kết quả là khớp, 
dòng dữ liệu đó sẽ được in ra màn hình.

**Tính toán số học**

Chương trình dưới đây thực hiện đếm số sinh viên họ Hoang nếu có thì giá trị của biến count được tăng lên 1 đơn vị. Biến này được khởi tạo giá trị ban đầu bằng 0 với từ khóa BEGIN.
```
$ awk 'BEGIN {count = 0;}
> $2 ~ /Hoang/ {count++;}
> END {print "Ketqua =", count;}' name
Ketqua =2
```

Kết thúc chương trình, giá trị của biến count được in ra chính là số 
sinh viên họ Hoang
### 3.	Các thao tác với file

Lệnh `sort` : sắp xếp tệp tin theo thứ tự tăng dần
```
$ cat file1
Toan 9.2
Lý 7.8
Van 6.7
Hoa 7.8
Anh 8.5
```
```
$ cat file1 | sort 
Anh 8.5
Hoa 7.8
Ly 7.8
Toan 9.2
Van 6.7
```
Lệnh `sort –r` : sắp xếp theo thứ tự giảm dần
```
$ cat file1 | sort –r 
Van 6.7
Toan 9.2
Ly 7.8
Hoa 7.8
Anh 8.5
```
Lệnh `uniq` được sử dụng để loại bỏ trùng lặp trong một tập tin văn bản. 
Nó yêu cầu các mục trùng lặp được loại bỏ là liên tiếp.
```
$ cat file1 
Anh 8.5
Hoa 7.8
Ly 7.8
Toan 9.2
Van 6.7
Hoa 7.8
```
```
$ sort file1 | uniq
Anh 8.5
Hoa 7.8
Ly 7.8
Toan 9.2
Van 6.7
```
```
$ sort file1 | uniq -c
1 Anh 8.5
2 Hoa 7.8
1 Ly 7.8
1 Toan 9.2
1 Van 6.7
```
Lệnh `paste` được sử dụng để kết hợp các trường từ các tập tin khác nhau
```
$ cat name
1 Nga
2 Linh
3 Phuong
```
```
$cat age
34
46
29
```
```
$paste name age
1 Nga 34
2 Linh 46
3 Phuong 29
```

Lệnh `join` kết hợp hai tập tin trên cùng 1 trường
```
$ cat name
1 Nga
2 Linh
3 Phuong
```
```
$cat age
1 34
2 46
3 29
```
```
$ join name age
1 Nga 34
2 Linh 46
3 Phuong 29
```

 `Grep` Tìm kiếm trong văn bản
 
```
$ cat name
1 Hoang Anh
2 Hoang Hanh
3 Ngoc Linh
4 Van Hoa
```
```
$ grep Hoa* names
1 Hoang Anh
2 Hoang Hanh
4 Van Hoa
```
Các tr tiện ích được sử dụng để chuyển đổi ký tự chỉ định sang ký tự khác 
```
$ cat name
1 Hoang Anh
2 Hoang Hanh
3 Ngoc Linh
4 Van Hoa
```
```
$ cat name | tr a-z A-Z
1 HOANG ANH
2 HOANG HANH
3 NGOC LINH
4 VAN HOA
```
Các wc(word count) đếm số dòng, ký tự, và từ trong một tập tin hoặc danh sách các tập tin.
```
$cat name
1 Hoang Anh
2 Hoang Hanh
3 Ngoc Linh
4 Van Hoa
```
```
 $wc -l name
4 name
$wc -c name
47 name
$wc -w name
12 name
``

Lệnh `cut`  được sử dụng để thao tác với file cột dựa trên và được thiết kế 
để trích xuất các cột cụ thể. Dấu phân cách cột mặc định là ký tự tab. 
Một dấu phân cách khác nhau có thể được cung cấp dưới dạng tùy chọn lệnh.
```
$ cut -d" " -f1 name
1
2
3
4
```
```
$ cut -d" " -f2 name
Hoang
Hoang
Ngoc
Van
```

```
$ cut -d" " -f3 names.txt
Anh 
Hanh
Linh
Hoa
```