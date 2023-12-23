---
title: "Fix lỗi Detect and mount CD-ROM"
date: "2017-05-14"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
tags: 
  - "detect-and-mount-cd-rom"
  - "fix-loi"
  - "kali-linux"
  - "linux"
  - "sua-loi"
  - "thu-thuat"
header:
  image: /assets/images/kali-error.gif
  teaser: /assets/images/kali-error.gif
toc: true
breadcrumbs: true
---

Chào các bạn.

Trong quá trình cài đặt Kali Linux bằng USB, chắc hẳn có nhiều bạn bị vướng ở cái lỗi "**Detect and mount CD-ROM**". Cái này là do nó không tìm đc CD-ROM trên máy của bạn. Với các máy có ổ CD thì không sao nhưng nếu máy không có ổ CD hay laptop không có kèm ổ CD thì biết làm sao bây giờ??

![](/assets/images/kali-error.gif)

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-1035" src="images/13595968_842771769188470_671592470_n.jpg" alt="" width="768" height="576"></td></tr><tr><td class="tr-caption">Lỗi "Detect and mount CD-ROM" - Ảnh:</td></tr></tbody></table>

**Your installation CD-ROM couldn't be mounted. This probably means that the CD-ROM was not in the drive. If so you can insert it and try again.** _Try again to muont the CD-ROM?_ <Yes>                                <No>

### Phương án 1

Cách fix lỗi này rất đơn giản. Bạn chỉ cần rút USB ra tầm 3-4s rồi cắm lại rồi chọn **Yes** rồi nhấn **Continue** là quá trình cài đặt sẽ tiếp tục :)

### Phương án 2

![](/assets/images/mountcdrom-pic3-1.jpg)

Nếu các trên vẫn chưa được, bạn sẽ được chuyển ra Main Menu, từ đây hãy chọn dòng **Execute a shell**, gõ lệnh mount vào /cdrom:

#  mount -t vfat /dev/sdb1 /cdrom

Ở trên, USB của mình (và thông thường) là sdb hoặc sdb1 tùy trường hợp, các bạn thay lại thành tên ổ USB của bạn nhé của bạn nhé! (buốn biết ổ boot của bạn là ổ nào các bạn gõ lệnh mount rồi enter, để ý /**dev/...** , chỗ 3 chấm đó chính là ổ cần đánh ở lệnh mount -t vfat /dev/sdb1 /cdrom) Chúc các bạn thành công.

_Nguồn: TheKaliTools.Com_
