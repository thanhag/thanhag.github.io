---
title: "Hướng dẫn cài đặt  Ubuntu từ ổ cứng không cần USB CD/DVD"
date: "2017-05-10"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "ubuntu"
tags: 
  - "cai-he-dieu-hanh"
  - "cai-ubuntu-khong-can-usb"
  - "he-dieu-hanh"
  - "kali-linux"
  - "linux"
  - "ubuntu"
header:
  image: /assets/images/Ubuntu.png
  teaser: /assets/images/Ubuntu.png
toc: true
breadcrumbs: true
---

 

![](/assets/images/Ubuntu.png)

**Giới thiệu qua hệ điều hành Ubuntu , Linux:** Linux , ubuntu là hệ điều hành mã nguồn mở, sử dụng hoàn toàn miễn phí trên máy tính PC lẫn Laptop. hệ điều hành này sử dụng rất mượt mà ở những máy tính có cấu hình không cao có ram 2GB trở xuống, rất thích hợp cho việc giải trí, xem phim, nghe nhạc, học hành, lập trình code, dân văn phòng...Ngoài ra, nếu bạn là dân mê game như Windows thì đừng mơ đến với hệ điều hành Linux/ubuntu, bởi vì linux/ubuntu không hỗ trợ đầy đủ game như Windows, và rất ít nhà phát triển game hỗ trợ cho hệ điều hành Ubuntu này.**Đi vào chủ đề chính cách cài đặt Ubuntu trên ổ cứng không cần đĩa hay USB:** **Chuẩn bị:** - Một phần mềm Minitool partition wizard để tạo thêm 1 phân vùng chứa boot Ubuntu với định dạng Fat32 có dung lượng là 4GB trở xuống. - File ISO Ubuntu bất kỳ. - UltralSO - Công cụ BOOTICE Bạn có thể tải link này bao gồm công cụ có sẵn dạng Portable, UltralSo Portable, Boottice portable, và công cụ test khả năng boot ổ cứng, usb boot.

[Link Drive](https://drive.google.com/open?id=0B3FpmWUmd-t4Wm5jLWs5amRjTG8)

\----------------------------------------

**Cách làm: Bước 1**: Hãy sử dụng phần mềm **Minitool partition wizard** để tạo thêm 1 phân vùng 4GB định dạng Fat32 đặt với tên Ubuntu cho nhớ. hoặc bạn có thể tạo phân vùng bằng công cụ disk Management có sẵn trong Windows cũng được. **Bước 2:** Tải boot về sau đó mount file iso vào ổ ảo UltralSO sau đó copy toàn bộ vào phân vùng 4GB định dạng Fat32 mà bạn đã tạo trước đó. [Link file Iso](https://drive.google.com/open?id=0B3FpmWUmd-t4V2FuVUpENTNiaG8)

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/0000.png "0000")

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/000.png "000")

Hãy Copy toàn bộ vào phân vùng 4GB mà bạn đã tạo trên ổ cứng trước đó nhé

**Bước 3:** Truy cập vào phân vùng 4GB đó hãy copy file ISO Ubuntu vào mục ISO

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/116.png "11(6)")

**Bước 4:** Sau đó hãy click phải chuột vào file iso ubuntu và đổi tên thành **ubuntu** là xong.

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/221.png "22(1)")

**Bước 5:** Hình như chưa boot được, ta phải dùng công cụ

BootICE để nạp khả năng boot cho phân vùng này.Hãy chạy công cụ BootICE lên và chọn ổ cứng hdd mục đầu tiên sau đó nhấp chọn**Process MBR**

![](/assets/images/vforum.vn-252077-w2fuqfn.png)

**Bước 6:** Tiếp theo hãy tích chọn Mục Windows NT 5.x / 6.x MBR và sau đó nhấn **Install / config** --> Nếu bạn đang dùng Win XP thì chọn Windows NT 5.x MBR, nếu dùng Win 7 trở lên thì chọn **Windows NT 6.x MBR.**

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/333.png "333")Cuối cùng máy bạn có thể boot được vào Ubuntu như giao diện. ------------------------------------------- Mục 4: Boot Linux ISO để boot thẳng vào Ubuntu để cài đặt Hoặc chọn mục 5: **Boot Grub2**Ở đây mình chọn mục 5:

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/143.png "1(43)")

Chọn Boot ISO Linux

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/228.png "2(28)")Cuối cùng là chọn Ubuntu.iso để bắt đầu khởi động vào môi trường Ubuntu để trải nghiệm thử và cài đặt trong đó luôn.

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/323.png "3(23)")

Ấn Install ubuntu để cài đặt

![Hướng dẫn cài đặt Ubuntu/Linux trên ổ cứng không cần USB hay đĩa CD/DVD](/assets/images/screenshot-from-2016-06-10-09-18-26.png "screenshot from 2016 06 10 09 18 26")

Đến đây các bạn có thể tự cài đặt.

Chú ý nếu bạn cài đặt song song với windows thì hãy chú ý đến dữ liệu tránh bị mất khi cài đặt nhầm nhé

Nguồn: <http://vforum.vn>
