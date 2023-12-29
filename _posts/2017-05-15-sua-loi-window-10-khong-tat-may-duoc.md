---
title: "Sửa lỗi Window 10 không tắt máy được"
date: "2017-05-15"
categories: 
  - "he-dieu-hanh"
  - "thu-thuat-chung"
  - "window-10"
tags: 
  - "fix-loi-khong-shutdown"
  - "sua-loi-khong-tat-may"
  - "thu-thuat"
  - "thu-thuat-chung"
  - "win-10-khong-tat-may"
  - "window-10"
  - "window-10-khong-shutdown"
header:
  overlay_image: /assets/images/Turn-on-fast-startup-recommended.png
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)" 
  teaser: /assets/images/Turn-on-fast-startup-recommended.png
toc: true
breadcrumbs: true
---

### 1\. Nguyên nhân gây ra lỗi

Nguyên nhân gây ra lỗi này có thể là do:

- Driver không chuẩn.
- Có 1 hoặc nhiều **Process**, **Service** nào đó vẫn đang chạy ngầm, do đó dẫn đến hiện tượng màn hình thì tắt nhưng máy tính vẫn đang chạy.
- Máy tính bị nhiễm Malware.

2\. Một số cách sửa lỗi không tắt máy tính trên Windows 10

### 1\. Giải pháp 1

Có thể Microsoft đã nhầm lẫn khi kích hoạt tính năng Fast Bootup trong Power Option, và đây vô tình lại là nguyên nhân chính dẫn đến hiện tượng lỗi trên.

Để khắc phục lỗi không tắt máy tính trên Windows 10, bạn có thể thực hiện theo các bước dưới đây:

**Bước 1:**

Mở ứng dụng Settings bằng cách click biểu tượng **Windows**, sau đó tìm và click vào ứng dụng **Settings.**

Hoặc cách khác là nhấn tổ hợp phím Windows + I để mở ứng dụng Settings.

![ứng dụng Settings](/assets/images/setting-windows-10.png "ứng dụng Settings")

**Bước 2:**

Trên cửa sổ Settings, click chọn **System.**

**![chọn System](/assets/images/system-1.png "chọn System")**

**Bước 3:**

Trên cửa sổ System, nhìn sang khung bên trái tìm tùy chọn **Power & sleep**. Tiếp theo nhìn sang khung bên phải tìm và click chọn link **Additional power settings**.

![click chọn link Additional power settings](/assets/images/Power-and-sleep-1.png "click chọn link Additional power settings")

**Bước 4:**

Lúc này trên màn hình sẽ xuất hiện cửa sổ có tên Power Options. Tại đây bạn tìm và click chọn link **Choose what the power buttons** **do** ở khung bên trái như hình dưới đây.

![ chọn link Choose what the power buttons do](/assets/images/Choose-what-the-power-buttons-do-1.png " chọn link Choose what the power buttons do")

**Bước 5:**

Tiếp theo tìm và click chọn link **Change settings that are currently unavailable** như hình dưới đây:

![chọn link Change settings that are currently unavailable ](/assets/images/Change-settings-that-are-currently-unavailable.png "chọn link Change settings that are currently unavailable ")

**Bước 6:**

Lúc này tùy chọn Shutdown settings không còn màu xám nữa, bạn tiến hành bỏ tích mục **Turns on fast startup (recommended)** đi, sau đó click chọn **Save changes** để lưu lại thay đổi.

![ bỏ tích mục Turns on fast startup (recommended) ](/assets/images/Turn-on-fast-startup-recommended.png " bỏ tích mục Turns on fast startup (recommended) ")

Cuối cùng thử tắt máy tính Windows 10 của bạn xem lỗi đã đựơc khắc phục hay chưa.

### 2\. Giải pháp 2

**Bước 1:**

Kích chuột phải vào biểu tượng Windows ở góc dưới cùng bên trái, sau đó click chọn **Command Prompt (Admin)** để mở cửa sổ Command Prompt.

![ chọn Command Prompt (Admin)](/assets/images/command-prompt-admin.png " chọn Command Prompt (Admin)")

**Bước 2:**

Trên cửa sổ Command Prompt, sao chép và dán dòng lệnh dưới đây vào rồi nhấn Enter:

> shutdown /s /f /t 0

![Nhập lệnh](/assets/images/lenh.png "Nhập lệnh")

Ngay lập tức laptop Windows 10 của bạn sẽ tự động tắt.

### 3\. Giải pháp 3

Nếu đã áp dụng các giải pháp trên mà vẫn không thể khắc phục được lỗi, khi đó bạn có thể áp dụng một số giải pháp dưới đây để khắc phục lỗi:

\- Mở Task Manager để kiểm tra xem có process hoặc services không mong muốn nào đang chạy hay không. Mở Task Manager bằng cách nhấn tổ hợp phím **Ctrl + Shift + Esc**.

\- Nguyên nhân không tắt được laptop, máy tính Windows 10 của bạn có thể là do bạn mới cài đặt driver hoặc phần mềm nào đó. Trường hợp này hãy thử gỡ bỏ cài đặt driver hoặc phần mềm đó đi và kiểm tra xem máy tính, laptop windows 10 của bạn đã tắt được hay chưa.

\- Sử dụng phần mềm diệt virus để quét máy tính của bạn. Rất có thể nguyên nhân gây ra lỗi là do Malware.

Nguồn: Quantrimang.com
