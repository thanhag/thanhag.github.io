---
title: "Hướng dẫn sử dụng FTP trên host"
date: "2016-10-02"
categories: 
  - "wordpress"
tags: 
  - "ftp"
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/Filezilla-1-icon.png
  teaser: /assets/images/Filezilla-1-icon.png
toc: true
breadcrumbs: true
---

**FTP** là một khái niệm rất quan trọng vì trong suốt thời gian bạn sử dụng host để làm website, có thể bạn sẽ cần sử dụng FTP nhiều hơn là dùng control panel của host vì nó sẽ giúp bạn tiện lợi hơn trong việc upload/quản lý các tập tin và thư mục trên host vì sử dụng tính năng File Manager có trong control panel đôi lúc hơi rườm rà và bất tiện, cũng như ở trên đó bạn sẽ không thấy các tập tin hệ thống có tên là .htaccess, nên chúng ta sẽ cần sử dụng FTP để quản lý dữ liệu trên ổ cứng của host.

### FTP là gì?

FTP là chữ viết tắt của **File Transfer Protocol** (Giao thức chuyển nhượng tập tin), đây là một giao thức giúp bạn dễ dàng trao đổi các dữ liệu giữa máy tính của bạn với host và ngược lại. Tại FTP, bạn sẽ có quyền quản lý toàn bộ các dữ liệu dạng tập tin và thư mục có trên host ngoại trừ database. Tất cả các gói host bạn mua có hỗ trợ control panel cPanel, DirectAdmin,…đều hỗ trợ sẵn FTP qua cổng kết nối **21**.

### Cách kết nối vào FTP

Trước khi kết nối vào FTP trên host, mình cần các bạn đã chắc chắn trỏ tên miền về host mặc dù bước này không cần thiết vì bạn có thể kết nối vào cái hostname của host hoặc dịa chỉ IP của host nhưng ở đây mình sẽ chỉ hướng dẫn kết nối vào FTP qua tên miền trên host để tránh dài dòng.

![filezilla-1-icon](/assets/images/Filezilla-1-icon.png)

Để kết nối vào FTP trên host bạn cần phải sử dụng một ứng dụng chuyên làm việc này, nó được gọi là FTP Client. Hiện nay, bạn có thể sử dụng phần mềm [**FileZilla**](https://filezilla-project.org/download.php?type=client "Tải phần mềm FIleZilla") vì đây là FTP Client miễn phí tốt nhất hiện tại, hỗ trợ hầu hết mọi hệ điều hành hiện nay.

Sau khi cài đặt phần mềm FileZilla vào máy, bạn khởi động nó lên sẽ có giao diện như sau:

![filezilla](/assets/images/filezilla_thumb.jpg "filezilla")

Giải thích:

- 1 – Địa chỉ host hoặc IP của host cần truy cập, hãy điền tên miền website của bạn vào.
- 2 – Tên username truy cập vào host
- 3 – Mật khẩu truy cập vào host
- 4 – Cổng kết nối, cổng của giao thức FTP là 21, bạn không cần điền cũng được vì mặc định nó đã là 21

Điền xong các thông tin đó, các bạn ấn vào nút **Quickconnect** để bắt đầu kết nối. Kết nối thành công nó sẽ hiển thị ra như thế này.

![ftp](/assets/images/ftp.png)

Trong đó, bên tay trái là các dữ liệu trên máy tính và bên tay phải là các dữ liệu trên host. Bạn thấy thư mục public\_html chứ, đó là thư mục gốc trên host của bạn đó, nhấp vào đi rồi bạn sẽ thấy các tập tin và thư mục trên host của mình hiện ra.

![filezilla02](/assets/images/filezilla02_thumb.jpg "filezilla02")

Đối với các tập tin, bạn có thể ấn chuột phải và chọn Edit để sửa nội dung, ngoại trừ hình ảnh, chắc chắn rồi.

Nếu bạn muốn upload cái gì đó lên host qua FTP, bạn cứ truy cập vào thư mục cần upload vào trên FTP và di chuyển thư mục ở máy tính đến vị trí của tập tin cần upload, ấn chuột phải và chọn Upload.

![filezilla03](/assets/images/filezilla03_thumb.jpg "filezilla03")

Chờ đợi đến khi nào trên host xuất hiện cái tập tin bạn vừa upload thì thôi.

![filezilla04](/assets/images/filezilla04_thumb.jpg "filezilla04")

Tương tự, bạn có thể ấn chuột phải vào file nào đó trên host và chọn Download để tải về máy tính.

### Tạo tài khoản FTP riêng

FTP có một cái hay là bạn có thể tạo ra nhiều tài khoản FTP riêng và có thể chỉ định tài khoản đó chỉ có thể quản lý một thư mục nào đó trên host, rất có ích nếu bạn muốn cho người khác có quyền upload dữ liệu lên host của bạn mà không sợ người ta đụng chạm tới các dữ liệu khác.

Để làm được việc này, bạn đăng nhập vào control panel của host và tìm đến **FTP Accounts**.

Và mình thiết lập username và mật khẩu FTP cần tạo ra, đồng thời bạn có thể khai báo thư mục được áp dụng cho tài khoản FTP này và dung lượng tối đa tài khoản FTP này được phép sử dụng.

![screenshot-2016-10-02-09-00-05](/assets/images/Screenshot-2016-10-02-09.00.05.png)

Lưu ý là với các tài khoản FTP được chính bạn tạo ra, username của nó sẽ có dạng là username@domain-của-bạn.com nên khi đăng nhập, bạn phải nhập username là như thế. Như ví dụ với ảnh trên, mình tạo ra một tài khoản FTP với username là ftpaccount@sofsog.com và nó được quyền sử dụng thư mục /public\_html/sofsog.com/ftpaccount. Ấn nút Create FTP Account để kết thúc.

Bây giờ bạn có thể đăng nhập vào FTP bằng FileZilla, phần host bạn vẫn để là domain-của-bạn.com, chỉ khác username mà thôi.

### Lời kết

Phần FTP này tạm thời bạn chỉ cần biết như vậy thôi và như thế đã đủ để bạn quản trị website của mình rồi.
