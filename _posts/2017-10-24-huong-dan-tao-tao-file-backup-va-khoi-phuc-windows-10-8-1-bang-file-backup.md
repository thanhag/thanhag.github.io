---
title: "Hướng dẫn tạo tạo file backup và khôi phục windows 10, 8.1 bằng file backup"
date: "2017-10-24"
categories: 
  - "he-dieu-hanh"
  - "thu-thuat-chung"
  - "window-10"
tags: 
  - "8-1-bang-file-backup"
  - "ghost-win-10"
  - "ghost-windows-10"
  - "he-dieu-hanh"
  - "huong-dan-tao-tao-file-backup-va-khoi-phuc-windows-10"
  - "khoi-phuc-win-10"
  - "khoi-phuc-windown-10"
  - "thu-thuat-chung"
header:
  image: /assets/images/huong-dan-tao-file-backup-win-10.jpg
  teaser: /assets/images/huong-dan-tao-file-backup-win-10.jpg
toc: true
breadcrumbs: true
---

 Ghost là cách nhiều người chọn để tạo bản backup windows và phục hồi lại khi máy tính bị trục trặc với nhiều cách khác nhau như sử dụng đĩa ghost, onekey ghost... Mỗi cách đều có ưu điểm riêng, tuy nhiên trên windows 8.1 10 thì bạn có thể dễ dàng tạo 1 bản "ghost" bằng chức năng tương tự gọi là System image backup.System image backup sẽ giúp bạn tạo 1 bản backup cho phân vùng windows hiện tại và có thể dễ dàng phục hồi lại khi máy bị sự cố vào được hoặc không vào được windows.

## **1\. Tạo bản backup cho windown 10, 8.1:**

Trước tiên các bạn vào **My Computer** --> **Open Control Panel.**

![Hướng dẫn tạo tạo file backup và khôi phục windows 10](/assets/images/Hướng-dẫn-tạo-tạo-file-backup-và-khôi-phục-windows-10.jpg)

Chọn **File History**, nếu để dạng icon lớn thì các bạn vào **Control Panel** --> **System and Security** --> **File History** để chọn chức năng này

![huong dan tao file backup win 10](/assets/images/huong-dan-tao-file-backup-win-10.jpg)

 Tiếp tục chọn **System Image Backup** ở góc trái phía dưới

![Hướng dẫn tạo tạo file backup và khôi phục windows 10 2](/assets/images/Hướng-dẫn-tạo-tạo-file-backup-và-khôi-phục-windows-10-2.jpg)

Chọn tiếp **Create a system image**

Chọn ổ đĩa mà bạn muốn lưu file backup sau đó nhấn **Next**

![Hướng dẫn tạo tạo file backup và khôi phục windows 10 3](/assets/images/Hướng-dẫn-tạo-tạo-file-backup-và-khôi-phục-windows-10-3.jpg)

Tại cửa sổ này windows sẽ hiển thị thêm việc tạo file backup cho ổ đĩa nào, các bạn chỉ cần để mặc định là các ổ đĩa hệ thống và nhấn **Next**

![Hướng dẫn tạo tạo file backup và khôi phục windows 10](/assets/images/Hướng-dẫn-tạo-tạo-file-backup-và-khôi-phục-windows-10-1.jpg)

Một cửa sổ Xác nhận thông tin việc tạo file backup ví dụ ở đây mình tạo file backup sẽ mất 37GB tại ổ F. Chọn **Start Backup** để bắt đầu

![Hướng dẫn tạo tạo file backup và khôi phục windows 10](/assets/images/Hướng-dẫn-tạo-tạo-file-backup-và-khôi-phục-windows-10-5.jpg)

Quá trình backup sẽ diễn ra khoảng 5 -10 phút tùy theo máy và dữ liệu

## **2\. Phục hồi lại phân vùng vừa backup** **trực tiếp từ windows**

Tương tự việc tạo bản ghost, để phục hồi lại phân vùng windows đã tạo các bạn sẽ có 2 cách, 1 là khi máy tính vẫn vào được windows và 2 là khi bị lỗi không vào được.

Trường hợp thứ nhất là khi máy tính vào được thì tương tự việc tạo bạn chọn **Recovery**

![Hướng dẫn tạo tạo file backup và khôi phục windows 10-2](/assets/images/Hướng-dẫn-tạo-tạo-file-backup-và-khôi-phục-windows-10-2-1.jpg)

Tiếp tục chọn **Open System Restore**

Check vào phần **Show more restore points** và chọn bản **System Image Restore Point** mà bạn muốn phục hồi

![Hướng dẫn tạo tạo file backup và khôi phục windows 10-3](/assets/images/Hướng-dẫn-tạo-tạo-file-backup-và-khôi-phục-windows-10-3-1.jpg)

Một cửa sổ xác nhận việc phục hồi xuất hiện, các bạn lưu ý là việc phù hồi này sẽ **trả lại trạng thái của ổ đĩa hệ thống lúc bạn tạo file backup** tất cả các file dữ liệu. Nên **nếu có dữ liệu mới các bạn phải tiến hành copy sang các ổ đĩa khác để tránh việc mất dữ liệu.**

 Sau khi chọn **Finish** máy tính sẽ **restart** lại và việc phục hồi sẽ được tiến hành, các bạn đợi cho tới khi hoàn thành.

## **3\. Phục hồi lại máy tính khi không vào được windows**

Để phục hồi được **bản backup** đã tạo khi windows bị hỏng nặng không vào được thì bạn cần có 1 USB boot hoặc đĩa DVD cài windows. Tiến hành cài đặt bình thường tới cửa sổ **Install** --> chọn **Repair your windows**

![khoi phuc may tinh khi khong vao duoc window](/assets/images/khoi-phuc-may-tinh-khi-khong-vao-duoc-window.png)

Tiếp tục chọn **Troubleshoot**

![khoi phuc may tinh khi khong vao duoc window](/assets/images/khoi-phuc-may-tinh-khi-khong-vao-duoc-window-2.jpg)

**Advanced Options**

![khoi phuc may tinh khi khong vao duoc window](/assets/images/khoi-phuc-may-tinh-khi-khong-vao-duoc-window-3.jpg)

**System Image Recovery**

![khoi phuc may tinh khi khong vao duoc window](/assets/images/khoi-phuc-may-tinh-khi-khong-vao-duoc-window-4.jpg)

Sau một vài bước xác nhận các bạn sẽ có thể dễ dàng phục hồi lại windows đã backup

![khoi phuc may tinh khi khong vao duoc window](/assets/images/khoi-phuc-may-tinh-khi-khong-vao-duoc-window-5.jpg)

Hy vọng bài viết sẽ giúp ích cho các bạn
