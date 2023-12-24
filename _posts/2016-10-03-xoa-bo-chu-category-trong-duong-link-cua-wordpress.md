---
title: "Xóa bỏ chữ category trong đường link của Wordpress"
date: "2016-10-03"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "seo"
  - "wordpress"
  - "wordpress-co-ban"
  - "xoa-bo-chu-category"
header:
  image: /assets/images/xoa-bo-chu-category-trong-duong-link-cua-wordpress.png
  teaser: /assets/images/xoa-bo-chu-category-trong-duong-link-cua-wordpress.png
toc: true
breadcrumbs: true
---

Nhằm chống lại sự dài dòng của đường link category trong WordPress, mà mặc định nó là `“home/category/name/”` thì tôi đang dùng một custom code để làm việc này, tuy nhiên các bạn cũng hoàn toàn có thể làm được điều tương tự với một plugin của WordPress. Khoan hãy nhắc tới plugin đó, giờ ta bàn lý do tại sao chúng ta nên xóa nó:

![Xóa bỏ chữ Categogy trong đường link của wordpress](/assets/images/xoa-bo-chu-category-trong-duong-link-cua-wordpress.png)

Xóa Category Base ra khỏi đường dẫn của WordPress

Trước hết, dưới góc độ của một người làm seo như tôi thì đường link càng dài tôi càng ghét, đúng hơn là càng sâu thì càng không có lợi, vì [Google](http://www.jamviet.com/tag/google "Google") nó sợ các đường link bẫy con bọ của nó, ví dụ như các đường link sâu /home/a/b/c/d/Random/ thì nó vừa mất thời gian lại tốn công sức, vì thế càng sâu thì nó càng thận trọng, nên càng gần đầu và càng nông càng tốt.

Lý do thứ hai là bạn ghét nó, thế thôi ! Nhiều khi cảm thấy thừa thãi !

### Cài đặt

Trên [WordPress Plugin Directory](http://wordpress.org/extend/plugins/ "WordPress Plugin Directory") có khá nhiều plugin có thể trợ giúp bạn trong việc xóa Category Base trong đường dẫn, các bạn có thể tham khảo:

1\. Remove Category Base: <https://wordpress.org/plugins/remove-category-url/>

2\. WP no category Base: <https://wordpress.org/plugins/wp-no-category-base/>

Cả hai cái đều làm việc dưới một nguyên tắc là xóa đoạn /category/ trong rewrite tag, làm cho WordPress hiểu đường dẫn category chỉ có /category-name/ thôi.

### Sử dụng plugin Yoast SEO

Plugin [Yoast SEO](http://sofsog.com/wordpress/huong-dan-cai-dat-va-cau-hinh-plugin-yoast-seo-vao-wordpress-wordpress-seo-by-yoast) rất thân thuộc với chúng ta, gần đây đã cung cấp chức năng này trong plugin, các bạn có thể kích hoạt nó lên bằng cách:

Truy cập [SEO](http://sofsog.com/tag/seo) > Advance > Permalinks và bật nút xóa chữ Category đi:

![Bật xóa chữ Category trong đường link](/assets/images/remove_categorylink.jpg)

Bật xóa chữ Category trong đường link

\* Lưu ý là để điều chỉnh lại đường dẫn không có category base trong Menu hoặc trong toàn bộ link trên trang, ta dùng hàm hack sau cho vào trong file functions.php nhé:

```php
/* xóa đường link của category */

function\_nice_category_link($link) {
    return str_replace('/category/', '/' , $link);
}

add_filter('category_link', '_nice_category_link');
```

Và bây giờ thử truy cập đường link của Category và thưởng thức thành quả mới nào !

Chúc các bạn thành công !

Nguồn: jamviet
