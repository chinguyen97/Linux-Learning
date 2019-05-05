## Logical Volume Manager 

### 1. Giới thiệu về Logical Volume Manager (LVM)
#### 1.1. LVM là gì?
**Logical Volume Manager**: Gom nhiều đĩa cứng vật lý thành 1 đĩa ảo lớn hơn trên đấy tạo ra các vùng lưu trữ để sử dụng.
#### 1.2 Vai trò của LVM

LVM là kỹ thuật quản lý việc thay đổi kích thước lưu trữ của ổ cứng
+ Không để hệ thống bị gián đoạn hoạt động
+ Không làm hỏng dịch vụ
+ Có thể kết hợp Hot Swapping (thao tác thay thế nóng các thành phần bên trong máy tính)

**Ưu điểm.**
+ Có thể tạo ra các vùng dung lượng lớn nhỏ tuỳ ý.
+ Có thể thay đổi các vùng dung lượng đó dễ dàng, linh hoạt mà không cần thay đổi dung lượng các partition.

**Nhược điểm.**
+ Các bước thiết lập phức tạp, khó khăn hơn.
+ Càng gắn nhiều đĩa cứng và thiết lập càng nhiều LVM thì hệ thống khởi động càng lâu.
+ Khả năng mất dữ liệu khi một trong số các đĩa cứng vật lý bị hỏng.
+ Windows không thể nhận ra vùng dữ liệu của LVM. Nếu bạn Dual-boot Windows sẽ không thể truy cập dữ liệu chứa trong LVM.

### 1.3 Các thành phần trong LVM
![lvm1](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM1.png)

+ **Hard drives – Drives**

Thiết bị lưu trữ dữ liệu, ví dụ: `/dev/sda`

+ **Partition**

Partitions là các phân vùng của Hard drives, gồm 2 loại là **primary partition** và **extended partition**
++ **Primary partition**: Phân vùng chính, có thể khởi động; Mỗi đĩa cứng có thể có tối đa 4 phân vùng này
++ Extended partition: Phân vùng mở rộng, có thể tạo những vùng luân lý

+ **Physical Volumes**

Là một cách gọi khác của partition trong kỹ thuật LVM, nó là những thành phần cơ bản được sử dụng bởi LVM. 

Một Physical Volume không thể mở rộng ra ngoài phạm vi một ổ đĩa.

+ **Volume Group**

Nhiều Physical Volume kết hợp thành Volume Groups.
Trong đó người dùng có thể tạo, thay đổi kích thước, lưu trữ, gỡ bỏ và sử dụng.
+ **Logical Volume**

Volume Group được chia nhỏ thành nhiều Logical Volume, 
mỗi Logical Volume có ý nghĩa tương tự như partition. 
Nó được dùng cho các mount point và được format với những định dạng khác nhau như ext2, ext3, ext4,…

Khi dung lượng của Logical Volume được sử dụng hết ta có thể đưa thêm ổ đĩa mới bổ sung cho Volume Group và do đó tăng được dung lượng của Logical Volume

### 2. Hướng dẫn sử dụng LVM
#### 2.1 Chuẩn bị

+ Add thêm một số ổ cứng vào máy ảo
#### 2.2 Tạo Logical Volume trên LVM
+ B1: Kiểm tra các Hard Drives có trên hệ thống

Sử dụng câu lệnh `lsblk`

![LVM2](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM2.png)

Trong đó sdb, sdc các Hard Drives mà mình mới thêm vào
+ B2. Tạo Partition

Từ các Hard Drives trên hệ thống, bạn tạo các partition. 

Ví dụ ở đây, từ sdb, mình tạo các partition bằng cách sử dụng lệnh sau `fdisk /dev/sdb`

![LVM3](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM3.png)

	+ Bạn chọn **n** để bắt đầu tạo partition
	+ Bạn chọn **p** để tạo partition primary
	+ Bạn chọn **1** để tạo partition primary 1
	+ Tại **First sector** (2048-20971519, default 2048) bạn để mặc định
	+ Tại Last sector, +sectors or +size{K,M,G} (2048-20971519, default 20971519) bạn chọn +1G để partition bạn tạo ra có dung lượng 1 G
	+ Bạn chọn **w** để lưu lại và thoát.
 
Tiếp theo bạn thay đổi định dạng của partition vừa mới tạo thành LVM

![LVM4](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM4.png)

	+ Bạn chọn **t** để thay đổi định dạng partition
	+ Bạn chọn **8e** để đổi thành LVM
 
Tương tự, bạn tạo thêm các partition primary từ sdb

![VL5](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM5.png)

Tạo các partition primary từ `sdc` bằng lệnh `fdisk /dev/sdc`

+ B3. Tạo Physical Volume

Tạo các Physical Volume là `/dev/sdb1` và `/dev/sdc1` bằng các lệnh sau:
```
$ pvcreate /dev/sdb1
```
```
# pvcreate /dev/sdc1
```
Kiểm tra các Physical Volume bằng câu lệnh **pvs** hoặc có thể sử dụng lệnh **pvdisplay**

![VL6](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM6.png)

+ B4. Tạo Volume Group

Tiếp theo, nhóm các Physical Volume thành 1 Volume Group bằng cách sử dụng câu lệnh sau:
```
$ vgcreate vg-demo1 /dev/sdb1 /dev/sdc1
```

![VL7](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM7.png)

Trong đó **vg-demo1** là tên của Volume Group
Có thể sử dụng câu lệnh sau để kiểm tra lại các Volume Group đã tạo
```
$ vgs
```
```
$ vgdisplay
```
![LVM8](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM8.png)

+ B5. Tạo Logical Volume

Từ một Volume Group, Có thể tạo ra các Logical Volume bằng cách sử dụng lệnh sau:
```
$ lvcreate -L 1G -n lv-demo1 vg-demo1
```
	+ **-L**: Chỉ ra dung lượng của logical volume
	+ **-n**: Chỉ ra tên của logical volume
	+ **lv-demo1** là tên Logical Volume
	+ **vg-demo1** là Volume Group mà mình vừa tạo ở bước trước

Lưu ý: Có thể tạo nhiều Logical Volume từ 1 Volume Group

Để kiểm tra lại các Logical Volume đã tạo
```
$ lvs
```
Hoặc
```
$ lvdisplay
```
![LVM9](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM9.png)

+ B6. Định dạng Logical Volume

Để format các Logical Volume thành các định dạng như ext2, ext3, ext4, ta có thể làm như sau:
```
# mkfs -t ext4 /dev/vg-demo1/lv-demo1
```
![LVM10](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM10.png)

+ B7. Mount và sử dụng
Trong bài lab này, mình sẽ tạo ra một thư mục để mount Logical Volume đã tạo vào thư mục đó
```
# mkdir demo1
```
![LVM11](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM11.png)

Tiến hành mount logical volume lv-demo1 vào thư mục demo1 như sau:
```
# mount /dev/vg-demo1/lv-demo1 demo1
```

![LVM12](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM12.png)

Kiểm tra lại dung lượng của thư mục đã được mount:
```
df -h
```
![LVM13](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM13.png)

#### 2.3 Thay đổi dung lượng Logical Volume trên LVM

Ở phần này, chúng ta sẽ tìm hiểu làm thế nào để có thể thay đổi dung lượng của 
1 Logical Volume đã được tạo ở phần trước.
Trước khi thay đổi dung lượng, cần phải kiểm tra các thông tin hiện có:
`$ vgs`

`$ lvs`

`$ pvs`

![LVM14](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM14.png)

Ở đây, mình đã tạo được Logical Volume là `lv-demo1`, 
và giả sử Logical Volume này dung lượng đã đầy và chúng ta cần tăng kích thước của nó.
Logical Volume này thuộc Volume Group `vg-demo1`, 
để tăng kích thước, bước đầu tiên phải kiểm tra xem Volume Group 
còn dư dung lượng để kéo giãn Logical Volume không. 
Logical Volume thuộc 1 Volume Group nhất định, Volume Group đã cấp 
phát hết thì Logical Volume cũng không thể tăng dung lượng được. 

Để kiểm tra, ta dùng lệnh sau: `vgdisplay`

![LVM15](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM15.png)

Volume Group ở đây vẫn còn dung lượng để cấp phát, ta có thể nhận thấy điều này qua 2 trường thông tin là VG Status resizable và Free PE / Size 510 / 1.99 GiB với dung lượng Free là 510x4 = 2040 Mb

Để tăng kích thước Logical Volume ta sử dụng câu lệnh sau:

```
$ lvextend -L +50M /dev/vg-demo1/lv-demo1
```

Với -L là tùy chọn để tăng kích thước

![LVM16](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM16.png)

Kiểm tra lại bằng cách dùng lệnh: `$ lvs`

![LVM17](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM17.png)

Sau khi tăng kích thước cho Logical Volume thì Logical Volume đã được 
tăng nhưng file system trên volume này vẫn chưa thay đổi, 
bạn phải sử dụng lệnh sau để thay đổi:

```
$ resize2fs /dev/vg-demo1/lv-demo1
```
![LVM18](https://github.com/chinguyen97/Linux-Learning/blob/master/images/LVM18.png)

Để giảm kích thước của Logical Volume, trước hết các bạn phải 
umount Logical Volume mà mình muốn giảm
```
$ umount /dev/vg-demo1/lv-demo1
```
Tiến hành giảm kích thước của Logical Volume
```
$ lvreduce -L 20M /dev/vg-demo1/lv-demo1
```
Sau đó tiến hành format lại Logical Volume
```
$ mkfs.ext4 /dev/vg-demo1/lv-demo1
```
Cuối cùng là mount lại Logical Volume
```
$ mount /dev/vg-demo1/lv-demo1 demo1
```
Kiểm tra kết quả ta được như sau: `$ df -h`

#### 2.4 Thay đổi dung lượng Volume Group

Trước tiên, các bạn cần kiểm tra lại các partition và Volume Group

`$ vgs`

`$ lsblk`

Tiếp theo, nhóm thêm 1 partition vào Volume Group như sau:

```
$ vgextend /dev/vg-demo1 /dev/sdb3
```
Ở đây, muốn nhóm vào Volume Group phải là Physical Volume nên hệ thống đã tự động tạo cho mình Physical Volume và nhóm vào Volume Group.
Chúng ta có thể cắt 1 Physical Volume ra khỏi Volume Group như sau:
```
$ vgreduce /dev/vg-demo1 /dev/sdb3
```

#### 2.5 Xóa Logical Volume, Volume Group, Physical Volume

+ Xóa Logical Volumes

Trước tiên ta phải Umount Logical Volume
```
$ umount /dev/vg-demo1/lv-demo1
```
Sau đó tiến hành xóa Logical Volume bằng câu lệnh sau:
```
$ lvremove /dev/vg-demo1/lv-demo1
```
Ta kiểm tra lại kết quả: `lvs`

+ Xóa Volume Group

Trước khi xóa Volume Group, phải xóa Logical Volume.

Xóa Volume Group bằng cách sử dụng lệnh sau:
```
$ vgremove /dev/vg-demo1
```
+ Xóa Physical Volume
```
$ pvremove /dev/sdb3
```

**Tài liệu tham khảo:**

[1] https://bachkhoa-aptech.edu.vn/gioi-thieu-ve-logical-volume-manager.html

[2] https://www.tecmint.com/extend-and-reduce-lvms-in-linux/

