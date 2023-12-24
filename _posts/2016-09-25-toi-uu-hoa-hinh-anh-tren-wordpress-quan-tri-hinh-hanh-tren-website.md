---
title: "Tối ưu hóa hình ảnh trên WordPress (Quản trị hình hảnh trên website wordpress)"
date: "2016-09-25"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "image-cleanup"
  - "wordpress"
  - "wordpress-co-ban"
header:
  
  teaser: /assets/images/Cleanup.png
toc: true
breadcrumbs: true
---

Việc lưu trữ và quản lý các file hình ảnh có trên website không phải là một vấn đề lớn đối với bạn nếu website bạn chỉ có số lượng vài trăm tấm ảnh. Thế nhưng đợi đến lúc bạn tự nhận ra mình phải bắt tay vào việc tối ưu lại hình ảnh, tìm cách quản lý nó thì chắc cũng trễ rồi, dĩ nhiên lúc đó bạn sẽ cực hơn rất nhiều.

Do đó, để giúp cho những người mới hiểu hơn về tính năng Media Library trên WordPress thì mình xin viết một bài đầy đủ về những gì bạn cần biết liên quan đến việc quản lý hình ảnh trên website.

### I. Kiểm soát các size ảnh có trên website

#### 1.1) Tìm hiểu size ảnh

Trong WordPress, để tối ưu hình ảnh hiển thị thì nó có hỗ trợ chức năng tự động cắt một tấm ảnh ra nhiều size khác nhau, dĩ nhiên mỗi size ảnh sẽ là một tấm ảnh.

Mặc định WordPress có 3 size ảnh như thế này:

![toi-uu-hinh-anh-tren-web-1](/assets/images/toi-uu-hinh-anh-tren-web-1.png)

Và điều này có nghĩa là một tấm ảnh sẽ có 4 files khác nhau. Hãy cùng mở thư mục **/wp-content/uploads** ra mà xem nhé.

![toi-uu-hinh-anh-tren-web-2](/assets/images/toi-uu-hinh-anh-tren-web-2.png)

Thế nó sinh ra thì nó sẽ được sử dụng như thế nào?

Mặc định WordPress có 3 size hình ảnh được tao ra bởi hàm `add_image_size()` với 3 key là:

- _thumbnail_
- _medium_
- _large_

Nếu trong theme có hàm gọi file media tương ứng với tên size hoặc số size của nó thì nó sẽ tự được lôi ra, chẳng hạn như họ muốn lôi ảnh với size dạng thumbnail thì là:

the\_post\_thumbnail( 'thumbnail' );

Ngoài ra khi chèn ảnh vào bài, bạn cũng có thể lựa chọn size cần chèn để tránh chèn các ảnh to qua làm bài viết tải lâu hơn.

![wpmedia-insertmedia-3](/assets/images/wpmedia-insertmedia-3.png)

Nhìn chung chức năng này có một ưu điểm là khiến website bạn hiển thị ảnh gọn hơn, load nhẹ hơn.

#### 1.2) Xóa size ảnh

Nhưng nó có một nhược điểm là về lâu dài khi nó tự sinh ra quá nhiều ảnh thì nó sẽ làm bạn tốn nhiều dung lượng ổ cứng hơn.

Vậy thì **làm sao để WordPress không sinh thêm ảnh** ra nữa? Cách đơn giản nhất là bạn hãy vào **Settings -> Media** và đưa tất cả các thông số về 0 như trong ảnh dưới.

![wpmedia-resetsize-4](/assets/images/wpmedia-resetsize-4.png)

Đưa các tham số về 0 để tắt tự động sinh ra ảnh.

Nhưng không chỉ dừng lại ở đó. Nếu bạn có cài thêm một số plugin mà trong đó họ có khai báo một size ảnh mới thì nó sẽ tiếp tục tạo ảnh ra, chẳng hạn như plugin _NextGen Gallery_, _Yet Another Related Posts_,…Vậy làm thế nào để ngăn chặn chúng không sinh thêm size ảnh nữa? Đó là hãy [cài plugin](http://thachpham.com/wordpress/wordpress-tutorials/tim-va-cai-plugin.html) [AJAX Thumbnail Rebuild](https://wordpress.org/plugins/ajax-thumbnail-rebuild/ "AJAX Thumbnail Rebuild plugin").

Sau đó bạn truy cập vào phần **Tools -> Rebuild Thumbnail** là bạn sẽ thấy danh sách các key size ảnh đang có trên website là các ký tự in nghiêng.

![wpmedia-allimagesize-5](/assets/images/wpmedia-allimagesize-5.png)

Bạn chèn đoạn code sau vào file [functions.php trong theme](http://thachpham.com/wordpress/wordpress-development/huong-dan-file-function.html) để vô hiệu hóa nó.

function remove\_unused\_image\_size( $sizes) {

   unset( $sizes\['thumbnail'\]);
   unset( $sizes\['medium'\]);
   unset( $sizes\['large'\]);
   unset( $sizes\['post-thumbnail'\]);
   unset( $sizes\['twentyfourteen-full-width'\]
);
   return $sizes;
}
add\_filter('intermediate\_image\_sizes\_advanced', 'remove\_unused\_image\_size');

Nhớ thay đổi lại tên key của size ảnh cho phù hợp với bạn và mỗi size là một dòng unset nhé. Kể từ bây giờ khi bạn upload ảnh lên thì nó sẽ không tự cắt ra các size mà bạn đã xóa nữa.

Thế khi xóa size ảnh rồi thì các file ảnh cũ của size đó có được xóa không? Câu trả lời đơn giản là không, nhưng bạn có thể xóa nó. Hãy xem tiếp phần 1.3.

#### 1.3) Xóa các ảnh không sử dụng

![cleanup](/assets/images/Cleanup.png)

Ảnh không sử dụng ở đây nghĩa là file ảnh đó không được đính kèm vào bài viết nào cả. Để xóa các ảnh đó, bạn có thể sử dụng plugin miễn phí **[Image Cleanup](https://wordpress.org/plugins/image-cleanup/ "Image Cleanup plugin")**.

Cách sử dụng plugin Image Cleanup bạn có thể tham khảo ở [bài này](http://thachpham.com/wordpress/wp-plugin/xoa-bot-anh-khong-su-dung.html "Xóa bớt ảnh không sử dụng trong WordPress").

### II. Tạo gallery ảnh trên WordPress

Mặc định WordPress không chỉ cho phép bạn chèn từng tấm ảnh vào bài mà còn hỗ trợ bạn tạo cho nó một gallery riêng – nghĩa là sẽ hiển thị nhiều hình ảnh cùng lúc trong bài viết.

Để tạo Gallery, bạn ấn vào nút Add Media trên khung soạn thảo và chọn Create Gallery, sau đó chọn các tấm ảnh cần thêm vào gallery và ấn nút Create New Gallery.

![wpmedia-creategallery-6](/assets/images/wpmedia-creategallery-6.png)

Sau khi tạo gallery, bạn có thể thay đổi thứ tự hình ảnh và ấn nút Insert Gallery phía dưới là xong. Sau khi chèn gallery vào bài thì ảnh sẽ hiển thị theo dạng thế này.

![wpmedia-previewgallery-7](/assets/images/wpmedia-previewgallery-7.png)

Hình ảnh hiển thị dạng grid.

Nếu bạn muốn có thêm hiệu ứng click vào sẽ mở hình ảnh với size lớn bằng popup thì cài thêm plugin[Responsive Lightbox](https://wordpress.org/plugins/responsive-lightbox).

Nhưng gallery này chỉ là dạng cơ bản mà thôi, nếu bạn muốn chèn gallery chuyên nghiệp với nhiều tùy chọn hơn như hiển thị slide thì bạn nên dùng plugin NextGen Gallery mà mình đã [hướng dẫn tại đây](http://sofsog.com/2016/09/25/tao-gallery-anh-trong-wordpress-voi-plugin-nextgen-gallery/ "Tạo gallery ảnh đẹp với plugin Nextgen Gallery").

### III. Tối ưu dung lượng hình ảnh

Hình ảnh trên web có thể sẽ có dung lượng và chất lượng ảnh vượt quá nhu cầu sử dụng của bạn mà trong khi đó bạn có thể giảm dung lượng hình ảnh xuống mà không bị mất đi chất lượng ảnh.

Để làm việc đó hoàn toàn tự động, bạn cần cài plugin **[EWWW Image Optimizer](https://wordpress.org/plugins/ewww-image-optimizer/ "Ewww Image Optimizer")** hoàn toàn miễn phí và có hỗ trợ giảm dung lượng ảnh hàng loạt, đồng thời khi bạn upload ảnh lên bài thì nó cũng sẽ tự giảm dung lượng luôn.

![wpmedia-optimizeimage-8](/assets/images/wpmedia-optimizeimage-8.jpg)

Cái hay của plugin này đó là có hỗ trợ nén ảnh thông qua dịch vụ Cloud của họ nếu host của bạn yếu không thể nén ảnh được. Khi sử dụng tính năng cloud, bạn cần phải trả một số tiền nhỏ hàng tháng nhưng bù lại tài nguyên của máy chủ sẽ không bị tiêu hao mỗi lần nén.

### IV. Sửa ảnh trực tiếp trên WordPress

Trong WordPress có rất nhiều tính năng giúp bạn sửa ảnh trực tiếp ngay trên website mà có thể nhiều người đã bỏ qua. Để sử dụng chức năng này, bạn vào Media -> chọn một tấm ảnh bất kỳ và ấn Edit.

Tại đây bạn có thể đảo chiều ảnh, crop ảnh hoặc thay đổi kích thước của ảnh.

![wpmedia-editimage-9](/assets/images/wpmedia-editimage-9.jpg)

Sau khi sửa xong và save lại, WordPress sẽ tự động xuất ra một tấm ảnh là kết quả sau khi chỉnh sửa.

### V. Tăng tốc thời gian load ảnh với cache

Hình ảnh đa phần trên website sẽ không cần chỉnh sửa mà chỉ upload lên hoặc xóa đi, nên tốt nhất là bạn nên thiết lập cache trình duyệt cho các file ảnh để khách truy cập vào website nhanh hơn ở lần truy cập thứ 2 trở đi do cache đã được lưu trong máy tính ở quãng thời gian nhất định.

Để làm việc này trên host, bạn mở file .htaccess ở thư mục gốc website ra và chèn đoạn dưới đây vào:

<FilesMatch "(?i)^.\*\\.(ico|flv|jpg|jpeg|png|gif|js|css|woff)$">
ExpiresActive On
ExpiresDefault A2592000
</FilesMatch>

Số 2592000 nghĩa là số giây sẽ được lưu lại trong cache của trình duyệt và nó sẽ tự làm mới sau quãng thời gian này. Bạn có thể đặt một con số khác lâu hơn.

### Lời kết

Đó là những kinh nghiệm của mình trong việc tối ưu hóa quy trình quản lý và sử dụng hình ảnh trên website WordPress và hy vọng nó cũng sẽ có ích cho bạn. Hãy nhớ rằng mặc dù lưu hình ảnh trên host sẽ làm bạn tốn băng thông và dung lượng hơn nhưng nó lại an toàn cho bạn thay vì sử dụng các liên kết hình ảnh trỏ ra bên ngoài vì không ai biết được các ảnh đó có bị gì sau này hay không. Hơn nữa, các cấu hình hosting hiện đại bây giờ đều thừa khả năng để cung cấp dung lượng và băng thông cho một số lượng hình ảnh khá lớn nên bạn không cần lo lắng.

Nguồn: Thạch Phạm Blog
