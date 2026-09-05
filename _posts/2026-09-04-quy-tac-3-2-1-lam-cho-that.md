---
published: true
title: Quy tắc 3-2-1 làm cho thật - ngồi đếm lại mới biết mình thiếu gì
date: '2026-09-04'
categories:
  - server
  - thu-thuat-chung
tags:
  - backup
  - NAS
  - 3-2-1
  - RAID
  - snapshot
series: "Tự dựng server tại nhà"
series_thu_tu: 5
cap_do: "Cơ bản"
header:
  teaser: >-
    /assets/images/2026/2026-09-04-quy-tac-3-2-1-sofsog.com01.jpg
  og_image: >-
    /assets/images/2026/2026-09-04-quy-tac-3-2-1-sofsog.com01.jpg
excerpt: >-
  Ai đọc về sao lưu cũng thuộc quy tắc **3-2-1**, nhưng ít người ngồi đếm xem mình
  có thật hay không. Mình vừa đếm toàn bộ dữ liệu của mình, và kết quả không giống
  thứ mình vẫn đinh ninh.
toc: true
breadcrumbs: true
permalink: /server/quy-tac-3-2-1-lam-cho-that
---

Ai đọc về sao lưu cũng thuộc quy tắc 3-2-1: ba bản sao, hai loại phương tiện, một bản để ngoài nhà. Ít người ngồi đếm xem mình có thật hay không. Mình vừa đếm, và kết quả khác thứ mình vẫn đinh ninh.

{% include series-nav.html %}

![Hình sơ đồ quy tắc 3-2-1 gồm ba bản sao, hai loại lưu trữ và một bản để ngoài nhà sofsog.com](/assets/images/2026/2026-09-04-quy-tac-3-2-1-sofsog.com01.jpg)

Sơ đồ trên là quy tắc ở dạng gọn nhất, và phần lớn bài viết về sao lưu dừng lại đúng ở đây. Bài này đi tiếp: mình lấy đúng ba ô đó áp vào dữ liệu thật của mình rồi đếm. Chú ý mẩu giấy vàng góc dưới bên phải — **sao lưu là để khôi phục** — vì đó là chỗ mình trượt, và cũng là mục cuối cùng của bài.

## Vì sao 3-2-1 hay thất bại

Không phải vì quy tắc khó hiểu. Nó thất bại vì người ta cố áp cho **mọi thứ** cùng lúc.

Nhìn con NAS 1,9 TB rồi tính chuyện nhân ba chỗ đó lên, thấy tốn kém và mất công quá, thế là bỏ. Rồi vài tháng sau lại thấy áy náy, lại tính, lại bỏ.

Bước đầu tiên không phải mua ổ cứng. Nó là **ngồi phân loại**.

## Phân loại trước khi sao lưu

Mình chia dữ liệu làm ba nhóm, và cách đối xử với mỗi nhóm khác hẳn nhau.

**Không thể tạo lại.** Ảnh và video gia đình, chứng từ kế toán, kho mật khẩu. Mất là mất vĩnh viễn, không tiền nào mua lại được. Nhóm này bắt buộc đủ ba bản.

**Tạo lại được nhưng tốn công.** Dữ liệu làm việc, tệp cấu hình, ghi chú. Mất thì dựng lại được, nhưng mất vài ngày tới vài tuần. Nhóm này nên có ít nhất hai bản, ưu tiên thêm bản thứ ba khi có điều kiện.

**Mất cũng được.** Phim tải về. Mình có gần một terabyte phim trên NAS và **không sao lưu một byte nào** trong đó. Cần thì tải lại. Nếu đem nhân ba chỗ này lên thì chi phí sao lưu của mình tăng gấp mấy lần mà chẳng bảo vệ được thứ gì đáng giá.

Nói ra chuyện cố tình không sao lưu nghe hơi ngược, nhưng chính nó làm quy tắc 3-2-1 trở nên khả thi. Bảo vệ mọi thứ như nhau thì cuối cùng không bảo vệ được gì.

## Ngồi đếm thật

Đây là bảng mình liệt kê ra, không phải bảng lý thuyết:

| Dữ liệu | Bản chính | Bản hai | Bản ngoài nhà | Đủ chưa |
|---|---|---|---|---|
| Ảnh, video gia đình | Synology Photos trên NAS | Google Photos | có | Đủ |
| Dữ liệu công ty (16 GB) | máy ở văn phòng | NAS ở nhà | có | Đủ |
| Vault ghi chú | Gitea trên NAS | GitHub | GitLab | Đủ |
| Kho mật khẩu (8,4 MB) | NAS | bản chép ngày cùng NAS | Cloudflare R2 | Đủ |
| NodeWarden (86 MB) | Cloudflare | Koofr | NAS kéo về | Đủ |
| **Dữ liệu cá nhân (200 GB)** | **PC ở nhà** | **NAS ở nhà** | **chưa có** | **Thiếu** |
| Phim tải về | NAS | không | không | Cố ý bỏ |

Ngồi đếm xong mới thấy hai chuyện mình không ngờ.

## Dữ liệu công ty lại được bảo vệ tốt hơn dữ liệu cá nhân

Chuyện này không đến từ tính toán nào cả. Đơn giản vì máy làm việc đặt ở văn phòng còn con NAS đặt ở nhà, nên bản chính và bản sao tự nhiên nằm ở hai toà nhà khác nhau. Đúng tinh thần "một bản ngoài nhà" mà chẳng phải cố gắng gì.

Còn dữ liệu cá nhân thì ngược lại. Bản chính nằm trên PC ở nhà, bản sao nằm trên NAS cũng ở nhà, cách nhau vài mét. Đủ hai bản, nhưng cùng chung một đám cháy, một vụ trộm, một lần mất điện làm hỏng thiết bị.

[Vụ cháy văn phòng năm 2020](/ke-toan/luu-tru-chung-tu-ke-toan-10-nam) đã dạy mình đúng bài này, vậy mà sáu năm sau ngồi đếm lại vẫn thấy mình mắc lại ở chỗ khác.

## Thứ nhỏ được bảo vệ kỹ hơn thứ lớn

Chuyện thứ hai còn buồn cười hơn.

Kho mật khẩu 8,4 MB có ba bản trải ba nơi, có khử trùng lặp, có lịch kiểm tra phục hồi. NodeWarden 86 MB cũng ba bản. Cộng lại chưa tới 100 MB mà được chăm sóc kỹ nhất hệ thống.

Trong khi 200 GB dữ liệu cá nhân thì chỉ có hai bản cùng một nhà.

Lý do rất người: thứ nhỏ thì đẩy lên mây dễ, rẻ, cấu hình một lần rồi quên. Thứ lớn thì tốn tiền lưu trữ, tốn thời gian đẩy lên, và phải ngồi nghĩ xem đẩy cái gì. Nên ta làm cái dễ trước, rồi tưởng mình đã xong.

## Snapshot và RAID không tính là bản sao

Con NAS của mình bật snapshot cho tám thư mục chia sẻ và chạy RAID 5. Nghe thì có vẻ đã an toàn lắm.

Nhưng cả hai đều **nằm trên cùng một mảng đĩa**. Snapshot cứu bạn khỏi xoá nhầm và khỏi mã độc tống tiền, RAID cứu bạn khỏi một ổ chết. Không cái nào cứu bạn khỏi cháy, trộm, sét đánh, hay hỏng cả mảng.

Trong bảng đếm ở trên, mình cố tình không tính snapshot vào cột nào. Nó là lớp phục hồi nhanh, không phải bản sao lưu. Chỗ này mình đã viết kỹ hơn ở [bài về lưu trữ chứng từ](/ke-toan/luu-tru-chung-tu-ke-toan-10-nam) và [bài chọn NAS](/server/chon-nas-dau-tien-mua-dung-san-hay-tu-lap).

## Kế hoạch vá chỗ hổng

Phản xạ đầu tiên là đi mua thêm dung lượng đám mây cho đủ 200 GB. Mình sẽ không làm vậy.

Trong 200 GB đó, phần thật sự không thể tạo lại chắc chắn nhỏ hơn nhiều — phần lớn là tệp cài đặt, dữ liệu tạm, bản sao của thứ đã có ở nơi khác. Việc đúng là mở thư mục đó ra, phân loại theo ba nhóm ở đầu bài, rồi chỉ đẩy nhóm thứ nhất lên mây.

Làm vậy thì chi phí sao lưu có thể chỉ bằng một phần nhỏ, mà rủi ro giảm gần hết. Đây là công việc ngồi lọc chứ không phải công việc mua sắm, nên nó hay bị hoãn — mình cũng đang hoãn, và bài này viết ra một phần để tự thúc mình.

## Một cảnh báo về bản ngoài nhà

Bản ngoài nhà của ảnh gia đình mình là Google Photos. Nó chống được cháy và trộm, nhưng nó là tài khoản của một dịch vụ bên thứ ba.

Tài khoản bị khoá, bị chiếm, hoặc dịch vụ đổi chính sách thì bản đó biến mất mà bạn không kịp phản ứng. Bản sao trên mây bảo vệ bạn khỏi thảm hoạ vật lý, không bảo vệ bạn khỏi việc mất quyền vào tài khoản.

Vì vậy nếu bản ngoài nhà duy nhất của bạn là một tài khoản đám mây, hãy bật xác thực hai lớp cho nó và cất mã khôi phục ở nơi không nằm trong chính tài khoản đó.

## Phép thử duy nhất đáng tin

Bảng đếm ở trên chỉ nói bạn **có** bao nhiêu bản. Nó không nói bản nào mở ra được.

Mình đã viết chuyện này trong [bài về Vaultwarden](/server/vaultwarden-tren-nas-kho-mat-khau-cho-ca-nha): script sao lưu của mình chạy đúng suốt bảy tháng, rồi mình phát hiện nó có thể báo thành công trong khi không sao lưu gì cả, chỉ vì gọi lệnh bằng tên trần và không kiểm tra mã lỗi.

Nếu chỉ nhớ một câu từ bài này, hãy nhớ câu đó: **một bản sao lưu chưa từng được mở ra thử thì chưa phải bản sao lưu**. Mỗi vài tháng, chọn ngẫu nhiên vài tệp từ mỗi dòng trong bảng của bạn, khôi phục ra một thư mục riêng, mở lên xem. Mất mười lăm phút.

Chúc các bạn thành công.

## Link tham khảo

[https://www.backblaze.com/blog/the-3-2-1-backup-strategy/](https://www.backblaze.com/blog/the-3-2-1-backup-strategy/)

[https://restic.readthedocs.io](https://restic.readthedocs.io)
