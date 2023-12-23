---
title: "Hướng dẫn lấy tên file và lấy tên thư mục trên Windows và chuyển thành văn bản (Text)"
date: "2023-11-21"
categories: 
  - "thu-thuat-chung"
tags: 
  - "cmd"
  - "dir"
  - "lay-ten-file"
  - "lay-ten-thu-muc"
  - "thu-thuat-chung"
header:
  image: /assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text-2.png
  teaser: /assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text-2.png
toc: true
breadcrumbs: true
---

Chào các bạn, bài viết này mình sẽ giới thiệu đến các bạn lệnh DIR trong DOS. Có thể nói lệnh DIR là một lệnh rất hay trong DOS. Bằng cách áp dụng linh hoạt lệnh này, các bạn có thể dễ dàng, nhanh chóng lấy ra được danh sách tên các file, lấy tên thư mục trên Windows. Lệnh DIR sẽ thực hiện liệt kê ra danh sách tên các file và thư mục nằm trong một thư mục nào đó mà mình cần. Muốn liệt kê ra tên các file và thư mục nằm trong thư mục nào thì mình dùng lệnh cd để đi đến thư mục đó rồi thực hiện lệnh DIR. Hoặc từ một thư mục bất kỳ, thực hiện lệnh DIR với đường dẫn đầy đủ đến thư mục mà mình cần liệt kê danh sách tên file, thư mục. Ví dụ, trong ổ D mình có thư mục “Hoc tap”, giờ mình muốn biết trong thư mục này chứa những file, thư mục con nào mình thực hiện theo 2 cách như hình dưới

![Hướng dẫn lấy tên file và thư mục trên Windows và chuyển thành văn bản (Text)](/assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text.png) Hình 1: Đi đến thư mục cần liệt kê sau đó thực hiện lệnh DIR

![Hướng dẫn lấy tên file và thư mục trên Windows và chuyển thành văn bản (Text) 2](/assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text-2.png) Hình 2: Từ một thư mục bất kỳ, thực hiện DIR với đường dẫn đầy đủ của thư mục cần liệt kê

Trong ví dụ trên, lệnh DIR không có tham số, các bạn thấy kết quả hiển thị rất nhiều các thông tin như ngày giờ tạo, dung lượng của file, thư mục. Mặc định, các file, thư mục có tên tiếng Việt có dấu sẽ không hiển thị đúng trong DOS. Do đó, nếu sử dụng lệnh DIR đối với các thư mục chứa file, thư mục có tên tiếng Việt có dấu, kết quả hiển thị sẽ không đúng. Để khắc phục lỗi này, các bạn thực hiện theo hướng dẫn Hiển thị tiếng Việt có dấu trong cửa sổ DOS của Windows của mình.

Lệnh DIR có nhiều tham số, trong hướng dẫn này mình giới thiệu một số tham số có tính ứng dụng cao, áp dụng nhiều trong thực tế. Đầu tiên phải nói đến tham số /b (Bare format). Với tham số này, kết quả của lệnh DIR sẽ loại bỏ hết các thông tin như ngày giờ tạo, dung lượng của file, thư mục. Vẫn sử dụng lệnh DIR với thư mục “Hoc tap” trong ổ D mình được kết quả như hình dưới

![Hướng dẫn lấy tên file và thư mục trên Windows và chuyển thành văn bản (Text) 3](/assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text-3.png) Hình 3: DIR với tham số /b

Các bạn có thể thấy trong hình 3 ở trên, với tham số **/b** lệnh DIR chỉ liệt kê danh sách tên các file và thư mục, bỏ hết các thông tin như ngày tạo, dung lượng file, thư mục. Trong hầu hết các ứng dụng của lệnh DIR, mình đều sử dụng tham số **/b** này.

Một số tham số khác như:

a là hiện file ẩn d là Directory (thư mục) s là System (Hệ thống) h là Hidden (Ẩn)

Tùy vào nhu cầu mà mình sử dụng các thuộc tính con ở trên cho hợp lý. Nguyên tắc sử dụng các thuộc tính con này như sau: Muốn liệt kê danh sách tên các file, thư mục thỏa mãn thuộc tính nào, mình sẽ cho thuộc tính đó đi kèm với tham số **/a**. Còn nếu muốn liệt kê danh sách tên các file, thư mục không thỏa mãn thuộc tính nào, mình sẽ thêm – thuộc tính đó kèm theo tham số **/a**. Từ đây, mình có một số các ví dụ điển hình như sau

Liệt kê danh sách tên tất cả các thư mục trong ổ C (bao gồm cả thư mục hệ thống và ẩn)

![Hướng dẫn lấy tên file và thư mục trên Windows và chuyển thành văn bản (Text) 4](/assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text-4.png) dir /ad /b

Liệt kê danh sách tên tất cả các file nằm ở ngoài cùng của ổ C (bao gồm cả file hệ thống và ẩn)

```dir /a-d /b```

(Bản chất là loại bỏ thuộc tính thư mục -d)

Liệt kê danh sách tên tất cả các thư mục hệ thống

```dir /ads /b```

Liệt kê danh sách tên tất các thư mục ẩn

```dir /adh /b```

Liệt kê danh sách tên tất cả các file hệ thống

```dir /as-d /b```

Liệt kê danh sách tên tất cả các file ẩn

```dir /ah-d /b```

Trong trường hợp này của mình, các file hệ thống và file ẩn là một nên kết quả của 2 lệnh DIR trên cho kết quả như nhau.

Bằng cách kết hợp các thuộc tính của tham số /a các bạn có thể linh hoạt lấy ra được danh sách tên các file và thư mục mà các bạn muốn.

Mình chuyển sang tham số cuối cùng, tham số **/s**. Tham số này sẽ lấy ra đường dẫn dầy đủ của các file và thư mục bao gồm cả các file, thư mục nằm trong thư mục con mà mình đang thực hiện lệnh DIR. Đây là tham số rất hay bởi khi thực hiện các lệnh sao chép, đổi tên, di chuyển hay xóa file, thư mục mình đều cần đến đường dẫn đầy đủ đến các file và thư mục. Khi áp dụng tham số **/s**, bao giờ mình cũng đi kèm với tham số **/b** để loại bỏ các thông tin không cần thiết.

Ví dụ mình cần lấy ra danh sách đường dẫn đầy đủ của tất cả các file trong thư mục “Ca nhạc” ở ổ D, mình thực hiện lệnh sau

```dir /a-d /b /s d:\\"Ca nhạc"`
``
Hoặc mình cần lấy ra danh sách tên tất cả các thư mục trong thư mục “Hoc tap” của ổ E, mình thực hiện lệnh sau

![Hướng dẫn lấy tên file và thư mục trên Windows và chuyển thành văn bản (Text) 5](/assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text-5.png) 

```dir /ad /b /s E:\\"Hoc tap"```

Khi đã liệt kê được danh sách tên tất cả các file và thư mục như đã làm ở trên, các bạn có thể dễ dàng kết xuất danh sách này ra một file Text.

![Hướng dẫn lấy tên file và thư mục trên Windows và chuyển thành văn bản (Text) 6](/assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text-6.png) 

```dir /ad /b /s E:\\"Hoc tap" >DanhSachThuMuc.txt```

Kết quả:

![Hướng dẫn lấy tên file và thư mục trên Windows và chuyển thành văn bản (Text) 7](/assets/images/Hướng-dẫn-lấy-tên-file-và-thư-mục-trên-Windows-và-chuyển-thành-văn-bản-Text-7.png) 

File text được tạo ra ngay thư mục đang chạy lệnh CMD

Chúc các bạn thành công

Xem thêm: [Thủ thuật chung](https://sofsog.com/thu-thuat-chung)

