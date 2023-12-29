---
title: "Hướng dẫn Nginx – Phần 3: Cài đặt SSL"
date: "2018-05-17"
categories: 
  - "database"
  - "thiet-ke-web"
  - "ubuntu"
  - "wordpress"
tags: 
  - "cai-ssl-tren-nginx"
  - "cau-hinh-nginx"
  - "huong-dan-nginx"
  - "lets-encrypt"
  - "nginx"
  - "nginx-co-ban"
  - "nginx-for-beginner"
header:
  overlay_image: /assets/images/Huong-dan-nginx-SSL-sofsog.com_.png
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)" 
  teaser: /assets/images/Huong-dan-nginx-SSL-sofsog.com_.png
toc: true
breadcrumbs: true
permalink: /thiet-ke-web/wordpress/huong-dan-nginx-phan-cai-dat-ssl
---

Bài này hoặc **loạt bài _hướng dẫn nginx_** này (nếu mình có thời gian) mình thực hiện bằng cách vừa học vừa viết lại , nguồn từ internet, chủ yếu mình lược dịch lại từ các trang web nước ngoài. Mục đích vừa để chia sẻ vừa để lại lưu trữ (sau này mình quên có thể vào để xem lại).

Nên đọc Hướng dẫn Nginx – Phần 1 và 2 trước:

[Hướng dẫn Nginx – Phần 1: Các khái niệm cơ bản](https://sofsog.com/thiet-ke-web/wordpress/huong-dan-nginx-phan-cac-khai-niem-ban)

[Hướng dẫn Nginx – Phần 2: Performance](https://sofsog.com/thiet-ke-web/wordpress/huong-dan-nginx-phan-performance)

Tiếp tục phần 3:

## **SSL và TLS**

**SSL** (standing for Socket Secure Layer) là một giao thức cung cấp kết nối an toàn qua HTTP.

**SSL** 1.0 được phát triển bởi Netscape và không bao giờ được phát hành công khai do các lỗi bảo mật nghiêm trọng. **SSL** 2.0 được phát hành vào năm 1995, cũng có một số vấn đề, dẫn đến việc ra đời SSL 3.0, được phát hành vào năm 1996

Phiên bản đầu tiên của [TLS](https://vi.wikipedia.org/wiki/Transport_Layer_Security) (Transport Layer Security) được viết dưới dạng bản nâng cấp lên SSL 3.0. Sau đó, TLS 1.1 và 1.2 xuất hiện. Thời điểm hiện tại, **TSL** 1.3 sắp ra mắt (đây thực sự là điều đáng để chờ đợi).

![Hướng dấn nginx](/assets/images/Huong-dan-nginx-SSL-sofsog.com_.png)

Về mặt kỹ thuật, **SSL** và **TLS** là khác nhau (vì mỗi thứ mô tả phiên bản khác nhau của một giao thức) - nhưng mọi người thường dùng chung tên của chúng.

## **Thiết lập SSL/TLS cơ bản**

Để xử lý lưu lượng HTTPS, bạn cần có chứng chỉ SSL / TLS. Thường tốn phí, hoặc bạn có thể sử dụng chứng chỉ miễn phí thông qua Let’s encrypt (Bên dưới có hướng dẫn đăng ký)

Khi bạn có chứng chỉ, bạn có thể chỉ cần bật HTTPS bằng cách:

- bắt đầu lắng nghe trên cổng `443` (cổng mặc định mà trình duyệt sẽ sử dụng khi bạn nhập `https://sofsog.com`)
- cung cấp chứng chỉ và key của nó

```nginx
server {
  listen 443 ssl default_server;
  listen [::]:443 ssl default_server;

  ssl_certificate /etc/nginx/ssl/sofsog.crt;
  ssl_certificate_key /etc/nginx/ssl/sofsog.key;
}
```

Chúng ta cũng có thể chỉnh cấu hình:

- chỉ sử dụng giao thức TLS. Tất cả các phiên bản SSL không được sử dụng nữa do các lỗ hổng nổi tiếng
- sử dụng mật mã máy chủ bảo mật được xác định trước (trường hợp tương tự như với các giao thức - những ngày đó chỉ một vài mật mã được coi là an toàn)

Hãy nhớ rằng các cài đặt ở trên luôn thay đổi. Bạn nên xem lại chúng thường xuyên.

```nginx
ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_ciphers EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:!MD5;
ssl_prefer_server_ciphers on;

server {
  listen 443 ssl default_server;
  listen [::]:443 ssl default_server;

  ssl_certificate /etc/nginx/ssl/sofsog.crt;
  ssl_certificate_key /etc/nginx/ssl/sofsog.key;
}
```
## **TLS Session Resumption**

Sử dụng HTTPS, đặt **TLS handshake** ở đầu trang của TCP. Điều này tăng đáng kể thời gian, trước khi truyền dữ liệu thực tế được thực hiện. Giả sử bạn đang yêu cầu **/image.jpg** từ Warsaw và kết nối với máy chủ gần nhất ở Berlin:

```terminal
Open connection

TCP Handshake:
Warsaw  ->------------------ synchronize packet (SYN) ----------------->- Berlin
Warsaw  -<--------- synchronise-acknowledgement packet (SYN-ACK) ------<- Berlin
Warsaw  ->------------------- acknowledgement (ACK) ------------------->- Berlin

TLS Handshake:
Warsaw  ->------------------------ Client Hello  ---------------------->- Berlin
Warsaw  -<------------------ Server Hello + Certificate ---------------<- Berlin
Warsaw  ->---------------------- Change Ciper Spec -------------------->- Berlin
Warsaw  -<---------------------- Change Ciper Spec --------------------<- Berlin

Data transfer:
Warsaw  ->---------------------- /image.jpg --------------------------->- Berlin
Warsaw  -<--------------------- (image data) --------------------------<- Berlin

Close connection
```

Để lưu 1 vòng trong khi _**TLS handshake,**_ và chi phí tính toán để tạo ra một key mới, chúng ta có thể sử dụng lại các tham số phiên (session parameters) trong yêu cầu đầu tiên (first request). Máy khách (client) và máy chủ (server) có thể lưu trữ các thông số phiên (session parameters)  phía sau Session ID key

```nginx
server {
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 1h;
}

```

## **OCSP Stapling****(xếp chồng****OCSP: Online Certificate Status Protocol)**

Chứn chỉ SSL  có thể bị thu hồi bất kỳ lúc nào. Để trình duyệt biết liệu chứng chỉ đã cho không còn hợp lệ, cần phải thực hiện truy vấn bổ sung qua Giao thức trạng thái chứng chỉ trực tuyến (OCSP). Thay vì yêu cầu người dùng thực hiện truy vấn OCSP đã cho, chúng ta có thể thực hiện nó trên máy chủ, lưu trữ kết quả và phục vụ phản hồi OCSP cho khách hàng, trong quá trình _**TLS handshake**_. Nó được gọi là _**OCSP stapling**_

```nginx
server {
  ssl_stapling on;
  ssl_stapling_verify on;                               # Xác minh phản hồi OCSP
  ssl_trusted_certificate /etc/nginx/ssl/lemonfrog.pem; # khai báo cho nginx vị trí của tất cả các chứng chỉ trung gian

  resolver 8.8.8.8 8.8.4.4 valid=86400s;                # độ phân giải của tên máy chủ phản hồi OCSP
  resolver_timeout 5s;
}
```

## **Security headers**

Dưới đây là một số _**header**_, đáng để bật tính bảo mật. Để biết thêm_**header**_ và thông tin chi tiết, bạn chắc chắn nên xem [OWASP Secure Headers Project.](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project)

### HTTP Strict-Transport-Security

Ciết tắt HSTS, thực thi tác _**user-agent**_ để gửi tất cả yêu cầu đến nguồn gốc (origin) qua HTTPS.

`add_header Strict-Transport-Security "max-age=31536000; includeSubdomains; preload";`

### X-Frame-Options

Cho biết liệu trình duyệt có nên hiển thị hay không một trang trong khung (_**frame**_), một thẻ _**iframe**_ hoặc một thẻ đối tượng (_**object**_)

`add_header X-Frame-Options DENY;`

### X-Content-Type-Options

Điều này sẽ ngăn các trình duyệt khỏi đánh hơi các file,  loại trừ loại file. File sẽ được hiểu là điều được khai báo trong Content-Type header.

`add_header X-Content-Type-Options nosniff;`

## Server tokens

Một phương pháp hay khác là ẩn thông tin về máy chủ web của bạn, trong trường  response header HTTP:

`Server : nginx/1.13.2`

Điều này có thể được thực hiện bằng cách tắt _**server_tokens directive**_

`server_tokens off;`

## Bonus về Let’s Encrypt

### Cài đặt

Cập nhật mới nhất có thể tìm thấy [ở đây](https://certbot.eff.org/lets-encrypt/ubuntuother-nginx)

Đối với mục đích thử nghiệm sử dụng [staging environment](https://letsencrypt.org/docs/staging-environment/),  để không phải exhaust [rate limits](https://letsencrypt.org/docs/rate-limits/).

### Tạo chứng chỉ mới

```terminal
certbot certonly --webroot --webroot-path /var/www/netguru/current/public/  \
          -d foo.netguru.co \
          -d bar.netguru.co
```

Hãy chắc chắn rằng nó có thể được gia hạn đúng cách

`certbot renew --dry-run`

Đảm bảo bạn đã thêm gia hạn tự động vào crontab. Chạy `crontab -e` và thêm dòng sau:

```terminal
0 3 * * * /usr/bin/certbot renew --quiet --renew-hook "/usr/sbin/nginx -s reload"
```


Kiểm tra xem SSL có hoạt động bình thường không thông qua [ssllabs](https://www.ssllabs.com/ssltest/)

## Kết luận

Cảm ơn các bạn đã đọc đến đây. Loạt bài này sẽ không thể có được nếu không có số lượng lớn tài nguyên được tìm thấy trên internet. Dưới đây là một số trang web tuyệt vời mà mình thấy đặc biệt hữu ích khi viết loạt bài này:

- [nginx docs](https://nginx.org/en/docs/)
- [nginx blog](https://www.nginx.com/blog/)
- [nginx fundamentals on udemy](https://www.udemy.com/nginx-fundamentals/)
- [Ilya Grigorik blog](https://www.igvita.com/), và cuốn sánh của anh ta: [High Performance Browser Networking](https://hpbn.co/)
- [Martin Fjordvald blog](https://blog.martinfjordvald.com/)

Mình sẽ rất vui khi thấy một số phản hồi hoặc thảo luận, vì vậy, vui lòng để lại nhận xét hoặc liên lạc lại bằng bất kỳ cách nào thuận tiện! Bạn có thích hướng dẫn này không? Bạn có gợi ý gì về chủ để tiếp theo không? Hoặc có thể bạn phát hiện ra một số lỗi? Hãy cho mình biết nhé và hẹn gặp lại bạn lần sau!

 Lược dịch từ: netguru.co
