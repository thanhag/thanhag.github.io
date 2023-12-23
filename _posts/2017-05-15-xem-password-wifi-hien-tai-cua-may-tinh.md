---
title: "Xem password wifi hiện tại của máy tính"
date: "2017-05-15"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
  - "ubuntu"
  - "window-10"
tags: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "linux"
  - "password-wifi"
  - "thu-thuat-chung"
  - "ubuntu"
  - "xem-pass-wifi"
  - "xem-password-wifi"
header:
  image: /assets/images/windows-wifi-password.png
  teaser: /assets/images/windows-wifi-password.png
toc: true
breadcrumbs: true
---

Máy tính của bạn đang kết nối mạng bằng wifi, khi bạn muốn kết nối mạng cho một thiết bị khác, ví dụ như điện thoại, nhưng bạn không nhớ hoặc không biết password wifi, hướng dẫn này sẽ giúp bạn giải quyết trên cả 3 hệ điều hành phổ biến  là Window, Mac OS và Linux.

### Hệ điều hành Windows

Mở command prompt bằng quyền admimistrator. Vào Run, gõ "cmd", nhấn chuột phải vào icon của command prompt  chọn Run as Administrator. Gõ dòng lệnh bên dưới vào:

netsh wlan show profile name=labnol-office key=clear

Thay "labnol-office" thành tên Wifi mà bạn đang kết nối (Wireless SSID)

Nếu bạn chỉ muốn xem password và không cần xem các thông tin khác thì gõ dòng bên dưới:

netsh wlan show profile name=labnol-office key=clear | findstr Key

![If you do not see the WiFi Password](/assets/images/windows-wifi-password.png)

Nếu bạn vẫn không thấy password, có thể là bạn không mở command prompt bằng quyền administrator

### Hệ điều hành Mac OS X

Mở Spotlight (Cmd+Space) và gõ termial để mở Terminal. Ở command line, gõ dòng lệnh sau đây vào:

security find-generic-password -wa labnol-office

Thay đổi labnol-office thành tên Wifi mà bạn đang kết nối (Wireless SSID), sau đó điền username và password của Mac của bạn vào.

### Hệ điều hành Linux

Mở terminal, gõ dòng lệnh sau: (thay đổi labnol-office thành tên Wifi mà bạn đang kết nối (Wireless SSID))

sudo cat /etc/NetworkManager/system-connections/labnol-office | grep psk=

Hoặc nếu bạn không nhớ tên wifi thì gõ dòng lệnh sau:

sudo grep psk= /etc/NetworkManager/system-connections/\*

Nguồn: labnol.org
