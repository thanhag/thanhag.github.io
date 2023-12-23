---
title: "Hướng dẫn chuyển host và đổi domain wordpress bằng plugin duplicator"
date: "2017-08-17"
categories: 
  - "thiet-ke-web"
  - "wordpress"
tags: 
  - "chuyen-host"
  - "chuyen-host-wordpress"
  - "doi-donain"
  - "huong-dan-backup-wordpress"
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/5-Free-Backup-Solutions-For-WordPress.png
  teaser: /assets/images/5-Free-Backup-Solutions-For-WordPress.png
toc: true
breadcrumbs: true
---

Duplicator là plugin giúp bạn sao lưu, phục hồi dữ diệu website wordpress một cách dễ dàng và nhanh chóng. Ngoài ra nó còn tự động **đổi toàn bộ thiết lập trên website sang tên miền mới**

Xem thêm: [Sao lưu dữ liệu WordPress thủ công](http://sofsog.com/thiet-ke-web/wordpress/huong-dan-backup-du-lieu-wordpress "Cách backup (sao lưu) dữ liệu WordPress thủ công")

#### Cách sử dụng plugin Duplicator

Sau khi cài plugin Duplicator, bạn vào**Duplicator -> Packages -> Create New**

![duplicator-newpackage](/assets/images/duplicator-newpackage.png)

Sau đó bạn có thể đặt tên package nếu muốn, hoặc ấn vào phần **Archive** để tùy chọn loại bỏ một số dữ liệu mà bạn không muốn nó mang theo nếu cần, còn không cứ để nguyên và ấn Next.

![duplicator-newpackage02](/assets/images/duplicator-newpackage02.png)

Bước này nó sẽ tiến hành quét sơ dữ liệu của bạn để kiểm tra dung lượng và báo cáo chi tiết xem cấu hình của bạn có thích hợp để xuất dữ liệu ra hay không vì thường nếu website của bạn có nhiều dữ liệu mà host yếu quá thì sẽ không chạy được.

![duplicator-newpackage03](/assets/images/duplicator-newpackage03.png)

Nếu nó chỉ báo Warning (Warn) một số phần thôi thì bạn vẫn có thể dùng được, chỉ là thời gian hơi lâu một chút. Bạn có thể ấn nút Build để bắt đầu tạo gói sao lưu dữ liệu từ plugin này, thời gian đợi có thể nhanh hay chậm tùy vào độ lớn của dữ liệu.

Sau khi nó làm xong, bạn có thể tải tập tin dữ liệu và file **installer.php** về máy. File installer.php này là file mà bạn cần bắt buộc để chạy khi cần phục hồi dữ liệu lại trên host khác.

![duplicator-newpackage-finish](/assets/images/duplicator-newpackage-finish.png)

Bây giờ mình cần khôi phục dữ liệu này trên host khác, thì sẽ upload file .zip (dữ liệu của website) và installer.php (công cụ phục hồi) lên host.

Sau đó vào File Manager của host tìm tập tin .zip vừa upload lên và chọn Extract.

Tiếp tục chạy file installer.php trên host theo đường dẫn _<http://domain/installer.php>_.

![duplicator-restore-01](/assets/images/duplicator-restore-01.png)

Hãy nhập thông tin database của bạn vào, bạn nên tạo sẵn database mới từ trước, nhập xong nhớ ấn nút **Test Connection** để xem bạn đã nhập đúng thông tin database hay chưa.

Sau đó chọn Advanved Options và đánh dấu vào **Manual package extraction**. Cuối cùng chọn đồng ý các điều khoản và ấn nút Run Deployment.

![](/assets/images/2017-duplicator1.png)

Kế tiếp, nó sẽ hỏi bạn thiết lập tên miền mới và tạo tài khoản admin mới cho website nếu muốn. Thường thì bạn chạy file **installer.php** ở tên miền nào thì nó sẽ tự xác định website sử dụng tên miền đó. Sau khi chắc chắn xong thông tin thì ấn nút **Run Update**.

![duplicator-restore-03](/assets/images/duplicator-restore-03.png)

Cuối cùng là nó hiện ra bảng này tức là dữ liệu đã khôi phục thành công.

![duplicator-restore-04](/assets/images/duplicator-restore-04.png)

Bây giờ thì dữ liệu của bạn đã được chuyển qua host mới và sử dụng một tên miền mới. Việc của bạn cần làm bây giờ là:

- Vào Settings -> Permalinks và ấn Save Changes.
- Vào Duplicator -> Tools -> Cleanup -> ấn vào Delete Reserved Files để xóa bản backup kia đi để tránh kẻ xấu chạy file installer.php.
- Tắt plugin Duplicator cho đỡ vướng víu.

Vậy thôi đó, thấy đơn giản không nào? Thực ra đây là một plugin rất có ích với mình vì nó giúp mình chuyển host nhanh hơn hoặc đơn giản là mình cần lấy một bản WordPress nào đó cài ra thành nhiều website khác mà không cần phải làm nhiều thao tác. Nên nếu bạn chưa rành về kỹ thuật, có nhu cầu đổi domain cho WordPress hoặc chuyển host thì có thể sử dụng plugin này để đơn giản hóa các bước làm việc.

Chúc bạn thành công!

Nguồn: Thachpham.com
