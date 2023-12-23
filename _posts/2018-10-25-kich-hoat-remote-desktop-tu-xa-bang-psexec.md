---
title: "Kích hoạt Remote Desktop từ xa bằng psexec - Enable RDP remotely"
date: "2018-10-25"
categories: 
  - "he-dieu-hanh"
  - "internet"
  - "thu-thuat-chung"
header:
  image: /assets/images/Sofsog.com-Kích-hoạt-Remote-Desktop-từ-xa-bằng-psexec-Enable-RDP-remotely.jpg
  teaser: /assets/images/Sofsog.com-Kích-hoạt-Remote-Desktop-từ-xa-bằng-psexec-Enable-RDP-remotely.jpg
toc: true
breadcrumbs: true
---

**Remote desktop protocol (RDP)** là một giao thức hỗ trợ để điều kiển máy tính window từ xa. Bài viết này chỉ dành cho những bạn nào đã biết về RDP rồi và muốn kích hoạt **RDP** từ một máy tính nào đó trong mạng nội bộ.

![Sofsog.com-Kích hoạt Remote Desktop từ xa bằng psexec - Enable RDP remotely](/assets/images/Sofsog.com-Kích-hoạt-Remote-Desktop-từ-xa-bằng-psexec-Enable-RDP-remotely.jpg)

Để kích hoạt **RDP** bạn có thể mở máy cần kích hoạt lên và thực hiện. Tuy nhiên trường hợp bạn cần kích hoạt nhiều máy trong mạng nội bộ thì cách này không khả thi.

Giải pháp là kích hoạt **RDP** bằng dòng lệnh từ máy tính quản lý mạng nội bộ của mình, sử dụng **psexec**.

Dưới đây là một vài tập lệnh để bật **RDP** trên máy tính từ xa từ một máy tính khác trên cùng một miền. Lưu ý rằng bạn cần phải là quản trị viên và bạn sẽ chỉ kích hoạt RDP cho chính mình chứ không phải toàn bộ nhóm bảo mật.

1. Download **pstools** [ở đây](http://bit.ly/2uim3aR) hoặc [ở đây](https://technet.microsoft.com/en-us/sysinternals/pstools.aspx) và giải nén vào folder đặt tên là **pstools** trong ổ **C** (như sau **C:\\pstools)**
2. Mở Command prompt (CMD) bằng quyền Administrator
3. Thay đổi đường dẫn thành c:\\pstools
4. Chạy dòng lệnh bên dưới: (thay đổi các chữ màu đỏ cho phù hợp với mạng của các bạn)

psexec \\\\**hostname.sofsog.com** reg add "hklm\\system\\currentcontrolset\\control\\terminal server" /f /v fDenyTSConnections /t REG\_DWORD /d 0

4\. Chạy thêm lệnh này để mở các cổng cần thiết trong tường lửa trên máy từ xa: (thay đổi các chữ màu đỏ cho phù hợp với mạng của các bạn)

psexec \\\\hostname.sofsog.com netsh firewall set service remoteadmin enable

[Sofsog.com](https://sofsog.com/) chúc các bạn thành công.
