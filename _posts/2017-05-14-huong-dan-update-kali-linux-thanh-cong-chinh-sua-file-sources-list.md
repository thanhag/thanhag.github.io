---
title: "Hướng dẫn update Kali linux thành công (chỉnh sửa file sources.list)"
date: "2017-05-14"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
tags: 
  - "kali-linux"
  - "linux"
  - "update-kali-linux"
  - "upgrade-kali-linux"
header:
  image: /assets/images/hqdefault.jpg
  teaser: /assets/images/hqdefault.jpg
toc: true
breadcrumbs: true
permalink: /thu-thuat-chung/huong-dan-update-kali-linux-thanh-cong-chinh-sua-file-sources-list
---

Như các bạn đã biết thì Linux có thể được update thông qua Terminal bằng lệnh _apt-get update._ Nhưng trên Kali Linux. Phần lớn các bạn thực hiện lệnh đó sẽ gặp thất bại. Vì vậy, hôm nay mình hướng dẫn các bạn cách để Update Kali Linux lên phiên bản mới nhất

![](/assets/images/hqdefault.jpg)

### **B1: Các bạn mở Terminal lên và gõ lệnh sau**

**_leafpad /etc/apt/sources.list_** **B2: Khi một trình soạn thảo dạng Notepad hiện ra các bạn làm như sau** - Nếu đây là lần đầu bạn thực hiện lệnh này. Hãy xóa hết tất cả những dòng trong file và thêm 4 dòng phía dưới vào - Nếu đây không phải lần đầu bạn thực hiện lệnh này. Chỉ thêm 4 dòng dưới đây vào

### **_deb <http://http.kali.org/kali> kali-rolling main contrib non-free_** **_deb-src <http://http.kali.org/kali> kali-rolling main contrib non-free_** **_deb <http://old.kali.org/kali> sana main non-free contrib_** **_deb-src <http://old.kali.org/kali> sana main non-free contrib_** **B3: Quay lại Terminal và thực hiện lần lượt 2 lệnh sau**

**_apt-get update_** **_apt-get upgrade_** **_apt-get update --fix-missing_**

Nguồn: linuxteamvietnam.blogspot.com
