---
published: true
title: Thêm hệ thống bình luận vào blog Jekyll bằng Staticman
date: '2024-01-06'
categories:
  - thiet-ke-web
  - thu-thuat-chung
tags:
  - blog
  - Jekyll
  - Staticman
  - Comments
header:
  teaser: >-
    /assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com01.jpg
  overlay_image: >-
    /assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com01.jpg
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)"
excerpt: >-
  Staticman là một dịch vụ bên thứ ba được sử dụng để thêm chức năng bình luận động vào các trang web tĩnh, bao gồm cả các trang web được xây dựng bằng Jekyll. Nó cho phép người dùng gửi bình luận từ giao diện người dùng và lưu trữ dữ liệu bình luận trên repository Git.
toc: true
breadcrumbs: true
permalink: /thiet-ke-web/them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman
---

## Cách hoạt động của Staticman

Staticman hoạt động dựa trên webhook và sử dụng **API GitHub** để tương tác với repository. Khi người dùng gửi bình luận, **Staticman** sẽ tạo một `pull request` mới chứa dữ liệu bình luận và sau đó bạn có thể xem và quản lý bình luận thông qua **GitHub**.

Staticman hỗ trợ nhiều loại định dạng dữ liệu như `YAML`, `JSON`, hoặc hầu hết các định dạng dữ liệu khác. Bạn cũng có thể tùy chỉnh các trường bình luận và áp dụng các quy tắc xác thực hoặc kiểm duyệt nếu cần.

Với sự linh hoạt và tích hợp dễ dàng (hoặc tương đối khó) vào các trang web tĩnh, Staticman đã trở thành một lựa chọn phổ biến để thêm tính năng bình luận vào các trang web tĩnh như blog Jekyll.

## Lưu ý trước khi thực hiện

Mình thiết lập hệ thống bình luận với **Staticman** trên trang blog [sofsog.com](Sofsog.com) này với những lưu ý sau:

- Blog này chạy trên nền tảng [Jekyll](https://jekyllrb.com/), sử dụng chủ đề [Minimal mistakes](https://github.com/mmistakes/minimal-mistakes) được lưu trữ trên **GitHub** và đang chạy ổn định.
- **Staticman** sẽ được mình thực hiện cài đặt trên máy chủ **Windows Server 2012** *vì mình đã có sẵn nó*. Trường hợp nếu bạn thực hiện trên một máy chủ linux khác thì các bước cũng không khác là bao. Trên máy chủ này:
  - Đã cài đặt [Git](https://git-scm.com/) và thiết lập thông tin người dùng đầy đủ
  - Đã cài đặt `Node.js 8.11.3+` của mình là `20.10.0`
  - Đã cài đặt [nginx](https://nginx.org/en/docs/windows.html)
  - Đã tạo `A record` cho subdomain trỏ đến `IPv4 address` của máy chủ này thành công, trường hợp của mình là `staticman.sofsog.com` được thực hiện trên [Cloudflare](https://www.cloudflare.com/), lưu ý chọn **mã hóa ssl một chiều từ Client đến Cloudflare**.

![Hình Thêm hệ thống bình luận vào blog Jekyll bằng Staticman sofsog.com](/assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com01.jpg)

## Bước 1: Tạo `Github token` có quyền truy cập và chỉnh sửa vào kho lưu trữ trang Blog của bạn

- Đăng nhập vào tài khoản GitHub của bạn.

- Truy cập vào trang `Settings` (Cài đặt) của tài khoản GitHub của bạn. Bạn có thể truy cập bằng cách nhấp vào ***hình ảnh đại diện của bạn ở góc trên bên phải*** của trang và chọn `Settings` (Cài đặt) từ menu thả xuống.

- Trong trang "Settings", chọn `Developer settings` (Cài đặt phát triển) từ menu bên trái.

- Trong menu bên trái, chọn "Personal access tokens" (Mã thông báo truy cập cá nhân). Chọn tiếp `Tokens (classic)`

- Trên trang `Personal access tokens (classic)`, chọn `Generate new token` (Tạo mã thông báo mới), chọn `Generate new token (classic)`. Trường hợp Github yêu cấu nhập Mật khẩu thì cứ nhập vào.

- Đặt tên cho token ở ô `Note`, chọn thời hạn là `No expiration`, chọn các quyền truy cập mà bạn muốn cấp cho token. Để có toàn bộ quyền truy cập, hãy chọn tất cả các quyền trong danh sách. **Lưu ý rằng cấp quyền truy cập toàn bộ có thể có tác động lớn và cần được sử dụng cẩn thận**.

- Sau khi bạn chọn các quyền truy cập, cuộn xuống cuối trang và nhấp vào nút `Generate token` (Tạo mã thông báo).

- GitHub sẽ tạo ra một mã thông báo truy cập mới cho bạn. Có dạng tương tự như sau:

   ```bash
   ghp_aX1akjsdhf87iune8923h92n3n20893nZk
   ```

Copy và lưu trữ mã thông báo này một cách an toàn (sẽ được dùng ở bước cài đặt staticman), **vì nó sẽ chỉ hiển thị một lần duy nhất**. Không chia sẻ hoặc tiết lộ mã thông báo truy cập này với bất kỳ ai vì có thể sử dụng nó để thao tác với kho lưu trữ, tạo, sửa đổi hoặc xoá các tệp tin, và thực hiện các hoạt động khác trên GitHub.

## Bước 2: Cài đặt Staticman trên Windows Server 2012

Vào máy chủ **Windows Server 2012** (mình vào bằng Remote Desktop). Di chuyển đến thư mục nơi bạn muốn clone dự án, ví dụ `C:\Projects`, sau đó `click phải chuột` vào vùng trống rồi chọn `Git Bash Here` để mở chương trình dòng lệnh của Git. Sử dụng lệnh sau để `clone` dự án **staticman**.

```bash
git clone https://github.com/eduardoboucas/staticman
```

Git sẽ bắt đầu tải về toàn bộ nội dung của dự án từ kho lưu trữ GitHub. Sau khi tải xong, bạn vào thư mục dự án bằng lệnh

```bash
cd staticman
```

Cài đặt các phụ thuộc thông qua npm

```bash
npm install
```

Chờ quá trình cài đặt phụ thuộc hoàn tất, bạn tạo một tệp có tên `config.production.json` trong thư mục gốc của kho lưu trữ với các cấu hình cơ bản được bỏ trống bằng cách copy và dán lệnh sau vào terminal:

```bash
echo '{
   "githubToken": "",
   "rsaPrivateKey": "",
   "port": 81
}' > config.production.json
```

Thêm `config.production.json` làm ngoại lệ cho `.gitignore` bằng lệnh:

```bash
echo "\n\!config.production.json" >> .gitignore
```

Tạo `RSA Private Key`: Vào trang [Travistidwell](https://travistidwell.com/jsencrypt/demo/)

![Hình Thêm hệ thống bình luận vào blog Jekyll bằng Staticman sofsog.com](/assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com02.jpg)

Copy và lưu trữ lại `Private Key` và `Public Key`

Mở lại tệp `config.production.json` và điền các thông tin cần thiết như `githubToken` (đã tạo `Github token` ở `Bước 1`) và `rsaPrivateKey` (đã copy ở bước `Tạo RSA Private Key`). **Lưu ý quan trọng**, `Private Key` bạn copy ở bước trên sẽ có nhiều hàng, bạn phải xử lý sao cho nó chỉ **nằm trên 1 hàng (không có dấu xuống dòng)**, nếu không sẽ bị báo lỗi (chỗ này mất của mình vài ngày). Sau khi thực hiện xong, tệp `config.production.json` sẽ có dạng tương tự như sau:

```json
{
  "githubToken": "ghp_aX1akjsdhf87iune8923h92n3n20893nZk",
  "rsaPrivateKey": "-----BEGIN RSA PRIVATE KEY-----MII+87ND<Sofsog.com: dữ liệu giả để ví dụ> <Đảm bảo đoạn này nằm trên 1 hàng, không có dấu xuống dòng>mawrs94zQibtal-----END RSA PRIVATE KEY-----",
  "port": 81
}
```

Ở đây mình để cổng `81`, các bạn có thể thay đổi cổng thích hợp nếu muốn.

Trở lại chương trình dòng lệnh của Git, chuyển đổi biến môi trường `NODE_ENV` sang `production` bằng lệnh sau:

```bash
export NODE_ENV=production
```

Đến đây, nếu chạy trên server linux thì đã có thể chạy ngon, nhưng mình thực hiện trên **Windows Server 2012** nên phải thay đổi một chút ở tệp `package.json` của dự án staticman, `dòng số 7`:

```json
"prestart": "if [ ! -d node_modules ]; then npm install; fi",
```

Sẽ được thay đổi thành:

```json
"prestart": "IF NOT EXIST node_modules (npm install)",
```

**Chạy staticman** bằng lệnh:

```bash
npm start
```

Nếu không có gì bất ngờ thì màn hình dòng lệnh sẽ hiển thị như dưới này:

```bash
Administrator@WIN-44BF83HERJU MINGW64 /c/Projects/staticman (master)
$ npm start

> staticman@3.0.0 prestart
> IF NOT EXIST node_modules (npm install)
> staticman@3.0.0 start
> node index.js

Staticman API running on port 81
```

Như vậy là đã thành công, và `API Staticman` đang chạy trên cổng `81` của máy chủ của bạn. Kiểm tra bằng cách mở ***trình duyệt trên máy chủ*** và truy cập vào:

```bash
http://localhost:81/
```

Nếu thấy hiển thị dòng chữ `Hello from Staticman version 3.0.0!` là thành công.

## Bước 3: Cấu hình Nginx cho Staticman trên Windows Server 2012

Trong thư mục giải nén `Nginx`, ví dụ `C:\nginx-1.24.0\`, tạo thêm một thư mục có tên `sites-enabled`. Vào thư mục `sites-enabled`, tạo tệp `saticman.sofsog.com.conf` với nội dung tương tự như sau:

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name staticman.sofsog.com;
    location / {
         proxy_set_header        X-Forwarded-Proto $scheme;
         proxy_set_header        X-Real-IP $remote_addr;
         proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
         proxy_set_header        Host $http_host;
         proxy_pass              http://127.0.0.1:81;
     }
}
```

Lưu ý thay đổi chỗ `staticman.sofsog.com` và cổng `81` thành thông số của bạn.

Thêm thư mục `sites-enabled` vào cấu hình gốc của nginx bằng cách mở tệp cấu hình gốc của `Nginx`, trường hợp của mình là tệp `C:\nginx-1.24.0\conf\nginx.conf`.

Thêm dòng `include "C:/nginx-1.24.0/sites-enabled/*.conf";` (dấu `/` phải thay đổi lại giống như trên linux) vào khối mã `http {...}`, sau khi thêm, thì khối mã sẽ tương tự như sau:

```nginx

...

http {
    include       mime.types;
    default_type  application/octet-stream;
    include "C:/nginx-1.24.0/sites-enabled/*.conf"; # thêm dòng này

...

}

...

```

Kiểm tra lại các tệp cấu hình của Nginx trên **Windows Server 2012** bằng cách vào thư mục cài đặt Nginx, ví dụ `C:\nginx-1.24.0\`, mở `cmd` ở đây và gõ:

```bash
nginx -t
```

Nếu xuất hiện chữ `successful` là không có sai xót, gõ tiếp lệnh `start nginx` để chạy nginx lần đầu, trường hợp nginx đã đang chạy rồi thì gõ `nginx -s reload` để nó tải lại các tệp cấu hình.

Kiểm tra lại bằng cách mở trình duyệt từ một máy tính bất kỳ và truy cập vào **staticman.sofsog.com** (thay đổi cho đúng tên miền của bạn), nếu thấy hiển thị dòng chữ `"Hello from Staticman version 3.0.0!"` tương tự như khi ta vào `localhost:81` từ máy chủ là thành công.

## Bước 4: Thêm hệ thống bình luận bằng Staticman trên trang Blog nền tảng [Jekyll](https://jekyllrb.com/), sử dụng chủ đề [Minimal mistakes](https://github.com/mmistakes/minimal-mistakes)

### Sửa tệp `_config.yml`

Chủ đề [Minimal mistakes](https://github.com/mmistakes/minimal-mistakes) đã hỗ trợ sẵn sàng cho việc thêm thống bình luận bằng Staticman, các bước còn lại thật sự đơn giản, đầu tiên mở tệp `_config.yml`, thêm vào:

```yml
repository  : "user-name-github/user-name-github.github.io"
comments:
  provider  : "staticman_v2"
  staticman:
    branch    : "master"
    endpoint  : https://staticman.sofsog.com/v2/entry/ # Thay bằng tên miền của bạn
```

### Tạo tệp `staticman.yml`

Đảm bảo tệp `staticman.yml` đang hiện có trong thư mục gốc của bạn, nếu chưa có thì tạo nó, với nội dung như sau:

```yml
comments:
  allowedFields:
    - name
    - email
    - url
    - message
  allowedOrigins:
    - sofsog.com # Thay bằng tên miền trang blog của bạn
  branch: master
  commitMessage: 'Bình luận mới bởi {fields.name}'
  filename: 'comment-{@timestamp}'
  format: yaml
  generatedFields:
    date:
      type: date
      options:
        format: iso8601
  moderation: true
  path: '_data/comments/{options.slug}'
  requiredFields:
    - name
    - email
    - message
  transforms:
    email: md5
```

### Kiểm tra, phê duyệt bình luận

`Commit` và `Push` các thay đổi để `Build` lại trang blog.

Sau khi `Build` lại xong, các bạn vào blog của mình ở bất kỳ bài viết nào để bình luận thử.

Phê duyệt bình luận bằng cách truy cập vào kho lưu trữ trang blog của bạn trên Github, vào `Pull requests`, chọn bình các bình luận chờ duyệt, chọn `Merge pull request` để phê duyệt.

Chờ vài giây để Github `Build` lại trang blog của bạn, sau đó vào bài viết để kiểm tra xem bình luận đã xuất hiện chưa.

## Bước 5: Đăng ký Akismet hoặc reCAPTCHA V2 để chống thư rác

Mình sẽ chỉ hướng dẫn thực hiện đăng ký **reCAPTCHA V2** để phòng chống thư rác cho hệ thống bình luận. Trước tiên bạn phải đăng ký và sử dụng **reCAPTCHA V2** của Google , hãy tuân theo các bước sau:

### Truy cập vào trang quản lý reCAPTCHA

Truy cập vào trang web reCAPTCHA của Google: [recaptcha](https://www.google.com/recaptcha)
Nhấp vào nút `Get Started with Enterprise` ở góc phải trên cùng của trang, sau đó đăng nhập vào tài khoản Google của bạn.

### Tạo một reCAPTCHA mới

Trong trang tiếp theo hãy chọn hoặc [tạo dự án Google Cloud](https://cloud.google.com/resource-manager/docs/creating-managing-projects). Sau đó thực hiện các bước theo hướng dẫn của Google.

Hoặc bằng cách đơn giản hơn, nhấn vào link "`Switch to create a classic key`", rồi điền các thông tin cần thiết cho reCAPTCHA như sau:

Nhãn (Label): Đặt tên cho reCAPTCHA của bạn để có thể nhận biết nó trong quản lý.

Loại reCAPTCHA: Chọn "reCAPTCHA V2".

![Đăng ký Akismet hoặc reCAPTCHA để chống thư rác Sofsog.com](/assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com04.png)

Tên miền: Nhập tên miền của trang web cá nhân của bạn mà bạn muốn bảo vệ bằng reCAPTCHA.

Chọn "Tôi không phải là người máy" (I'm not a robot).

Đọc và chấp nhận các điều khoản và điều kiện của reCAPTCHA.

Nhấp vào nút `"SUBMIT"` để hoàn thành quá trình tạo reCAPTCHA.

### Lấy khóa reCAPTCHA cho trang Blog cá nhân của bạn

Sau khi tạo reCAPTCHA thành công, trang quản lý sẽ hiển thị hai mã khóa quan trọng:

**Site key**: Đây là mã khóa công khai (public key) được sử dụng để tích hợp reCAPTCHA vào trang web của bạn.

```bash
6Lfgx2oUBBBBBBZJmldPnrBPme8OwqgyedPSuIfE
```

**Secret key**: Đây là mã khóa bí mật (secret key) được sử dụng để xác thực và gửi yêu cầu kiểm tra reCAPTCHA từ trang web của bạn tới Google. Để sử dụng cho trang Jekyll, bạn cần mã hoá nó, mình sẽ nói ở bước sau

```bash
6LfgKLJSHKSJDFHSKJDHFFakeData-84UR9Hw
```

Sao chép cả hai mã khóa này và lưu trữ chúng một cách an toàn.


### Tích hợp reCAPTCHA vào hệ thống bình luận của Blog

Bình thường bạn cần điều chỉnh mã nguồn của trang web cá nhân của bạn để thêm **reCAPTCHA V2**. Tuy nhiên với Blog nền tảng [Jekyll](https://jekyllrb.com/), sử dụng chủ đề [Minimal mistakes](https://github.com/mmistakes/minimal-mistakes) này, chỉ cần làm vài bước đơn giản:

- Mã hoá `Secret key` bằng cách [dùng hệ thống Staticman](https://staticman.net/docs/encryption), mở trình duyệt, truy cập vào:
  
  ```bash
  https://{STATICMAN_BASE_URL}/v2/encrypt/<Secret key chỗ này>
  ```

  Ví dụ, đối với dữ liệu trong hướng dẫn này là:

  ```bash
  https://staticman.sofsog.com/v2/encrypt/6LfgKLJSHKSJDFHSKJDHFFakeData-84UR9Hw
  ```

  ![2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com05](/assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com05.png)

  Sao chép đoạn đã mã hoá này và lưu trữ

- Thêm vào tệp `_config.yml` đoạn sau đây, thay đổi thành dữ liệu của bạn, `siteKey` là mã khóa công khai mà bạn lấy được của google, `secret` là đoạn bạn vừa mới mã hoá và sao chép về.
  
  ```yml
  reCaptcha:
    siteKey: "6Lfgx2oUBBBBBBZJmldPnrBPme8OwqgyedPSuIfE"
    secret: "ZYBJ5jA0g1D2PCabgjg43zNbKy0GuabCslrRJop5qG75Nqykf3/wrgrw873xovXAU2pT/2UoKOVH1c07OtY5r9AUKcfTbuZo9kL9X7xRnEOfgi1JuoZK9ENHSGsr++WfVLZB+BNpnyc2vvRzFXJAuUftHQYsdQfNkybsG2iH/JY="
  ```

- Thêm vào tệp `staticman.yml` tương tự như trên, nhưng đừng quên `enabled: true`

  ```yml
  reCaptcha:
      enabled: true
      siteKey: "6Lfgx2oUBBBBBBZJmldPnrBPme8OwqgyedPSuIfE"
      secret: "ZYBJ5jA0g1D2PCabgjg43zNbKy0GuabCslrRJop5qG75Nqykf3/wrgrw873xovXAU2pT/2UoKOVH1c07OtY5r9AUKcfTbuZo9kL9X7xRnEOfgi1JuoZK9ENHSGsr++WfVLZB+BNpnyc2vvRzFXJAuUftHQYsdQfNkybsG2iH/JY="
  ```

`Commit` và `Push` các thay đổi để `Build` lại trang blog.

Sau khi `Build` lại xong, các bạn vào blog của mình để thử bình luận thêm lần nữa.

![Hình Thêm hệ thống bình luận vào blog Jekyll bằng Staticman sofsog.com](/assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com03.jpg)

Cảm ơn bạn nào đã kiên nhẫn đọc đến đây.

Chúc các bạn thành công.

## Link tham khảo

[https://mmistakes.github.io/minimal-mistakes/docs/configuration/#recaptcha-support-v2-only](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#recaptcha-support-v2-only)

[https://nithiya.gitlab.io/post/staticman-jekyll-gitlab/#site-nav](https://nithiya.gitlab.io/post/staticman-jekyll-gitlab/#site-nav)

[https://vincenttam.gitlab.io/post/2018-09-16-staticman-powered-gitlab-pages/2/](https://vincenttam.gitlab.io/post/2018-09-16-staticman-powered-gitlab-pages/2/)

[https://staticman.net/docs/getting-started.html](https://staticman.net/docs/getting-started.html)