---
title: "Hướng dẫn tăng tốc cho Wordpress bằng Cache"
date: "2016-10-04"
categories: 
  - "wordpress"
tags: 
  - "cache-trong-wordpress"
  - "huong-dan-wordpress"
  - "seo"
  - "tang-toc-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/Huong-dan-tang-toc-cho-wordpress-bang-cache.png
  teaser: /assets/images/Huong-dan-tang-toc-cho-wordpress-bang-cache.png
toc: true
breadcrumbs: true
permalink: /thiet-ke-web/wordpress/huong-dan-tang-toc-cho-wordpress-bang-cache
---

Khi tìm hiểu về các bài viết [tăng tốc WordPress](http://sofsog.com/wordpress/plugin-tang-toc-cho-wordpress), có thể bạn sẽ thấy mình nhắc qua khá nhiều hình thức lưu bộ nhớ đệm cho website (hay còn gọi là Cache/Caching), đây là một trong **các phương pháp để tăng tốc website WordPress** rất tốt. Nên nhiều bạn có phản hồi là nên dùng cái nào, dùng hết được không,..vâng vâng,…Do vậy bây giờ mình sẽ làm một bài tổng hợp về các hình thức caching trong WordPress mà mình biết được để nói về công dụng của nó, khả năng ứng dụng cũng như nhược điểm để mọi người có cái nhìn tổng quan hơn.

![Hướng dẫn tăng tốc cho wordpress bằng Cache](/assets/images/Huong-dan-tang-toc-cho-wordpress-bang-cache.png)

### 1\. HTML Caching

Đây là hình thức lưu bộ nhớ đệm đơn giản và hầu hết cho thể áp dụng cho mọi website (trừ những trang phụ thuộc vào cookie/session như giỏ hàng, thanh toán trong website bán hàng).

Hình thức này nghĩa là nó sẽ lưu nội dung của một trang được truy cập bởi một người mới nhất thành một tập tin HTML tĩnh và sẽ được lưu ở một nơi cố định trong ổ cứng của máy chủ. Sau đó, máy chủ sẽ được cấu hình để tự động sử dụng lại tập tin HTML tĩnh này mà không cần phải thông qua các bước xử lý đến máy chủ như khi truy cập vào website bình thường.

#### Ưu điểm

- Dễ thiết lập, các plugin caching như WP Super Cache và W3 Total Cache (phương thức Disk) sử dụng kỹ thuật này.
- Tương thích hầu hết trên mọi webserver.
- Tốc độ cải thiện rất đáng kể, nếu website bạn có ổ cứng SSD thì sẽ còn bá đạo hơn.
- Không cần cài đặt thêm software nào cho Webserver.

#### Nhược điểm

- Tốn bộ nhớ nếu website của bạn có nhiều trang và được ghi cache liên tục, vì mỗi lần ghi cache nó sẽ tốn kha khá bộ nhớ.
- Các tính năng tải dạng động như đếm lượt xem không hoạt động.
- Bị xung đột với session/cookie vì khi lưu nó lưu cả cái session của người truy cập đầu tiên.
- Khó có khả năng sử dụng cho các website lớn.

#### Các plugin cho kỹ thuật này

- WP Super Cache (dành cho Shared Host)
- W3 Total Cache (dành cho máy chủ riêng/VPS)
- WP Fastest Cache (Dễ sử dụng, dành cho Shared Host)
- GatorCache

#### Khi nào nên sử dụng HTML Caching

- Tất cả website từ nhỏ tới trung bình đều dùng được.
- Khi bạn cần cải thiện tốc độ tải trang mà website không có những dữ liệu động được truy xuất thường xuyên.
- Nếu bạn dùng Shared Host thì chỉ có thể áp dụng phương thức này.

### 2\. Opcode Caching

Opcode Caching là một thành phần mở rộng (extension) của PHP để làm gia tăng hiệu suất xử lý của nó bằng cách lưu lại kết quả trả về cho lần xử lý đầu tiên và xử dụng nó cho các lần gửi truy vấn tiếp theo để tránh việc một đoạn code phải xử lý nhiều lần mà trả về cùng 1 kết quả. Nhưng dữ liệu cache này sẽ được lưu vào RAM.

Opcode Caching hoạt động tốt hay không phụ thuộc vào Opcache System (một hệ thống tiền xử lý của phương thức này), trong danh sách Opcache System thì mình biết được có một số cái tên sau dùng khá tốt:

- **Zend Opcache** – Sử dụng tốt hầu hết trên mọi website, không cần cấu hình nhiều, dễ cài đặt.
- **APC** – Một extension được xử dụng khá phổ biến trên các phiên bản PHP 5.4 và PHP 5.5, ưu điểm là khả năng tùy biến cao, bù lại nó hơi khó cấu hình.
- **XCache** – Cũng là một sự thay thế khá tốt cho APC nhưng XCache dễ cấu hình hơn, sử dụng ít RAM hơn APC.

Ngoài ra còn một số system khác như eAccelerator, WinCache nhưng nó đều đã rất củ kỹ, không nên dùng ở thời điểm hiện tại.

#### Ưu điểm

- Tiết kiệm CPU và tốc độ xử lý truy vấn PHP.

#### Nhược điểm

- Hầu như chỉ sử dụng được ở server riêng – nơi bạn có thể tự cài software.
- Chỉ hoạt động với PHP 5.4 trở lên.
- Hơi tốn RAM vì nó được dùng để lưu cache.
- APC không hoạt động nếu bạn có cài thêm PHP Handler là suPHP. Và mỗi lần sửa code PHP, bạn phải tự xóa cache.

#### Các plugin cho kỹ thuật này

Do đây là một kỹ thuật cache nên nó sẽ làm việc với kỹ thuật Object Caching trong WordPress với các plugin dưới đây. Đừng nên cài vào nếu bạn không chắc chắn server của mình đã được cài một trong các system ở trên.

- [EM Object Cache](https://wordpress.org/plugins/em-object-cache/ "EM Object Cache")
- [W3 Total Cache](https://wordpress.org/plugins/w3-total-cache/ "Object Cache") (Object Cache & Database Cache)
- [APC Object Cache Backend](https://wordpress.org/plugins/apc/)
- [XCache Object Cache Backend](https://wordpress.org/plugins/xcache/)
- [Opcache Dashboard](https://wordpress.org/plugins/opcache/)
- [WP FFPC](https://wordpress.org/plugins/wp-ffpc/)

#### Khi nào nên sử dụng Opcode Cache

- Nếu bạn có quá nhiều truy vấn trong website bằng code PHP.
- Có thể sử dụng cùng lúc với các kỹ thuật caching khác.
- Có nhiều RAM quá không biết làm gì.

### 3\. Object Caching

Đây là một phương thưc riêng trong WordPress vì mã nguồn này có hỗ trợ phương thức lưu cache cho các đối tượng như query, session hoặc bất cứ cái gì đó được xử lý bằng code PHP trong WordPress, thông qua một hàm tên là [wp\_cache](http://codex.wordpress.org/Class_Reference/WP_Object_Cache "wp_cache").

Phương thức này không thể sử dụng độc lập mà nó cần sự hỗ trợ của các system cache khác như:

- **XCache**
- **APC**
- **Memcached**
- **Redis**

Tuy rằng nó cần một system hỗ trợ mà hầu hết là các system đó sẽ hỗ trợ lưu cache vào RAM nhưng Object Cache vẫn có thể hoạt động được bằng cách ghi cache vào ổ cứng, bằng cách dùng plugin W3 Total Cache và chọn method là Disk.

#### Ưu điểm

- Làm giảm thời gian xử lý các đối tượng dữ liệu trên website, cả frontend lẫn backend.
- Tiết kiệm CPU cho máy chủ.

#### Nhược điểm

- Lần đầu tiên truy xuất dữ liệu sẽ khá chậm, đặc biệt là nếu bạn dùng Memcached và website có nhiều plugins.

#### Các plugin cho phương thức này

Do nó là một phương thức riêng trong WordPress nên điều bạn cần là viết code sử dụng phương thức này. Tuy nhiên, bạn vẫn có thể dùng các plugin mà mình đã kể ở phần Opcode Cache vì các plugin đó có nhiệm vụ áp dụng Opcode Cache System cho việc lưu Object Cache.

Nếu bạn sử dụng Memcached, bạn có thể cài plugin **[Memcached is Your Friend](https://wordpress.org/plugins/memcached-is-your-friend/)** để làm object cache, chỉ cần cài vào không cần làm gì thêm.

#### Khi nào nên sử dụng

- Nên sử dụng khi dùng server riêng và sử dụng thông qua các system cache khác (đã kể ở trên).

### 4\. Browser Cache

Hình thức này nghĩa là website sẽ ép trình duyệt lưu một bản cache trong bộ nhớ của trình duyệt trên máy tính người dùng để các lần truy cập tiếp theo của họ có tốc độ tốt hơn, vì lúc này các file được lưu ở cache không phải mất công tải lại một lần nữa. Thường thì kỹ thuật này trình duyệt sẽ lưu cache cho các file tĩnh trong website như hình ảnh, CSS, Javascript,…và nếu website bạn đang bật gzip thì nó sẽ lưu luôn nội dung của toàn website.

#### Ưu điểm

- Cải thiện tốc độ đáng kể vì họ vừa không gửi tủy vấn xử lý, vừa không mất công gửi kết nối để tải dữ liệu đã được lưu cache về.
- Có thể áp dụng với hầu hết tất cả website.

#### Nhược điểm

- Nếu website bạn đã xóa cache mà trình duyệt của họ vẫn còn lưu thì khi họ vào, nó vẫn hiển thị dữ liệu cũ.
- Người dùng phải F5 liên tiếp 2 lần để thực hiện xóa cache.

#### Các plugin hỗ trợ kỹ thuật này

- [WP Super Cache](https://wordpress.org/plugins/wp-super-cache/ "WP Super Cache")
- [W3 Total Cache](https://wordpress.org/plugins/w3-total-cache/ "W3 Total Cache")
- [WP Rocket](http://wp-rocket.me/ "WP Rocket") (Trả phí)
- [Quick Cache](https://wordpress.org/plugins/quick-cache/ "QuickCache")

### 5\. Database Caching

Hãy tưởng tượng rằng mỗi lần khách truy cập họ sẽ gửi một truy vấn vào webserver (Apache hoặc NGINX), sau đó webserver sẽ gửi truy vấn này đến PHP để nó xử lý và nếu truy vấn này có yêu cầu lấy dữ liệu từ database thì PHP sẽ gửi dến database (MySQL Server/MariaDB Server). Ở công đoạn xử lý trong database, nó sẽ tiến hành đánh dấu lại dữ liệu có trong database (indexing) và sau đó mới lấy nội dung mà khách truy cập cần để trả về. Và chuyện gì sẽ xảy ra nếu database của bạn có dung lượng lên đến đơn vị GB và có nhiều truy vấn gửi đến cùng lúc? (không kể đến các truy vấn đã được cache bởi các kỹ thuật khác).

Đó là lý do tại sao Database Caching lại ra đời, trong database caching còn có rất nhiều kiểu cache khác nhau như lưu cache cho toàn table hoặc lưu cache cho từng loại dữ liệu riêng biệt. Nếu bạn có ý định áp dụng database caching vào WordPress thì mình khuyến khích bạn nên sử dụng một plugin chuyên biệt để làm việc này như W3 Total Cache là lựa chọn rất tốt, ngoài ra bạn nên sử dụng nó cùng với một system cache có hỗ trợ database như Memcached chẳng hạn.

Trường hợp bạn muốn tự viết code trong WordPress để tùy chỉnh dữ liệu muốn được lưu database cache thì có thể áp dụng [Transient API](http://thachpham.com/wordpress/wordpress-development/wordpress-transient-api-cache.html "Transient API – Lưu cache cho đối tượng trong WordPress").

#### Ưu điểm

- Tiết kiệm thời gian xử lý nhận dữ liệu từ database.

#### Nhược điểm

- Tốn RAM.
- Chỉ thích hợp khi dùng server riêng với sự hỗ trợ của Memcached.
- Sẽ làm backend hơi chậm vì có quá nhiều dữ liệu cần lưu cache. Dùng W3 Total Cache sẽ hạn chế bớt việc lưu cache các truy vấn không nên lưu.
- Mình không biết tại sao vì chưa debug nhiều nhưng vài trường hợp, website sẽ trở nên chậm chạp hơn lúc chưa dùng database caching. Bạn nên test kỹ trước khi dùng chính thức.

#### Khi nào nên sử dụng

- Website có nhiều lượt truy cập cùng và gửi truy vấn thường xuyên đến database để lấy dữ liệu.

### Lời kết

Mặc dù có thể các kỹ thuật lưu cache thường dùng trong WordPress có thể sẽ nhiều hơn danh sách này nhưng mình chỉ liệt kê ra các kỹ thuật mà mình đã từng sử dụng và biết tới, và đây cũng là các kỹ thuật rất phổ biến ở các website lớn. Tuy nhiên, điều này không có nghĩa là bạn áp dụng hết toàn bộ 5 kỹ thuật này là website có tốc độ tải tốt nhất mà chỉ nên chọn ra một số kỹ thuật phù hợp với quy mô của website cũng như khả năng đáp ứng của máy chủ.

Nguồn: Thạch Phạm Blog
