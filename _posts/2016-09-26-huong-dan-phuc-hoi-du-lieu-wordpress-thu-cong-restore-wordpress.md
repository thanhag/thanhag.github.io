---
title: "Hướng dẫn phục hồi dữ liệu WordPress thủ công (restore WordPress)"
date: "2016-09-26"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  
  teaser: /assets/images/Backup_center_icon.png
toc: true
breadcrumbs: true
---

Tuy rằng việc phục hồi dữ liệu website WordPress có thể ít xảy ra mà thường là chỉ làm khi website bị lỗi không khôi phục được hoặc chuyển host, đổi tên miền. Nhưng việc nắm vững các kỹ thuật phục hồi dữ liệu cơ bản cũng sẽ giúp bạn đỡ phải loay hoay khi gặp sự cố.

Trong bài này, mình sẽ hướng dẫn các bạn cách phục hồi dữ liệu website WordPress bằng thủ công trên host. Tuy là thủ công nhưng đa phần các quy trình phục hồi dữ liệu đều làm như thế này.

![backup_center_icon](/assets/images/Backup_center_icon.png)

**Xem nếu chưa biết**: [Cách sao lưu (backup) dữ liệu WordPress thủ công](http://sofsog.com/2016/09/26/huong-dan-backup-du-lieu-wordpress/ "Cách backup (sao lưu) dữ liệu WordPress thủ công").

Để phục hồi được dữ liệu của website WordPress hoàn chỉnh nhất, bạn cần có:

- Một file nén chứa mã nguồn của website.
- Một file .sql chứa database của website.

Ngoài ra, khi phục hồi bạn nên tạo một database mới hoàn toàn và thư mục cần khôi phục tập tin trên host cũng phải được trống hoàn toàn.

### Cách phục hồi dữ liệu WordPress thủ công

#### Bước 1. Phục hồi mã nguồn

Để phục hồi mã nguồn thì dễ hơn, đó bạn là hãy upload file nén chứa mã nguồn của website lên host thông qua tính năng File Manager.

![cpanel-filemanager-1](/assets/images/cpanel-filemanager-1.jpg)

Sau khi upload xong, hãy chọn file nén và ấn Extract.

![restore-wp-thucong-02](/assets/images/restore-wp-thucong-02.jpg)

Giải nén xong bạn đã có các thư mục và tập tin mã nguồn của website trên host rồi.

![restore-wp-thucong-02-3](/assets/images/restore-wp-thucong-02-3.jpg)

Ok, bây giờ bạn hãy mở tập tin wp-config.php ra và sửa các đoạn sau đây thành thông tin database mới của bạn rồi lưu lại.

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">01</div><div class="line number2 index1 alt1">02</div><div class="line number3 index2 alt2">03</div><div class="line number4 index3 alt1">04</div><div class="line number5 index4 alt2">05</div><div class="line number6 index5 alt1">06</div><div class="line number7 index6 alt2">07</div><div class="line number8 index7 alt1">08</div><div class="line number9 index8 alt2">09</div><div class="line number10 index9 alt1">10</div><div class="line number11 index10 alt2">11</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="php comments">/**The name of the database for WordPress */</code></div><div class="line number2 index1 alt1"><code class="php plain">define(</code><code class="php string">'DB_NAME'</code><code class="php plain">, </code><code class="php string">'TÊN-DATABASE'</code><code class="php plain">);</code></div><div class="line number3 index2 alt2"></div><div class="line number4 index3 alt1"><code class="php comments">/** MySQL database username*/</code></div><div class="line number5 index4 alt2"><code class="php plain">define(</code><code class="php string">'DB_USER'</code><code class="php plain">, </code><code class="php string">'USERNAME-DATABASE'</code><code class="php plain">);</code></div><div class="line number6 index5 alt1"></div><div class="line number7 index6 alt2"><code class="php comments">/**MySQL database password */</code></div><div class="line number8 index7 alt1"><code class="php plain">define(</code><code class="php string">'DB_PASSWORD'</code><code class="php plain">, </code><code class="php string">'MẬT-KHẨU-DATABASE'</code><code class="php plain">);</code></div><div class="line number9 index8 alt2"></div><div class="line number10 index9 alt1"><code class="php comments">/** MySQL hostname*/</code></div><div class="line number11 index10 alt2"><code class="php plain">define(</code><code class="php string">'DB_HOST'</code><code class="php plain">, </code><code class="php string">'localhost'</code><code class="php plain">);</code></div></div></td></tr></tbody></table>

#### Bước 2. Khôi phục database

Để khôi phục database, bạn hãy truy cập vào phpMyAdmin trên host.

![backup-database-4](/assets/images/backup-database-4.jpg)

Truy cập công cụ PhpMyAdmin

Và chọn database cần khôi phục.

![backup-wp-thucong-5](/assets/images/backup-wp-thucong-5.jpg)

Và chọn Import trên thanh công cụ.

![restore-wp-thucong-06](/assets/images/restore-wp-thucong-06.jpg)

Rồi upload tập tin .sql chứa database của website bạn lên và ấn Go, các thiết lập khác giữ nguyên.

![restore-wp-thucong-07](/assets/images/restore-wp-thucong-07.jpg)

Nếu nó báo thành công thế này là được rồi.

![localhost-to-host-08](/assets/images/localhost-to-host-08.jpg)

Bây giờ hãy kiểm tra tiền tố của database xem có trùng với thiết lập trong file wp-config.php trên host không nhé. Tiền tố database là các ký tự trước dấu “\_” của các bảng dữ liệu (table).

![restore-wp-thucong-09](/assets/images/restore-wp-thucong-09.jpg)

Và đây là đoạn thiết lập tiền tố database trong file wp-config.php, hai cái này phải trùng nhau thì website mới chạy được.

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">01</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="php variable">$table_prefix</code> &nbsp;<code class="php plain">= </code><code class="php string">'wp_'</code><code class="php plain">;</code></div></div></td></tr></tbody></table>

#### Bước 3. Cập nhật permalink

Sau khi khôi phục lại dữ liệu xong, bạn cần phải flush permalink trong website bằng cách vào Settings -> Permalinks và ấn nút Save Changes là được.

Hoàn tất rồi đó, bây giờ hãy kiểm tra xem website của bạn đã hoạt động tốt chưa nhé.

Nguồn: Thạch Phạm Blog
