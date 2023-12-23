---
title: "Cài đặt Pinta - phần mềm chỉnh sửa ảnh cho Linux"
date: "2017-05-14"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
tags: 
  - "chinh-sua-anh-tren-linux"
  - "gioi-thieu-pinta"
  - "kali-linux"
  - "linux"
  - "pinta"
header:
  image: /assets/images/pinta-trinh-sua-anh-tren-linux-1.jpg
  teaser: /assets/images/pinta-trinh-sua-anh-tren-linux-1.jpg
toc: true
breadcrumbs: true
---

Bài viết này mình xin giới thiệu với các bạn một phần mềm chỉnh sửa ảnh trên hệ điều hành Linux – Pinta. Đây là một phần mềm khá hữu ích với những ai làm việc thường xuyên thực hiện chỉnh sửa các ảnh.

Trên Windows thì nói đến chỉnh sửa ảnh thì không thể không nhắc đến Photoshop hoặc phần mềm có sẵn trong hệ điều hành Windows – MS Paint.

Trên Linux thì sao, mặc định như Linux Mint 17.1 mà mình đang sử dụng thì nó cũng đã có sẵn phần mềm GIMP Image Editor để chỉnh sửa ảnh; một số người so sánh GIMP với Photoshop về tính năng thì mình nghĩ nó cũng giống Photoshop về khoản khó sử dụng. Bản thân mình cũng đã sử dụng nó cho việc chỉnh sửa các ảnh để upload lên bài viết của mình nhưng khá nhọc nhằn nên mình muốn tìm một phần mềm tương tự như MS Paint – phần mềm dễ sử dụng hơn và tiện hơn cho công việc. ![](/assets/images/pinta-trinh-sua-anh-tren-linux-1.jpg) **Pinta là gì?** Pinta là một phần mềm vẽ/chỉnh sửa hình ảnh mã nguồn mở và miễn phí , một phiên bản sau của Paint.NET. Nó cung cấp một giao diện tiện dụng cho người dùng và khá dễ dàng trong việc chỉnh sửa hình ảnh.

Hướng dẫn cài đặt trên kali linux:

sudo add-apt-repository ppa:pinta-maintainers/pinta-stable

sudo apt-get update

sudo apt-get install pinta
