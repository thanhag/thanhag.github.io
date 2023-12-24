---
title: "Hướng dẫn Nginx - Phần 1: Các khái niệm cơ bản"
date: "2018-05-10"
categories: 
  - "database"
  - "server"
  - "wordpress"
tags: 
  - "cau-hinh-nginx"
  - "huong-dan-nginx"
  - "nginx"
  - "nginx-co-ban"
  - "nginx-for-beginner"
header:
  image: /assets/images/Huong-dan-nginx-sofsog.com_.png
  teaser: /assets/images/Huong-dan-nginx-sofsog.com_.png
toc: true
breadcrumbs: true
permalink: /thiet-ke-web/wordpress/huong-dan-nginx-phan-cac-khai-niem-ban
---

Bài này hoặc **loạt bài** này (nếu mình có thời gian) mình thực hiện bằng cách vừa học vừa viết lại, nguồn từ internet, chủ yếu mình lược dịch lại từ các trang web nước ngoài. Mục đích vừa để chia sẻ vừa để lại lưu trữ (sau này mình quên có thể vào để xem lại). Ok, dài dòng đủ rồi, vào bài thôi:

Xem thêm bài liên quan:

[Hướng dẫn Nginx – Phần 2: Performance](https://sofsog.com/thiet-ke-web/wordpress/huong-dan-nginx-phan-performance)

## Giới thiệu về nginx

Nếu bạn tìm tới bài viết này chắc cũng đã hiểu sơ qua về _**Nginx**_. _**Nginx**_ ban đầu được tạo ra như một máy chủ web để giải quyết [vấn đề C10k](https://en.wikipedia.org/wiki/C10k_problem) . Và như một máy chủ web (web server) , nó có thể phục vụ dữ liệu của bạn với tốc độ gần bằng ánh sáng. Nhưng _**Nginx**_ không chỉ là một máy chủ web. Bạn có thể sử dụng nó như một [reverse proxy](https://vi.wikipedia.org/wiki/Reverse_proxy), làm cho việc tích hợp dễ dàng với các máy chủ ngược dòng chậm hơn (slower upstream servers) (như Unicorn, hoặc Puma). Bạn có thể phân phối lưu lượng truy cập của bạn một cách hoàn hảo (load balancer: cân bằng tải), stream media, thay đổi kích thước ảnh khi đang di chuyển, cache nội dung, và nhiều thứ nữa.

![Huong-dan-nginx-sofsog.com](/assets/images/Huong-dan-nginx-sofsog.com_.png) Huong-dan-nginx-sofsog.com

Kiến trúc cơ bản của _**nginx**_ bao gồm một quy trình tổng (Master process) và các công nhân (workers) của nó. Master process phải đọc file cấu hình và duy trì những "process worker", trong khi các workers thực hiện xử lý các yêu cầu thực tế.

## Các lệnh cơ bản

Để bắt đầu _**nginx**_, bạn chỉ cần gõ:

`sudo nginx`

Trong lúc _**nginx**_ đang chạy, bạn có thể quản lý nó bằng cách gửi các lệnh thích hợp:

`sudo nginx -s signal_thich-hop`

#### Một số Signal có sẵn

- `stop`: shutdown nhanh _**nginx**_
- `quit`: shutdown một cách cẩn thận, duyên dáng (^\_^) (Chờ đợi các workers hoàn thành các tiến trình của chúng rồi mới tắt)
- `reload`: Tải lại file cấu hình
- `reopen`: Mở lại các file nhật ký (file log)

## Directive và Context (chỉ thị và bối cảnh, cái này tốt nhất là không dịch)

Theo mặc định, file cấu hình của _**nginx**_ có thể được tìm thấy trong các đường dẫn sau:

- `/etc/nginx/nginx.conf`,
- `/usr/local/etc/nginx/nginx.conf`, hoặc
- `/usr/local/nginx/conf/nginx.conf`

### Trong file cấu hình này bao gồm

- **directive**: tùy chọn chứa tên và thông số (name và parameters), phải được kết thúc bằng dấu chấm phẩy.

```Nginx
gzip on;
```

- **context**: Đây là nơi để bạn có thể khai báo các directive (tương tự như phạm vi "scope" trong các ngôn ngữ lập trình)

```Nginx
worker_processes 2; # directive trong global context (chỉ thị trong ngữ cảnh chung)

http {              # http context (ngữ cảnh http)
    gzip on;        # directive trong http context

  server {          # server context (ngữ cảnh server)
    listen 80;      # directive trong server context
  }
}
```

## Các loại directive

Bạn phải cẩn thận khi sử dụng một **directive** trong nhiều **context**, vì mô hình kế thừa (inheritance model) là khác  nhau đối với các **directive** khác nhau. Có 3 loại **directive**, mỗi loại lại có mô hình kế thừa (inheritance model) riêng.

### Normal

**Directive** này chỉ có một giá trị cho mỗi **context**. Ngoài ra, nó chỉ có thể được định nghĩa một lần trong **context**.  Các **subcontext** (ngữ cảnh con) có thể ghi đè **directive** cha (parent directive), nhưng việc ghi đè này chỉ hợp lệ trong đã **subcontext** nêu.

```Nginx
gzip on;
gzip off; # Không hợp lệ, vì chỉ có một directive trong cùng một context.
```

```Nginx
server {
  location /downloads {
    gzip off;
  }

  location /assets {
    # gzip được bật ở đây
  }
}
```

### Array

Việc thêm nhiều **directive** trong cùng một **context** sẽ thêm vào các giá trị, thay vì ghi đè chúng hoàn toàn. Việc định nghĩa một **directive** trong một **subcontext** sẽ ghi đè tất cả các giá trị cha trong **subcontext** đã cho.

```Nginx
error_log /var/log/nginx/error.log;
error_log /var/log/nginx/error_notive.log notice;
error_log /var/log/nginx/error_debug.log debug;

server {
  location /downloads {
    # Dòng dưới này sẽ ghi đè toàn bộ các directive đã cho bên trên
    error_log /var/log/nginx/error_downloads.log;
  }
}
```

#### Action directive (chỉ thị hành động)

Hành động (action) là loại **directive** thay đổi mọi thứ. Hành vi kế thưa chúng sẽ phụ thuộc vào mô-đun.

Ví dụ, trong trường hợp **rewrite directive**, mỗi **directive** phù hợp sẽ được thực hiện:

```Nginx
server {
  rewrite ^ /foobar;

  location /foobar {
    rewrite ^ /foo;
    rewrite ^ /bar;
  }
}
```

Nếu user nạp: `/sample`:

- **server rewrite** được thực hiện , rewriting từ `/sample`, thành `/foobar`
- **location `/foobar`** khớp (subcontext)
- **location rewrite** ở dòng đầu tiền sẽ được thực hiện, rewriting từ `/foobar`, thành `/foo`
- **location rewrite** ở dòng thứ hai được thực hiện tiếp sau đó, rewriting từ `/foo`, thành `/bar`

Một ví dụ khác với **return directive**:

```Nginx
server {
  location / {
    return 200;
    return 404;
  }
}
```

Trong trường hợp bên trên, trạng thái 404 được trả về ngay lập tức.

## Processing requests

Bên Trong _**nginx**_, ban có thể chỉ định nhiều máy chủ ảo, mỗi máy chủ được mô tả bằng **_server { }_** **context** (ngữ cảnh server)

```Nginx
server {
  listen      \*:80 default\_server;
  server\_name sofsog.com;

  return 200 "Hello from sofsog.com";
}

server {
  listen      \*:80;
  server\_name server2.com;

  return 200 "Hello from server2.com";
}

server {
  listen      \*:81;
  server\_name server3.com;

  return 200 "Hello from server3.com";
}
```

Đoạn cấu hình trên cung cấp cho _**nginx**_ hiểu cách xử lý các yêu cầu gửi đến. _**Nginx**_ trước tiên sẽ kiểm tra **directive _listen_** để kiểm tra xem máy chủ ảo (virtual server) nào đang  lắng nghe trên sự kết hợp giữa **IP:port** đã cho. Sau đó, giá trị từ **directive _server\_name_** được kiểm tra dựa trên "H_ost_ header" lưu trữ tên miền của máy chủ.

_**Nginx**_ sẽ chọn máy chủ ảo theo thứ tự sau:

1. Danh sách server trên IP:port, với  một `server_name` directive phù hợp (match)
2. Danh sách server trên IP:port, với `default_server` được đánh dấu
3. Danh sách server trên IP:port, đầu tiên được định nghĩa
4. Nếu không có kết quả phù hợp, từ chối kết nối.

Trong ví dụ cấu hình bên trên, kết quả sẽ là:

```bash
Gửi yêu cầu đến: server2.com:80     => "Hello from server2.com"
Gửi yêu cầu đến www.server2.com:80 => "Hello from sofsog.com"
Gửi yêu cầu đến server3.com:80     => "Hello from sofsog.com"
Gửi yêu cầu đến server2.com:81     => "Hello from server3.com"
Gửi yêu cầu đến server3.com:81     => "Hello from server3.com"
```

## _`server_name`_ directive

**_`server_name`_ directive** chấp nhận nhiều giá trị. Nó cũng xử lý các ký tự đại diện và biểu thức thông dụng. (wildcard và regular expressions)

```Nginx
server_name sofsog.com www.sofsog.com; # exact match
server_name *.sofsog.com;              # wildcard matching
server_name sofsog.*;                  # wildcard matching
server_name ~^[0-9]*\.sofsog\.com$;   # regular expressions matching
```

Khi có sự không rõ ràng, _**nginx**_ sử dụng thứ tự sau:

1. Tên chính xác
2. Tên ký tự đại diện dài nhất bắt đầu bằng dấu sao, vd: “\*.example.org”
3. Tên ký tự đại diện dài nhất kết thúc bằng dấu sao, vd: “mail.\*”
4. Biểu thức thông dụng (regular expressions) khớp đầu tiên (Theo thứ tự xuất hiện trong file cấu hình)

_**Nginx**_ sẽ lưu trữ 02 hash tables (bảng băm) là: tên chính xác, tên ký tự đại diện dài nhất bắt đầu bằng dấu sao, tên ký tự đại diện dài nhất kết thúc bằng dấu sao. Nếu kết quả không nằm trong bất kỳ bảng nào, các biểu thức thông đụng (regular expressions) sẽ được kiểm tra tuần tự.

Gần ghi nhớ rằng:

```Nginx
server_name .sofsog.com;
```

Là viết tắt của:

```Nginx
server_name  sofsog.com  www.sofsog.com  *.sofsog.com;
```

Nhưng giữa 2 cách viết trên vẫn có sự khác biệt là: _**.sofsog.com**_ được lưu trữ trong bảng thứ hai, có nghĩa là nó chậm hơn một chút so với khai báo rõ ràng (sofsog.com www.sofsog.com \*.sofsog.com)

## **_`listen`_ directive**

Trong hầu hết các trường hợp, bạn sẽ thấy rằng **_`listen`_ directive** chấp nhận các giá trị IP:port

```Nginx
listen 127.0.0.1:80;
listen 127.0.0.1;    # Sẽ mặc định cổng 80

listen *:81;
listen 81;           # mặc định tất cả các IP (tên miền) được sử dụng

listen [::]:80;      # IPv6 addresses
listen [::1];        # IPv6 addresses
```

Tuy nhiên, bạn cũng có thể chỉ định **UNIX-domain sockets**

```Nginx
listen unix:/var/run/nginx.sock;
```

Bạn thậm chí có thể sử dụng _hostname_

```Nginx
listen localhost:80;
listen sofsog.com:80;
```

Điều này nên được sử dụng thận trọng, vì tên máy chủ (_hostname_) có thể không được giải quyết khi khởi chạy _**nginx**_, khiến _**nginx**_ không thể liên kết trên TCP socket đã cho.

## Cấu hình cơ bản nginx

Với tất cả kiến ​​thức bên trên,  chúng ta có thể tạo và hiểu cấu hình tối thiểu cần thiết để chạy _**nginx**_

```Nginx
# /etc/nginx/nginx.conf

events {}                   # Bối cảnh events cần được xác định để xem xét cấu hình hợp lệ

http {
 server {
    listen 80;
    server_name  sofsog.com  www.sofsog.com  *.sofsog.com;

    return 200 "Hello";
  }
}
```

## _`root`_, _`location`_, và _`try_files`_ **directive**

### _`root`_ directive

_`root`_ directive khai báo thư mục gốc cho các yêu cầu, cho phép _**nginx**_ ánh xạ yêu cầu gửi đến (incoming request) vào file hệ hống.

```Nginx
server {
  listen 80;
  server_name sofsog.com;
  root /var/www/sofsog.com;
}
```

Điều này cho phép _**nginx**_ trả lại nội dung máy chủ theo yêu cầu

```Nginx
sofsog.com:80/index.html     # returns /var/www/sofsog.com/index.html
sofsog.com:80/foo/index.html # returns /var/www/sofsog.com/foo/index.html
```

### _`location`_ directive

_`location`_ directive đặt cấu hình tùy thuộc vào URI được yêu cầu.

_location \[modifier\] path_

```Nginx
location /foo {

# ...

}
```

Khi không có _modifier nào được chỉ định, path được coi là tiền tố (prefix), và mọi thứ phía sau nó đều hợp lệ._

Như ví dụ bên trên, kết quả bên dưới này đều hợp lệ (match):

```Nginx
/foo
/fooo
/foo123
/foo/bar/index.html
...
```

Ngoài ra, nhiều **_`location`_ directives** có thể được sử dụng trong một _**context**_ nhất định.

```Nginx
server {
  listen 80;
  server_name sofsog.com;
  root /var/www/sofsog.com;

  location / {
    return 200 "root";
  }

  location /foo {
    return 200 "foo";
  }
}
```

```Nginx
sofsog.com:80   /       # => "root"
sofsog.com:80   /foo    # => "foo"
sofsog.com:80   /foo123 # => "foo"
sofsog.com:80   /bar    # => "root"
```

**_Nginx_** cũng cung cấp vài modifiers, có thể được sử dụng kết hợp với **_location_**. Những modifiers đó tác động đến khối **_location_** nào mà được sử dụng, vì mỗi modifier, đã được chỉ định ưu tiên.

```Nginx
\=           - Exact match
^~          - Preferential match
~ && ~*     - Regex match
no modifier - Prefix match
```

_**Nginx**_ đầu tiên sẽ kiểm tra bất kỳ "exact match" nào. Nếu nó không tìm thấy, nó sẽ tìm kiếm những preferential. Nếu match này cũng thất bại, các regex match sẽ được kiểm tra theo thứ tự xuất hiện của chúng. Nếu mọi thứ không thành công, thì giá trị tiền tố cuối cùng (prefix match) sẽ được sử dụng.

```Nginx
location /match {
  return 200 'Prefix match: matches everything that starting with /match';
}

location ~* /match[0-9] {
  return 200 'Case insensitive regex match';
}

location ~ /MATCH[0-9] {
  return 200 'Case sensitive regex match';
}

location ^~ /match0 {
  return 200 'Preferential match';
}

location = /match {
  return 200 'Exact match';
}
```

```Nginx
/match     # => 'Exact match'
/match0    # => 'Preferential match'
/match1    # => 'Case insensitive regex match'
/MATCH1    # => 'Case sensitive regex match'
/match-abc # => 'Prefix match: matches everything that starting with /match'
```

### _`try_files`_ directive

**Directive** này sẽ thử các đường dẫn (path) khác nhau, trả về bất cứ gì được tìm thấy

```Nginx
try_files $uri index.html =404;
```

Ví dụ bên trên: đối với yêu cầu /foo.html, nó sẽ cố gắng trả về các file theo thứ tự sau:

1. $uri ( /foo.html )
2. index.html
3. Nếu không tìm thấy: 404.

Điều thú vị là, nếu chúng ta định nghĩa _try\_files_ trong **_server_ context** và sau đó xác định _location_ khớp với tất cả các yêu cầu, _try\_files_ của chúng ta sẽ không được thực hiện. Điều này xảy ra vì _try\_files_ trong _**server** **context**_ định nghĩa vị trí giả (_pseudo-location_) của riêng nó, đó là _location_ kém cụ thể nhất có thể. Do đó, định nghĩa  _location /_ sẽ cụ thể hơn vị trí giả (_pseudo-location_) của chúng ta.

```Nginx
server {
  try_files $uri /index.html =404;

  location / {
  }
}

```

Do đó, bạn nên tránh _try_files_ trong _**server** **context**_ :

```Nginx
server {
  location / {
    try_files $uri /index.html =404;
  }
}
```

## Kết luận

Cảm ơn các bạn đã đọc đến đây. Loạt bài này sẽ không thể có được nếu không có số lượng lớn tài nguyên được tìm thấy trên internet. Dưới đây là một số trang web tuyệt vời mà mình thấy đặc biệt hữu ích khi viết loạt bài này:

- [nginx docs](https://nginx.org/en/docs/)
- [nginx blog](https://www.nginx.com/blog/)
- [nginx fundamentals on udemy](https://www.udemy.com/nginx-fundamentals/)
- [Ilya Grigorik blog](https://www.igvita.com/), và cuốn sánh của anh ta: [High Performance Browser Networking](https://hpbn.co/)
- [Martin Fjordvald blog](https://blog.martinfjordvald.com/)

Mình sẽ rất vui khi thấy một số phản hồi hoặc thảo luận, vì vậy, vui lòng để lại nhận xét hoặc liên lạc lại bằng bất kỳ cách nào thuận tiện! Bạn có thích hướng dẫn này không? Bạn có gợi ý gì về chủ để tiếp theo không? Hoặc có thể bạn phát hiện ra một số lỗi? Hãy cho mình biết nhé và hẹn gặp lại bạn lần sau!

Lược dịch từ: netguru.co
