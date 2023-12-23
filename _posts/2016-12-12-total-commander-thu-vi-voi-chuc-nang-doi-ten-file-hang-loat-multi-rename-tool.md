---
title: "Total Commander thú vị với chức năng đổi tên file hàng loạt (multi rename tool)"
date: "2016-12-12"
categories: 
  - "thu-thuat-chung"
tags: 
  - "doi-ten-file-hang-loat"
  - "multi-rename"
  - "total-commander"
header:
  image: /assets/images/Huong-dan-doi-ten-file-hang-loat.png
  teaser: /assets/images/Huong-dan-doi-ten-file-hang-loat.png
toc: true
breadcrumbs: true
---

![%image_alt%](/assets/images/toltal-rename-mh.png)

Mình rất hay dùng Total Commander để ftp lên hosting nhưng mình lại không hề biết Total Commander còn rất nhiều chức năng tuyệt vời, mà điển hình là chức năng Rename file hàng loạt với nhiều tùy chỉnh chi tiết cho người dùng, đảm bảo bạn sẽ thích mê!

Trên mạng có khá nhiều bài viết về total commander tuy nhiên mới chỉ dừng lại ở mức là giới thiệu chứ chưa đi vào chi tiết kỹ từng phần, hoặc có hướng dẫn cũng chưa kỹ lắm, vì thế bài viết này mình sẽ đi kỹ về chức năng này, chúng ta cùng tìm hiểu nhé!

**Download phần mềm:**

Vào trang chủ: [http://www.ghisler.com/](http://www.ghisler.com/) tìm phiên bản phù hợp

Hoặc vào Softpedia: [](http://www.softpedia.com/get/PORTABLE-SOFTWARE/System/File-management/Windows-Portable-Applications-Portable-Total-Commander-Utility.shtml#download)

Hoặc link drive: [](https://drive.google.com/open?id=1XxlLw4OfslPSssDvcTcm7BMR4hgfOh8A)

**Giờ thực hành nào!** - Đầu tiên Mở Total Commander, tìm đến chỗ các file cần rename, sau đó bạn có thể chọn 1 file để rename hoặc chọn nhiều file (bằng cách nhấn giữ ctrl sau đó bấm chọn từng file), muốn bỏ chọn file nào thì nhấn chuột phải lên file đó.

![Đổi tên file hàng loạt](/assets/images/toltal-rename-1.png)

(hình demo - những file được chọn sẽ có màu đỏ)

Sau khi chọn xong các file cần đổi tên ta chuyển bước tiếp theo

\- Vào Files/ Multi-rename tool (xem hình)

![%image_alt%](/assets/images/toltal-rename-2.png)

\- Hộp thoại Multi-rename tool hiện ra với nhiều khung tùy chỉnh (xem hình)

![Hướng dẫn đổi tên file hàng loạt](/assets/images/toltal-rename-3.png)

Giải thích các tùy chỉnh: mình sẽ giải thích theo các khu vực được đánh số trên hình, bạn xem hình để đối chiếu nhé! Các tùy chỉnh bạn có thể bấm vào để sử dụng, hoặc gõ trực tiếp.

**\+ Khu vực 1:** Tùy chỉnh phần tên file cho kết quả xuất ra. (phần đuôi file sẽ được hiệu chỉnh ở khu vực khác) - \[N\] Name: phần tên gốc với đầy đủ ký tự. - \[N#-#\] Range: trích lấy 1 chuỗi ký tự từ phần tên file ban đầu. Vd: \[N1-3\]: chỉ lấy các ký tự từ 1 đến 3 trong phần tên file. - \[C\] Counter: đánh số vào phần tên xuất ra. (Tùy chỉnh mục \[C\] ở khu vực được đánh số 4, đọc phần giải thích về khu vực 4 để hiểu rõ hơn) Các tùy chọn này có thể kết hợp với nhau ví dụ \[N\]\[N1-3\]\[C\], hoặc đứng 1 mình như \[N\]

**\+ Khu vực 2:** Tùy chỉnh phần đuôi file cho kết quả xuất ra Hiểu tương tự như khu vực 1 - \[E\] Ext: phần đuôi file ban đầu với đầy đủ ký tự ( ví dụ ban đầu là .jpg thì nếu viết \[E\] thì kết quả xuất ra sẽ vẫn là .jpg).

\- \[E#-#\] Range: trích lấy 1 chuỗi ký tự từ phần tên đuôi file ban đầu. Vd: \[E1-3\]: chỉ lấy các ký tự từ 1 đến 3 trong phần tên đuôi file. Ví dụ muốn tùy chỉnh .docx --> .doc thì bạn viết \[E1-3\]

\- \[C\] Counter: đánh số vào phần đuôi file xuất ra. (Tùy chỉnh mục \[C\] ở khu vực được đánh số 4, đọc phần giải thích về khu vực 4 để hiểu rõ hơn) Các tùy chọn này có thể kết hợp với nhau ví dụ \[E1-3\]\[C\] hoặc độc lập như \[E1-3\]

+ **Khu vực 3:** Search and Replace, chức năng này rất hay nè, thix nhứt :X - Search for: tìm trong tên file (bao gồm cả tên + đuôi file), tìm gì thì bạn gõ vào khung này - Replace with: sau khi tìm thấy từ cần tìm trong mục Search for, thì sẽ thay thế bằng gì, bạn gõ vào khung này Nếu bạn không cần dùng thì khu vực 3 có thể bỏ qua không cần viết gì hết

**\+ Khu vực 4:** Tùy chỉnh \[C\] Counter ở Khu vực 1 và 2 Tùy chỉnh biến đếm \[C\] , nếu bạn sử dụng \[C\] trong kết quả rename thì bạn cần phải để ý mục này. - Start at: đánh số từ số mấy - Step by: bước nhảy - Digits: con số đơn vị cho \[C\]

**\+ Khu vực 5:** List các tên files ban đầu mà bạn đã chọn **\+ Khu vực 6:** Tên mới, sẽ thay đổi nếu bạn thay đổi các tùy chỉnh ở các khu vực 1,2,3,4. Vì thế trong khi bạn tùy chỉnh ở các khu vực 1,2,3 hoặc 4 thì hãy để ý khu vực này.

Sau đây là 2 ví dụ:

![Hướng dẫn đổi tên file hàng loạt](/assets/images/toltal-rename--demo1.png) ![Hướng dẫn đổi tên file hàng loạt](/assets/images/toltal-rename--demo2.png)

Đối chiếu các khu vực bạn sẽ hiểu ngay thôi :D

Ngoài ra nó còn nhiều lệnh ẩn khác nữa, có thời gian thì mình sẽ tìm hiểu rùi cập nhật thêm sau :D

\- Sau khi đã thiết lập xong các tùy chọn, bạn nhấn Start để thực hiện đổi tên. Các file của bạn sẽ được đổi tên nhanh chóng.

Nguồn: hatodotcom.blogspot.com
