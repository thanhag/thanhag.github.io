---
published: true
title: PrivateBin trên NAS - link chia sẻ text có mật khẩu, không giới hạn 31 ngày
date: '2026-09-04'
categories:
  - server
  - thu-thuat-chung
tags:
  - PrivateBin
  - NAS
  - Docker
  - Tailscale
  - bảo mật
series: "Tự dựng server tại nhà"
series_thu_tu: 6
cap_do: "Nâng cao"
header:
  teaser: >-
    /assets/images/2026/2026-09-04-privatebin-tren-nas-sofsog.com01.png
  overlay_image: >-
    /assets/images/2026/2026-09-04-privatebin-tren-nas-sofsog.com01.png
  og_image: >-
    /assets/images/2026/2026-09-04-privatebin-tren-nas-sofsog.com01.png
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)"
excerpt: >-
  Cần một đường link chứa text, mở ra phải nhập mật khẩu mới đọc được, và **không tự
  hết hạn sau 31 ngày** như Bitwarden Send. Bài này là toàn bộ cấu hình thật, kèm bốn
  cạm bẫy mình đã vấp khi dựng.
toc: true
breadcrumbs: true
permalink: /server/privatebin-tren-nas-chia-se-text-co-mat-khau
---

Mình cần một đường link chứa đoạn text, ai mở phải nhập mật khẩu mới đọc được, và quan trọng nhất là **không tự biến mất sau 31 ngày**. Bài này viết chi tiết hơn mấy bài trước: đầy đủ tệp cấu hình, đầy đủ lệnh, và bốn chỗ mình đã vấp.

{% include series-nav.html %}

## Vì sao Bitwarden Send không giải được

Bitwarden có tính năng **Send** làm đúng việc này, nhưng thời hạn tối đa là 31 ngày.

Mình đã thử chỉnh phía máy chủ Vaultwarden và không được. Lý do: **giới hạn 31 ngày nằm trong ứng dụng Bitwarden phía người dùng**, không nằm ở máy chủ. Sửa biến môi trường của Vaultwarden bao nhiêu cũng vô ích vì ứng dụng mới là nơi áp giới hạn đó.

Nên mình dựng PrivateBin bên cạnh, làm đúng một việc mà Send không làm được.

![Hình trình soạn thảo PrivateBin với ô Expires đặt thành Never sofsog.com](/assets/images/2026/2026-09-04-privatebin-tren-nas-sofsog.com01.png)

Đây là chỗ khác biệt nằm gọn trong một ô chọn: **`Expires` để `Never`**. Cạnh nó là ô `Password` và ô `Burn after reading` — xoá sạch ngay sau lần mở đầu tiên. Ba thứ đó là toàn bộ lý do mình dựng thêm một dịch vụ nữa thay vì cố ép Bitwarden Send làm việc nó không làm được.

## PrivateBin làm việc theo kiểu nào

PrivateBin **mã hoá ngay trong trình duyệt** trước khi gửi lên máy chủ. Khoá giải mã nằm ở phần sau dấu `#` của URL, mà theo chuẩn HTTP thì phần này **không bao giờ được gửi lên máy chủ**.

Nghĩa là máy chủ giữ một khối dữ liệu đã mã hoá mà chính nó không đọc được. Kể cả bạn là người quản trị, kể cả có toàn quyền trên NAS, mở tệp paste ra cũng chỉ thấy chuỗi rối.

Điều đó dẫn tới hệ quả cần nhớ: **mất phần sau dấu `#` là mất nội dung vĩnh viễn**. Không có nút khôi phục nào cả.

![Hình trang README của dự án PrivateBin trên GitHub sofsog.com](/assets/images/2026/2026-09-04-privatebin-tren-nas-sofsog.com02.png)

Dự án là bản rẽ nhánh từ ZeroBin, mã nguồn mở, và README nói thẳng điều quan trọng nhất: máy chủ **không biết gì** về nội dung được lưu. Một chi tiết nhỏ đáng để ý lúc mình chụp tấm này — README còn ghi `Current version: 2.0.5` trong khi bản `latest` mình vừa kéo về đã là `2.0.6`. Đọc README để hiểu dự án thì tốt, nhưng đừng dùng nó để biết mình đang chạy phiên bản nào.

## Kiến trúc ba lớp

| Lớp | Nhiệm vụ |
|---|---|
| PrivateBin trong Docker, bind `127.0.0.1:8082` | mã hoá nội dung, quản lý mật khẩu và hạn dùng |
| `tailscale serve --https=10443` | cấp chứng chỉ HTTPS thật, chỉ cho tailnet vào |
| Bind vào localhost | chặn cả máy trong mạng LAN nhà |

Lớp thứ ba là chỗ nhiều người làm khác mình. Bind vào `127.0.0.1` nghĩa là **ngay cả máy tính trong nhà cũng không mở được** nếu không đi qua Tailscale. Đường vào chỉ có một.

## Bước 1: Tệp docker-compose.yml

Toàn bộ đặt trong `/volume1/docker/privatebin/`:

```yaml
services:
  privatebin:
    image: privatebin/nginx-fpm-alpine:latest
    container_name: privatebin
    restart: unless-stopped
    ports:
      - "127.0.0.1:8082:8080"
    volumes:
      - /volume1/docker/privatebin/data:/srv/data
      - /volume1/docker/privatebin/conf.php:/srv/cfg/conf.php:ro
    environment:
      - TZ=Asia/Ho_Chi_Minh
```

Dòng đáng chú ý nhất là `"127.0.0.1:8082:8080"`. Nếu bạn viết `"8082:8080"` như phần lớn hướng dẫn trên mạng thì Docker hiểu là `0.0.0.0`, tức **mọi máy trong mạng LAN đều mở được** mà chẳng cần Tailscale. Thêm `127.0.0.1:` vào đầu là khác biệt giữa một dịch vụ kín và một dịch vụ hở.

Tệp `conf.php` gắn vào chế độ `:ro` để container không sửa được nó.

## Bước 2: Tệp conf.php

PrivateBin đọc cấu hình dạng INI, nhưng tệp phải mở đầu bằng một dòng PHP để nếu ai đó gọi thẳng vào tệp qua trình duyệt thì nhận `403` thay vì thấy nội dung:

```ini
;<?php http_response_code(403); /*

[main]
name = "PrivateBin"
discussion = false
opendiscussion = false
password = true
fileupload = false
burnafterreadingselected = false
defaultformatter = "plaintext"
sizelimit = 10485760

[model]
class = Filesystem

[model_options]
dir = "/srv/data"

[expire]
default = "never"

[expire_options]
5min = 300
10min = 600
1hour = 3600
1day = 86400
1week = 604800
1month = 2592000
1year = 31536000
never = 0

[traffic]
limit = 10

[purge]
limit = 300
batchsize = 10
;*/
```

Giải thích mấy dòng quan trọng:

`discussion` và `opendiscussion` đặt `false` để tắt phần bình luận dưới mỗi paste. Dịch vụ này để gửi mật khẩu, không phải diễn đàn.

`password = true` bật ô nhập mật khẩu khi tạo paste. Đây là lý do chính dựng nó.

`fileupload = false` chỉ cho gửi text. Bật lên thì thư mục dữ liệu phình rất nhanh.

`[model] class = Filesystem` lưu paste ra tệp thay vì dùng cơ sở dữ liệu. Ít thành phần hơn, sao lưu chỉ là chép thư mục.

`[expire] default = "never"` là mặc định khi mở trang. Đây chính là thứ Bitwarden Send không cho.

`[traffic] limit = 10` là số giây tối thiểu giữa hai lần tạo paste từ cùng một địa chỉ IP.

## Bước 3: Quyền thư mục dữ liệu

Bước này mà bỏ qua thì container vẫn chạy nhưng không lưu được gì:

```bash
sudo chown -R 65534:82 /volume1/docker/privatebin/data
```

`65534` là user `nobody`, tức tiến trình php-fpm bên trong container. `82` là group `www-data` của nginx. Container chạy dưới hai định danh đó, nên thư mục phải thuộc về chúng thì mới ghi được.

## Bước 4: Khởi động

```bash
sudo /usr/local/bin/docker compose \
  -f /volume1/docker/privatebin/docker-compose.yml up -d
```

Kiểm tra container sống chưa:

```bash
sudo /usr/local/bin/docker logs --tail 20 privatebin
```

## Bước 5: Mở ra qua Tailscale

```bash
sudo /usr/local/bin/tailscale serve --bg --yes \
  --https=10443 http://127.0.0.1:8082
```

Rồi xác nhận:

```bash
tailscale serve status
```

```
nas-nha.<ten-tailnet>.ts.net:10443 (tailnet only)
|-- / proxy http://127.0.0.1:8082
```

Dòng **`(tailnet only)`** là thứ phải nhìn thấy. Nếu nó ghi khác, dịch vụ của bạn đang mở ra Internet.

Đừng dùng `tailscale funnel` cho việc này. Funnel đẩy dịch vụ ra Internet công cộng, biến một kho mật khẩu riêng thành mục tiêu bị quét.

## Bốn cạm bẫy đã vấp

### 1. Thiếu section `[model]` thì trang trả 500 với thân rỗng

Đây là lỗi tốn thời gian nhất. PrivateBin **không** tự rơi về giá trị mặc định cho section này — nó ném ngoại lệ thẳng, và nginx trả về `500` với nội dung trống trơn. Trình duyệt không hiện gì để bạn lần ra.

Cách duy nhất thấy được nguyên nhân là đọc log container. Nhớ điều này thì tiết kiệm được cả buổi tối.

### 2. Cổng 443, 8443 và 5001 đều đã bận

DSM giữ cổng `443`, và Tailscale trên máy này chạy ở chế độ kernel networking nên phải chiếm socket thật, không lách được. `serve --https=443` sẽ báo *address already in use*. Hai cổng quen thuộc khác là 8443 và 5001 cũng đã có chủ.

Mình dùng **10443**. Con số không quan trọng, quan trọng là kiểm tra trước cho đỡ mất công.

### 3. HTTP thuần làm PrivateBin hỏng hoàn toàn

Cạm bẫy này tinh vi nhất và đáng để hiểu kỹ.

Nếu bỏ `tailscale serve` mà bind thẳng container vào địa chỉ Tailscale của NAS, đường link sẽ là `http://` trần. Khi đó **trang mở lên bình thường nhưng không tạo được paste**.

Lý do: PrivateBin mã hoá bằng **WebCrypto**, cụ thể là `crypto.subtle`. Trình duyệt chỉ cấp API này trong *secure context*, tức HTTPS hoặc localhost. Trên HTTP thuần, `crypto.subtle` đơn giản là không tồn tại, và trang không có cách nào mã hoá nội dung.

Vậy nên `tailscale serve` ở đây **bắt buộc**, không phải để cho tiện. Nó là thứ cấp chứng chỉ HTTPS thật, và không có nó thì phần mềm không hoạt động.

### 4. `sudo` trên DSM không thấy `/usr/local/bin`

Gõ `sudo tailscale ...` hay `sudo docker ...` sẽ nhận *command not found*, dù chạy không có `sudo` thì tìm thấy bình thường. Nguyên nhân là `sudo` trên DSM dùng một biến `PATH` khác.

Ghi đủ đường dẫn tuyệt đối là xong: `sudo /usr/local/bin/tailscale`, `sudo /usr/local/bin/docker`.

## Khi trang trắng mà log không nói gì

Sau lần vật lộn với lỗi `500` ở trên, mình viết một script chẩn đoán chạy năm bước, để lần sau có sự cố thì chỉ cần gọi nó.

Bước quan trọng nhất là bước cuối: nó chạy thẳng `index.php` bằng PHP với `display_errors` bật, nên ngoại lệ thật hiện ra thay vì bị nginx nuốt mất:

```bash
docker exec privatebin sh -c 'php -d display_errors=1 -d error_reporting=E_ALL -r "
  \$_SERVER[\"REQUEST_METHOD\"]=\"GET\";
  \$_SERVER[\"REMOTE_ADDR\"]=\"127.0.0.1\";
  chdir(\"/srv\");
  try { require \"/srv/index.php\"; }
  catch (Throwable \$e) { echo \"\n>>> \" . get_class(\$e) . \": \" . \$e->getMessage() . \"\n\"; }
"'
```

Bốn bước còn lại kiểm tra: log container, container đang chạy dưới user nào, thư mục `/srv/data` có ghi được không, và `conf.php` có phân tích được không. Bước kiểm tra quyền ghi làm bằng cách tạo một tệp thử rồi xoá đi — cách chắc chắn hơn là ngồi đọc quyền bằng mắt.

## Thu hồi một link đã gửi

**Cách chính:** ngay sau khi tạo paste, PrivateBin hiện một **link xoá** riêng. Lưu nó lại. Mở link đó là paste biến mất, không cần SSH, không cần quyền root.

**Nếu đã mất link xoá** thì phải vào tận đĩa. Mình viết một script nhỏ để làm việc đó cho an toàn, vì thư mục dữ liệu còn chứa `salt.php`, `traffic_limiter.php` và `purge_limiter.php`. Xoá nhầm mấy tệp đó là hỏng cả dịch vụ.

Cách script phân biệt: **ID paste luôn là 16 ký tự hex**, nên nó lọc bằng biểu thức chính quy `^[0-9a-f]{16}$` và bỏ qua mọi thứ khác.

```sh
tim_paste() {
    find "$DATA" -type f -name '*.php' | while read -r f; do
        b=$(basename "$f" .php)
        if echo "$b" | grep -qE '^[0-9a-f]{16}$'; then
            echo "$f"
        fi
    done
}
```

Script nhận cả URL đầy đủ rồi tự cắt lấy ID, hiện tệp sắp xoá kèm ngày tạo, và bắt gõ đúng chữ `xoa` để xác nhận. Xoá xong nó kiểm tra lại tệp đã biến mất chưa rồi mới báo thành công.

Cẩn thận tới mức đó vì đây là thao tác không hoàn tác được.

## Những gì cách làm này không làm được

Nói thẳng để bạn khỏi dựng xong mới phát hiện.

**Người ngoài tailnet không mở được link.** Đây là giới hạn lớn nhất. Người nhận cần đủ ba thứ: URL đầy đủ kèm phần sau dấu `#`, mật khẩu, và **đang ở trong tailnet của bạn**. Gửi cho người lạ hay đối tác thì cách này không dùng được — muốn vậy phải bật Funnel, mà như đã nói ở trên, đó là đánh đổi mình không chọn.

**Bộ đếm giới hạn có thể chặn nhầm.** Qua `tailscale serve`, PrivateBin có thể thấy mọi yêu cầu đến từ cùng một địa chỉ. Nhiều người tạo paste cùng lúc sẽ vướng `[traffic] limit`. Gặp trường hợp đó thì hạ về `0`.

**Thư mục dữ liệu sẽ phình dần.** Cơ chế dọn dẹp trong `[purge]` chỉ đụng tới paste **đã hết hạn**. Paste đặt `never` thì không bao giờ bị dọn — đúng như ta muốn, nhưng nghĩa là phải tự để mắt.

**Không có bản sao lưu thì mất hết.** Toàn bộ paste nằm trong thư mục `data`. Nó nhỏ nên dễ bị bỏ quên khi lập kế hoạch sao lưu, mà mất là mất luôn vì nội dung đã mã hoá không thể dựng lại từ đâu khác.

Chúc các bạn thành công.

## Link tham khảo

[https://privatebin.info/](https://privatebin.info/)

[https://github.com/PrivateBin/PrivateBin/wiki/Configuration](https://github.com/PrivateBin/PrivateBin/wiki/Configuration)

[https://tailscale.com/kb/1242/tailscale-serve](https://tailscale.com/kb/1242/tailscale-serve)

[https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts](https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts)
