---
title: "Hướng dẫn cài đặt phần mềm trên kali linux"
date: "2022-08-17"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
tags: 
  - "cai-dat-phan-mem"
  - "he-dieu-hanh"
  - "huong-dan-cai-dat-phan-mem-tren-kali-linux"
  - "kali-linux"
  - "linux"
  - "thu-thuat-chung"
header:
  teaser: /assets/images/installsoftwarelinux-pic0.png
toc: true
breadcrumbs: true

permalink: /thu-thuat-chung/huong-dan-cai-dat-phan-mem-tren-kali-linux
---

Không giống như Windows, trên Kali Linux và các phiên bản GNU/Linux khác có rất nhiều cách cài đặt phần mềm với các dạng file khác nhau, chúng ta cùng nhau tìm hiểu nào!


![Cài phần mềm trên linux](/assets/images/installsoftwarelinux-pic0.png)

## Quản lý phần mềm bằng Apt

**Apt (Advanced Packaging Tool)** là phần mềm hệ thống để quản lý các ứng dụng trên Kali Linux, cũng như các hệ điêu hành GNU/Linux khác. Kho ứng dụng khổng lồ của được thống kê từ trang Ubuntu Apps. Tuy nhiên các lệnh từ apt chỉ có thể chạy dưới quyền **SuperUser**. Để cài đặt gói phần mềm qua Apt ta sử dụng lệnh:

```bash
apt-get install <package>
```

_**Lưu ý**: package là tên gói bạn muốn cài đặt._ Tương tự để gỡ một gói ta dùng lệnh:

```bash
apt-get remove <package>
```

Và để tìm kiếm:
```bash
apt-cache search <keyword>
```
_**Lưu ý**: keyword là từ khóa bạn cần tìm._

## Cài đặt phần mềm từ gói .deb

Để cài đặt một phần mềm từ gói \*.deb ta sử dụng dpkg:

```bash
dpkg -i <filename.deb>
```

`-i` hoặc `--install` : là tham số yêu cầu cài đặt gói. `<filename.deb>` : là tên file `.deb` bạn muốn cài. Lệnh kiểm tra các gói đã cài trong hệ thống:

```bash
dpkg -l
```

`-l` hoặc `--list` : tham số yêu cầu hiển thị danh sách package. Gỡ bỏ một package:

```bash
dpkg -r <package>
```

`-r` hoặc `--remove` : tham số yêu cầu gỡ bỏ. `<package>` : là tên package muốn gỡ. _**Lưu ý**: tên package không phải là tên gói .deb, hãy sử dụng dpkg -l để kiếm tra._

## Cài đặt phần mềm từ file .rpm

File .rpm là là gói cái đặt dành cho các **OS của RedHat**, tuy nhiên ta có thể cài đặt các phần mềm này trên Kali Linux nhờ vào một phần mềm trung gian, đó là **alien**.

Đầu tiên ta cần cài đặt alien trước:

```bash
apt-get install alien
```

Sau đó ta dùng phần mềm alien để chuyển gói .rpm sang .deb:

```bash
alien <filename.rpm>
```

`<filename.rpm>` là tên gói .rpm muốn chuyển. Rồi thực hiện cài đặt file .deb đó.

## Cài đặt phần mềm từ file nén tar gz bz2

Các file có đuôi **.tar**; **tar.gz**; **tar.bz** thì đó là file nén, ta có thể giải nén bằng **Archive Manager** hoặc bằng lệnh:

```bash
tar -xvfz <filename>
```

`-x` hoặc `--extract`, `--get`: tham số yêu cầu giải nén.

`-v`, `--verbose`: tham số yêu cầu hiển thị danh sách các file đang giải nén lên **Terminal**. Tham số này có thể bỏ tùy thích.

`-f` hoặc `--file=<filename>`: chọn file.

`-z` hoặc `--gzip`, `--gunzip`, `--ungzip`: tham số yêu cầu tìm và giải nén tar trong file gzip. Nếu là file .tar thì không cần tham số này.

`<filename>` : tên file nén. Sau đó bạn hãy xem mình giải nén được những file gì để tiếp tục.

## Cài đặt phần mềm từ file thực thi

Nếu phần mềm tải về là một file có thể chạy trực tiếp thì hãy chạy file đó bằng lệnh thực thi:

```bash
./<filename>
```

`<filename>` là tên file cần chạy. Các dạng file này bao gồm: .py, .bundle,...

Xem thêm chủ đề: [Kali Linux](https://sofsog.com/thu-thuat-chung/he-dieu-hanh/kali-linux)

## Những cách khác cài đặt khác

Tất nhiên trong phạm vi bài viết mình không thể kể hết tất cả được, tuy nhiên một các rất hiệu quả khác đó chính là đọc file README kèm theo, hoặc tìm đọc **FAQ** trên trang chủ phần mềm. Các bạn có thể đóng góp bình luận bên dưới bài viết để để mình tổng hợp và cập nhật.

Nguồn: thekalitools.com
