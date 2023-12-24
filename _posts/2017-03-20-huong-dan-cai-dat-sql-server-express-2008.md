---
title: "Hướng dẫn cài đặt SQL Server Express 2008"
date: "2017-03-20"
categories: 
  - "database"
tags: 
  - "huong-dan-cai-dat-sql-2008"
  - "sql"
  - "sql-2008"
header:
  image: /assets/images/SQL-Server-2008.png
  teaser: /assets/images/SQL-Server-2008.png
toc: true
breadcrumbs: true
---

Bài viết này như một ghi chú cá nhân.

# 1\. Download

 Chúng ta download SQLServer Express 2008 Release 2, bao gồm cả công cụ trực quan, tại:

- [http://www.microsoft.com/en-us/download/details.aspx?id=30438](http://www.microsoft.com/en-us/download/details.aspx?id=30438)

![%image_alt%](/assets/images/20474.png)

Bạn có thể download theo 2 cách:

1. Download 2 file tại (1) và (2)
    - (1) để cài đặt SQLServer
    - (2) để cài đặt tool quản lý trực quan
2. Download 1 file tại (3), nó là tổng hợp của (1) và (2) trong cùng 1 file.

![%image_alt%](/assets/images/20476.png)

Để nhanh gọn, bạn nên download 1 file tại (3)

![%image_alt%](/assets/images/20653.png)

Sau khi download thành công:

![%image_alt%](/assets/images/20480.png)

# 2- Cài đặt

 Cài đặt:

![%image_alt%](/assets/images/20492.png)

![%image_alt%](/assets/images/20496.png)

![%image_alt%](/assets/images/20498.png)

Chọn tất cả các tính năng.

![%image_alt%](/assets/images/20500.png)

Chọn: Named Instance

![%image_alt%](/assets/images/20502.png)

![%image_alt%](/assets/images/20504.png)

Tiếp theo bạn lựa chọn chế độ "Mix Mode" điều đó cho phép bạn login vào SQL server theo 2 cách:

1. Sử dụng Username/password đăng nhập của windows.
2. Sử dụng username/password của SQLServer

![%image_alt%](/assets/images/20506.png)

![%image_alt%](/assets/images/20508.png)

Chờ cho tới khi việc cài đặt hoàn tất.

# 3- Cấu hình SQL Server

Đây là việc quan trọng các cấu hình này cho phép bạn kết nối vào cơ sở dữ liệu từ một máy tính khác trong mạng LAN.

![%image_alt%](/assets/images/20613.png)

Vào chức năng:

- SQL Server Configuration Management

Chức năng này cho phép bạn cấu hình để có thể từ một máy tính khác truy cập vào SQL Server thông qua IP hoặc Server name.

![%image_alt%](/assets/images/20615.png)

Bạn cần Start service: **SQL Server Browser**. Nhấn phải chuột vào nó chọn Property.

![%image_alt%](/assets/images/20617.png)

Chuyển chế độ Start service sang Automatic (tự động).

![%image_alt%](/assets/images/20619.png)

Sau đó nhấn Start, để khởi động dịch vụ.

![%image_alt%](/assets/images/20621.png)

![%image_alt%](/assets/images/20623.png)

![%image_alt%](/assets/images/20625.png)

Tiếp theo bật TPC/IP cho phép máy tính khác kết nối vào SQL Server thông qua IP.

![%image_alt%](/assets/images/20629.png)

![%image_alt%](/assets/images/20631.png)

Tương tự bật: **Named Pipes**, cho phép máy tính khác kết nối vào **SQL Server** thông qua Server name.

![%image_alt%](/assets/images/20633.png)

Tiếp theo, đảm bảo rằng **SQL Server** của bạn đang chạy dưới chế độ **Network Service**.

![%image_alt%](/assets/images/20637.png)

![%image_alt%](/assets/images/20639.png)

Sau khi cấu hình xong, restart lại service của SQL Server.

![%image_alt%](/assets/images/20673.png)

# 4- Sử dụng SQL Server Management Studio

![%image_alt%](/assets/images/20675.png)

![%image_alt%](/assets/images/20643.png)

![%image_alt%](/assets/images/20645.png)

Trong trường hợp bạn kết nối vào SQL Server trên máy địa phương, bạn có thể sử dụng dấu chấm, để đại diện cho tên máy.

![%image_alt%](/assets/images/20677.png)

Đây là hình ảnh sau khi đăng nhập vào **SQL Server Management Studio**.

![%image_alt%](/assets/images/20647.png)

Chúng ta tạo thử một database có tên simplehr.

![%image_alt%](/assets/images/20649.png)

![%image_alt%](/assets/images/20651.png)

![%image_alt%](/assets/images/20685.png)

![%image_alt%](/assets/images/20687.png)


```sql
Create table My_Table  (
   ID int primary key,
   Name Varchar(32)
);
Insert into My_Table(Id,Name)
values (1 , 'Tom Cat');
```

![%image_alt%](/assets/images/20691.png)