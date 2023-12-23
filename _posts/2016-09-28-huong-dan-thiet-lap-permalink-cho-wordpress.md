---
title: "Hướng dẫn thiết lập Permalink cho WordPress"
date: "2016-09-28"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/Permalink.png
  teaser: /assets/images/Permalink.png
toc: true
breadcrumbs: true
---

Đây là nơi mà bạn sẽ bật tính năng đường dẫn tĩnh cho toàn bộ website thay vì sử dụng cấu trúc đường dẫn động. Đường dẫn tĩnh nghĩa là địa chỉ post, page, category, tag,…của bạn sẽ được biểu diễn bằng tên cụ thể chứ không phải dạng số.![permalink](/assets/images/Permalink.png)

- **Common Settings**: Các thiết lập thông dụng.
  - **Default**: Cấu trúc đường dẫn mặc định (đường dẫn động).
  - **Day and name**: cấu trúc đường dẫn với kiểu hiển thị đầy đủ ngày tháng đăng post và tên post.
  - **Month and name**: cấu trúc đường dẫn với kiểu hiển thị tháng, năm và tên post.
  - **Numeric**: Cấu trúc đường dẫn hiển thị ID của post thay vì tên.
  - **Post name**: Chỉ hiển thị tên post trên đường dẫn
  - **Custom Structure**: Tùy chỉnh cấu trúc đường dẫn tùy ý, xem thêm phần cuối bài viết.
- **Optional**: Các thiết lập tùy chọn không bắt buộc.
  - **Category base**: Tên đường dẫn mẹ của các đường dẫn tới trang category. Mặc định nó sẽ là <http://domain/category/tên-category/>, nếu bạn điền “chuyen-muc” vào đây thì nó sẽ hiển thị là <http://domain/chuyen-muc/tên-category>.
  - **Tag base**: Tên đường dẫn mẹ của đường dẫn tới các trang tag. Mặc định nó sẽ là <http://domain/tag/tên-tag/>, nếu bạn điền “the” vào đây thì nó sẽ hiển thị là <http://domain/the/tên-tag>.

### Nói thêm về Custom Structure

Nếu bạn chọn tùy chọn này, bạn có thể cấu trúc đường dẫn giống như bạn thích. Cấu trúc được xác định ở đây thông qua các từ khóa cấu trúc (được bọc bởi ký tự %), dưới đây là một số từ khóa cấu trúc:

- **%year%** – năm đăng post.
- **%monthnum%** – tháng đăng post.
- **%day%** – ngày đăng post.
- **%hour%** – giờ đăng post.
- **%minute%** – phút đăng post.
- **%second%** – giây đăng post.
- **%post\_id%** – số ID của post.
- **%postname%** – tên của post (được rút lại thành kiểu “tieu-de-bai-viet”).
- **%category%** – tên category của post (nếu bạn chọn 2 category, nó sẽ hiển thị 1 trong 2 và cố định).
- **%author%** – tên tác giả của post.

Ví dụ như kiểu đường dẫn post là <http://domain/tên-category/tên-post> thì mình sẽ điền ở phần Custom Structure là _/%category%/%postname%_.

#### Lỗi 404 khi thiết lập Permalink trên localhost

Nếu bạn đã bật permalink của website mà bị lỗi 404 ở localhost thì có thể localhost của bạn chưa bật mod\_rewrite của Apache.

Bạn hãy tìm mở file httpd.conf trong thư mục localhost (đối với XAMPP thì mở Control Panel của XAMPP -> Config -> httpd.conf) và tìm tất cả các thiết lập **AllowOverride None** đổi thành **AllowOverride All**. Sau đó Stop Apache và Start lại.

#### Lỗi 404 khi thiết lập permalink trên host

Nếu bạn đang dùng host thông thường mà bị lỗi 404 khi bật permalink lên thì có thể file .htaccess trong thư mục gốc của bạn trên host chưa có các thiết lập rewrite đường dẫn.

Bạn hãy vào host bằng FTP và mở file .htaccess ra (nếu chưa có thì tạo) và copy đoạn này vào:

\# BEGIN WordPress
<IfModule mod\_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\\.php$ - \[L\]
RewriteCond %{REQUEST\_FILENAME} !-f
RewriteCond %{REQUEST\_FILENAME} !-d
RewriteRule . /index.php \[L\]
</IfModule>

# END WordPress

Chúc các bạn thực hành thành công.
