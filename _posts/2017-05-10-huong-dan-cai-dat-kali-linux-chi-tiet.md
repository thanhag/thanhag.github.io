---
title: "Hướng dẫn cài đặt Kali Linux chi tiết"
date: "2017-05-10"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
tags: 
  - "huong-dan-cai-kali-linux"
  - "kali-linux"
  - "setup-kali-linux"
header:
  image: /assets/images/Huong-dan-cai-dat-Kali-limux-1.png
  teaser: /assets/images/Huong-dan-cai-dat-Kali-limux-1.png
toc: true
breadcrumbs: true
---

Trên mạng mình thấy có rất nhiều bài viết hướng dẫn rồi, tuy nhiên chưa sâu và đầy đủ. Sau đây mình sẽ hướng dẫn các bạn cái đặt Kali  Linux 2.0 (Kali Sana) một cách chi tiết nhất bằng hình ảnh. Cùng bắt đầu nào!

### Cấu hình cài tối thiểu

- Dung lượng trống ổ cứng tối thiểu là 8 GB
- CPU kiến ​​trúc i386 và amd64.
- Tối thiểu là 512MB RAM.

### Chuẩn bị cài đặt

– USB Boot Kali linux – Kết nối wifi hoặc Ethernet. (lưu ý là ghi số IP address của Modems mạng Wifi để khi có yêu cầu thì điền vào) – Điện thoại smartphone hoặc một máy tính khác: Để hỗ trợ nếu xảy ra lỗi hay quên quy trình cài đặt.

### CÀI ĐẶT KALI LINUX

#### **_Bước 1_. Đưa USB Boot vào máy và khởi động lên:**

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-973" src="images/Huong-dan-cai-dat-Kali-limux-1.png" alt="" width="638" height="479"></td></tr><tr><td class="tr-caption">Khởi động USB boot.</td></tr></tbody></table>

#### **_Bước 2_. Cấu hình cài đặt cơ bản:**

Chọn ngôn ngữ hiển thị.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img src="images/a2-1.png"></td></tr><tr><td class="tr-caption" style="text-align: center;">Lựa chọn ngôn ngữ.</td></tr></tbody></table>

Lựa chọn quốc gia của bạn.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-975" src="images/Huong-dan-cai-dat-Kali-limux-3.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Lựa chọn quốc gia.</td></tr></tbody></table>

Loại bàn phím các bạn mặc định sẽ chọn _American English_.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-976" src="images/Huong-dan-cai-dat-Kali-limux-4.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Lựa chọn bàn phím.</td></tr></tbody></table>

Sau đó đợi khoảng một phút để cài đặt các thành phần từ CD-ROM. Nếu bạn bị lỗi ở bước này. [Xem bài Sửa lỗi “Detect and mount CD-ROM”.](http://sofsog.com/thu-thuat-chung/fix-loi-detect-and-mount-cd-rom)

 **_Bước 3_. Cấu hình Kali Linux:**

 Điền hostname cho Kali Linux. Điền vào _thekalitools_.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-977" src="images/Huong-dan-cai-dat-Kali-limux-5.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Điền hostname.</td></tr></tbody></table>

Phần điền domain cho Kali Linux có thể bỏ trống. Mật khẩu cho tài khoản root.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-978" src="images/Huong-dan-cai-dat-Kali-limux-6.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Điền mật khẩu.</td></tr></tbody></table>

Lựa chọn múi giờ của bạn. Chọn _Eastern_.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-979" src="images/Huong-dan-cai-dat-Kali-limux-7.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Lựa chọn múi giờ.</td></tr></tbody></table>

#### **_Bước 4_. Lựa chọn phân vùng cài đặt:**

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-980" src="images/Huong-dan-cai-dat-Kali-limux-8.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Lựa chọn phân vùng cài đặt.</td></tr></tbody></table>

Đến bước này ta sẽ có 2 sự lựa chọn, một là để Kali Linux **Tự động phân vùng cài đặt (Guided – use entire disk)**, hai là ta sẽ **Phân vùng thủ công (Manual)**.

**PHÂN VÙNG TỰ ĐỘNG**

<table class="tr-caption-container" style="height: 733px; width: 1026px;" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td style="width: 1030px;"><img class="aligncenter size-full wp-image-981" src="images/Huong-dan-cai-dat-Kali-limux-9.jpg" alt="" width="1600" height="1050"></td></tr><tr><td class="tr-caption" style="width: 1030px; text-align: center;">Tự động phân vùng cài đặt.</td></tr></tbody></table>

**_Lưu ý_:** Phân vùng tự động có thể làm mất các phân vùng khác dẫn đến mất dữ liệu **PHÂN VÙNG THỦ CÔNG** Ở đây mình xin chia ra làm 4 bước nhỏ nữa để dễ cho các bạn theo dõi.

**_Bước 4a. Tạo phân vùng trống (FREE SPACE)._** Ở ví dụ dưới là ổ cứng mới hoàn toàn nhé. Có thể bạn sẽ không cần qua bước này!

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter wp-image-982" src="images/Huong-dan-cai-dat-Kali-limux-10.jpg" alt="" width="805" height="264"></td></tr><tr><td class="tr-caption" style="text-align: center;">Tạo phân vùng trống</td></tr></tbody></table>

_**Bước 4b. Tạo phân vùng hệ thống /-root (ext4)**_ Đầu tiên chọn vào phần _FREE SPACE_ rồi chọn _Continue_.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr style="height: 527.188px;"><td style="height: 527.188px;"><img class="aligncenter size-full wp-image-983" src="images/Huong-dan-cai-dat-Kali-limux-11.png" alt="" width="800" height="525"></td></tr><tr style="height: 27px;"><td class="tr-caption" style="height: 27px; text-align: center;">Tạo phân vùng hệ thống.</td></tr></tbody></table>

Chọn Tạo phân vùng mới – Create a new partition.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-984" src="images/Huong-dan-cai-dat-Kali-limux-12.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Create a new partition.</td></tr></tbody></table>

Điền vào dung lượng hệ thống bạn muốn tạo. **_Lưu ý_**: chừa dung lượng để tạo phân vùng swap linux (bằng lượng ram).

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-985" src="images/Huong-dan-cai-dat-Kali-limux-13.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Điền dung lượng hệ thống.</td></tr></tbody></table>

Lựa chọn loại phân vùng là _Primary_.

Chọn vị trí phân vùng, chọn Trước (_Beginning –_ **nên chọn**) hoặc Sau (_End_).

Dòng Use as: chọn như hình

Dòng Mount point: cũng chọn dấu / như hình

Hoàn thành cài đặt tạo phân vùng hệ thống, chọn _Done setting up the partition_.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-986" src="images/Huong-dan-cai-dat-Kali-limux-14.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Done setting up the partition.</td></tr></tbody></table>

_**Bước 4c. Tạo phân vùng swap cho Kali Linux (swap).**_

Phân vùng này có tác dụng khi linux dùng hết ram hiện có thì sẽ sử dụng swap này để làm ram (theo mình biết là vậy) Chọn vào phần _FREE SPACE_ và nhấn _Continue_ để bắt đầu tạo phân vùng.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-987" src="images/Huong-dan-cai-dat-Kali-limux-15.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Tạo phân vùng swap.</td></tr></tbody></table>

Điền vào dung lượng dùng tạo phân vùng swap.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-988" src="images/Huong-dan-cai-dat-Kali-limux-16.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Điền dung lượng swap.</td></tr></tbody></table>

Chọn loại phân vùng là _Logical_.

 Tiếp theo ta cần chỉ định đây là phân vùng swap. Chọn vào _Use as:_ ấn _Continue_.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-989" src="images/Huong-dan-cai-dat-Kali-limux-17.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Chỉ định là phân vùng swap.</td></tr></tbody></table>

Chọn _swap area_ và ấn _Continue_.

 Hoàn thành cài đặt phân vùng swap, chọn _Done setting up the partition_.

![](/assets/images/a12.14-copy.png)

_**Bước 4d. Lưu phân vùng.**_

<table class="tr-caption-container" style="height: 422px;" width="812" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td style="width: 808px;"><img class="aligncenter size-full wp-image-992" src="images/Huong-dan-cai-dat-Kali-limux-18.jpg" alt="" width="1600" height="525"></td></tr><tr><td class="tr-caption" style="width: 808px; text-align: center;">Lưu phân vùng.</td></tr></tbody></table>

#### **_Bước 5_. Đợi cài đặt Kali Linux:**

Như vậy đến đây là bạn đã cấu hình xong hết, tiếp theo chỉ cần đợi quá trình cài đặt hoàn thành. Thông thường bước này mất khoảng 30 phút, vì vậy các bạn hãy mở youtube trên smartphone và coi một tập phim đi nhé ????

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-medium wp-image-997" src="images/Huong-dan-cai-dat-Kali-limux-223.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Loading… quá trình cài đặt Kali Linux.</td></tr></tbody></table>

#### **_Bước 6_. Cấu hình mạng:**

Ở phần _Use a network mirror_ chọn _Yes_ để trình cài đặt tìm mirror gần nhất với bạn. Nếu bạn chọn _No_ thì các package sẽ được tải và cài đặt từ repositories mặc định của trình cài đặt.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-994" src="images/Huong-dan-cai-dat-Kali-limux-20.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">Network Mirror</td></tr></tbody></table>

Tiếp theo, phần Cấu hình _HTTP Proxy_, bỏ trống nếu không sử dụng.

 Kết thúc quá trình cấu hình mạng là đợi một lát hoàn tất cấu hình.

 **_Bước 7_. GRUB Boot loader:**

Bước đến đây, các bạn chọn Yes nếu muốn cài đặt GRUB boot, và chọn ổ cứng muốn cài đặt.

<table class="tr-caption-container" style="height: 298px;" width="817" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td style="width: 813px;"><img class="aligncenter size-full wp-image-995" src="images/Huong-dan-cai-dat-Kali-limux-21.jpg" alt="" width="1600" height="525"></td></tr><tr><td class="tr-caption" style="width: 813px; text-align: center;">Cấu hình GRUB boot loader.</td></tr></tbody></table>

#### **_Bước 8_. Hoàn thành quá trình cài đặt:**

Đợi thêm một tý để xong quá trình cài boot. Đến đây, nếu bạn thấy màn hình này hiện lên, có nghĩa là quá trình cài đặt đã thành công tuyệt đối.

<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center"><tbody><tr><td><img class="aligncenter size-full wp-image-996" src="images/Huong-dan-cai-dat-Kali-limux-22.png" alt="" width="800" height="525"></td></tr><tr><td class="tr-caption" style="text-align: center;">CÀI ĐẶT THÀNH CÔNG</td></tr></tbody></table>

Tiếp theo, trình cài đặt sẽ tự động xoá Live và các mục rác trong lúc cài đặt. Và khởi động lại máy.

Nguồn: thekalitools.com
