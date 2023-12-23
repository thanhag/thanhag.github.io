---
title: "Hướng dẫn tạo FTP Server trên Windows 10"
date: "2017-06-04"
categories: 
  - "he-dieu-hanh"
  - "thu-thuat-chung"
  - "window-10"
tags: 
  - "ftp-server-tren-win-10"
  - "he-dieu-hanh"
  - "huong-dan-tao-ftp-server-tren-windows-10"
  - "tao-ftp-server-tren-window"
  - "thu-thuat-chung"
  - "window-10"
header:
  image: /assets/images/FPT-server-windows-10.jpg
  teaser: /assets/images/FPT-server-windows-10.jpg
toc: true
breadcrumbs: true
---

Nếu muốn tạo một đám mây riêng để chia sẻ và chuyển đổi các file có lưu lượng lớn mà không bị giới hạn, bạn có thể tạo một FTP Server (File Transfer Protocol Server) trên máy tính Windows 10 của mình.

![FPT Server](/assets/images/FPT-server-windows-10.jpg "FPT Server")

## 1\. Cài đặt FTP Server trên Windows 10

Tương tự như trên các phiên bản trước, trên Windows 10 cũng được tích hợp các yếu tố cần thiết để chạy FTP Server. Thực hiện các bước dưới đây để cài đặt FTP Server trên máy tính Windows 10 của bạn:

1\. Nhấn tổ hợp phím **Windows + X** để mở Menu Power rồi chọn **Programs and Features (Apps and Features)**

2\. Click chọn liên kết **Turn Windows features on or off**. (Có thể vào ô tìm kiếm và gõ dòng này vào)

![ Turn Windows features on or off](/assets/images/Turn-Windows-features-on-or-off.jpg " Turn Windows features on or off")

3\. Mở rộng Internet Information Services sau đó đánh tích vào tùy chọn **FTP Server**.

4\. Mở rộng FTP Server rồi đánh tích chọn **FTP Extensibility**.

5\. Đánh tích chọn **Web Management Tools** với các tùy chọn mặc định.

6\. Click chọn **OK** để bắt đầu cài đặt.

![chọn OK ](/assets/images/click-ok.jpg "chọn OK ")

7\. Click chọn **Close**.

## 2\. Cấu hình FTP site trên Windows 10

Sau khi đã cài đặt các yếu tố cần thiết để chạy FTP Server trên máy tính Windows 10 của bạn, tiếp theo tiến hành tạo một FTP site:

1\. Nhấn tổ hợp phím **Windows + X** để mở menu Power User rồi chọn **Control Panel.**

2\. Mở **Administrative Tools**.

3\. Kích đúp chuột vào **Internet Information Services (IIS) Manager**.

![Internet Information Services (IIS) Manager](/assets/images/Internet-Information-services-IIS-Manager.jpg "Internet Information Services (IIS) Manager")

4\. Mở rộng bảng Connection rồi kích chuột phải vào **Site.**

5\. Chọn **Add FTP Site**.

![ Add FPT Site](/assets/images/Add-FTP-Site.jpg " Add FPT Site")

6\. Đặt tên cho FTP site mới của bạn rồi nhập đường dẫn đến thư mục FTP mà bạn muốn sử dụng để gửi và nhận các file.

**Lưu ý:**

Bạn có thể sử dụng nút Make New Folder để tạo một thư mục cụ thể chứa file FTP.

7\. Click chọn **Next**.

![chọn Next](/assets/images/chon-next.jpg "chọn Next")

8\. Trên giao diện Binding and SSL Settings, bỏ tất cả các thiết lập mặc định, thay đổi tùy chọn **SSL** thành **No SSL**.

9\. Click chọn **Next.**

**![chọn Next](/assets/images/no-ssl.jpg "chọn Next")**

10\. Tại mục Authentication, đánh tích chọn tùy chọn **Basic.**

11\. Tại mục Authorization chọn **Specified users** từ menu drop-down.

12\. Nhập địa chỉ email tài khoản Windows 10 hoặc tên tài khoản Local cho phép bạn truy cập FTP Server.

13\. Đánh tích chọn tùy chọn **Read** và **Write.**

14\. Click chọn **Finish.**

**![ chọn Finish](/assets/images/finissh.jpg " chọn Finish")**

## 3\. Làm thế nào để cho phép FTP Server thông qua Windows Firewall (tưởng lửa)?

Nếu Windows Firewall (tường lửa) đang hoạt động trên máy tính của bạn, Firewall sẽ chặn bất kỳ một kết nối nào đang cố gắng truy cập FTP Server.

Thực hiện các bước dưới đây để cho phép FTP Server thông qua Firewall (tường lửa):

1\. Mở Start Menu, sau đó nhập Windows Firewall và khung Search rồi nhấn Enter.

2\. Click chọn liên kết **Allow an app or feature through Windows Firewall**.

![Allow an app or feature through Windows Firewall](/assets/images/Allow-an-app-or-feature-through-Windows-Firewall.jpg "Allow an app or feature through Windows Firewall")

3\. Click chọn **Change Settings**.

4\. Chọn **FTP Server** và đánh tích vào cả 2 tùy chọn **Private** và **Public**.

5\. Click chọn **OK.**

**![Change Settings](/assets/images/change-setting.jpg "Change Settings")**

Từ giờ bạn có thể sử dụng FTP client để kết nối với FTP Server mà bạn vừa tạo trên Local Network (mạng nội bộ).

## 4\. Cấu hình Router để cho phép các kết nối bên ngoài như thế nào?

Để máy chủ FTP Sever của bạn có thể kết nối Internet, bạn phải cấu hình Router để mở số cổng 21 trong TCP/IP cho phép kết nối với máy tính của bạn.

1\. Nhấn tổ hợp phím **Windows + X** để mở Menu Power User rồi chọn **Command Prompt.**

2\. Nhập lệnh **ipconfig** vào cửa sổ Command Prompt rồi nhấn Enter.

3\. Note địa chỉ IP Default Gateway lại. Địa chỉ IP Default Gateway chính là địa chỉ Router của bạn.

![địa chỉ IP Default Gateway](/assets/images/Default-Gateway.jpg "địa chỉ IP Default Gateway")

4\. Mở trình duyệt mặc định trên máy tính của bạn.

5\. Trên thanh địa chỉ bạn nhập địa chỉ IP của Router (chính là địa chỉ IP Default Gateway mà bạn note ở trên) rồi nhấn Enter.

6\. Đăng nhập bằng thông tin Router của bạn.

7\. Tìm mục Port Forwarding (thông thường tùy chọn này ở dưới mục thiết lập WAN hoặc NAT).

8\. Tạo một Port Forwarding mới bao gồm các thông tin dưới đây:

**Service name:** Bất kỳ một tên nào mà bạn muốn sử dụng. Chẳng hạn như FPT-Server.

**Port rage:** Sử dụng cổng 21.

**Địa chỉ TCP/IP của máy tính**: Mở Command Prompt sau đó nhập ipconfig vào cửa sổ Command Prompt. Địa chỉ IPv4 là địa chỉ TCP/IP của máy tính.

**Local TCP/IP port:** Sử dụng cổng 21.

**Protocol**: TCP.

![ Port Forwarding ](/assets/images/thiet-lap-port-forwarding.jpg " Port Forwarding ")

9\. Áp dụng thay đổi và lưu lại cấu hình Router mới.

## 5\. Truy cập FTP Server trên bất kỳ một máy tính nào đó

Dưới đây là cách kiểm tra FTP Server nhanh nhất sau khi đã cấu hình Firewall (tường lửa) và Port Forwarding 21 trên Router:

Mở trình duyệt mặc định trên máy tính của bạn sau đó nhập vào thanh địa chỉ trình duyệt địa chỉ IP, định dạng liên kết FTP rồi nhấn Enter.

Địa chỉ IP của bạn chẳng hạn là <FTP://192.168.1.105>.

![Địa chỉ IP](/assets/images/dia-chi.jpg "Địa chỉ IP")

Để kiểm tra FTP Server kết nối Internet, truy cập Google hoặc Bing rồi tìm kiếm **What's my IP?**

Note lại kết quả địa chỉ IP rồi nhập địa chỉ IP đó vào thanh địa chỉ trình duyệt sử dụng định dạng liên kết là FTP rồi nhấn Enter.

## 6\. Làm thế nào để upload file trên FTP Server Windows 10?

1\. Nhấn tổ hợp phím **Windows + E** để mở File Explorer.

2\. Trên thanh địa chỉ, nhập địa chỉ IP Public của bạn cùng định dạng FTP, chẳng hạn như <FTP://172.217.3.14>.

3\. Nhập tên người dùng và mật khẩu.

4\. Đánh tích tùy chọn **Save password.**

5\. Click chọn **Log on.**

**![Log on](/assets/images/log-on.jpg "Log on")**

Ngoài ra bạn có thể kích chuột phải vào **Quick Access** ở khung bên trái rồi chọn **Pin current folder to Quick Access** để dễ dàng kết nối lại FTP server trong những lần tiếp theo.

![Pin current folder to Quick Access](/assets/images/Quick-access.jpg "Pin current folder to Quick Access")

## 7\. Tạo nhiều tài khoản FTP trên Windows 10 như thế nào?

Nếu muốn cho phép nhiều người truy cập FTP Server bạn phải tạo một tài khoản Windows 10 mới cho mỗi người dùng truy cập, liên kết các tài khoản này với thư mục FTP và cấu hình cài đặt phù hợp. Để làm được điều này, bạn thực hiện theo các bước dưới đây:

### Thêm một tài khoản người dùng mới trên Windows 10

1\. Nhấn tổ hợp phím **Windows + I** để mở trình đơn Settings.

2\. Click chọn **Accounts.**

3\. Click chọn **Family & other users.**

4\. Click chọn tiếp **Add someone else to this PC.**

**![Add someone else to this PC](/assets/images/Add-someone-else-to-this-PC.jpg "Add someone else to this PC")**

5\. Click chọn liên kết **I don't have this person's sign-in information.**

**![I don't have this person's sign-in information](/assets/images/I-don-have-this-person-sign-in-information.jpg "I don't have this person's sign-in information")**

6\. Click chọn liên kết **Add a user without a Microsoft account**.

![ Add a user without a Microsoft account](/assets/images/Add-a-user-without-a-Microsoft-account.jpg " Add a user without a Microsoft account")

7\. Nhập thông tin tài khoản người dùng rồi click chọn **Next** để hoàn tất.

![Nhập thông tin tài khoản người dùng ](/assets/images/dien-thongtin-tai-khoan.jpg "Nhập thông tin tài khoản người dùng ")

### Thêm một tài khoản người dùng để truy cập thư mục FPT

1\. Kích chuột phải vào thư mục FPT rồi chọn **Properties**.

2\. Click chọn thẻ **Security.**

3\. Click chọn **Edit.**

**![Edit](/assets/images/edit.jpg "Edit")**

4\. Click chọn **Add.**

**![ Add](/assets/images/add.jpg " Add")**

5\. Nhập tài tên tài khoản người dùng rồi click chọn **Check Name.**

**![Check Name](/assets/images/check-name.jpg "Check Name")**

6\. Click chọn **OK.**

7\. Tại mục Group or user names, chọn tên tài khoản người dùng mà bạn vừa tạo rồi chọn quyền cho phép phù hợp.

![Group or user names](/assets/images/group-or-username.jpg "Group or user names")

8\. Click chọn **Apply**.

9\. Click chọn **OK.**

### Cấu hình tài khoản người dùng mới để truy cập FPT Server

1\. Nhấn tổ hợp phím **Windows + X** để mở Menu Power User rồi chọn **Control Panel.**

2\. Mở Administrative Tools.

3\. Kích đúp chuột chọn **Internet Information Services (IIS) Manager.**

4\. Mở rộng **Sites.**

5\. Chọn **FTP site** sau đó kích đúp chuột vào **Authorization Rules**.

![Authorization Rules](/assets/images/Authorization-Rules.jpg "Authorization Rules")

6\. Kích chuột phải rồi chọn **Add Allow Rules.**

**![Add Allow Rules](/assets/images/Add-Allow-Rules.jpg "Add Allow Rules")**

7\. Chọn **Specified user** rồi nhập tên tài khoản người dùng mới mà bạn vừa tạo.

8\. Thiết lập quyền cho phép **Read** và **Write** nếu bạn muốn cho phép người dùng truy cập.

9\. Click chọn **OK**.

![chọn OK](/assets/images/click-chon-ok.jpg "chọn OK")

Nguồn: Quantrimang.com
