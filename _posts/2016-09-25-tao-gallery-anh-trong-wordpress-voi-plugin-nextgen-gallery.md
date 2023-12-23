---
title: "Tạo gallery ảnh trong wordpress với plugin Nextgen Gallery"
date: "2016-09-25"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "nextgen-gallery"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/nextgen-logo.png
  teaser: /assets/images/nextgen-logo.png
toc: true
breadcrumbs: true
---

Mặc dù trong WordPress đã tích hợp sẵn tính năng chèn gallery bằng cách ấn vào nút Add Media trong khung soạn thảo, nhưng nhược điểm của nó là không phải theme nào cũng hỗ trợ phần đó, hơn nữa cách hiển thị gallery mặc định cũng không được chuyên nghiệp và khó quản lý.

Nếu bạn đang cần tìm một giải pháp nhúng gallery ảnh vào bài chuyên nghiệp, dễ quản lý, dễ tùy biến thì bạn nên tìm đến plugin **NextGen Gallery** rất lâu đời và nổi tiếng này.

![nextgen-logo](/assets/images/nextgen-logo.png)

[Tải plugin](http://wordpress.org/plugins/nextgen-gallery/ "Tải plugin NextGen Gallery") [Xem demo](http://www.nextgen-gallery.com/demos-of-all-nextgen-gallery-types/ "Demo NextGen Gallery")

### Giới thiệu NextGen Gallery

NextGen Gallery là một plugin khá lâu đời rồi và hiện nay họ vẫn phát triển rất mạnh mẽ, cập nhật thường xuyên. Nó được sử dụng nhiều không chỉ vì có nhiều tính năng nổi bật mà còn hỗ trợ rất nhiều add-on khác nhau mà bạn có thể tìm bằng cách gõ chữ NextGen Gallery trong thư viện plugin WordPress.

Plugin bao gồm những tính năng chính đó là tải nhiều ảnh lên gallery cùng lúc (có hỗ trợ dạng file .zip), hiển thị gallery vào bài theo nhiều kiểu khác nhau.

Plugin này hiện có hai bản là miễn phí và trả phí, bản trả phí bạn sẽ có thêm nhiều hiệu ứng hiển thị ảnh chuyên nghiệp hơn mà bạn có thể tìm hiểu thêm [tại đây](http://www.nextgen-gallery.com/nextgen-pro/ "NextGen Gallery Pro").

### Cách sử dụng NextGen Gallery

Ngay sau khi cài đặt xong plugin, bạn sẽ thấy menu tên là Gallery hiển thị trong admin như thế này:

![nextgen-gallery-menu-1](/assets/images/nextgen-gallery-menu-1.jpg)

Điều bạn cần xem đầu tiên đó là ấn vào mục **Other Options** để xem và thiết lập các cài đặt trước khi tải ảnh lên nhé. Trong mục đó ta có như sau:

![nextgen-gallery-other-options-2](/assets/images/nextgen-gallery-other-options-2.jpg)

Trang tùy chỉnh Other Options của NextGen Gallery

Ở trang này, bạn sẽ xem được đường dẫn thư mục lưu ảnh trong Gallery tại phần _Where would you like galleries stored?_ hoặc nếu bạn muốn nó tự thu nhỏ ảnh lại thì ấn vào nút Yes tại phần _Automatically resize images after upload_ và chỉnh size ảnh cần thu nhỏ phía dưới.

Ở mục Thumbnail Options là bạn sẽ thiết lập lại thông số kích cỡ hình ảnh ở định dạng thumbnail, mình nghĩ số đẹp nhất là 200 x 150. Nhưng bạn thiết lập sao mà bạn thích là được.

### Cách tạo Gallery và up ảnh vào Gallery

Nếu bạn chưa có Gallery nào thì để tạo Gallery bạn vào Gallery -> Add Gallery / Images. Sau đó chọn Create new Gallery và đặt tên cho gallery, cuối cùng là ấn Add Files để đưa ảnh từ máy tính lên.

![nextgen-gallery-add-gallery-3](/assets/images/nextgen-gallery-add-gallery-3.jpg)

Tạo gallery mới

Sau khi thêm ảnh xong thì ấn nút Start Upload để bắt đầu đưa ảnh lên máy chủ.

![nextgen-gallery-upload-4](/assets/images/nextgen-gallery-upload-4.jpg)

Bắt đầu upload ảnh lên gallery

Sau khi upload thành công thì bạn vào phần Manage Galleries sẽ thấy danh sách các gallery đã tạo kèm theo thống kê có bao nhiêu ảnh trong gallery đó.

### Chèn gallery vào post/page

Mặc dù NextGen Gallery đã hỗ trợ nút chèn gallery vào bài từ lâu nhưng mình không hiểu được tại sao mà mình vừa thử với phiên bản WordPress mới nhất ở theme mặc định thì nó không hoạt động. Nên ở đây mình hướng dẫn cách chèn gallery bằng shortcode cho nó lành.

Để chèn Gallery vào bài thì bạn có thể sử dụng shortcode sau, **nhớ xóa khoảng trắng** đi nhé.

\[ngg\_images gallery\_ids="1" display\_type="photocrati-nextgen\_basic\_thumbnails" \]

Bạn sửa số ID thành số ID của Gallery mà bạn cần chèn nhé. Còn tham số display\_type là kiểu gallery bạn muốn hiển thị, bạn có thể xem danh sách các kiểu gallery theo dạng shortcode [**tại đây**](http://www.nextgen-gallery.com/nextgen-gallery-shortcodes/ "NextGen Gallery Shortcode").

Kết quả ta đã có:

![show-nextgen-gallery-5](/assets/images/show-nextgen-gallery-5.jpg)

Hiển thị gallery vào bài

Thế là xong rồi đấy, bạn có thể chọn nhiều kiểu hiển thị khác.

### Một số addon hay dành cho NextGen Gallery

Xem toàn bộ danh sách [**tại đây**](http://www.nextgen-gallery.com/nextgen-gallery-extension-plugins/ "Danh sách addons dành cho NextGen Gallery").

### Một số tips khi sử dụng NextGen

- Bạn có thể thêm watermark vào ảnh tại Gallery -> Other Options -> Watermark.
- Bạn có thể thêm ảnh nhanh vào gallery đã có bằng cách up chồng vào hoặc upload ảnh vào thư mục có sẵn bằng FTP.
- Sử dụng Albums và Tags để quản lý Gallery hiệu quả nếu bạn có nhiều Gallery khác nhau.

Đó là những gì mình muốn nói qua plugin này. Nhìn chung, tuy là miễn phí nhưng NextGen Gallery đã làm tốt vai trò của nó là việc chèn nhiều hình ảnh vào WordPress nhanh chóng và hiển thị đúng kiểu gallery mặc dù bản miễn phí còn có ít hiệu ứng.

Nguồn: Thạch Phạm Blog
