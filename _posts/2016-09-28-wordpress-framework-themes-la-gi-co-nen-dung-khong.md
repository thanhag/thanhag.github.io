---
title: "WordPress Framework Themes là gì? Có nên dùng không?"
date: "2016-09-28"
categories: 
  - "wordpress"
tags: 
  - "framework-themes"
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/genesis-logo.png
  teaser: /assets/images/genesis-logo.png
toc: true
breadcrumbs: true
---

Khái niệm **WordPress Themes** chắc ai cũng biết rồi, đơn giản dễ hiểu thì nó là một thành phần giao diện của WordPress. Còn Framework Themes chúng ta được hiểu là một cái khung sẵn hoặc một thư viện bao gồm nhiều tính năng để hình thành các theme con.

![genesis-logo](/assets/images/genesis-logo.png)

Về cơ bản, các Theme Framework đã được tối ưu hóa và dựng sẵn một cái khung để chúng ta thiết kế theme được nhanh chóng và thuận tiện hơn. Và nếu bạn là người mới tập thiết kế theme cho WordPress thì nên sử dụng những framework theme để chúng ta không cần viết lại những vòng lặp, hàm trong WordPress vào bản thiết kế mà chỉ cần làm việc với HTML và CSS để tùy biến màu sắc, bố cục cho theme.

### Những lợi ích khi sử dụng Framework Theme

- Tiết kiệm thời gian khi thiết kế theme cho WordPress. Không cần thông qua bước tạo các thành phần cho theme như single.php, header.php, sidebar.php và viết các vòng lặp.
- Các thẻ HTML và CSS được viết theo chuẩn thiết kế W3C.
- Học cách thiết kế một theme cho WordPress một cách nhanh nhất.
- Dễ dàng tùy biến thành nhiều loại theme khác nhau tùy thuộc vào khả năng sử dụng CSS, HTML và những thành phần liên quan tạo nên một theme nhờ sự linh hoạt của các lớp (class) giúp bạn dễ dàng tùy chỉnh các thuộc tính cho nó.
- Tối ưu hóa máy tìm kiếm (SEO).

Tương tự như một theme thông thường, theme framework có loại trả phí và miễn phí và chất lượng có thể sẽ nhỉnh hơn trong việc tùy biến và thư viện các theme con. Trong bài viết này, mình sẽ chỉ đề cập đến các theme framework miễn phí.

## Một số theme framework miễn phí tốt nhất

**Mới cập nhật**: [Danh sách Theme Framework miễn phí tốt nhất](http://sofsog.com/wordpress/theme-framework-mien-phi-tot-nhat "Tổng hợp Theme Framework miễn phí – Live Update").

## Cách tùy biến theme framework và tạo một child theme

Ở trên mình đã giới thiệu những framework theme tốt nhất dành cho WordPress. Nếu các bạn thích “chơi trội” thì có thể để luôn “bộ xương” để sử dụng mà không cần tùy biến thêm thắt gì cả  . Tuy nhiên nếu bạn muốn tùy biến nó thì ít nhất bạn phải biết cách tạo một child theme dành cho nó rồi sau đó chỉnh sửa trên child theme.

### Child theme là gì?

Hiểu đơn giản là một theme con dành cho một framework nào đó. Nó thừa hưởng tất cả các đặc tính và chức năng của theme framework và bạn có thể cải tiến nó hơn.

### Cách tạo một child theme

Thật ra tạo một child theme sẽ không có gì khó khăn cho lắm. Để tạo được một child theme thì trước tiên bạn cần upload một theme framework lên thư mục _wp-content/themes_. Và child theme của nó sẽ được thừa hưởng tất cả các đặc tính mà nó sở hữu như widget, shortcode, khuôn mẫu,..v.v…

Sau khi bạn đã upload một theme framework lên thư mục kể trên. Việc tiếp theo cần làm là tạo một thư mục riêng dành cho child theme trong thư mục _wp-content/themes_ (tức là nằm ngang hàng với các theme khác), sau đó tạo một file styles.css và chứa một số thông tin bắt buộc trong theme, ví dụ như sau:

/\*
Theme Name: Demo Child Theme
Theme URI: www.example.com
Description: Child theme đơn giản
Author: Sofsog
Author URI: Sofsog.com
Template: frameworkname
Version: 1.0
Tags: child theme
\*/

Nếu bạn đã từng khám phá các file style.css của các theme WordPress thì sẽ hiểu những thông tin trên là như thế nào. Tuy nhiên khác với các phần khai báo thông tin theme khác, các bạn sẽ thấy đoạn khai báo trên xuất hiện thêm thẻ `Template: frameworkname` để khai báo tên thư mục của framework. Ví dụ như sau:

Template: hybrid

Vậy là bạn đã có một child theme mang đầy đủ các đặc tính của framework và bạn có thể bắt đầu kích hoạt sử dụng nó. Tuy nhiên nó cũng chẳng khác gì framework theme ban đầu cả vì bạn chưa thêm một số thuộc tính CSS cho nó. Bạn có thể thêm các thuộc tính CSS cho child theme vào file style.css ở trên.

### Tùy biến child theme với Action và Filter

Action và Filter là hai tính năng chính để bạn có thể tùy biến giao diện child theme của các theme framework dễ dàng, ngoài ra nó cũng giúp bạn rất nhiều trong việc làm plugin.

**Cần xem**: [Hướng dẫn Action & Filter toàn tập](# "Action Hook và Filter Hook toàn tập")

##  Lời kết

Theme Framework mang lại rất nhiều ưu điểm và tiện lợi trong việc thiết kế một theme dành cho riêng mình. Tuy nhiên để khai thác tối đa những điểm mạnh đó yêu cầu bạn phải nắm rõ một số kiến thức nhất định về những vòng lặp và hàm của WordPress, hiểu khái niệm làm việc của chúng trong themes và tất nhiên sẽ bao gồm luôn một chút kiến thức về PHP và CSS.

Vì vậy khi bắt đầu làm quen với các theme framework, đừng vội vã tìm hiểu các tùy chỉnh nâng cao sử dụng hook mà chỉ nên tập trung vào phần tùy biến màu sắc và bố cục theme dựa vào CSS và HTML, sau đó đọc kỹ phần giới thiệu và hướng dẫn sử dụng các vòng lặp, hooks trong các framework theme để có thể nắm bắt được một số vòng lặp có sẵn của nó.

Nguồn: Thạch Phạm Blog
