---
title: "Hướng dẫn tắt bàn phím ảo tự động mở trên Windows 10"
date: "2017-10-24"
categories: 
  - "he-dieu-hanh"
  - "thu-thuat-chung"
  - "window-10"
tags: 
  - "he-dieu-hanh"
  - "huong-dan-tat-ban-phim-ao-tu-dong-mo-tren-windows-10"
  - "keyboard"
  - "on-screen-keyboard"
  - "osk"
  - "thu-thuat-chung"
  - "tu-khoi-dong-ban-phim-ao"
  - "vo-hieu-ban-phim-ao"
  - "windows-10"
header:
  image: /assets/images/3841305_Cach_sua_loi_one_screen_keyboard_xuat_hien_Windows_10.jpg
  teaser: /assets/images/3841305_Cach_sua_loi_one_screen_keyboard_xuat_hien_Windows_10.jpg
toc: true
breadcrumbs: true
---

Việc bàn phím ảo (On-Screen Keyboard) liên tục xuất hiện mỗi khi bạn khởi động máy tính, và mỗi lần như vậy bạn phải tắt nó đi thủ công rất phiền phức. Mình sẽ hướng dẫn cách tắt nó hoàn toàn luôn:

##  **Cách 1:**

- Bạn vào ô search ở thanh taskbar, gõ chữ “**Control Panel**”, gõ Enter.
- Trong cửa sổ mới xuất hiện, bạn vào **Ease of Access > Ease of Access Center > Use the computer without a mouse or keyboard**
- Bỏ chọn ô “**Use On-Screen Keyboard**” đi.
- Click **Apply** > **OK** và khởi động (**restart**) lại máy là xong.

Ở lần khởi động kế tiếp, bạn sẽ thấy là bàn phím ảo không còn popup lên nữa, và trong trường hợp bạn cần xài thì nó vẫn có thể được chạy lên bình thường từ Start Menu.

![Cach_sua_loi_one_screen_keyboard_xuat_hien_Windows_10.jpg](/assets/images/3841305_Cach_sua_loi_one_screen_keyboard_xuat_hien_Windows_10.jpg "Bấm vào để phóng to.")

Nếu vẫn còn bị, chuyển sang cách 2.

## **Cách 2:**

- Trên màn hình **Start** hoặc trong **Menu Start**, gõ **Services.msc** và nhấn **Enter**.
- Cửa sổ **Services Management Console** sẽ mở ra. Xác định vị trí dịch vụ **Touch Keyboard and Handwriting Panel Service**.

[![](/assets/images/Touch-Keyboard-Service.png)](https://sofsog.com/wp-content/uploads/2017/10/Touch-Keyboard-Service-1.png)

- Nhấp đúp chuột vào dịch vụ đó. Trong hộp thoại **Touch Keyboard and Handwriting Panel Service**, tìm đến mục **Startup type** và chọn tùy chọn **Disabled** để vô hiệu hóa Touch Keyboard.
- Nhấn **OK**.

## **Cách 3: Chỉnh sửa trong Registry**

- Nhấn tổ hợp Windows+R hoặc click Start -> Run rồi nhập vào đó: **regedit**

![Tắt bàn phím ảo trên Windows 7](/assets/images/ban-phim-ao-windows-7-3.jpg "Tắt bàn phím ảo trên Windows 7")

- Sau đó nhấn Enter để mở cửa sổ **Registry Editor**.
- Bạn duyệt theo đường dẫn sau: HKEY\_CURRENT\_USER\\Software\\Microsoft\\Windows NT\\Current Version\\Accessibility

![Tắt bàn phím ảo trên Windows 7](/assets/images/ban-phim-ao-windows-7-4.jpg "Tắt bàn phím ảo trên Windows 7")

- Nhìn sang khung bên phải, click đúp chuột trái vào **Configuration** hoặc click phải rồi chọn **Modify**. Xóa chữ **osk** tại mục **Value data**. Sau đó nhấn **OK** để áp dụng.

![Tắt bàn phím ảo trên Windows 7](/assets/images/ban-phim-ao-windows-7-5.jpg "Tắt bàn phím ảo trên Windows 7")

- Đóng cửa sổ **Registry Editor**, khởi động lại máy tính để kiểm tra

**Lời kết:**

Mình từng bị lỗi này, tắt bằng cách 1 vẫn không được, sử dụng cách 2 thì được, tuy nhiên, cách này sẽ vô hiệu hóa luôn các tính năng nhận dạng chữ viết trên windows luôn, cho nên các bạn hãy cân nhắc khi sử dụng.
