---
title: "Xóa ảnh không sử dụng trong wordpress bằng Plugin Image Cleanup"
date: "2016-09-25"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "image-cleanup"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/Cleanup.png
  teaser: /assets/images/Cleanup.png
toc: true
breadcrumbs: true
---

Có một nhược điểm khó chịu là nếu bạn chỉnh size ảnh trong Settings -> Media, hoặc để mặc định thì mỗi khi upload ảnh lên bài viết thì nó sẽ tự tạo ra nhiều size ảnh khác nhau cho tấm ảnh đó để phục vụ nhu cầu sử dụng. Điều này có ưu điểm là nếu bạn sử dụng thumbnail cho bài viết, thì nó sẽ lấy ảnh size nhỏ ra hiển thị để đỡ mất thời gian tải ảnh lớn.

Thế nhưng các size ảnh khác như Medium, Large không sử dụng đến hoặc bất kỳ size nào tự sinh ra khi cài plugin thì sao? Bạn có thể vào thư mục uploads trên host mà tự xóa đi nhưng như thế thật là thảm họa nếu bạn có nhiều thư mục ảnh khác nhau. Vậy thì ở đây chúng ta sẽ có giải pháp là sử dụng plugin [Image Cleanup](https://wordpress.org/plugins/image-cleanup/).

### Chức năng chính của Image Cleanup

Công việc của nó chính là hỗ trợ bạn xóa toàn bộ các ảnh không sử dụng trong bài viết (chưa được attachment) hoặc hỗ trợ bạn đưa tất cả bọn nó ra một thư mục khác và hỗ trợ khôi phục lại nếu bạn thấy cần đống ảnh dư thừa đó.

### Cách sử dụng

Khi cài plugin xong, bạn vào phần **Tools -> Image Cleanup** để sử dụng nó.

Tại đây bạn sẽ thấy nó hiển thị ra như sau:

![image-cleanup-dashboard](/assets/images/image-cleanup-dashboard.jpg)

Như dấu mũi tên, phần màu đỏ chính là số lượng ảnh mà bạn không hề sử dụng đến trong bài. Hãy ấn chọn nó để xem chi tiết hình ảnh. Tốt hơn hết, hãy ấn vào nút Index Images để nó tiến hành quét lại lần cuối cùng để có thống kê chính xác hơn.

Danh sách chi tiết các ảnh không sử dụng là như thế này:

![image-cleanup-unused](/assets/images/image-cleanup-unused.jpg)

Nếu bạn muốn xóa nó toàn bộ, chỉ cần ấn chọn tất cả và chọn công cụ **Delete** ở phần **Bulk Actions** và ấn nút Apply là được. Nếu bạn có nhiều ảnh thì có thể bạn sẽ cần làm trên nhiều trang vì mỗi trang nó chỉ hiển thị 100 tấm mà thôi.

Còn nếu bạn không muốn xóa, thì có thể chọn tùy chọn **Move File** để đưa nó vào một thư mục khác để quản lý.

Lưu ý: Nếu hình ảnh chưa được attach vô bài nào mà chỉ sử dụng **featured images** thì nó sẽ xem như là ảnh không được sử dụng cho bài nào, và nó sẽ bị xóa.

### Xóa toàn bộ ảnh thumbnail bằng lệnh Linux

Nếu bạn đang chạy website trên máy chủ Linux mà bạn có thể truy cập vô SSH để dùng lệnh, hoặc đang làm website trên máy Linux thì có thể sử dụng lệnh sau để xóa toàn bộ ảnh có tên là abc-123-\*x\*.\*.

$ find . | grep "w\*\[0-9\]x\[0-9\].\[png|gif|jpg\]\*" | xargs rm -f

Yên tâm là nếu bạn đặt tên ảnh kiểu `tên-file-01.jpg` đều không bị ảnh hưởng.

Nguồn: Thạch Phạm Blog
