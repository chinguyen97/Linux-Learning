Khi bạn cần tìm kiếm một file bất kỳ trên hệ thống Linux bạn có thể sử dụng các 
lệnh **Which**, ** Whereis**, **find**, hoặc **locate**

## 1. Sử Dụng Lệnh **which**

Lệnh **which** trả về đường dẫn tuyệt đối của file thực thi được gọi. 

Theo mặc định, lệnh which chỉ hiển thị file thực thi đầu tiên phù hợp. 
Để hiển thị tất cả các file thực thi phù hợp, bạn sử dụng thêm tùy chọn -a.

```
which -a passwd
```
Ngoài ra bạn có thể tìm kiếm nhiều file thực thi bằng cách thêm các file cùng một lúc 
```
which passwd firefox
```

Để biết thêm thông tin về lệnh which, nhập `man which` vào cửa sổ **Terminal** rồi nhấn **Enter**.

## 2. Sử Dụng Lệnh **whereis**

Lệnh `whereis` xác định vị trí các file binary file, source code, manual page trong hệ thống linux

Cú pháp : 
```
whereis [options]
```
Ví dụ: `$ whereis -m passwd`
Các tùy chon: 
-b : tìm kiếm binary file
-m: tìm kiếm man page
-s: tìm kiếm source code

Để biết thêm thông tin về lệnh `whereis`, nhập lệnh `man whereis` vào cửa sổ **Terminal** rồi nhấn **Enter**.

## 3. Sử Dụng Lệnh **find**

Lệnh `find` là 1 lệnh tìm kiếm file và thư mục rất hay và phổ biến sử dụng trên linux. 
Người dùng có thể tìm kiếm các file theo tên, chủ tên file, nhóm, phân loại, quyền cho phép, ngày tháng, và các tiêu chí khác.
Lệnh `find` mặc định tìm kiếm trên thư mục hiện tại. 
Muốn tìm thư mục khác phải sử dụng các tùy chọn.
#### a. Tìm kiếm cơ bản 
+ Tìm kiếm theo tên đầy đủ
+ Tìm kiếm theo tên không đầy đủ
VD: 
```
$ find –name file*
```
Kết quả trả ra tất cả các file có lên bắt đầu bằng "file"

Lệnh `find` phân biệt chữ hoa chữ thường. Muốn không có sự phân biết này
thì thêm tùy chọn `–iname`

Muốn tìm ở thư mục nào sử dụng cd chuyển đến thư mục đó. Hoặc sử dụng ‘/’

VD: Bạn đang ở thư mục home muốn tìm file bắt đầu bằng pass
```
$ find –name pass*
```
Ko ra kết quả
```
$ find / -name pass* 
```
Kết quả trả ra tất cả các file trong hệ thống bắng đầu bằng "pass"
+ Tìm kiếm file với phần mở rộng 
```
$ find /etc -name *.conf
```
Kết quả trả ra tất cả các file có phần mở rộng là `.conf` trong `/etc` 
+ Tìm kiếm file ẩn
```
$ find / -type f –name “.*”
```
+ Tìm kiếm file theo owner 
```
$ find –user chichi
```
Kết quả trả ra tất cả các file có chủ sở hữu là chichi
+ Tìm kiếm file theo group 
```
$ find –group chichi
```
+ Tìm file theo phân quyền 
```
$ find –type f –perm 664
```
Kết quả tất xả các file có quyền 664 sẽ được tìm thấy
+ Tìm kiếm file chỉ có quyền đọc
```
$ find / -perm /u=r
```
Tất cả các file có người dùng có quyền đọc sẽ được tìm thấy.
+ Tìm kiếm file rỗng 
```
$ find –type f –empty
```

+ TÌm kiếm file chỉnh sửa trong vòng 50 -100 ngày
```
$ find –mtime +50 –mtime -100
```
+ Tìm file theo dung lượng
```
$ find –size 50M
```
Kết quả trả ra file có dung lượng 50M
```
$ find –size +50M –size -100M
```
Kết quả trả ra các file có dung lượng trong khoảng 50M-100M
+ Tìm kiếm trên nhiều thư mục
```
$ find /opt /usr –name net* -type f
```
Kết quả trả ra tất cá các file có tên mở dầu net trong thư mục /opt và /urs 

#### b. Tìm kiếm nâng cao
+ Tìm và xóa file có dung lượng trên 100M
```
$ find / -size +100M –exec rm –rf {}\;
```
+ Để tìm và xóa tất cả các tệp kết thúc bằng .swp:
```
$ find -name "*.swp" -exec rm {} ’;’
$ find -name "*.swp" -ok rm {} \;
```

+ Tìm và chmod 644 file có phần mở rộng là .txt  
```
$ find -name "*.txt" -type f -exec chmod 644 {} \; 
```
+ Tìm file có phần mở rộng là .mp3 và copy file đó đến thư mục /tmp/MusicFiles
```
$ find . -type f -name "*.mp3" -exec cp {} /tmp/MusicFiles \;
```

+ Tìm file có chứa nội dụng cần tìm kiếm
```
$ find /home -type f -exec grep -l 'linux' {} \;
```
Kết quả trả ra tất cả các file mà nội dung có chứa linux

+ Tìm file theo tên hoặc phần mở rộng hoặc kích thước (-o = OR)
```
$ find / \( -name '*.txt' -o -name 'doc*' -o -size +5M \)
```
Lưu ý rằng bạn phải kết thúc lệnh bằng ‘;’hoặc \;  
2 cách kết thúc hoạt động giống nhau ngoại trừ việc \; tìm kiếm sẽ nhắc 
bạn cho phép trước khi thực hiện lệnh. 

## 4. Sử dụng lệnh **locate**


### Tài liệu tham khảo
https://secure.vinahost.vn/ac/knowledgebase/220/Hng-dn-s-dng-lnh-find-tr-Linux.html


