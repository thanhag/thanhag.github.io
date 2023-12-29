---
title: "Tối ưu hóa dung lượng cho WordPress"
date: "2016-09-26"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  overlay_image: /assets/images/media-library-wordpress.jpg
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)" 
  teaser: /assets/images/media-library-wordpress.jpg
toc: true
breadcrumbs: true
---

Khi quản trị website, dung lượng của toàn bộ mã nguồn website của mình góp phần rất quan trọng vào việc vận hành website đó trong thời gian dài ở tương lai. Ví dụ như nếu tổng dung lượng website thấp, thì việc di chuyển website sang các server khác cũng dễ dàng hơn, hay việc backup dữ liệu cũng nhanh mà không phải gặp trở ngại. Còn ngược lại, dung lượng quá cao so với dung lượng thật sự của website sẽ gây rất nhiều khó khăn, nhất là việc backup sẽ vất vả hơn nhiều.

Trong bài này mình sẽ chia sẻ một chút về những việc cần biết và nên làm với website để tiết kiệm dung lượng mà vẫn đảm bảo không ảnh hưởng đến sự vận hành của website.

## Tối ưu hình ảnh trước khi upload

![media-library-wordpress](/assets/images/media-library-wordpress.jpg)WordPress có một trình quản lý hình ảnh mạnh mẽ và mình khuyến khích mọi người nên upload ảnh trực tiếp lên host của website để chúng ta tiện tái sử dụng hay quản lý, một mặt cũng giúp các hình ảnh của mình được đảm bảo hơn việc upload lên các dịch vụ lưu trữ hình ảnh khác.

Tuy nhiên không phải cứ hình ảnh nào chúng ta cũng upload lên website mà hầu như là cần phải tối ưu lại trước khi upload lên. Giả sử tấm ảnh của bạn có độ phân giải lên tới 2k, 3k (chiều rộng tối đa) nhưng thực chất người dùng trên website không cần như thế, bởi vì nếu chiều rộng nội dung trên website chỉ có 800px thì tấm ảnh của bạn cho dù là có nét đến mấy đi chăng nữa nhưng nó cũng chỉ hiển thị có 800px thôi và muốn xem full thì phải click vào, nhưng cái này chỉ dành cho những website cần ảnh phải chất lượng cao như website nhiếp ảnh, wallpaper. Với các website bán hàng thì ảnh cũng chỉ nên có chiều rộng tối đa là 1000px vì nhiêu đó là đủ để khách hàng xem sản phẩm rồi, nếu to quá thì website tải rất chậm và lúc đó mới thật sự là mất khách hơn là ảnh nhỏ.

**Tham khảo**: [Tối ưu hình ảnh cho website](http://sofsog.com/2016/09/25/toi-uu-hoa-hinh-anh-tren-wordpress-quan-tri-hinh-hanh-tren-website/)

Kế tiếp là đôi khi dung lượng hình ảnh lại quá cao so với chất lượng cần thiết của nó để hiển thị lên website. Do vậy trước khi upload bạn nên giảm dung lượng hình ảnh một cách hợp lý, giảm dung lượng đôi khi chất lượng hình ảnh sẽ khó mà nhận thấy sự khác nhau với mắt thường nên bạn không cần qua lo lắng. Bạn có thể cài plugin EWWW Image Optimizer, WP Smush hoặc chịu chơi hơn thì đầu tư $5/tháng sử dụng Kraken để hình ảnh tự tối ưu khi bạn upload lên website.

Và cuối cùng là hãy kiểm soát với các tập tin ảnh tự sinh ra của WordPress mà đôi khi chúng ta không cần dùng đến, về cách quản lý các ảnh tự sinh ra và xóa bớt ảnh không sử dụng bạn có thể xem bài viết [**quản trị hình ảnh trên WordPress toàn tập**](http://sofsog.com/2016/09/25/toi-uu-hoa-hinh-anh-tren-wordpress-quan-tri-hinh-hanh-tren-website/) của mình.

## Không nên lưu bản backup ở host

Backup dữ liệu website với mục đích là để phục hồi lại dữ liệu website của mình khi dữ liệu bị hỏng hoặc host hiện tại có vấn đề không thể truy cập được mà cần di chuyển dữ liệu website qua một host khác. Vậy khi đó chúng ta lưu bản backup trên chính host đang chạy website gần như là vô nghĩa mà vừa nguy hiểm lại tốn dung lượng của host.

Bạn nên lưu giữ các tập tin backup này ở những nơi thật sự an toàn như các dịch vụ lưu trữ đám mây như_Dropbox, Google Drive_ hay _Amazon S3_ (nên dùng) bởi vì máy tính của mình chưa chắc đã an toàn và ổn định hơn cái host của mình, còn các dịch vụ lớn kia là họ đã rất uy tín rồi và hầu như không thể gián đoạn.

Bạn đừng nghĩ là khi backup chúng ta sẽ tải bản backup về máy và upload lên lại các dịch vụ kia, tốn thời gian lắm. Bạn có thể sử dụng plugin BackWPUp hoặc BackupBuddy để backup và nó tự gửi lên các dịch vụ lưu trữ kia một cách nhanh nhất.

**Xem thêm**: [Hướng dẫn sử dụng BackWPUp](#).

## **Kiểm tra log lỗi và không nên log khi chưa cần thiết**

Ngoài backup ra thì các tập tin log lỗi hoặc log truy cập (access log) trên host là thủ phạm chính của nguyên nhân hao tốn tài nguyên của host. Đối với các log lỗi website, chúng ta đôi lúc không cần phải lưu log lại liên tục vì đâu phải lúc nào cũng cần xem log lỗi, mà chỉ khi debug để tìm lỗi hay vá lỗi thì sẽ cần bật lên. Nếu bạn không muốn webserver lưu log lỗi trong website thì đơn giản là thêm đoạn sau vào _wp-config.php_ (tốt nhất là cho lên đầu, bên dưới `<?php` ).

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">01</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="php functions">error_reporting</code><code class="php plain">(0);</code></div></div></td></tr></tbody></table>

Bên cạnh đó là hãy chắn chắc bạn đã thiết lập `WP_DEBUG` là `false` trong _wp-config.php_ để tắt chế độ debug. Và hãy xóa đi các tập tin _.log_ hay _error\_log_ trên host nếu có nhé.

Đối với access log thì chúng ta không thể tắt đi nếu dùng Shared Host, còn nếu dùng máy chủ riêng thì có thể tắt đi bằng cách xóa dòng khai báo access log trong tập tin thiết lập webserver.

## Kiểm tra thư mục wp-content

Có rất nhiều plugin lưu lại những dữ liệu không cần thiết trong thư mục wp-content như các tập tin log của plugin hay các tập tin lưu tạm. Tại thư mục wp-content, ngoại trừ thư mục cache và hình ảnh thì chúng ta không nên lưu gì thêm ở đây.

## Không nên lưu video hoặc các tập tin nén

Với những website có nhiều video thì tốt nhất bạn nên upload lên Youtube nếu không cần che giấu video của mình. Hoặc nếu video của bạn cần trả phí thành viên mới xem được thì càng không nên upload lên host chạy WordPress vì các player thông thường có thể dễ dàng download thông qua những phần mềm hỗ trợ như Internet Download Manager là ví dụ điển hình, thay vào đó bạn có thể sử dụng [Wistia](https://wistia.com/pricing) hoặc [SproutVideo](https://sproutvideo.com/pricing) để chống download.

Còn đối với các tập tin nén để người khác download thì bạn có thể upload lên các dịch vụ lưu trữ như Mega.co.nz, Fshare hay sang sơn là tìm một dịch vụ máy chủ giá rẻ nhưng có ổ cứng cao để upload và cho người dùng download ở đó.

## Tối ưu database

Database cũng sử dụng ổ cứng trên host để lưu nên có nghĩa là database bạn càng lớn thì càng tốn dung lượng lưu trữ nhiều hơn, và khi backup toàn bộ website thì nó sẽ lưu vào bản backup nên dung lượng sẽ rất lớn.

Bạn hãy chắc chắn là đã t[ối ưu bảng wp\_options của database](#) thật tốt để không chứa nhiều dữ liệu rác, bên cạnh đó bạn cũng nên [làm sạch thủ công database](#) định kỳ để dữ liệu mình được thông suốt hơn. Vì bạn để càng lâu thì database sẽ càng lớn và lúc đó lại rất khó tối ưu.

Nếu bạn dùng WooCommerce thì hãy kiểm tra bảng _wp\_options_ có lớn không, nếu có thì do nó chứa nhiều session và transient không còn sử dụng đến, hãy chạy các lệnh sau nhiều lần để dọn dẹp bớt.

DELETEFROM\`wp\_options\` WHERE\`option\_name\` LIKE('\_transient%') ORDERBY\`option\_id\` LIMIT 20000;
DELETEFROM\`wp\_options\` WHERE\`option\_name\` LIKE('\_wc\_session\_expires%') ORDERBY\`option\_id\` LIMIT 20000;

Nếu database của bạn lớn thì cần chạy lệnh này nhiều lần, bởi vì mình nên limit nó xóa mỗi lần 20000 dòng để tránh host bị đơ do MySQL xử lý quá nhiều.

Hiện tại database của thachpham.com là chính xác 32MB, mình chưa xóa bớt các dữ liệu không dùng đến trong wp\_postmeta nữa. Nói như vậy để bạn hiểu rằng WordPress không ăn nhiều database như bạn tưởng.

## Lời kết

Qua nội dung bài ở trên thì mình cũng đã thấy việc tối ưu dung lượng website thực chất không quá phức tạp như chúng ta nghĩ nhưng lợi ích của nó thì rất to lớn, bởi lẽ bạn chắc chắn sẽ không thể nào lưu trữ website trên cùng 1 host trong thời gian dài mà có thể sẽ cần chuyển đi nơi khác, và việc dữ liệu nhẹ sẽ giúp chúng ta làm các việc này nhanh và đơn giản hơn.

Vậy mã nguồn của thachpham.com có dung lượng bao nhiêu? Chính xác là 800MB chưa nén, nén lại dạng tar.gz còn được hơn 700MB.

Nguồn: Thạch Phạm Blog
