---
title: "Hướng dẫn thay đổi font chữ tiêu đề bài viết trong Wordpress"
date: "2016-10-02"
categories: 
  - "wordpress"
tags: 
  - "doi-font-tieu-de"
  - "doi-font-worpresss"
  - "huong-dan-wordpress"
  - "sua-file-style-css"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/Sua-font3.png
  teaser: /assets/images/Sua-font3.png
toc: true
breadcrumbs: true
permalink: /thiet-ke-web/wordpress/huong-dan-thay-doi-font-chu-tieu-de-bai-viet-trong-wordpress
---

Đôi lúc khi cài đặt một theme đẹp nào đó về, thì lại phát hiện ra theme sử dụng những font chữ lạ, làm cho trang web của bạn hiển thị tiếng việt không đẹp, chữ không đều, bị lỗi, ....

Khi gặp trường hợp như vậy, giải pháp tốt nhất là các bạn thường tìm cách đổi font, đối với nội dung bài bài viết thì các bạn có thế đổi font bằng các Plugin như [Easy Google Fonts](https://wordpress.org/plugins/easy-google-fonts/ "Easy Google Font") hoặc [WP Google Fonts](https://wordpress.org/plugins/wp-google-fonts/) ... để đổi font.

Nhưng đối với tiêu đề bài viết hoặc menu, .... có thể sẽ không đổi được. Trường hợp này chỉ còn cách thay đổi trong file style.css của font. Cách làm cũng khá đơn giản, không cần các bạn phải biết code, mình sẽ hướng dẫn các bạn cách thay đổi font cho tiêu đề bài viết, thay đổi các thứ khác cũng tương tự.

Đầu tiên, bạn vào trang web của bạn trên trình duyệt Chrome (các trình duyệt khác cũng tương tự), vào chỗ nào hiện ra tiêu đề bị lỗi font, **click phải** vào vùng trống, chọn **kiểm tra** (hoặc phím tắt: Ctrl+shift+I).

![sua-font1](/assets/images/Sua-font1.png)

Bạn sẽ thấy phần code hiện ta, bạn lấy chột rà vào code vào click vào những tam giác màu đen cho đến khi tìm được phần bị lỗi font, xem hình:

![sua-font2](/assets/images/Sua-font2.png)

Bạn để ý thấy trước nội dung bị lỗi ở bên code có chữ class = "entry-title"

Tức là font bị lỗi nằm ở phần entry-title

Bạn dùng ftp hoặc vào host tải file **style.css** về chỉnh sửa(file này nằm trong thư mục ..../wp-content/themes/tên-theme-bạn-dang-dùng)

Bạn dùng chương chình Notepad hoặc nodepad++, hoặc dreamweaver ... để sửa, mình dùng dreamweaver, bạn Ctrl+F tìm chữ **entry-title**

![sua-font3](/assets/images/Sua-font3.png)

Nhìn hình trên bạn thấy font-family: 'Oswald', tức là font 'Oswald'  này là nguyên nhân gây lỗi mất thẩm mỹ tiếng việt trên web của bạn. (thực tế bạn tìm sẽ có một tên font khác)

Bạn tiếp tục Ctrl+F tìm chữ 'Oswald'  (Tên font bị lỗi của bạn) xem có chỗ nào sài font này nữa không, thường thì còn vài chỗ nữa.

Thay toàn bộ  'Oswald'  (Tên font bị lỗi của bạn) thành font khác mà bạn chắc chắn là sẽ không bị lỗi nữa ví dụ 'Roboto' (sửa thủ công hoặc dùng  chức năng Replace all). save file đã sửa này lại.

Cuối cùng up file **style.css (**đã chỉnh sửa) lên host (đè lên file cũ)

Xong, vào web xem lại (nhớ xóa bộ nhớ cache nếu site bạn có dùng cache) sẽ thấy kết quả.

![sua-font4](/assets/images/Sua-font4.png)

Chúc bạn thành công!
