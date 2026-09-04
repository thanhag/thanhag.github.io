---
published: true
title: NodeWarden hay Vaultwarden - chạy song song mấy tháng rồi mình chốt cái nào
date: '2026-09-04'
categories:
  - server
  - thu-thuat-chung
tags:
  - NodeWarden
  - Vaultwarden
  - Bitwarden
  - Cloudflare Workers
  - bảo mật
series: "Tự dựng server tại nhà"
series_thu_tu: 7
cap_do: "Nâng cao"
excerpt: >-
  Bài Vaultwarden trước mình hẹn sẽ viết tiếp sau khi có kết luận. Giờ có rồi:
  mình chốt **NodeWarden**. Bài này nói rõ đánh đổi bảo mật là gì, và những gì
  mình đã làm để bù lại.
toc: true
breadcrumbs: true
permalink: /server/nodewarden-hay-vaultwarden-chot-cai-nao
---

Ở [bài về Vaultwarden](/server/vaultwarden-tren-nas-kho-mat-khau-cho-ca-nha) mình viết là đang chạy song song cả hai và chưa chốt cái nào. Giờ đã chốt: mình dùng **NodeWarden**.

{% include series-nav.html %}

Bài này không phải bài hướng dẫn cài. Nó là lý do chọn, đánh đổi cụ thể phải trả, và những gì mình làm để bù lại đánh đổi đó.

## Vì sao chốt NodeWarden

Lý do rất đời thường: **nó tiện hơn và ít lỗi vặt hơn**.

Tiện, vì nó chạy trên Cloudflare Workers nên không cần mạng riêng. Ở đâu có Internet là dùng được, không phải nhớ bật Tailscale, không phụ thuộc con NAS ở nhà còn sống hay không.

Ít lỗi vặt, vì tiện ích trình duyệt của Bitwarden khi nối vào Vaultwarden thỉnh thoảng nạp lỗi. Không thường xuyên, nhưng đủ để khó chịu. Một trình quản lý mật khẩu thì phải luôn sẵn sàng, chứ mỗi lần trục trặc lại phải nghĩ xem lỗi ở đâu thì mất hết ý nghĩa.

Đổi lại là một phần bảo mật. Phần đó cụ thể thế nào, mình nói ngay dưới đây thay vì nói chung chung.

## Hai kiến trúc khác nhau ở đâu

| | Vaultwarden | NodeWarden |
|---|---|---|
| Chạy ở đâu | Docker trên NAS nhà mình | Cloudflare Workers |
| Dữ liệu nằm ở | ổ cứng của mình | Cloudflare D1 và R2 |
| Truy cập từ ngoài | phải qua Tailscale | mọi nơi có Internet |
| Máy chủ chết thì | tự mình sửa | Cloudflare lo |
| Thuật toán bảo vệ khoá | đổi được sang Argon2id | **khoá cứng PBKDF2** |
| Chi phí | tiền điện NAS | miễn phí ở quy mô cá nhân |

Dòng áp chót là đánh đổi lớn nhất, và mình sẽ nói kỹ.

## Đánh đổi cụ thể phải trả

### KDF bị khoá cứng, không nâng cấp được

NodeWarden dùng **PBKDF2 600.000 vòng** và không cho đổi sang Argon2id, dù hàm kiểm tra tham số trong mã nguồn có hỗ trợ Argon2id.

Đi tìm chỗ chặn thì thấy hai lớp độc lập. Endpoint đổi KDF trả về thông báo không hỗ trợ. Đường đổi qua endpoint mật khẩu cũng bị chặn riêng. Tạo tài khoản mới cũng không lách được, vì giao diện web ghi cứng loại KDF, và phần mã hoá phía trình duyệt chỉ có PBKDF2 chứ không có Argon2 — ép qua API thì chính giao diện đó không mở khoá được tài khoản vừa tạo.

Hệ quả cần hiểu rõ: **chống bẻ khoá ngoại tuyến giờ chỉ còn dựa vào độ mạnh của mật khẩu chính**. Không có lớp bù nào khác. Argon2id chống được tấn công bằng GPU tốt hơn PBKDF2 nhiều, và ở đây mình không có lựa chọn đó.

### Tệp sao lưu không được mã hoá

Đây là điều mình chỉ biết sau khi đọc mã nguồn phần tạo bản sao lưu, và nó quan trọng hơn cả mục trên.

Bản backup là tệp ZIP nén kiểu lưu trữ thuần, bên trong có một tệp JSON chứa nguyên các dòng cơ sở dữ liệu, gồm cả **mã bí mật của xác thực hai lớp ở dạng đọc được**.

Nghĩa là ai lấy được tệp backup thì lớp xác thực hai lớp coi như vô hiệu, và nội dung kho chỉ còn được bảo vệ bằng độ mạnh mật khẩu chính. Ba việc bắt buộc phải làm theo:

Thư mục chứa backup phải giới hạn quyền chặt, và **đừng để nó lọt vào phạm vi đồng bộ của Synology Drive** hay bất kỳ thư mục chia sẻ nào mở ra ngoài.

Khi mở tệp zip ra kiểm tra thì chỉ xem tệp kê khai, đừng mở tệp dữ liệu.

Và đừng bao giờ gửi tệp backup qua chat hay email như một tệp bình thường.

### Hai chỗ còn lại

Chính sách bảo mật nội dung của ứng dụng vẫn cho phép mã nội tuyến, làm nó mất phần lớn tác dụng chống tấn công chèn mã. Không sửa được nếu không tự chỉnh mã nguồn.

Và tên miền mình dùng là **miền miễn phí**. Nếu bị thu hồi hoặc tài khoản đăng ký bị chiếm, kẻ tấn công dựng được trang đăng nhập giả ngay trên chính tên miền đó — mật khẩu mạnh không cứu được tình huống này. Đây là chỗ mình sẽ đổi sang tên miền trả phí.

## Những gì đã làm để bù lại

Mấy việc dưới đây là thứ khiến mình yên tâm chuyển hẳn sang NodeWarden.

### Ẩn toàn bộ giao diện web

Biến `HIDE_WEB_VAULT` bật lên thì mọi đường dẫn giao diện web trả về `404`, chỉ còn phần API cho tiện ích trình duyệt và ứng dụng điện thoại. Kiểm chứng bằng cách gọi thử: trang chủ, trang cài đặt, tệp manifest đều `404`, còn các đường API vẫn trả về bình thường.

Kẻ tấn công dò trúng tên miền cũng không có trang đăng nhập nào để thử mật khẩu.

**Phải đặt biến này kiểu `Secret`, không phải `Text`.** Lý do rất dễ sập bẫy: tệp cấu hình của Worker không khai báo khối biến môi trường, mà lệnh triển khai sẽ ghi đè biến của Worker theo đúng tệp cấu hình đó. Biến kiểu văn bản thêm tay trên bảng điều khiển sẽ **bị xoá ở lần triển khai kế tiếp**, và giao diện web lặng lẽ hiện lại mà không ai báo. Biến kiểu bí mật thì lệnh triển khai không đụng tới.

Cũng đừng sửa tệp cấu hình trong bản sao mã nguồn để thêm khối đó. Bản sao đang sạch so với gốc, sửa vào là mất khả năng cập nhật nhanh khi có bản mới.

Đổi lại, khi đang ẩn thì mất Backup Center, Log Center, quản lý thiết bị và đổi mật khẩu qua web. Việc sao lưu tự động vẫn chạy vì nó là tác vụ định kỳ của Worker, không liên quan giao diện.

### Bật HSTS

Đặt ở Cloudflare, thời hạn sáu tháng, áp cho cả tên miền con. **Tắt Preload**, vì đây là miền miễn phí, mà vào danh sách preload là một cam kết rất khó gỡ về sau.

Bộ tiêu đề bảo mật sau khi lên phiên bản mới gồm HSTS, chính sách chặn nhúng khung, chặn đoán kiểu tệp, chính sách giới thiệu nguồn, và thẻ chặn công cụ tìm kiếm lập chỉ mục.

Đáng chú ý: bản cũ **không có tiêu đề bảo mật nào** — chính sách bảo mật nội dung chỉ nằm trong thẻ meta, mà theo chuẩn thì chỉ thị chặn nhúng khung bị bỏ qua khi đặt ở đó. Tức là trang đăng nhập có thể bị nhúng vào khung của trang khác. Chỉ riêng việc cập nhật phiên bản đã đóng lỗ này.

### Giới hạn tần suất đã có sẵn, và mình đã đo

Mình không tin vào tài liệu, nên bắn thử 35 yêu cầu liên tiếp vào đường dẫn kiểm tra tài khoản. Kết quả: đúng **30 lần trả về `200` rồi 5 lần trả về `429`**.

Cấu hình trong mã nguồn là 30 yêu cầu mỗi phút cho các đường nhạy cảm, 120 cho đọc, 200 cho API đã xác thực, và **sai mật khẩu 10 lần thì khoá 2 phút**.

Có một bài viết tiếng Việt hồi tháng 4 chê NodeWarden thiếu giới hạn tần suất. Thông tin đó đã lỗi thời.

### Đóng đăng ký và khoá tài khoản GitHub

Sau người dùng đầu tiên, mọi tài khoản mới đều phải có mã mời. Đây là mặc định của phần mềm chứ không phải mình cấu hình.

Còn tài khoản GitHub thì **bắt buộc bật xác thực hai lớp**. Lý do: Worker được xây từ bản sao mã nguồn của mình, nên ai chiếm được tài khoản GitHub là đẩy được mã độc vào trình duyệt đang mở kho mật khẩu. Mình cũng giữ cách đồng bộ thủ công và **không bật tự động đồng bộ**, để không có đường nào tự chạy mà mình không nhìn thấy.

## Chuỗi sao lưu ba lớp

| Lớp | Nơi lưu | Cơ chế |
|---|---|---|
| Bản chính | Cloudflare D1 | Worker tự chạy |
| Ngoài nhà | Koofr qua WebDAV | NodeWarden tự đẩy, 24 giờ một lần, giữ 30 bản |
| Tại chỗ | NAS | Cloud Sync tự kéo về, giữ cả bản Koofr đã dọn |

Trên NAS hiện có 10 tệp, mỗi tệp đúng 8.955.540 byte. Dung lượng giống hệt nhau từng ngày cho thấy đây là bản kết xuất toàn bộ mỗi lần, không phải sao lưu tăng dần. Khác hẳn cách restic làm ở bài Vaultwarden, nơi mỗi lần chỉ ghi thêm vài chục KB.

### Vì sao phải vòng qua Koofr

Câu hỏi hợp lý là sao không đẩy thẳng từ Worker về NAS.

Vì tác vụ định kỳ của Worker chạy trên hạ tầng biên của Cloudflare, nó chỉ gọi được những địa chỉ công khai. NAS của mình chỉ có địa chỉ trong mạng Tailscale nên Worker không nhìn thấy.

Muốn đẩy thẳng thì phải mở dịch vụ chia sẻ tệp của NAS ra Internet. Mà phần cấu hình đích trong NodeWarden chỉ nhận địa chỉ, tên đăng nhập và mật khẩu — **không gửi được tiêu đề tuỳ chỉnh**, nên không khoá đường hầm đó bằng mã dịch vụ của Cloudflare Access được.

Nên mình chọn hướng ngược lại: **để NAS kéo về**. Toàn bộ kết nối là đi ra, không mở thêm cổng nào. Đúng nguyên tắc đã dùng cho [Tailscale](/server/tailscale-vao-nas-tu-xa-khong-mo-port) và [PrivateBin](/server/privatebin-tren-nas-chia-se-text-co-mat-khau).

Phần đồng bộ trên NAS phải đặt **một chiều, chỉ tải bản mới về**. Để hai chiều thì có ngày NAS xoá nhầm rồi đẩy lệnh xoá ngược lên, mất luôn bản gốc. Nhớ tick thêm tuỳ chọn không xoá tệp ở đích khi nguồn đã xoá. Nhờ vậy bản trên NAS thành kho lưu trữ dài hạn chứ không chỉ là bản sao.

## Kiểm tra backup khi giao diện web đang ẩn

Vì đã ẩn giao diện nên không vào Backup Center được. Kiểm tra từ NAS qua SSH:

```bash
ls -la /volume1/.../Backup/nodewarden
unzip -p /volume1/.../Backup/nodewarden/<ten-file>.zip manifest.json
```

Tệp kê khai cho biết phiên bản ứng dụng, thời điểm kết xuất và số lượng bản ghi từng bảng để đối chiếu. Lần kiểm ngày 27/08/2026: phiên bản 1.8.0, 4.598 mục mật khẩu, 81 thư mục, 0 tệp đính kèm.

Nhắc lại vì quan trọng: **chỉ mở tệp kê khai, đừng mở tệp dữ liệu**.

## Phục hồi là ghi đè toàn bộ

Chỗ này phải biết trước khi cần dùng.

Đọc mã nguồn phần nhập dữ liệu thì chỉ có hai chế độ: mặc định chỉ chạy được trên một hệ thống trống, còn chế độ thay thế thì **xoá sạch toàn bộ các bảng rồi nạp lại**. Không có chế độ gộp. Mọi mục thêm vào sau ngày sao lưu sẽ mất.

Sau khi phục hồi, mật khẩu chính quay về mật khẩu tại thời điểm sao lưu, dấu bảo mật đổi nên **văng đăng nhập trên mọi thiết bị**, và mã xác thực hai lớp quay về giá trị cũ.

Bảng dữ liệu của tính năng gửi tệp tạm **không nằm trong bản sao lưu**.

Mình đã thử phục hồi thật trên chính tài khoản đang dùng ngày 27/08/2026 và thành công. Nói lại lần nữa điều đã viết ở [bài 3-2-1](/server/quy-tac-3-2-1-lam-cho-that): một bản sao lưu chưa từng được mở ra thử thì chưa phải bản sao lưu.

## Vậy bạn nên chọn cái nào

Không né bằng câu mỗi bên có cái hay riêng.

**Chọn Vaultwarden** nếu bạn coi trọng việc dữ liệu nằm trên phần cứng mình cầm được, và chấp nhận phải bật mạng riêng mỗi lần dùng. Nó cũng cho bạn đổi sang thuật toán bảo vệ khoá mạnh hơn, thứ NodeWarden không có.

**Chọn NodeWarden** nếu bạn muốn dùng ở mọi nơi mà không phải nghĩ, và chấp nhận dữ liệu nằm trên hạ tầng của bên khác cùng thuật toán bảo vệ khoá không nâng cấp được.

Mình chọn cái thứ hai, nhưng chỉ sau khi đã ẩn giao diện web, bật HSTS, đo lại giới hạn tần suất, khoá tài khoản GitHub bằng xác thực hai lớp, và dựng đủ ba lớp sao lưu. Nếu bỏ qua mấy bước đó thì đánh đổi bảo mật sẽ lớn hơn nhiều so với những gì mình mô tả ở đây.

Và dù chọn bên nào, **mật khẩu chính phải thật mạnh**. Với NodeWarden thì nó gần như là lớp phòng thủ cuối cùng.

Chúc các bạn thành công.

## Link tham khảo

[https://github.com/shuaiplus/nodewarden](https://github.com/shuaiplus/nodewarden)

[https://github.com/dani-garcia/vaultwarden](https://github.com/dani-garcia/vaultwarden)

[https://developers.cloudflare.com/workers/configuration/secrets/](https://developers.cloudflare.com/workers/configuration/secrets/)

[https://bitwarden.com/help/kdf-algorithms/](https://bitwarden.com/help/kdf-algorithms/)
