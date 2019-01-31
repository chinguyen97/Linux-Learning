## Security Linux

Root có quyền cao nhất trong hệ thống linux, có khả năng thực hiện tất 
cả các công việc quản trị hệ thống như thêm tài khoản, thay đổi mật khẩu,
 cài đặt phần mềm,...
 
####Lệnh `su`

+Chuyển đến tài khoản người dùng root đến người dùng root đại diện cho quyền 
hạn cao nhất của người dùng (root user) và yêu cầu mật khẩu root.

Nhấn `exit` để thoát khỏi root 

`Su` còn đc dùng khi chuyển sang tài khoản của người dùng khác 

Ví dụ Đang ở người dùng root muốn chuyển sang user chichi sử dụng lệnh `su chichi`.

####Lệnh `sudo` 
Cấu trúc : `Sudo command`
`Sudo` nâng cao đặc quyền của người dùng cá nhân. Khi bạn thực thi lệnh sudo, 
hệ thống sẽ nhắc bạn nhập mật khẩu của tài khoản người dùng hiện tại trước 
khi chạy lệnh với tư cách là người dùng root. 

Lệnh `Sudo passwd` để kích hoạt tài khoản người dùng root và tạo mật khẩu cho nó.

** Tóm lại: **

`Su` chuyển đến người dùng root, bắt buộc người dùng chia sẻ root pasword với người dùng khác. Nên bảo mật kém.

`Sudo` cho phép người dùng sử dụng tài khoản của họ để chạy câu lệnh hệ thống. Yêu cầu tài khoản người dùng hiện tại. 
Thường được sử dụng hơn.

Lệnh `sudo su` Thay vì yêu cầu hệ thống chuyển tới người dùng root hệ thống yêu cầu thực hiện lệnh su 

####Lệnh `chage`

Để thay đổi các thiết lập về mật khẩu cho user chúng ta cũng sử dụng lệnh **chage** với các **option**:
•	-m days : Đặt số ngày tối thiểu giữa các thay đổi mật khẩu. 
Zero cho phép người dùng thay đổi mật khẩu bất cứ lúc nào.
•	-M days : Đặt số ngày tối đa mà mật khẩu vẫn hợp lệ.
•	-E date : Đặt ngày mà tài khoản người dùng sẽ hết hạn và tự động bị hủy kích hoạt
•	-W days : Đặt số ngày trước khi mật khẩu hết hạn mà người dùng sẽ được cảnh báo thay đổi mật khẩu.
•	-I days : Đặt số ngày sau khi hết hạn mật khẩu mà tài khoản bị khóa.