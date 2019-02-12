## Basic Commands

### 1. **pwd**- print name of current/working directory 
Pwd cho biết bạn đang đứng ở đâu.

### 2. **cd** : đổi vị trí trên file
|Command|Mô tả|
|------|-----|
|cd|Chuyển đến thư mục home|
|Cd ..|Chuyển đến thư mục trước đó.|
|cd../../..|	|
|Cd / or cd ~|Chuyển về / (root)|
|Cd -|Chuyển đến thư mục vừa thoát|

### 3. **ls** : xem trong file có những gì.
|Command|Mô tả|
|-----|----|
|ls|Liệt kê các tệp tin trong thư mục|
|ls –a|Liệt kê cả tệp tin ẩn|
|ls –l or ll|Liệt kê chi tiết|
|Tree|Hiện thị  dạng cây của filesystem|
|Tree -d|Chỉ liệt kê danh sách thư mục , không có các file|


Lệnh `ls` hỗ trợ tùy chọn `-l` sẽ giúp bạn có thêm thông tin về các tệp được liệt kê –: ls –l
 Ví dụ:
```
$ls -l /
total 100
drwxr-xr-x   2 root root 4096 Th01 9 2019 bin
drwxr-xr-x   3 root root 4096 Th01 9 2019 boot
drwxrwxr-x   2 root root 4096 Th01 9 2019 cdrom
.....
```

+ Cột đầu tiên - Thể hiện loại tệp và sự cho phép trên tệp. 
+ Cột thứ hai - Thể hiện số lượng khối bộ nhớ được lấy bởi tệp hoặc thư mục.
+ Cột thứ ba - Chủ sở hữu
+ Cột thứ tư - Nhóm sở hữu
+ Cột thứ năm - Kích thước tệp theo byte.
+ Cột thứ sáu - Thể hiện ngày và thời gian khi tệp này được tạo hoặc sửa đổi lần cuối.
+ Cột thứ bảy - Tên tệp hoặc thư mục

Trong ví dụ liệt kê ls -l , mọi dòng tệp bắt đầu bằng d , - hoặc l . 
Các ký tự này cho biết loại tệp được liệt kê.

|Tiền tố|Mô tả|
|----|-----|
|-|Tệp thông thường, chẳng hạn như tệp văn bản ASCII, tệp nhị phân, hoặc liên kết phần cứng.|
|b|Block Chặn tệp tin đặc biệt. Chặn tập tin thiết bị input/output như ổ cứng vật lý.|
|c|Character Ký tự tập tin đặc biệt. Tập tin input/output thô như ổ cứng cật lý.|
|d|Directory Tập tin thư mục có chứ một danh sách tập tin thư mục khác.|
|l|Symbolic link file. Links on any regular file.|
|p|pipe một cơ chế cho truyền thông liên tiến trình.|
