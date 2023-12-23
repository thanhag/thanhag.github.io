---
title: "Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com)"
date: "2017-08-23"
categories: 
  - "thiet-ke-web"
  - "thu-thuat-chung"
  - "wordpress"
tags: 
  - "email-ten-mien-rieng"
  - "huong-dan-tao-email-ten-mien-rieng-mien-phi"
  - "huong-dan-wordpress"
  - "thiet-ke-web"
  - "wordpress"
  - "yandex"
  - "yandex-com"
header:
  image: /assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com_.jpg
  teaser: /assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com_.jpg
toc: true
breadcrumbs: true
---

Mình hướng dẫn sử dụng dịch vụ miễn phí của **Yandex.com**

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com)](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com_.jpg) Hướng dẫn tạo email tên miền riêng miễn phí với Yandex.com

Email theo tên miền riêng của bạn (ví dụ admin@TenMienCuaBan.com thay vì địa chỉ chung @gmail.com, @live.com như thông thường) đem lại sự chuyên nghiệp cho email của bạn.

**Điều kiện đầu tiên:** Bạn bắt buộc bạn phải có tên miền riêng (tất nhiên rồi)

###  I. Đăng ký Yandex

Bạn hãy đăng ký một tài khoản Yandex [tại đây](https://passport.yandex.com/registration),:

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 1](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-1.png) Đăng ký Yandex.com

Điền thông tin vào các ô tương ứng, chỗ "Mobile number" bạn điền chính xác số điện thoại của mình vào, thêm +84 đầu và bỏ số không (ví dụ +849\*\*\*\*\*\*23).  Nhấn **Send code,** chờ tin nhắn, lấy mã số và điền vào rồi nhấn **Confirm** để xác nhận.

Bạn cũng có thể xác nhận bằng cách bấm vào **I don’t have a mobile phone number ,** chọn câu hỏi và trả lời bảo mật để thay thế số điện thoại.

Xong thì bấm **Register**.

Ngay lập tức bạn được chuyển đến trang thông tin cá nhân như bên dưới, hãy update lại thông tin nếu cần.

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 1](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-2.png) Trang thông tin cá nhân của Yandex

### II. Thêm tên miền vào tài khoản Yandex

Truy cập vào [domain.yandex.com](https://domain.yandex.com/) , trong ô **Enter a domain name for your mailbox** bạn gõ vào tên miền cần thêm vào và nhấn **Connect domain.**

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 1](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-3.png) Thêm tên miền vào tài khoản Yandex

**1\. Giờ là bước xác nhận tên miền của bạn:**

Có 3 cách xác nhận: mình hướng dẫn cách 1 và cánh 2 thôi nhá:

Cách 1:Bạn tải file htmt như trong hình: **bfabb924dc40.html** nội dung trong file là **bfcfea3a2be8.** rồi up lên thư mục gốc của trang web của bạn. (lưu ý: tên file và nội dung của bạn đương nhiên phải khác mình rồi, đây chỉ là ví dụ)

Xong bấm vào nút **Verify domain ownership.**

Cách 2:

Cách này không cần bạn phải có Web Hosting, bạn vào trang quản lý DNS của tên miền, tạo 1 record **CNAME** với tên như quy định và trỏ đến **`mail.yandex.com`** là được.

Xong bấm vào nút **Verify domain ownership.** (Cách này chờ xác nhận hơi lâu, có thể là 24 giờ)

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 1](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-4.png) Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 1

**2\. Cấu hình record MX**

Trong trang quản lý DNS, bạn hãy **xóa hết record MX hiện tại**

Tạo một record MX khác:

- Subdomain name — **@** (trường hợp không điền @ được thì bạn có thể điền luôn tên miền của mình vào đây)
- Type of record — **MX**
- Data — **mx.yandex.net.**
- Priority — **10**

Nếu bạn có dùng [cloudflare](http://sofsog.com/thiet-ke-web/wordpress/huong-dan-su-dung-cloudflare) thì cấu hình giống như hình là ok:

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com)](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com_.png) Cấu hình **Record MX** ở cloudflare

Sau khi xong, nhấn nút **Verify MX records** để xác nhận.

Record cần thời gian để cập nhật.

Bạn có thể vào trang [mxtoolbox.com](https://mxtoolbox.com/)  để kiểm tra việc cấu hình MX của mình, nếu xuất hiện hình tương tự bên dưới tức là cầu hình đúng:

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 1](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-1-1.png)

Nhưng vẫn phải chờ thằng [yandex](https://domain.yandex.com) nó cập nhật, mình thì nôn nóng nên cứ ngồi bấm **Verify MX records** liên tục.

Nếu làm đúng thì trong trang Yandex của bạn sẽ nhận sẽ xuất hiện dòng chữ **Domain connected** màu xanh lè như hình dưới đây:

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 2](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-2-1.png)

Vậy là xong các bước thêm tên miền và xác nhận đủ thứ trên đời.

### III. Sử dụng Yandex.com

**1\. Tạo link đăng nhập theo tên miền của bạn luôn:**

Vào trang cấu hình DNS, Tạo một record CNAME tên là **mail** (tên này bắt buộc), trỏ đến **`domain.mail.yandex.net`**

Từ lần sau bạn có thể sử dụng đường dẫn **<http://mail.TenMienCuaBan.com>** để đăng nhập webmail.

**2\. Cấu hình SPF và DKIM:** Để mail không bị chuyển vào spam

Nếu muốn email gửi đi không bị chuyển vào Spam, bạn cần cấu hình [SPF](https://support.google.com/a/answer/33786?hl=en) và [DKIM](https://support.google.com/a/answer/174124?hl=en) cho tên miền.

Trong trang quản lý [Mail for Domain](https://domain.yandex.com/), hãy click vào link **DNS editor**. (xem hình)

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 2](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-2-1.png)

Trong bảng **DNS records** bên dưới bạn sẽ thấy có rất nhiều record, hãy chú ý 2 record **SPF** và **DKIM** : (khoanh đỏ)

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 3](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-3-1.png)

Vào trang quản lý DNS cấu hình thêm 2 record y chang phần khoanh đỏ bên trên.

Nếu dùng [CloudFlare](http://sofsog.com/thiet-ke-web/wordpress/huong-dan-su-dung-cloudflare) thì sẽ trông tương tự như sau:

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 4](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-4-1.png)

Vậy là bạn đã hoàn thành xong toàn bộ bước cấu hình cho tên miền rồi đó.

**3\. Tạo email:**

Trong trang [Mail for Domain](https://domain.yandex.com/) phần **New mailbox** bạn hãy nhập địa chỉ email muốn tạo rồi nhấn nút _Add_.

Từ account thứ 2 trở đi, bạn hãy nhấn link **Add mailbox** để nhập thêm. Giới hạn 1.000 mailbox.

**4\. Tạo địa chỉ email mặc định:**

**Email mặc định** là khi người khác gửi email vào các địa chỉ không tồn tại có đuôi là tên miền của bạn ví dụ: 341243@sofsog.com, dfjdlkjf@sofsog.com (các email này mình chưa tạo bao giờ), thì các email được người khác gửi vào đó sẽ chuyển vào **email mặc định.**

Để cấu hình địa chỉ mặc định, nhấn vào link **Configure domain.**

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com) 5](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-5-1.png)

Ở phần **Default address**, chọn địa chỉ mong muốn rồi nhấn nút **Select** là xong

**5\. Sử dụng phần mềm quản lý mail**

Nếu bạn muốn kiểm tra email trên mobile, hãy cài ứng dụng Yandex Mail.

- [Yandex.Mail Android](https://play.google.com/store/apps/details?id=ru.yandex.mail)
- [Yandex.Mail iOS](https://itunes.apple.com/us/app/yandex-mail/id441785419?mt=8)

Với những ứng dụng quản lý mail khác như Outlook, Thunderbird, Apple Mail… bạn hãy tham khảo [hướng dẫn này](https://yandex.com/support/mail/mail-clients.xml) để biết thông số cấu hình IMAP, POP3.

**6. Dùng Yandex SMTP để gửi mail với WordPress**

Để có thể gửi mail notification, mail thông báo đơn hàng với WordPress sử dụng Yandex SMTP, bạn hãy cài đặt plugin [WP Mail SMTP](https://wordpress.org/plugins/wp-mail-smtp/)

Vào **Setting>Mail** rồi cấu hình như sau.

Điền email vào **From Email**

Lưu ý là email này phải được đăng nhập vào hòm thư của yandex rồi (để kích hoạt email đó mà)

Điền các thông tin cần thiết như trong hình

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com)](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-1-2.png) SMTP Options sử dụng SSL như hướng dẫn của Yandex. Nếu bạn Send Test Email không được, hãy thử chuyển qua TLS, Các thông tin khác điền như trong hình, riêng Username và password là email của bạn (tất nhiên rồi)

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com)](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-2-2.png)

Điền một email nào đó vào ô **Send a Test Email TO:**

Bấm nút **Send Test Email** nếu báo **`bool(true)`** như hình là thành công.

![Hướng dẫn tạo email tên miền riêng miễn phí (Yandex.com)](/assets/images/Hướng-dẫn-tạo-email-tên-miền-riêng-miễn-phí-Yandex.com-3-2.png)

Giới hạn gửi mail của Yandex là 3.000 mail/ngày. Mỗi lần gửi chỉ được tối đa 35 người nhận (qua SMTP Server hoặc Mail Client) hoặc 50 người nhận (dùng giao diện web).

Nếu gửi email marketing, bạn hãy tham khảo [**MailChimp**](https://mailchimp.com), [**GetResponse**](https://www.getresponse.com) hoặc [**Sendy**](https://sendy.co/).

**7\. Forward mail sang địa chỉ khác từ Yandex**

Để forward mail **Yandex** sang địa chỉ mail khác ( chẳng hạn Gmail), bạn hãy login vào mail, nhấn biểu tượng răng cưa **All Settings**, chọn **Message filtering.**

![Forward mail sang địa chỉ khác từ Yandex](/assets/images/Forward-mail-sang-địa-chỉ-khác-từ-Yandex.png)

Chọn **Create filter** và tạo filter với điều kiện email gửi tới địa chỉ của bạn thì sẽ forward sang địa chỉ khác. Hình ảnh cấu hình như sau:

![Forward mail sang địa chỉ khác từ Yandex](/assets/images/Forward-mail-sang-địa-chỉ-khác-từ-Yandex-1.png)

Xong thì bấm nút **Create filter** lần nữa là ok

Vào email ở ô **Forward to** bên trên, tìm email mà Yandex gửi rồi bấm link  **confirm** để xác nhận (có thể mail xác nhận này sẽ nằm trong spam).

**8\. Hiển thị Avatar khi gửi mail từ Yandex đến Gmail**

Đầu tiên, bạn cần [đăng ký Google Account tại đây](https://accounts.google.com/SignUp?continue=https%3A%2F%2Fplus.google.com%2Fcollections%2Ffeatured), click **I prefer to use my current email address** rồi nhập địa chỉ email Yandex vừa tạo vào, như hình:

![Tao avarta cho email Yandex khi gui vao gmail](/assets/images/Tao-avarta-cho-email-Yandex-khi-gui-vao-gmail.png) Điền các thông tin cần thiết vào

Đăng ký xong sẽ xuất hiện hình dưới đây, vào email yandex để xác nhận

![Tao avarta cho email Yandex khi gui vao gmail](/assets/images/Tao-avarta-cho-email-Yandex-khi-gui-vao-gmail-1.png)

Sau khi đăng ký xong, vào trang [https://plus.google.com](https://plus.google.com/), bạn hãy click nút **_Join Google+_**  để tạo profile Google+, sau đó upload avatar lên.

Done.

**9\. Hiển thị tên khi gửi mail thay cho địa chỉ email**

Click vào biểu tượng bánh răng  ở trên cùng bên phải, chọn **Personal data, signature, picture** rồi nhập tên bạn muốn hiển thị trong ô **Your name** là xong.

Tại đây bạn cũng có thể add luôn **chữ ký** vào email.

### IV. Lời kết

Yandex là dịch vụ miễn phí rất đáng dùng, và mình đang dùng dịch vụ này.

Trong quá trình đăng ký, cấu hình và sử dụng nếu các bạn gặp khó khăn gì cứ để lại comment bên dưới, mình sẽ hỗ trợ hết mức có thể.

Cám ơn đã đọc bài đến đây, chúc bạn thành công.
