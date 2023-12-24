---
published: True
title: Hướng dẫn tạo VPS trên VULTR chi tiết nhất
date: 2023-12-23
toc: true #Thêm mục lục tự động
breadcrumbs: true  # disabled by default
# https://sofsog.com/thu-thuat-chung/he-dieu-hanh/ubuntu/huong-dan-tao-vps-tren-vultr-chi-tiet-nhat
permalink: /thu-thuat-chung/he-dieu-hanh/ubuntu/huong-dan-tao-vps-tren-vultr-chi-tiet-nhat
categories: 
  - "ubuntu"
tags: 
  - "ubuntu"
  - "vps"
  - "vultr"
header:
  image: /assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất.jpg
  teaser: /assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất.jpg

---

Chất lượng VPS trên Vultr thì khỏi phải bàn. Trang _**sofsog.com**_ của mình đang được host trên VPS của Vultr hown 5 năm nay. Trong hướng dẫn này chúng ta sẽ từng bước tạo 1 _**VPS trên Vultr**_ chạy hệ điều hành **Ubuntu-22.04-LTS.**

## Bước 1: Tạo tài khoản trên Vultr

Vào trang chủ của Vultr bằng link [https://www.vultr.com/?ref=7392243](https://www.vultr.com/?ref=7392243) - Đây là link ref của mình, các bạn vào bằng link này sẽ nhận được 100$ miễn phí để thử tất cả các chức năng của nền tảng Vultr (Lưu ý: Khách hàng được giới thiệu phải liên kết thẻ tín dụng hợp lệ hoặc phương thức Paypal để đủ điều kiện nhận khoản tín dụng 100 USD. Phần tín dụng 100 USD chưa sử dụng sẽ hết hạn sau 14 ngày).

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com-1](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất.jpg) Gõ email và password vào các ô tương ứng rồi bấm vào nút "**Create account**"

![](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-2.jpg) Bấm vào nút "**Add a Payment Method**" để liên kết thẻ tín dụng, ở đây mình liên kết bằng thẻ VISA (thẻ phải kích hoạt thanh toán qua internet nhé)

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-03.jpg)

Điền đầy đủ thông tin của bạn, lưu ý địa chỉ nhớ trùng khớp với ngân hàng nhé. Nhớ chọn **"I just want to link my credit card - $0.00 deposit"**. Vultr sẽ trừ 0$ chỉ để kiểm tra thẻ của bạn. Điền đầy đủ, kiểm tra chính xác thì bấm nút **"Pay with Credit Card".**

Sau khi liên kết thanh toán thành công, bạn tiếp tục bấm vào nút **"Update info"** để cập nhật thêm các thông tin chi tiết của bạn, phần này dễ mình bỏ qua nhé.

## Bước 2: Tạo VPS đầu tiên trên Vultr

Bấm vào nút **"Configure Instance"** (Hoặc tìm những nút gì liên quan **Instance** tương tự), sau dó chọn **Cloud Compute** như hình

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-04.jpg)

Chọn "CPU & Storage Technology", ở đây mình chọn **"Intel Regular Performance"** vì giá nó rẻ hơn mấy cái kia.

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com-04](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-07.jpg)

Lăn chuột xuống dưới để chọn Server Location. Nếu muốn kết nối nhanh từ Việt Nam thì mình khuyên nên chọn **Singapore** hoặc **Tokyo, Osaka**. Mình sẽ chọn **Singapore**.

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-05.jpg)

Lăn chuột xuống để chọn Server Image, tức là chọn hình ảnh của hệ điều hành trên server, mình chọn **Ubunu-22.04 LTS x64**.

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-06.jpg)

Tiếp tục xuống dưới để chọn Server size, tùy nhu cầu các bạn chọn, ở đây mình chọn loại rẻ nhất đang có **5$/tháng**.

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-08.jpg)

Kéo xuống dưới, chỗ **"Add Auto Backups"**, đây là tính năng tự động sao lưu của Vultr, nhưng tốn phí 1$/tháng, nếu hệ thống của bạn quan trọng thì cứ giữ nguyên, còn mình thì không cần, mình bỏ chọn nó như hình dưới đây

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-09.jpg) ![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-10.jpg)

Xong, còn các thứ khác mình để mặc định. Cuối cùng, bấm nút **"Deploy Now",** chờ một lúc để Vultr làm nhiệm vụ của mình. Quá trình tạo VPS trên Vultr sẽ mất khoảng 1 đến 2 phút. Sau đó bạn sẽ nhận được một email thông báo thành công từ Vultr kèm **thông tin IP** và cấu hình VPS. **Mật khẩu Root** ở trong trang Server information ở phần Password (bạn có thể click vào biểu tượng con mắt để nhìn mật khẩu).

## Bước 3: Cài đặt cơ bản trên VPS vừa tạo

Vào **Products > Compute**, click chọn vào VPS vừa tạo.

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-12.png)

Trong trang khu vực quản lý VPS của mình trên Vultr, bấm vào cái **nút hình máy vi tính góc phải, phía trên** để vào **noVNC** điều khiển VPS

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-11.jpg)

Bạn sẽ thấy dòng chữ "**vultr login:**" gõ vào tài khoản gốc mặc định **"root"**, sau đó bạn sẽ được hỏi **password**, có thể gõ trực tiếp hoặc copy và dán vào như hình bên dưới

![Hướng dẫn tạo VPS trên VULTR chi tiết nhất -sofsog.com](/assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất-sofsog.com-13.jpg)

### 1\. Thêm user

Sau khi kết nối VPS thành công, bạn cần tạo một user để làm việc hằng ngày, vì user **"root"** này rất quan trọng, không nên dùng nó thường xuyên. Ví dụ mình tạo 1 user "**sofsog**" và cài đặt quyền quản trị cho user này luôn bằng lệnh dưới (nhớ thay đổi sofsog bằng tên user bạn muốn tạo):

```bash
sudo adduser sofsog
```

Hệ thống sẽ yêu cầu bạn nhập một mật khẩu cho người dùng mới và xác nhận lại mật khẩu. Hãy nhập mật khẩu và nhấn Enter. Tiếp theo, bạn sẽ được yêu cầu cung cấp thông tin tùy chọn cho người dùng mới, bao gồm tên đầy đủ, số điện thoại, v.v. Bạn có thể nhập thông tin này hoặc bỏ qua bằng cách nhấn Enter cho các mục bạn không muốn cung cấp thông tin. Để cấp quyền quản trị cho người dùng sofsog, chạy lệnh sau:

```bash
sudo usermod -aG sudo sofsog
```

Bây giờ, người dùng sofsog này đã có quyền quản trị trên hệ thống Ubuntu. Bạn có thể sử dụng tài khoản đó để thực hiện các tác vụ quản trị.

### 2\. Mở SSH trên Ubuntu

Gõ lệnh sau và nhấn Enter để cài đặt gói **OpenSSH** Server:

```bash
sudo apt update
sudo apt install openssh-server
```

Trong quá trình cài đặt, bạn sẽ được yêu cầu nhập mật khẩu người dùng hiện tại. Hãy nhập mật khẩu và chờ cho quá trình cài đặt hoàn tất. Khi quá trình cài đặt thành công, dịch vụ SSH sẽ tự động được kích hoạt và chạy trên hệ thống Ubuntu của bạn. Bạn có thể kiểm tra trạng thái của dịch vụ SSH bằng cách chạy lệnh sau:

```bash
sudo systemctl status ssh
```

Nếu dịch vụ SSH đang hoạt động, bạn sẽ thấy thông báo với trạng thái "**active**" hoặc "**running**". Bây giờ, bạn có thể kết nối đến máy chủ Ubuntu qua SSH bằng cách sử dụng một công cụ SSH client như PuTTY (trên Windows) hoặc Terminal (trên macOS và Linux).

### 3\. Bật quyền truy cập ssh cho user mới cho

Đảm bảo rằng bạn đã tạo người dùng mới trên hệ thống Ubuntu. Mình đã tạo một user tên **sofsog** bên trên

Mở Terminal và sử dụng lệnh sau để mở tệp cấu hình SSH:

```bash
sudo nano /etc/ssh/sshd\_config
```

Tìm đến dòng **`#PermitRootLogin`** trong tệp cấu hình và bỏ dấu **"#"** ở đầu dòng nếu có, sau đó đặt giá trị thành **`yes`**. Điều này cho phép đăng nhập qua SSH bằng tài khoản người dùng thay vì tài khoản **root**. Nếu bạn không muốn cho phép đăng nhập **root** qua SSH, bạn có thể bỏ qua bước này. Lưu và đóng tệp cấu hình bằng cách nhấn **Ctrl + X**, sau đó nhấn **Y** để lưu thay đổi và **Enter** để xác nhận tên tệp. Thêm người dùng sofsog vào nhóm ssh bằng lệnh sau:

```bash
sudo usermod -aG ssh sofsog
```

Khởi động lại dịch vụ SSH để áp dụng các thay đổi bằng lệnh sau:

```bash
sudo systemctl restart ssh
```

Bây giờ, người dùng mới đã có quyền truy cập qua SSH. Bạn có thể sử dụng một công cụ SSH client để kết nối đến VPS trên VULTR với tên người dùng và mật khẩu của người dùng đó.

Đến đây bài viết đã quá dài rồi, các bạn còn chỗ nào chưa làm đươc liên quan đến VPS trên VULTR thì để lại bình luận bên dưới nhé. Chúc các bạn thành công.

Xem thêm: [Thủ thuật về Ubuntu](https://sofsog.com/thu-thuat-chung/he-dieu-hanh/ubuntu)
