## User Managerment

### 1. User 
User là người có thể truy cập đến hệ thống. User có username và password.Mỗi user còn có một định danh riêng gọi là UID. Định danh của người dùng bình thường sử dụng giá trị bắt đầu từ 500.

Có hai loại user: 
- Super user: root có thể chạy bất cứ lệnh nào trên hệ thống mà không bị hạn chế. Để tạo một người dùng mới, thay đổi thuộc tính của một người dùng cũng như xóa bỏ một người dùng chỉ khi có quyền root.

***Note***: Với phiên bản UbuntuDesktop mặc định tài khoản root sẽ bị vô hiệu hóa cho đến khi được kích hoạt lại. Việc kích hoạt đơn giản là thay đổi passwd root. 

```
sudo -i
passwd root
```

- Regular user: Thường bị giới hạn truy cập vào những file và thư mục có tính chất quan trọng.
 
### 1.1. Tạo user 

Cú pháp: 

`useradd -d homedir -g groupname -m -s shell -u userid accountname`

Các option của lệnh useradd:
- **-c** : Thêm mô tả cho user.
- **-d homedir** : Chỉ định thư mục home cho user.
- **-m** : Tạo thư mục home cho user.
- **-s shell** : Chỉ định shell mặc định cho user.
- **-g groupname**  Xác định một tài khoản nhóm cho tài khoản cá nhân này.
- **-u userid** Bạn có thể xác định ID cá nhân cho tài khoản này.
- **Accountname** Tên tài khoản cá nhân thực sự được tạo ra.

Ví dụ: Tạo username chi

 `useradd -m -c 'NguyenThiChi' chi`

File **/etc/passwd** chứa các tài khoản người dùng. Để kiểm tra đã tạo thành công tài khoản sử dụng lênh: `tail -n1 /etc/passwd`

### 1.2. Đặt pass cho user 
Cú pháp:  `passwd <username>`

Cũng giống như Microsoft Windows bạn vẫn có thể đặt những ràng buộc về mật khẩu cho user. Ví dụ như:
- Bắt buộc sử dụng mật khẩu có độ khó cao.
- Bắt buộc thay đổi mật khẩu sau một khoảng thời gian.
- Số lần cho phép nhập sai mật khẩu.
- Quy định độ dài tối thiểu và độ dài tối đa của mật khẩu.
- vvv

Bằng cách chỉnh sửa các thông số trong file **/etc/login.defs**.

Để xem các quy tắc đã được thiết lập cho một user ta sử dụng lệnh**chage**:

`chage -l chi`

Để thay đổi các thiết lập về mật khẩu cho user chúng ta cũng sử dụng lệnh chage với các option:
- **-m days** : Sets the minimum number of days between password changes. Zero allows the user to change the password at any time.
- **-M days** : Sets the maximum number of days for which a password stays valid.
- **-E date** : Sets a date on which the user account will expire and automatically be deactivated.
- **-W days** : Sets the number of days before the password expires that the user will be warned to change it.
- **-d days** : Sets the number of days since January 1, 1970, that the password was last changed.
- **-I days** : Sets the number of days after password expiration that the account is locked.

Ví dụ: ` chage -M 30 chi`

### 1.3. Xóa user 

` userdel -r <username>`

Tùy chọn -r đẻ gưc bỏ thư mục chính và mail của tài khoản.


- **Kiểm tra user thuộc group nào**
`groups <username>`

- **Khóa/Mở khóa người dùng**

Khóa `passwd -l <username>`

Mở `passwd -u <username>`
- 
- **Kiểm tra trạng thái user**

`passwd --status user`

Mở khóa có cờ: PS. Khóa có cờ LK

- **Kiểm tra uid**

`id`

### 3. Group 

**Group** là tập hợp nhiều **user**. Mỗi Group có 1 GID duy nhất. 

Thông thường khi ta tạo một user thì hệ thống sẽ tự tạo ra một group cùng tên đó và gán user vào group luôn. Nếu muốn tạo một group mới thì chúng ta sử dụng lệnh **groupadd**:

- **Tạo group:**
```
groupadd <groupname>
```
- **Xóa group**
```
groupdel <groupname>
```
- **Xem các user trong group**
```
members <groupname
```
- Thêm user vào group 
	- Để tạo mới một user và thêm nó vào group thì chúng ta sử dụng lệnh **useradd** như sau:

	`useradd -m -c -G group user `

	Ví dụ: `useradd -m -G chinguyen chi`

	- Hoặc để thêm một user đã có sẵn trong hệ thống vào group thì chúng ta sử dụng lệnh **usermod** như sau:

	`usermod -G group user`

	Ví dụ: `usermod -G chinguyen chi`

### 3. File lưu trữ dữ liệu về User và Group

### 3.1. /etc/passwd: 

Giữ tài khoản người dùng và thông tin mật khẩu. File này giữ các thông tin quan trọng về các tài khoản trên hệ thống Unix.

```
tail /etc/passwd
root:x:0:0:root:/root:/bin/bash
deamon:x:1:1:deamon:/usr/sbin:/usr/sbin/nologin
.....
chi:x:1001:1001::/home/chi:
```
Mỗi dòng khai báo 1 người dùng. Với 1 tài khoản thường gồm 7 trường. Dấu **:** phân tách giữa các trường.
- Trường 1: Tên người dùng.
- Trường 2: Mật khẩu đã được mã hóa
- Trường 3: UID
- Trường 4: GID
- Trường 5: Không quan trọng. Mô tả chi tiết về user ( Tên đầy đủ, địa chỉ, SĐT,...)
- Trường 6: Home directory: Phải là đường dẫn đầy đủ tới thư mục sẽ làm thư mục chủ cho user, mặc định đây sẽ là thư mục hiện hành (working direcroty) khi user đăng nhập. Nếu bạn chỉ đến 1 thư mục không tồn tại thì hệ thống sẽ tự gán là thư mục gốc (/) làm thư mục chủ.
- Trường 7: Shell: Đường dẫn đầy đủ tới login shell. Nếu để trống trường này thì login shell mặc định là file /bin/sh, nếu chỉ tới 1 file không tồn tại thì user không thể đăng nhập vào hệ thống từ giao diện console hoặc qua SSH bằng lệnh login. Nhưng user vẫn có thể đăng nhập thông qua giao diện đồ họa bằng cách sử dụng non-login shell.

Tài khoản bin: Cột cuối cùng ghi /sbin/nologin: Túc là người dùng bin ko thể đăng nhập trên hệ thống

UserID là 0 là người dùng có quyền hạn cao nhất trên hệ thống linux.

### 3.2. /etc/group

File /etc/group lưu trữ thông tin group
```
bin:x:1:root,bin
```
Gồm 4 trường. Các trường cách nhau bởi dấu **:**
+ Trường 1: Tên group
+ Trường 2: Mật khẩu shadow được mã hóa
+ Trường 3: Group ID
+ Trường 4: Thành viên group 

### 3.3. /etc/shadow

File /etc/shadow Lưu mật khẩu đã được mã hóa 
+ Trường 1: Tên người dùng
+ Trường 2: Mật khẩu. Dấu **\*** tức là mật khẩu bị chặn, vẫn có thể kết nối bằng các phương pháp khác. Dấu **!** Tài khoản bị khóa tạm thời. Rỗng, nghĩa là không đặt mật khẩu.
+ Trường 3: Thời gian từ ngày 1/1/1970 tới lần thay đổi mật khẩu gần nhất (tính bằng ngày).
+ Trường 4: Thời gian tối đa để thay đôi mật khẩu. 0 là thay đổi bất kỳ lúc nào ( tính bằng ngày )
+ Trường 5: Thời gian mật khẩu còn thời hạn ( tính bằng ngày ).
+ Trường 6: Thời gian cảnh báo mật khẩu sắp hết hạn ( tính bằng ngày)
+ Trường 7: Thời gian mà mật khẩu người dùng hết hạn (tính bằng ngày )
+ Trường 8: Thời gian mà người dùng bị vô hiêu hóa, tính từ ngày 1/1/1970 ( tính bằng ngày ).

### 3.4. /etc/gshadow

/etc/gshadow: File này giữ các thông tin tài khoản nhóm bảo mật.

#### Tài liệu tham khảo: https://help.ubuntu.com/lts/serverguide/user-management.html.en
