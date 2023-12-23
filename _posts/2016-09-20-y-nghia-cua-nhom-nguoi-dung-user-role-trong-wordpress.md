---
title: "Ý nghĩa của nhóm người dùng (User Role) trong Wordpress"
date: "2016-09-20"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "user-role"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/User-group.png
  teaser: /assets/images/User-group.png
toc: true
breadcrumbs: true
---

Như lúc tạo thêm người dùng bạn đã thấy, phần **Role** cho phép bạn chọn một trong năm nhóm người dùng là**Subscriber**, **Contributor**, **Author**, **Editor**, **Administrator**. Vậy ý nghĩa của các nhóm này là gì, quyền đặc trưng của từng nhóm ra sao? Mình sẽ giải thích trọn vẹn ở bài này để bạn hiểu rõ nhất vai trò của từng nhóm người dùng.

![user-group](/assets/images/User-group.png)

### Tổng quan vai trò của từng nhóm

Tuy là bạn thấy WordPress có 5 nhóm người dùng trong lúc tạo người dùng mới, nhưng thực ra nếu tính đầy đủ thì mặc định WordPress sẽ có tất cả là 6 nhóm người dùng, bao gồm:

- **Super Admin** – Nhóm người dùng cao nhất và có quyền quản trị toàn bộ hệ thống vì thực ra WordPress có tính năng tạo một mạng website nội bộ tên là WordPress MultiUser. Ngoài ra, Super Admin có quyền xóa các người dùng trong nhóm Administrator.
- **Administrator** – Nhóm người dùng có quyền sử dụng toàn bộ các tính năng có trong một website WordPress, không bao gồm các website khác trong mạng website nội bộ.
- **Editor** – Nhóm này có quyền đăng bài viết lên website (publish) và quản lý các post khác của những người dùng khác.
- **Author** – Nhóm này sẽ có quyền đăng bài lên website và quản lý các post của họ.
- **Contributor** – Nhóm này sẽ có quyền viết bài mới nhưng không được phép đăng lên mà chỉ có thể gửi để xét duyệt (Save as Review) và quản lý post của họ.
- **Subscriber** – Người dùng trong nhóm này chỉ có thể quản lý thông tin cá nhân của họ.

### Chi tiết vai trò của từng nhóm

Nếu chỉ giải thích bằng vài chữ như trên thì có thể bạn hiểu vai trò của mỗi nhóm, nhưng bạn có biết rằng mỗi quyền trong WordPress đều được biểu diễn bằng chữ kiểu “_quyen\_han_”, tức là chữ được viết thường và có dấu “\_” để ngăn cách. Lý do mình cần các bạn hiểu cái này đó là về sau khi dùng plugin để tùy biến quyền của nhóm người dùng, nên tốt nhất bạn nên xem qua để hiểu chi tiết từng quyền của mỗi nhóm người dùng.

Dưới đây là bảng chi tiết quyền hạn của từng nhóm người dùng mà mình chôm chỉa tại trang hướng dẫn của WordPress.

| Tên quyền | Super Admin | Administrator | Editor | Author | Contributor | Subscriber |
| --- | --- | --- | --- | --- | --- | --- |
| manage\_network | Y |  |  |  |  |  |
| manage\_sites | Y |  |  |  |  |  |
| manage\_network\_users | Y |  |  |  |  |  |
| manage\_network\_plugins | Y |  |  |  |  |  |
| manage\_network\_themes | Y |  |  |  |  |  |
| manage\_network\_options | Y |  |  |  |  |  |
| unfiltered\_html | Y |  |  |  |  |  |
| Tên quyền | Super Admin | Administrator | Editor | Author | Contributor | Subscriber |
| activate\_plugins | Y | Y |  |  |  |  |
| create\_users | Y | Y (single site) |  |  |  |  |
| delete\_plugins | Y | Y |  |  |  |  |
| delete\_themes | Y | Y (single site) |  |  |  |  |
| delete\_users | Y | Y |  |  |  |  |
| edit\_files | Y | Y |  |  |  |  |
| edit\_plugins | Y | Y (single site) |  |  |  |  |
| edit\_theme\_options | Y | Y |  |  |  |  |
| edit\_themes | Y | Y (single site) |  |  |  |  |
| edit\_users | Y | Y (single site) |  |  |  |  |
| export | Y | Y |  |  |  |  |
| import | Y | Y |  |  |  |  |
| Tên quyền | Super Admin | Administrator | Editor | Author | Contributor | Subscriber |
| install\_plugins | Y | Y (single site) |  |  |  |  |
| install\_themes | Y | Y (single site) |  |  |  |  |
| list\_users | Y | Y |  |  |  |  |
| manage\_options | Y | Y |  |  |  |  |
| promote\_users | Y | Y |  |  |  |  |
| remove\_users | Y | Y |  |  |  |  |
| switch\_themes | Y | Y |  |  |  |  |
| update\_core | Y | Y (single site) |  |  |  |  |
| update\_plugins | Y | Y (single site) |  |  |  |  |
| update\_themes | Y | Y (single site) |  |  |  |  |
| edit\_dashboard | Y | Y |  |  |  |  |
| Tên quyền | Super Admin | Administrator | Editor | Author | Contributor | Subscriber |
| moderate\_comments | Y | Y | Y |  |  |  |
| manage\_categories | Y | Y | Y |  |  |  |
| manage\_links | Y | Y | Y |  |  |  |
| edit\_others\_posts | Y | Y | Y |  |  |  |
| edit\_pages | Y | Y | Y |  |  |  |
| edit\_others\_pages | Y | Y | Y |  |  |  |
| edit\_published\_pages | Y | Y | Y |  |  |  |
| publish\_pages | Y | Y | Y |  |  |  |
| delete\_pages | Y | Y | Y |  |  |  |
| delete\_others\_pages | Y | Y | Y |  |  |  |
| delete\_published\_pages | Y | Y | Y |  |  |  |
| delete\_others\_posts | Y | Y | Y |  |  |  |
| delete\_private\_posts | Y | Y | Y |  |  |  |
| edit\_private\_posts | Y | Y | Y |  |  |  |
| read\_private\_posts | Y | Y | Y |  |  |  |
| delete\_private\_pages | Y | Y | Y |  |  |  |
| edit\_private\_pages | Y | Y | Y |  |  |  |
| read\_private\_pages | Y | Y | Y |  |  |  |
| Tên quyền | Super Admin | Administrator | Editor | Author | Contributor | Subscriber |
| edit\_published\_posts | Y | Y | Y | Y |  |  |
| upload\_files | Y | Y | Y | Y |  |  |
| publish\_posts | Y | Y | Y | Y |  |  |
| delete\_published\_posts | Y | Y | Y | Y |  |  |
| edit\_posts | Y | Y | Y | Y | Y |  |
| delete\_posts | Y | Y | Y | Y | Y |  |
| read | Y | Y | Y | Y | Y | Y |
| Tên quyền | Super Admin | Administrator | Editor | Author | Contributor | Subscriber |

### Cấp độ nhóm người dùng

Ngoài việc biểu diễn quyền hạn thông qua cái bảng ở trên, WordPress còn sử dụng một hệ thống cấp độ từ 01 đến 10 để biểu diễn quyền hạn của từng nhóm người dùng. Mặc dù bạn có thể sẽ thấy một số plugin có cho phép bạn chỉnh quyền theo thang cấp độ này nhưng tại thời điểm này trở đi, bạn không cần quan tâm nữa vì tính năng này đã được xóa bỏ khỏi WordPress từ phiên bản 3.0 vì quá dư thừa.

Ở bài tiếp theo, mình sẽ hướng dẫn các bạn cách sử dụng một plugin tên Advanced Access Manager để quản lý và phân quyền lại các nhóm người dùng, đồng thời có thể tạo ra một nhóm người dùng mới nếu bạn có nhu cầu.

Nguồn: Thạch phạm Blog
