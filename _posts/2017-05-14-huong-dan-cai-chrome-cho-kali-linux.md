---
title: "Hướng dẫn cài Chrome cho kali linux"
date: "2017-05-14"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
tags: 
  - "chrome-for-linux"
  - "huong-dan-cai-chrome-cho-linux"
  - "kali-linux"
  - "linux"
header:
  image: /assets/images/cai-dat-chrome-cho-lin.png
  teaser: /assets/images/cai-dat-chrome-cho-lin.png
toc: true
breadcrumbs: true
---

## **Bước 1:** Các bạn tải google chrome tại trang chỉ chính thức [tại đây](https://www.google.com/chrome/browser/desktop/)

Chọn phiên bản phù hợp và tiến hành tải về. Mặc định file tải về sẽ nằm trong thư mục Downloads

## **Bước 2:** Cài đặt google chrome bằng lệnh sau:

```terminal
cd Downloads
```

Lệnh này chuyển thư mục hiện tại đến thư mục Downloads

```terminal
ls
```

Kiểm tra xem google chrome được download về hay chưa

```terminal
dpkg -i google-chrome-stable\_current\_amd64.deb
```

Cài đặt google chrome

 **Lưu ý :** do mình sử dụng phiên bản Kali Linux 64bit nên mình Download bản 64bit, nếu các bạn sử dụng bản 32bit thì download bản 32bit và cài file tương tự.

**Trườn hợp quá trình bị lỗi :** nếu cài đặt không thành công thì thử cách sau:

```terminal
sudo apt-get update

sudo apt-get install libgconf2-4 libnss3-1d libxss1

sudo dpkg -i google-chrome-stable_current_amd64.deb

sudo apt-get install -f
```

## **Bước 3:** tạo user cho google chrome

```terminal
useradd -m chromeuser
```

Adduser là lệnh thêm user mới, chromeuser là tên user các bạn có thể đặt khác

```terminal
passwd chromeuser
```

Tạo mật khẩu cho user vừa tạo ( có thể bỏ qua ). **Bước 4:** Chạy thử google chrome

```terminal
gksu -u chromeuser google-chrome
```

Google chrome đã có thể chạy trên Kali Linux 2.0 _(Tuy nhiên khi chạy bằng user thông thường, chrome sẽ không có âm thanh, để có âm thanh bạn phải log in vào user đó, hoặc bạn có thể chạy trực tiếp bằng tài khoản root theo hướng dẫn bên dưới)_

## **Hướng dẫn chạy Googlechrome với quyền Root trong Kali (để có thể chạy âm thanh trong Kali)**

### **Bước 1:** Thêm vào  --user-data-dir bằng dòng lệnh sau

```
gedit $(which google-chrome)
```

Dòng lệnh trên sẽ mở ra khung soạn thảo các lệnh google chrome. Tiến hành thêm --user-data-dir vào phía cuối trình soạn thảo. Xem hình bên dưới

![](/assets/images/cai-dat-chrome-cho-lin.png)

### **Bước 2:** Khởi động chrome với tài khoản root, gõ lệnh sau vào cửa sổ terminal

```terminal
/usr/bin/google-chrome-stable %U --no-sandbox
```
