---
title: "Hướng dẫn Backup dữ liệu Wordpress"
date: "2016-09-26"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/5-Free-Backup-Solutions-For-WordPress.png
  teaser: /assets/images/5-Free-Backup-Solutions-For-WordPress.png
toc: true
breadcrumbs: true
---

Sao lưu dữ liệu website luôn là một trong các công việc quan trọng nhất mà bạn cần phải làm thường xuyên để bảo toàn dữ liệu trên website. Bởi vì khi website của bạn được đưa lên host, điều đó không có nghĩa là dữ liệu của bạn sẽ được an toàn tuyệt đối vì bạn cũng phải đề phòng các trường hợp tin tặc tấn công, hoặc rủi ro hơn là máy chủ có vấn đề.

Bởi vậy nếu không muốn mất dữ liệu, bạn phải sao lưu (backup) toàn bộ dữ liệu của website thường xuyên, và khi nào cần thì có thể khôi phục các dữ liệu dự phòng này lại.

![5-free-backup-solutions-for-wordpress](/assets/images/5-Free-Backup-Solutions-For-WordPress.png)

### Tổng quan về backup WordPress

Quy trình backup dữ liệu website WordPress nghĩa là bạn sẽ sao lưu tất cả các tập tin và thư mục liên quan đến mã nguồn website WordPress của bạn, rồi cất ở một nơi nào đó. Đồng thời, bạn cũng xuất cơ sở dữ liệu (database) ra thành một tập tin .sql để lưu lại ở nơi nào đó.

Và khi bạn gặp phải các trường hợp mất hoàn toàn dữ liệu, bạn có thể sử dụng lại được các dữ liệu dự phòng này. Sở dĩ bạn nên làm thường xuyên là vì dữ liệu trên website của bạn luôn được cập nhật mới nên làm càng thường xuyên sẽ càng hạn chế tổn thất khi có sự cố.

**Xem sau:** [Phục hồi dữ liệu WordPress thủ công.](http://sofsog.com/2016/09/26/huong-dan-phuc-hoi-du-lieu-wordpress-thu-cong-restore-wordpress/)

### Cách backup thủ công website WordPress trên host

Do host sử dụng cPanel phổ biến nhất nên mình sẽ hướng dẫn tập trung vào cách backup dữ liệu trên host sử dụng **cPanel**. Nếu bạn sử dụng máy chủ riêng thì xem [**serie này**](# "Backup - Restore dữ liệu trên máy chủ").

#### Bước 1. Backup mã nguồn

Để backup các dữ liệu mã nguồn nhanh nhất, đó là bạn truy cập vào **File Manager**.

![cpanel-filemanager-1](/assets/images/cpanel-filemanager-1-1.jpg)

Sau đó truy cập vào thư mục chứa mã nguồn website, ấn nút Select All để chọn tất cả và chọn Compress để nén dữ liệu.

![backup-wp-thucong-02](/assets/images/backup-wp-thucong-02.jpg)

Rồi chọn loại tập tin nén (nên chọn Zip hoặc Gzip), đặt tên cho tập tin nén được tạo ra và ấn nút Compress File(s) để nén toàn bộ mã nguồn lại.

![backup-wp-thucong-03](/assets/images/backup-wp-thucong-03.jpg) Ok, bây giờ bạn đã nén toàn bộ mã nguồn lại thành một file nén. Bạn có thể tải file này về máy rồi cất vào thư mục nào đó thật an toàn.

#### Bước 2. Backup database

Để backup database, bạn truy cập vào phần **phpMyAdmin** trên host.

![backup-database-4](/assets/images/backup-database-4-1.jpg)

Truy cập công cụ PhpMyAdmin

Chọn database của website bạn cần backup

![backup-wp-thucong-05](/assets/images/backup-wp-thucong-05.jpg)

Chọn Export trên thanh công cụ.

![backup-wp-thucong-06](/assets/images/backup-wp-thucong-06.jpg)

Để thiết lập như mặc định và ấn nút Go để nó bắt đầu tải về máy file .sql chứa database của website bạn.

![backup-wp-thucong-07](/assets/images/backup-wp-thucong-07.jpg)

Vậy là hoàn tất quá trình backup toàn bộ dữ liệu website WordPress của bạn rồi đó, bây giờ bạn hãy lưu file nén chứa mã nguồn của website và file .sql chứa database của website vào một nơi an toàn để lưu giữ nó. Và đừng quên lặp lại quá trình này thường xuyên.

Nếu bạn cần khôi phục lại dữ liệu từ các file backup này, hãy xem bài hướng dẫn khôi phục (restore) dữ liệu WordPress thủ công.

Nguồn: Thạch Phạm Blog
