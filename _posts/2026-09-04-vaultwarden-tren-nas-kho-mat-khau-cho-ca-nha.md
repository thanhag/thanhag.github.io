---
published: true
title: Vaultwarden trên NAS - kho mật khẩu cho cả nhà, không trả phí hằng tháng
date: '2026-09-04'
categories:
  - server
  - thu-thuat-chung
tags:
  - Vaultwarden
  - Bitwarden
  - NAS
  - Docker
  - restic
  - backup
series: "Tự dựng server tại nhà"
series_thu_tu: 3
cap_do: "Cơ bản"
excerpt: >-
  **Vaultwarden** là bản dựng lại của máy chủ Bitwarden, nhẹ tới mức chạy thoải mái
  trên một con NAS và dùng được với đúng ứng dụng Bitwarden sẵn có. Bài này là cách
  mình dựng nó, và quan trọng hơn nhiều: cách sao lưu để không mất kho mật khẩu.
toc: true
breadcrumbs: true
permalink: /server/vaultwarden-tren-nas-kho-mat-khau-cho-ca-nha
---

Kho mật khẩu là thứ mình muốn giữ trong nhà nhất. Vaultwarden là bản dựng lại của máy chủ Bitwarden bằng Rust, nhẹ tới mức chạy thoải mái trên một con NAS gia đình, và dùng được với đúng ứng dụng Bitwarden trên điện thoại lẫn tiện ích trình duyệt.

{% include series-nav.html %}

Bài này là cách mình dựng nó. Nhưng phần đáng đọc hơn nằm ở nửa sau: cách sao lưu, và một lỗi mình vừa phát hiện trong chính hệ thống sao lưu của mình khi ngồi viết bài này.

## Vì sao tự host

Dịch vụ quản lý mật khẩu trả phí hoạt động tốt. Mình tự host không phải vì tiếc tiền, mà vì kho mật khẩu là dữ liệu nhạy cảm nhất của một gia đình, và mình muốn nó nằm trên phần cứng mình cầm được.

Đổi lại, toàn bộ trách nhiệm giữ cho nó sống thuộc về mình. Nhà cung cấp trả phí lo backup thay bạn. Tự host thì backup hỏng là mất trắng, và không có bộ phận hỗ trợ nào để gọi.

Đó là lý do bài này dành phần lớn dung lượng cho việc sao lưu chứ không phải việc cài đặt. Cài Vaultwarden mất mười lăm phút. Làm cho nó đáng tin mới là phần thật sự tốn công.

## Điều kiện cần

Một con NAS chạy được Docker. Và một mạng riêng để truy cập từ ngoài — mình dùng [Tailscale, đã viết ở bài trước](/server/tailscale-vao-nas-tu-xa-khong-mo-port), nhờ đó **không phải mở cổng nào ra Internet**.

Điểm này quan trọng hơn nó có vẻ. Một máy chủ mật khẩu phơi thẳng ra Internet là mục tiêu bị quét liên tục. Nằm sau Tailscale thì chỉ thiết bị đã đăng nhập vào tài khoản của bạn mới nhìn thấy nó.

## Bước 1: Tệp docker-compose.yml

```yaml
version: "3.9"

services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    restart: unless-stopped
    ports:
      - "8443:80"
    environment:
      SIGNUPS_ALLOWED: "true"
      WEBSOCKET_ENABLED: "true"
    volumes:
      - /volume1/docker/vaultwarden/data:/data
      - /volume1/docker/vaultwarden/tls:/data/tls:ro
```

Toàn bộ dữ liệu nằm trong thư mục `data`. Sao lưu Vaultwarden thực chất là sao lưu đúng thư mục đó — kho của mình hiện **8,4 MB cho 544 tệp**, nhỏ tới mức dễ khiến người ta chủ quan không sao lưu.

`WEBSOCKET_ENABLED` cho phép các thiết bị nhận thay đổi ngay thay vì đợi lần đồng bộ sau.

## Bước 2: HTTPS bằng chứng chỉ Tailscale

Trình duyệt sẽ từ chối cho tiện ích Bitwarden nói chuyện với một máy chủ chạy HTTP trần. Bạn cần HTTPS thật.

Tailscale cấp chứng chỉ hợp lệ cho tên máy trong tailnet, miễn phí và tự gia hạn. Không phải mua chứng chỉ, không phải mở cổng 80 cho tổ chức cấp chứng chỉ xác minh, cũng không dính cảnh báo bảo mật như chứng chỉ tự ký. Đặt cặp tệp chứng chỉ vào thư mục `tls` rồi gắn vào container ở chế độ chỉ đọc như trong tệp cấu hình trên.

## Bước 3: Tạo tài khoản rồi khoá cửa lại

`SIGNUPS_ALLOWED: "true"` cho phép ai vào được địa chỉ này cũng tạo được tài khoản. Bạn cần nó lúc đầu để tạo tài khoản cho mình và cho người nhà.

Tạo xong thì **đổi lại thành `"false"`** rồi khởi động lại container. Đây là chỗ mình để quên khá lâu. Rủi ro có hẹp lại vì máy chủ chỉ nằm trong tailnet, nhưng đã khoá được cửa thì không có lý do gì để mở.

## Dùng trên máy và điện thoại

Cài đúng ứng dụng Bitwarden bình thường. Trước khi đăng nhập, vào phần cài đặt máy chủ và trỏ về địa chỉ máy chủ riêng của bạn thay vì máy chủ mặc định.

Từ đó mọi thứ hoạt động y như bản trả phí: tự điền mật khẩu, sinh mật khẩu mới, đồng bộ giữa các thiết bị. Điều kiện là thiết bị phải đang bật Tailscale — quên bật thì ứng dụng không đồng bộ được, và đây là câu hỏi đầu tiên cần tự hỏi mỗi khi thấy nó không chạy.

## Sao lưu: chép thư mục so với restic

Mình chạy song song hai cơ chế, và số liệu thật của chúng nói lên nhiều điều.

**Cách thứ nhất** là chép nguyên thư mục `data` sang một thư mục mới mỗi đêm. Đơn giản, ai cũng hiểu, và khôi phục chỉ là chép ngược lại. Hiện mình có **31 bản như vậy, từ 05/08 tới 04/09, tổng cộng 302 MB**.

**Cách thứ hai** là restic đẩy lên Cloudflare R2. Restic chỉ lưu phần dữ liệu thay đổi và khử trùng lặp phần giống nhau. Lần chạy gần nhất của mình:

```
Files:           0 new,     2 changed,   542 unmodified
Added to the repository: 511.517 KiB (39.138 KiB stored)
processed 544 files, 7.472 MiB in 0:06
snapshot 122c88b4 saved
```

Xử lý 7,472 MiB nhưng chỉ ghi thêm **39 KiB**, vì 542 tệp không đổi so với hôm trước.

Đặt cạnh nhau thì chênh lệch rất rõ:

| | Chép thư mục | restic |
|---|---|---|
| Số mốc phục hồi | 31 (mỗi ngày một bản) | tới 17, trải sáu tháng |
| Dung lượng chiếm | 302 MB | **8,67 MiB** |
| Nơi lưu | cùng con NAS | Cloudflare R2, ngoài nhà |

Restic giữ được nhiều mốc thời gian hơn, trải dài hơn, mà tốn chưa tới một phần ba mươi lăm dung lượng. Chính sách giữ bản của mình là bảy bản ngày, bốn bản tuần, sáu bản tháng:

```bash
restic forget --keep-daily 7 --keep-weekly 4 --keep-monthly 6 --prune
```

Bản chép thư mục vẫn có ích vì nó nằm ngay tại chỗ, khôi phục nhanh khi chỉ cần quay lại hôm qua. Nhưng nó nằm cùng con NAS với bản gốc, nên nó không phải là lớp chống thảm hoạ. Lớp đó là restic trên R2.

## Bản backup báo thành công mà không sao lưu gì

Đoạn này mình phát hiện đúng hôm viết bài, và nó đáng giá hơn mọi phần còn lại.

Script sao lưu cũ của mình gọi lệnh `restic` trần, tức là dựa vào biến `PATH` để tìm chương trình. Chạy dưới bộ lập lịch của DSM thì `PATH` có đủ, nên bảy tháng qua nó vẫn chạy đúng. Nhưng khi mình chạy tay script đó qua SSH:

```
===== Backup started at Fri Sep  4 11:00:19 WIB 2026 =====
./restic-backup.sh: line 24: restic: command not found
./restic-backup.sh: line 28: restic: command not found
===== Backup finished at Fri Sep  4 11:00:19 WIB 2026 =====
```

Nhìn dòng đầu và dòng cuối thì y hệt một lần sao lưu thành công. Script thoát với mã 0. Nếu chỉ liếc log hoặc chỉ dựa vào thông báo của bộ lập lịch, bạn sẽ tin rằng backup vẫn chạy.

Hai lỗi trong một script mười dòng. Thứ nhất là gọi chương trình bằng tên trần thay vì đường dẫn đầy đủ. Thứ hai, nghiêm trọng hơn, là **không kiểm tra mã lỗi ở bất kỳ đâu**. Bản sửa dùng đường dẫn tuyệt đối và bắt script gãy to tiếng:

```bash
RESTIC="/usr/local/bin/restic"

loi() {
  echo "===== LOI: $* - $(date) =====" >> "$LOGFILE"
  echo "LOI: $*" >&2
  exit 1
}

[ -x "$RESTIC" ] || loi "khong tim thay restic tai $RESTIC"
"$RESTIC" backup "$DATA" >> "$LOGFILE" 2>&1 || loi "restic backup that bai"
```

Nhân tiện, thông tin đăng nhập R2 trước đây nằm thẳng trong script, mà tệp đó để quyền `777`. Giờ chúng nằm trong một tệp `.env` quyền `600` và script nạp vào lúc chạy. Bài học chung: **script sao lưu cũng là một phần của hệ thống, nó cần được soi kỹ như phần còn lại.**

## Thử phục hồi

Mỗi vài tháng mình khôi phục một bản chụp ra thư mục riêng rồi mở thử, thay vì khôi phục đè lên dữ liệu đang chạy.

```bash
restic restore latest --target /volume1/docker/vaultwarden/restore-test
```

Kiểm tra thư mục kết quả có tệp cơ sở dữ liệu và các tệp đính kèm, dung lượng hợp lý. Mất năm phút, và nó là khác biệt giữa việc có backup thật với việc có một niềm tin.

## Vaultwarden hay NodeWarden

Nói thẳng hiện trạng: mình **đang chạy cả hai cùng lúc để so sánh**, chưa chốt cái nào.

Vaultwarden nằm trên NAS, sau Tailscale, dữ liệu hoàn toàn trong nhà. Đổi lại, mọi việc vận hành là của mình: NAS chết là kho mật khẩu ngừng, backup hỏng là mất, và bạn phải nhớ bật Tailscale.

NodeWarden chạy trên Cloudflare Workers, không cần máy chủ nào cả, truy cập được từ mọi nơi mà không cần mạng riêng. Tiện hơn hẳn. Nhưng dữ liệu nằm trên hạ tầng của bên khác.

Ai coi trọng việc dữ liệu nằm trong tầm tay thì chọn Vaultwarden. Ai coi trọng sự tiện lợi thì chọn NodeWarden. Mình chưa quyết được nên đang dùng song song vài tháng để tự trả lời. Bài về NodeWarden mình sẽ viết riêng sau khi có kết luận.

Chúc các bạn thành công.

## Link tham khảo

[https://github.com/dani-garcia/vaultwarden](https://github.com/dani-garcia/vaultwarden)

[https://restic.readthedocs.io](https://restic.readthedocs.io)

[https://tailscale.com/kb/1153/enabling-https](https://tailscale.com/kb/1153/enabling-https)
