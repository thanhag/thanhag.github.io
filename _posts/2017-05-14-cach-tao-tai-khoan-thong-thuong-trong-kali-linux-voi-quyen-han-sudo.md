---
title: "Cách tạo tài khoản thông thường trong Kali linux với quyền hạn sudo"
date: "2017-05-14"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
tags: 
  - "add-user-linux"
  - "kali-linux"
  - "linux"
  - "set-user-sudo"
  - "sudoers"
  - "user-in-linux"
header:
  
  teaser: /assets/images/Kali-Linux.png
toc: true
breadcrumbs: true
---

Như các bạn đã biết, Kali linux là một hệ điều hành mang tính bảo mật cực kỳ cao, cũng giống như các hệ điều hành ubuntu khác. Do đó, rất nhiều phần mềm chỉ được sử dụng với tài khoản thông thường chứ không phải là tài khoản root _(Tài khoản quản trị cao nhất)_ Bài viết này sẽ hướng dẫn các bạn tạo tài khoản user thông thường để có thể sử dụng các phần mềm thông dụng.

![](/assets/images/Kali-Linux.png)

Khi bạn đang ở trong tài khoản root, thực hiện các lệnh sau đây

## **Bước 1:** Mở cửa sổ lệnh terminal và gõ lệnh sau đây

```terminal
useradd -m user
```

tham số -m là để tạo đường dẫn home cho tài khoản

## **Bước 2:** Thiết lập mật khẩu cho tài khoản này với lệnh

```terminal
passwd username
```

Nó sẽ hiện ra bảng thông báo yêu cầu bạn nhập mật khẩu

Kế tiếp, tôi khuyến cáo bạn nên cho tài khoản này vào nhóm _"sudoers"_, vì khi đó chúng ta có thể sử dụng lệnh **sudo** để lấy quyền quản trị hệ thống _(nhằm cài đặt các phần mềm khác)_. Để vào nhóm _"sudoers"_ bạn gõ lệnh sau

```terminal
usermod -a -G sudo username
```

Tham số -a -G sudo là để thêm tài khoản này vào nhóm sudo.

## **Bước 3:** Thự hiện lệnh chsh để thiết lập login shell cho tài khoản

```terminal
chsh -s /bin/bash username
```

Nguồn: MysTown
