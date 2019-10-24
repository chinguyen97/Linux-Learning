## Security Linux

Root có quyền cao nhất trong hệ thống linux, có khả năng thực hiện tất 
cả các công việc quản trị hệ thống như thêm tài khoản, thay đổi mật khẩu,
 cài đặt phần mềm,...
 
### 1. Lệnh `su`

Chuyển đến tài khoản đến người dùng root đại diện cho quyền hạn cao nhất của người dùng (root user) và yêu cầu mật khẩu root.

Nhấn `exit` để thoát khỏi root 

`Su` còn đc dùng khi chuyển sang tài khoản của người dùng khác 

Ví dụ Đang ở người dùng root muốn chuyển sang user chichi sử dụng lệnh `su chichi`.

### 2. Lệnh `sudo` 

Cấu trúc : `Sudo command`

`Sudo` nâng cao đặc quyền của người dùng cá nhân. Khi bạn thực thi lệnh sudo, hệ thống sẽ nhắc bạn nhập mật khẩu của tài khoản người dùng hiện tại trước khi chạy lệnh với tư cách là người dùng root. 

Lệnh `Sudo passwd` để kích hoạt tài khoản người dùng root và tạo mật khẩu cho nó.

**Tóm lại:**

`Su` chuyển đến người dùng root, bắt buộc người dùng chia sẻ root pasword với người dùng khác. Nên bảo mật kém.

`Sudo` cho phép người dùng sử dụng tài khoản của họ để chạy câu lệnh hệ thống. Yêu cầu tài khoản người dùng hiện tại. 
Thường được sử dụng hơn.

Lệnh `sudo su` Thay vì yêu cầu hệ thống chuyển tới người dùng root hệ thống yêu cầu thực hiện lệnh su 


### 3. Thêm quyền cho user và sử dụng sudo

Sudo _ Superuser Do: Hiểu là tạm cho 1 phép 1 user thực thi lệnh trên linux với quyền 1 user root.

Đối với user gõ lệnh sudo, thì họ sẽ được hỏi mật khẩu của chính họ để xác nhận gửi yêu cầu thay vì sử dụng lệnh su để chuyển sang tài khoản root và nhập mật khẩu của root.

Nguyên tắc làm việc của sudo nói ngắn gọn như sau: nếu user gõ lệnh có sudo ở đằng trước thì yêu cầu này sẽ được hệ thống sẽ kiểm tra xem user đang gửi yêu cầu có trong danh sách sudoers hay không, nếu có thì sẽ cho phép thực thi, ngược lại sẽ lưu lại log (reported) và thông báo như bên dưới

```
[user@centos7 etc]$ sudo vi sudoers
[sudo] password for user: 
user is not in the sudoers file.  This incident will be reported.
```
Do người dùng user chưa được cấp phép sử dụng lệnh `sudo`. 
Bạn cần phải cấp quyền sudo cho user này bằng các có thể thêm user vào group mà group đó được phép sử dụng lệnh sudo hoặc trực tiếp chỉnh sửa file `/etc/sudoers` bằng cách thêm đoạn này vào dưới cùng rồi lưu lại:

[tên user] ALL=(ALL) ALL

Bây giờ có thể đăng nhập tài user và sử dụng sudo để cahyj lệnh với quyền root. 

### 4. Lệnh `chage`

Để thay đổi các thiết lập về mật khẩu cho user chúng ta cũng sử dụng lệnh **chage** với các **option**:
+ -m days : Đặt số ngày tối thiểu giữa các thay đổi mật khẩu. 
Zero cho phép người dùng thay đổi mật khẩu bất cứ lúc nào.
+ -M days : Đặt số ngày tối đa mà mật khẩu vẫn hợp lệ.
+ -E date : Đặt ngày mà tài khoản người dùng sẽ hết hạn và tự động bị hủy kích hoạt
+ -W days : Đặt số ngày trước khi mật khẩu hết hạn mà người dùng sẽ được cảnh báo thay đổi mật khẩu.
+ -I days : Đặt số ngày sau khi hết hạn mật khẩu mà tài khoản bị khóa.

**Tài liệu tham khảo:** https://bigvn.net/quan-ly-user-va-sudo-trong-centos/