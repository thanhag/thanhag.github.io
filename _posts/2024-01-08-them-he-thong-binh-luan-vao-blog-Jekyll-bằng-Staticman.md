---
published: false
title: Thêm hệ thống bình luận vào blog Jekyll bằng Staticman
# date: '2024-01-08'
categories:
  - thiet-ke-web
  - thu-thuat-chung
tags:
  - blog
  - Jekyll
  - Staticman
  - Comments
header:
  teaser: >-
    /assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bằng-Staticman-sofsog.com01.jpg
  overlay_image: >-
    /assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bằng-Staticman-sofsog.com01.jpg)
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)"
excerpt: >-
  Staticman là một dịch vụ bên thứ ba được sử dụng để thêm chức năng bình luận động vào các trang web tĩnh, bao gồm cả các trang web được xây dựng bằng Jekyll. Nó cho phép người dùng gửi bình luận từ giao diện người dùng và lưu trữ dữ liệu bình luận trên repository Git.
toc: true
breadcrumbs: true
permalink: /thiet-ke-web/them-he-thong-binh-luan-vao-blog-Jekyll-bằng-Staticman
---

## Cách hoạt động của Staticman

Staticman hoạt động dựa trên webhook và sử dụng **API GitHub** để tương tác với repository. Khi người dùng gửi bình luận, **Staticman** sẽ tạo một `pull request` mới chứa dữ liệu bình luận và sau đó bạn có thể xem và quản lý bình luận thông qua **GitHub**.

Staticman hỗ trợ nhiều loại định dạng dữ liệu như `YAML`, `JSON`, hoặc hầu hết các định dạng dữ liệu khác. Bạn cũng có thể tùy chỉnh các trường bình luận và áp dụng các quy tắc xác thực hoặc kiểm duyệt nếu cần.

Với sự linh hoạt và tích hợp dễ dàng (hoặc tương đối khó) vào các trang web tĩnh, Staticman đã trở thành một lựa chọn phổ biến để thêm tính năng bình luận vào các trang web tĩnh như blog Jekyll.

## Lưu ý trước khi thực hiện

Mình thiết lập hệ thống bình luận với **Staticman** trên trang blog [sofsog.com](Sofsog.com) này với những lưu ý sau:

- Blog này sử dụng chủ đề [Minimal mistakes Jekyll](https://github.com/mmistakes/minimal-mistakes) được lưu trữ trên **GitHub** và đang chạy ổn định.
- **Staticman** sẽ được mình thực hiện cài đặt trên máy chủ **Window server 2012** vì mình đã có sẵn nó. Trường hợp nếu bạn thực hiện trên một máy chủ linux khác thì các bước cũng không khác là bao. Trên máy chủ này:
  - Đã cài đặt [Git](https://git-scm.com/) và thiết lập thông tin người dùng đầy đủ
  - Đã cài đặt `Node.js 8.11.3+` của mình là `20.10.0`
  - Đã cài đặt [nginx](https://nginx.org/en/docs/windows.html)
  - Đã tạo `A record` cho subdomain trỏ đến `IPv4 address` của máy chủ này thành công, trường hợp của mình là `staticmain.sofsog.com` được thực hiện trên Cloudflare, lưu ý chọn mã hóa ssl một chiều từ Client đến Cloudflare là được.

![Hình Thêm hệ thống bình luận vào blog Jekyll bằng Staticman sofsog.com](/assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bằng-Staticman-sofsog.com01.jpg)

Chúc các bạn thành công!

Nguồn: [Sofsog.com](https://sofsog.com/)
