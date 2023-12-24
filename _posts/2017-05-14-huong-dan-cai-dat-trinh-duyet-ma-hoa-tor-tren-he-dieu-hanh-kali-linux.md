---
title: "Hướng dẫn cài đặt trình duyệt mã hóa Tor trên hệ điều hành Kali Linux"
date: "2017-05-14"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
tags: 
  - "huong-dan-cai-tor-tren-linux"
  - "kali-linux"
  - "linux"
  - "thu-thuat-chung"
  - "trinh-duyet-bao-mat"
  - "trinh-duyet-ma-hoa"
  - "trinh-duyet-tor"
header:
  image: /assets/images/Tor-2.sh_.png
  teaser: /assets/images/Tor-2.sh_.png
toc: true
breadcrumbs: true
---

Ắt hẳn các bạn đã biết sức mạnh của Tor, Tor là một trình duyệt mã hóa thông tin an toàn cho người sử dụng, Tor còn là đầu nối của các bạn lướt web đi vào deep web, nhược điểm duy nhất của Tor là đường truyền chậm mà thôi. Bài viết này sẽ hướng dẫn các bạn cách cài đặt trình duyệt Tor trên hệ điều hành Kali rất phổ biến hiện nay

![Trình duyet tor](/assets/images/Tor-2.sh_.png)

**Lưu ý:** Tor chỉ chấp nhận chạy trên tài khoản hệ điều hành không phải là root, để sử dụng Tor, bạn cần phải dùng tài khoản thông thường trong kali linux, nếu chưa biết cách tạo, bạn hãy xem ở [bài viết này](http://www.mystown.com/2016/02/cach-tao-tai-khoan-thong-thuong-trong.html) trước khi tiến hành cài đặt Tor

## **Bước 1:** Mở cửa sổ lệnh terminal command và gõ lệnh

```terminal
apt-get install tor
```

## **Bước 2:**

Truy cập địa chỉ [https://www.torproject.org/projects/torbrowser.html.en](https://www.torproject.org/projects/torbrowser.html.en) và download phiên bản trình duyệt Tor mà bạn muốn sử dụng, ở đây tôi download phiên bản 64 bit ubuntu, các bạn download về thư mục nào cũng được nhé, tôi download về thư mục **/Downloads/**

## **Bước 3:**

Ở cửa sổ terminal command tôi gõ lệnh cd để chuyển sang thư mục **Downloads** _(chuyển sang thư mục mà bạn đã download Tor)_

```terminal
cd Downloads/
```

## **Bước 4:** Giải nén tập tin Tor đã download về

```terminal
tar -xJf tor-browser-\*
```

Dấu * là tượng trưng cho các phiên bản mà bạn đã download về, bạn có thể nhấn tor và nhấn phím tab để tự động nhận ra tên file

## **Bước 5:** Sau khi giải nén, hãy chuyển đến thư mục **tor-browser-\***

Để xem tên thư mục là gì bạn gõ lệnh

```terminal
ls
```

Sau khi thấy tên thư mục, tiếp tục lệnh cd để di chuyển vào thư mục Tor

```terminal
cd tor-browser\*
```

Dấu \* là tượng trưng cho đuôi của tên thư mục _(Ở mỗi phiên bản có các đuôi khác nhau)_, bạn có thể nhấn tor-browser và nhấn phím tab để tự động nhận ra tên file

## **Bước 6:** Khởi động Tor với lệnh

```terminal
./start-tor-browser.desktop
```

**Lưu ý:** Để chạy Tor với quyền Root bạn cần phải tìm đến thư mục **Browser**, mở file **start-tor-browser** và sửa đổi như sau:

Di chuyển đến thư mục Browser

```terminal
cd Browser
```

ví dụ đường dẫn : root@kali:~/Downloads/tor-browser\_en-US/Browser#

Mở file **start-tor-browser**

```terminal
leafpad start-tor-browser
```

Tìm chữ root và thay thế đoạn sau

```terminal
if [ "`id -u`" -eq 0 ]; then
 complain "The Tor Browser Bundle should not be run as root.  Exiting."
        exit 1
fi
```

thành đoạn sau (đơn giản là thêm dấu # vào câu lệnh if)

```terminal
# if [ "`id -u`" -eq 0 ]; then

# complain "The Tor Browser Bundle should not be run as root.  Exiting."

# exit 1

# fi
```

Nguồn: mystown.com
