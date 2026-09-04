---
published: true
title: Lưu trữ chứng từ kế toán 10 năm - dựng kho tài liệu ở văn phòng thay vì Google Drive
date: '2026-09-04'
categories:
  - ke-toan
  - server
tags:
  - kế toán
  - lưu trữ
  - NAS
  - backup
  - chứng từ
header:
  teaser: >-
    /assets/images/2026/2026-09-04-luu-tru-chung-tu-sofsog.com01.png
  overlay_image: >-
    /assets/images/2026/2026-09-04-luu-tru-chung-tu-sofsog.com01.png
  overlay_filter: 0.55
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)"
excerpt: >-
  Luật bắt giữ chứng từ kế toán tối thiểu **10 năm**, và cho phép giữ dưới dạng
  điện tử nếu bảo đảm được ba điều kiện. Bài này nói về ba điều kiện đó, và vì sao
  một thư mục **Google Drive** của nhân viên không đáp ứng được cái nào cho tử tế.
toc: true
breadcrumbs: true
permalink: /ke-toan/luu-tru-chung-tu-ke-toan-10-nam
---

Ngày 11 tháng 9 năm 2020, văn phòng công ty mình cháy. Hồ sơ kế toán bằng giấy mất một phần, còn dữ liệu trong máy tính thì mất sạch vì ổ cứng hỏng hoàn toàn. Cả hai bản lưu đều nằm trong cùng một căn phòng, nên một đám cháy xoá được cả hai cùng lúc.

Bài này là những gì mình rút ra sau hôm đó, viết cho người làm kế toán chứ không phải cho dân IT.

## Luật yêu cầu gì

Nghị định 174/2016/NĐ-CP chia tài liệu kế toán thành ba mốc thời hạn. Điều 12 là nhóm giữ tối thiểu **5 năm**. Điều 13 là nhóm tối thiểu **10 năm**, gồm chứng từ dùng trực tiếp để ghi sổ và lập báo cáo tài chính, cùng tài liệu liên quan tới thanh lý và nhượng bán tài sản cố định. Điều 14 là nhóm giữ **vĩnh viễn**. Điều 15 nói thời hạn tính từ lúc nào.

Phần đáng chú ý hơn nằm ở Luật Kế toán 2015: **được phép lưu trữ trên phương tiện điện tử**, không bắt buộc in hết ra giấy. Nhưng kèm ba điều kiện — dữ liệu phải **an toàn**, phải **bảo mật**, và phải **tra cứu được trong suốt thời hạn lưu trữ**.

Có một điểm phân biệt dễ nhầm. Đơn vị kế toán nhà nước vẫn phải in sổ kế toán tổng hợp ra giấy để lưu. Với doanh nghiệp, việc in chứng từ và sổ chi tiết do người đại diện theo pháp luật quyết định.

Mình là kế toán chứ không phải luật sư. Các số điều ở trên bạn nên tự đối chiếu với văn bản gốc trước khi áp dụng cho đơn vị mình, nhất là khi đơn vị bạn có đặc thù riêng.

Ba điều kiện kia nghe như ngôn ngữ pháp lý, nhưng dịch sang việc thật thì rất cụ thể: **đừng để mất, đừng để người ngoài đọc được, và mười năm sau vẫn phải mở ra xem được**. Phần còn lại của bài là cách làm ba việc đó.

## Mười năm dữ liệu nhỏ hơn bạn tưởng

Trước khi bàn cách lưu, cần biết phải lưu bao nhiêu. Con số hay bị hình dung sai theo hướng phóng đại.

Ở công ty chính của mình, riêng máy của kế toán trưởng chứa khoảng **10 GB trong hai năm**. Phòng kế toán có năm người. Nếu bốn người còn lại phát sinh ít hơn, ước chừng cả phòng rơi vào **15–25 GB mỗi năm**. Mười năm là khoảng 150–250 GB. Mấy công ty phụ thì khối lượng chỉ bằng chừng một phần mười.

Đây là ước lượng từ một trường hợp cụ thể, không phải con số chuẩn cho mọi doanh nghiệp. Nhưng bậc độ lớn thì đáng tin: **toàn bộ mười năm chứng từ của một doanh nghiệp nhỏ nằm gọn trong một ổ cứng phổ thông**.

Nghĩa là dung lượng không phải vấn đề. Vấn đề là dữ liệu có sống nổi mười năm không, và tìm lại được không.

## Vì sao Google Drive cá nhân không giải được bài này

Drive đồng bộ tốt, tìm kiếm tốt, và ai cũng biết dùng. Mình không chê công cụ. Chỗ hỏng nằm ở quyền sở hữu và vòng đời.

Thư mục đó thuộc **tài khoản cá nhân của một người**. Người đó nghỉ việc, đổi mật khẩu, hoặc đơn giản là không nghe máy — công ty mất quyền vào kho chứng từ của chính mình. Đây không phải tình huống giả định, nó xảy ra mỗi khi có người rời phòng kế toán.

Quyền chia sẻ cũng loang ra theo thời gian mà không ai rà lại. Sau vài năm, thường không còn ai trả lời chính xác được câu hỏi ai đang đọc được thư mục đó.

Và Drive không có khái niệm thời hạn lưu trữ. Ai đó xoá nhầm một thư mục, ba mươi ngày sau thùng rác tự dọn, thế là xong. Không có gì trong hệ thống ràng buộc rằng tập tài liệu này phải sống đủ mười năm.

## RAID không phải là backup

Chỗ này mình muốn nói kỹ, vì đây là hiểu nhầm khiến người ta mất dữ liệu trong khi vẫn đinh ninh mình đã an toàn.

Một thiết bị lưu trữ có hai ổ cứng chạy RAID sẽ chịu được **một ổ chết**. Ổ hỏng, thay ổ mới, dữ liệu vẫn nguyên. Nghe rất giống backup nên nhiều người dừng ở đó.

Nhưng RAID chép mọi thao tác sang cả hai ổ ngay lập tức, kể cả thao tác sai. Xoá nhầm một thư mục thì nó biến mất khỏi cả hai ổ cùng lúc. Mã độc tống tiền mã hoá dữ liệu thì cả hai ổ cùng bị mã hoá. Và cháy văn phòng thì cả hai ổ cùng nằm trong đám cháy đó.

Vụ cháy năm 2020 của công ty mình đúng là trường hợp cuối. Bao nhiêu ổ cứng cũng vô nghĩa khi chúng ở chung một chỗ.

## Kho tài liệu nên dựng thế nào

Đặt kho trên một thiết bị của công ty, không phải máy cá nhân của ai. Một con NAS đặt ở văn phòng là đủ cho quy mô vài chục GB mỗi năm.

Cấu trúc thư mục nên phẳng và đoán được, vì người tra cứu sau này có thể không phải bạn:

```
Chung-tu/
├── 2026/
│   ├── 01-Hoa-don-dau-vao/
│   ├── 02-Hoa-don-dau-ra/
│   ├── 03-Phieu-thu-chi/
│   ├── 04-Ngan-hang/
│   ├── 05-Luong-BHXH/
│   └── 06-Hop-dong/
└── 2025/
    └── ...
```

Năm đứng trước vì thời hạn lưu trữ tính theo năm — hết hạn thì xử lý trọn một thư mục. Số thứ tự trước tên loại chứng từ để thư mục luôn xếp đúng thứ tự thay vì sắp theo bảng chữ cái.

Đặt tên file theo một khuôn cố định, ví dụ `2026-03-15_HD-vao_CongtyABC_12500000.pdf`. Ngày viết dạng năm-tháng-ngày để sắp xếp theo tên là ra đúng thứ tự thời gian. Có số tiền trong tên file thì nhiều lúc khỏi phải mở ra xem.

Mỗi người một tài khoản riêng, đừng dùng chung một tài khoản cho cả phòng. Người nghỉ việc thì khoá tài khoản đó, kho tài liệu không suy suyển gì.

![Hình danh sách tài khoản người dùng trên NAS, mỗi kế toán một tài khoản riêng sofsog.com](/assets/images/2026/2026-09-04-luu-tru-chung-tu-sofsog.com02.png)

## Ba lớp sao lưu

Bài học từ đám cháy nằm gọn trong mục này.

**Lớp một** là bản đang dùng hằng ngày, nằm trên NAS ở văn phòng.

![Hình máy trạm sao lưu liên tục lên NAS, báo backup hoàn tất sofsog.com](/assets/images/2026/2026-09-04-luu-tru-chung-tu-sofsog.com03.png)

**Lớp hai** là một ổ cứng ngoài, chép định kỳ rồi **cất ở địa điểm khác**. Nhà riêng, chi nhánh, két ở ngân hàng, chỗ nào cũng được miễn không cùng toà nhà với lớp một. Nếu năm 2020 công ty mình có lớp này thì bài viết đã không cần tồn tại.

**Lớp ba** là một bản trên dịch vụ đám mây. Lớp này chống được cả trường hợp mất cắp cả NAS lẫn ổ ngoài.

Và phần quan trọng nhất mà gần như ai cũng bỏ qua: **mỗi năm mở thử một bản backup ra xem**. Chọn ngẫu nhiên vài file, mở lên, đọc được thì thôi. Một bản sao lưu chưa từng được thử phục hồi thì chưa phải là bản sao lưu, nó chỉ là một niềm tin.

## Mười năm là quãng rất dài

Ổ cứng không sống được mười năm. Kế hoạch phải tính tới việc thay thiết bị giữa chừng, và chép dữ liệu sang thiết bị mới là một việc có lịch chứ không phải chuyện tính sau.

Định dạng file cũng vậy. Giữ chứng từ ở dạng PDF và ảnh thông thường thì mười năm sau vẫn mở được. Giữ ở định dạng riêng của một phần mềm nào đó thì phụ thuộc vào phần mềm ấy còn sống hay không.

Rủi ro lớn nhất lại là con người. Người dựng ra cách đặt tên và cấu trúc thư mục sẽ nghỉ việc vào một lúc nào đó, mang theo toàn bộ quy ước nằm trong đầu. Viết một trang hướng dẫn ngắn, để ngay trong thư mục gốc của kho, nói rõ thư mục nào chứa gì và tên file đọc thế nào. Một trang giấy đó có giá trị hơn nhiều so với công sức bỏ ra viết nó.

## Tra cứu được mới tính là lưu trữ

Điều kiện thứ ba của luật là tra cứu được trong suốt thời hạn. Đây là điều kiện hay bị coi nhẹ nhất.

Phép thử rất đơn giản: nhờ một người khác trong phòng tìm hộ một chứng từ của ba năm trước. Quá mười phút chưa ra thì kho tài liệu đó chưa đạt, dù dữ liệu vẫn còn nguyên vẹn.

File PDF scan nên bật nhận dạng chữ để tìm được theo nội dung bên trong chứ không chỉ theo tên file. Phần lớn máy scan văn phòng có sẵn tuỳ chọn này, chỉ là mặc định hay bị tắt.

## Bài này không thay được gì

Nói thẳng mấy giới hạn để bạn khỏi hiểu nhầm.

Đây không phải tư vấn pháp lý. Mình dẫn số điều để bạn biết đường tra, không phải để bạn trích dẫn lại.

Bản điện tử không thay thế được những bản gốc mà đơn vị bạn vẫn phải giữ bằng giấy. Scan xong đừng vội bỏ giấy đi.

Hoá đơn điện tử và chữ ký số thì mình chưa đụng tới ở đây. Hai thứ đó có quy định riêng và đủ dài để thành một bài khác.

Và trung thực với bạn: ở ba công ty mình đang làm, hiện trạng vẫn là mỗi nơi một mảnh — tủ hồ sơ ở kho, một phần trên Drive, dữ liệu MISA trên máy chủ nội bộ. Những gì viết ở trên là cách mình đang gom lại, chưa phải một hệ thống đã chạy trọn vẹn mười năm. Cái mình chắc chắn là bài học năm 2020: đừng để mọi bản lưu nằm chung một địa chỉ.

Chúc các bạn thành công.

## Link tham khảo

[https://luatvietnam.vn/ke-toan/luat-ke-toan-2015-101336-d1.html](https://luatvietnam.vn/ke-toan/luat-ke-toan-2015-101336-d1.html)

[https://luatvietnam.vn/ke-toan/nghi-dinh-174-2016-nd-cp-chinh-phu-111573-d1.html](https://luatvietnam.vn/ke-toan/nghi-dinh-174-2016-nd-cp-chinh-phu-111573-d1.html)
