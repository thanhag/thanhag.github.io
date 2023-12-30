## Việt hoá, cấu hình, Google analytic, bình luận file `_config.yml`

### Tạo bình luận bằng staticman không thành công vì dự án hình như đã lỗi thời
### Chốt cuối tạo bình luận bằng Facebook
### Thêm logo 88x88 vào `/assets/images/main` và thêm cấu hình vào file `_config.yml` 

```yml
logo: "/assets/images/main/Logo-Thanh88x88.png"
```
## Thẻ head

### favicon

- Tạo favicon theo hướng dẫn của [peateasea](https://peateasea.de/add-favicon-to-mm-jekyll-site/)
- Thêm file `_includes/head/custom.html` và thêm vào tệp này nội dụng như sau:

```html
<link rel="apple-touch-icon" sizes="180x180" href="/assets/images/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="/assets/images/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/assets/images/favicon-16x16.png">
<link rel="manifest" href="/assets/images/site.webmanifest">
<link rel="mask-icon" href="/assets/images/safari-pinned-tab.svg" color="#5bbad5">
<link rel="shortcut icon" href="/assets/images/favicon.ico">
<meta name="msapplication-TileColor" content="#2d89ef">
<meta name="msapplication-config" content="/assets/images/browserconfig.xml">
<meta name="theme-color" content="#ffffff">
```

## Thay đổi CSS

### Font chữ:

- `.page__hero-caption` font chữ của class này không hỗ trợ tiếng việc: xoá font chữ Georgia trong file font `_variables.scss`

### Tạo ảnh bìa của bài viết trắng đen và mờ và bụi:

Thêm vào file `_page.scss`, chỗ `--overplay` đoạn sau:

```css
    -webkit-mask-image: url(https://sofsog.com/assets/images/bui-va-vet-xuoc.png); /* hình ảnh sẽ được sử dụng làm mặt nạ cho phần tử*/
    -webkit-mask-size: 1000px 1000px;/* kích thước được đặt là 200px chiều rộng và 200px chiều cao. Điều này có nghĩa là hình ảnh mặt nạ sẽ được co giãn hoặc thu nhỏ để phù hợp với kích thước này.*/ 
    mask-image: url(https://sofsog.com/assets/images/bui-va-vet-xuoc.png); /*tương tự như trên, nhưng được sử dụng cho các trình duyệt không phải là WebKit (như Firefox, Edge, vv)*/
    
    mask-size: 1000px 1000px; /* tương tự như trên, nhưng được sử dụng cho các trình duyệt không phải là WebKit.*/
    filter: grayscale(100%); /* Điều chỉnh độ nhòe và chuyển đổi sang trắng đen tại đây */

```

Và chỗ `.wrapper` đoạn sau:

```css
// Làm mờ xung quanh chữ 3px là vừa, 2px không đủ rõ chữ
      backdrop-filter: blur(3px); 
```

## Sửa lỗi menu trên android không đè lên nút `Theo dõi` trên android

- Đã tạo [discussions](https://github.com/mmistakes/minimal-mistakes/discussions/4602) trên repo [mmistakes](https://github.com/mmistakes) nhưng chưa được ai quan tâm.
- Loading ... 