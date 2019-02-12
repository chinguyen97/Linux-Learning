## Compress the data
Dữ liệu thường được nén để tiết kiệm dung lượng ổ đĩa và giảm thời gian truyền tệp qua mạng. 

Linux sử dụng một số phương pháp để thực hiện việc nén như **gzip**, 
**bzip2**, **xz**, **zip**.
Những kỹ thuật này khác nhau về hiệu quả của việc nén (tiết kiệm được 
bao nhiêu dung lượng) và thời gian để nén; nói chung các kỹ thuật hiệu 
quả hơn mất nhiều thời gian hơn. 
Thời gian giải nén không thay đổi nhiều theo các phương pháp khác nhau.

Bài viết này mình đề cập đến 2 phương pháp gzip và zip
### 1.	Gzip 
GZIP chỉ có thể làm việc trên 1 tập tin hoặc 1 dòng dữ liệu. 
Do đó nó không thể lưu trữ được nhiều tập tin.
+ Cú pháp nén 1 tệp tin 
```
$ gzip filename
```
+ Giải nén: 
```
$ gzip –d filename.gz
```
Hoặc 
```
$ gumzip filname.gz
```

+ Tùy chọn -l Liệt kê thuộc tính file nén
```
$ gzip –l filename.gz
```
+ Thiết lập mức độ nén
```
$gzip –-fast filename
```
Hoặc 
```
$gzip --best filename
```
+ Tỉ lệ nén

1: Thấp nhất – nhưng nhanh nhất

9: Cao nhất – nhưng chậm nhất

Chúng ta có thể sử dụng tỉ lệ nén trong khoảng cho phép trên.
``` 
$gzip -5 filename
```
### 2. ZIP – UNZIP
Cú pháp: 
```
$ zip –[option] filename.zip filename
```
ZIP được dùng như 1 định dạng phổ biến nhất trên Internet. 
Nó thực hiện cả việc lưu trữ và nén dữ liệu.

Tùy chọn:
**r**: Sử dụng đệ quy – Dùng trong trường hợp nén nhiều file hay folder.

**9**: Mức độ nén cao nhất.

**d**: Xóa dữ liệu đã có trong file nén.

**l**: Liệt kê tập tin đang có bên trong file zip.

**u**: Cập nhật file đã có trong file zip.

+ Nén 1 file
```
$ zip filename.zip file1
```
+ Nén nhiều file, hoặc folder
```
$ zip –r filename.zip file1 file2 folder1 folder2
```
Thêm tùy chon “-9” để nén với mức cao nhất
+ Giải nén tập tin zip
```
$unzip filename.zip
```

