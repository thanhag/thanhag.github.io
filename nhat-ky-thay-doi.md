# Time

## 06/01/2024

- Vì build bị lỗi nên đã tìm cách quay trở lại bản commit chưa bị lỗi bằng cách: Vào Action, chọn stick xanh gần nhất click vào tìm mã commit, tìm được `29c442c`, nếu chưa thiết lập kết nối với repo GitHub thì chạy lệnh sau: `git remote add origin <url_repo_github>`. Trường hợp mình thường đã kết nối sắn. Sử dụng lệnh git push kết hợp với tùy chọn -f để đẩy ghi đè lên GitHub: `git push -f origin 29c442c:refs/heads/master`. Lưu ý rằng việc đẩy force (-f) có thể ghi đè lịch sử commit trên remote repository và làm thay đổi đáng kể. Hãy đảm bảo bạn đã sao lưu dữ liệu quan trọng và chỉ sử dụng git push -f khi bạn chắc chắn về hậu quả của việc này. Success
- Hiện tại thì `Bình luận` bằng `staticman` đã có Recapcha và thực hiện ổn định trên điện thoại. Chỉ có điểm yếu là chưa lồng vào nhau `nested comments`.
- Akismet: Chặn spam, đã có recapcha rồi nên thôi không cần nữa.

## Tạo nút cuối trang và đầu trang

## Tạo các trang donate

### Buy me a Coffe : <https://www.buymeacoffee.com/thanhag>

### Momo: <https://nhantien.momo.vn/0919466523>

### paypal.me: paypal.me/thanhag/3usd

## Việt hoá, cấu hình, Google analytic, bình luận file `_config.yml`

### Bình luận - Comments

- Ngày 06/01/2024, staticman đã chạy thành công trên window server 2012, chạy bằng các bước sau:
  - B1: chạy `export NODE_ENV=production`
  - B2: chạy `npm start`
  - Phiên bản node: `20.10.0`
  - Ghi chú lại cấu hình trong file `_config.yml`

  ```yml
  repository  : "thanhag/thanhag.github.io" # Git username/repo-name e.g. "mmistakes/minimal-mistakes"
  comments:
    provider  : "staticman_v2"
    staticman:
      branch    : "master"
      endpoint  : https://staticman.sofsog.com/v2/entry/
  ```

  - Link file `staticman.yml` thành công : [29c442c](https://github.com/thanhag/thanhag.github.io/commit/29c442caedbe33c4f626784122d22d27e561656b)
  
  - Ghi chú lại file nginx của staticman thành công:

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
  
  - Ghi chú lại `config.production.json` của staticman thành công:

  ```json
    {
    "githubToken": "ghp_aX1xxxxxxxxxxxxxxxZk",
    "rsaPrivateKey": "-----BEGIN RSA PRIVATE KEY-----MIICXQIBAAKBgQCY6qOC/xxxxxxxxxxxx+87NDmawrs94zQibtal-----END RSA PRIVATE KEY-----",
    "port": 81
    }
  ```

- Tạo bình luận bằng staticman dù đã lỗi thời nhưng vẫn thực hiện thành công:
  - Vẫn tiếp tục: Chỉ SSL một bên trên Cloundflare, cái Ngix, chạy cổng 81
  - Sửa file `staticman/lib/GitHub.js`

```javascript
//Cũ
      if (options.oauthToken) {
        authToken = options.oauthToken
      } else if (isLegacyAuth) {
        authToken = config.get('githubToken')
      } else if (isAppAuth) {
        authToken = await this._authenticate(options.username, options.repository)
      } else {
        throw new Error('Require an `oauthToken` or `token` option')
      }

//sửa thành
      if (isLegacyAuth) {
        authToken = config.get('githubToken')
      } else if (options.oauthToken) {
        authToken = options.oauthToken
      } else if (isAppAuth) {
        authToken = await this._authenticate(options.username, options.repository)
      } else {
        throw new Error('Require an `oauthToken` or `token` option')
      }
```

- Xóa phần `reCaptcha` trong file staticman
- Tạo RSA key online cho chắc ăn
- Tạo lại token classic của github cho chuẩn, cài đặt mọi quyền luôn cho chắc ăn
- Đến đây mọi thứ đã ok

- Chốt cuối tạo bình luận bằng Facebook
- Thêm favicon theo hướng dẫn [ở đây](https://peateasea.de/add-favicon-to-mm-jekyll-site/) làm để so sánh với favicon cũ, bản mới nhìn trên android thì thấy hơn, nhưng trên tab trình duyệt thì không rõ ràng mấy.
  - Đơn giản là thêm vào trang chủ rồi thêm hình ảnh mình vào, điều chỉnh cho phù hợp từng ứng dụng, rồi cuối cùng, path `/assets/images/favicon` vào, tải về, copy html về.
- Cấu hình cat và tag **Không thực hiện được khi host ở github, chỉ thực hiện thành công ở local**, đã trở về mặc định
  - Thêm vào Gemfile: `gem 'jekyll-archives'`
  - Thêm vào file `_confog.yml`
  
```yml
plugins:
- jekyll-archives  # Thêm chỗ này

# Ghi đè toàn bộ chỗ này
category_archive:
  type: jekyll-archives
  path: /
tag_archive:
  type: jekyll-archives
  path: /
# https://github.com/jekyll/jekyll-archives
jekyll-archives:
  enabled:
    - categories
    - tags
  layouts:
    category: archive-taxonomy
    tag: archive-taxonomy
  permalinks:
    category: /:name/
    tag: /:name/
  
```

## Thay đổi CSS

### Font chữ

- `.page__hero-caption` font chữ của class này không hỗ trợ tiếng việc: xoá font chữ Georgia trong file font `_variables.scss`

### Tạo ảnh bìa của bài viết trắng đen và mờ và bụi

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

## Thay đổi màu nền sang màu xám nhạt `#FAFAF9`

- Chỉ cần thêm đoạn sau vào file `_default.scss`
  
```scss

```

## Chế độ tối

- Mở `DevTools` chọn `Bảng điều kiển (Console)` copy đoạn javascript bên dưới để chạy, chuyển đối cứng 100% chuyển cả hình ảnh:

```javascript
javascript:(function(){
    document.documentElement.style.filter = document.documentElement.style.filter ? '' : 'invert(100%)'
})();
```

```javascript
javascript:(function(){
    var body = document.body;
    var currentColor = window.getComputedStyle(body).getPropertyValue('background-color');
   if (currentColor === 'rgb(0, 0, 0)' || currentColor === 'black') 
  {
          body.style.backgroundColor = 'white';
          body.style.color = 'black';

        }else if (currentColor === 'rgb(255, 255, 255)' || currentColor === 'white') {
          body.style.backgroundColor = 'black';
          body.style.color = 'white';
  }
})();
```

### Thực hiện trên local

Thêm đoạn màu trong file `_dark.scss` vào `_default.scss`, (đoạn dưới không tác dụng vì biến $ được biên dịch trước khi hiển thị, đang tìm cách khác)

```scss
// Thêm đoạn này để xử lý darkmode
[data-scheme=dark] {
   /* Colors */
   $background-color: #252a34 !default;
   $text-color: #eaeaea !default;
   $primary-color: #00adb5 !default;
   $border-color: mix(#fff, $background-color, 20%) !default;
   $code-background-color: mix(#000, $background-color, 15%) !default;
   $code-background-color-dark: mix(#000, $background-color, 20%) !default;
   $form-background-color: mix(#000, $background-color, 15%) !default;
   $footer-background-color: mix(#000, $background-color, 30%) !default;
   $link-color: mix($primary-color, $text-color, 40%) !default;
   $link-color-hover: mix(#fff, $link-color, 25%) !default;
   $link-color-visited: mix(#000, $link-color, 25%) !default;
   $masthead-link-color: $text-color !default;
   $masthead-link-color-hover: mix(#000, $text-color, 20%) !default;
   $navicon-link-color-hover: mix(#000, $background-color, 30%) !default;

   .author__urls.social-icons i,
   .author__urls.social-icons .svg-inline--fa,
   .page__footer-follow .social-icons i,
   .page__footer-follow .social-icons .svg-inline--fa  {
   color: inherit;
   }

   .ais-search-box .ais-search-box--input {
   background-color: $form-background-color;
   }
}
```

Tạo nút checkbox, thêm đoạn dưới vào file `masthead.html`

```html
<label class="c-scheme-switch" for="scheme-checkbox">
               <span class="visually-hidden">Enable dark mode</span>
               <input type="checkbox" id="scheme-checkbox" tabindex="0" class="c-scheme-switch_input">
               <div class="c-scheme-switch_slider">
                  <svg aria-hidden="true" focusable="false" viewBox="0 0 24 24" height="17.25" width="17.25" xmlns="http://www.w3.org/2000/svg" stroke="currentcolor" class="sun-icon icon">
                     <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364-.707-.707M6.343 6.343l-.707-.707m12.728.0-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"></path>
                  </svg>
                  <div class="c-scheme-switch_slider-track"></div>
                  <svg aria-hidden="true" focusable="false" viewBox="0 0 24 24" height="17.25" width="17.25" xmlns="http://www.w3.org/2000/svg" fill="none" stroke="currentcolor" class="moon-icon icon">
                     <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003.0 0012 21a9.003 9.003.0 008.354-5.646z"></path>
                  </svg>
               </div>
            </label>
```

Thêm javascript dưới vào file `head.html`:

```html
<!-- Xử lý nút bật tắt chế độ tối -->

<script>
  const currentScheme = localStorage.getItem("scheme");
  let uncheckBox = !1; // Gán giá trị này là false
  
  function disableDarkMode() {
      document.documentElement.setAttribute("data-scheme", "light"), localStorage.setItem("scheme", "light")
  }
  
  function enableDarkMode() {
      document.documentElement.setAttribute("data-scheme", "dark"), localStorage.setItem("scheme", "dark")
  }
  // Nếu biến lấy đưỢc từ trình duyệt là dark thì bật dark và ngược lại
  currentScheme === "dark" ? enableDarkMode() : 
  currentScheme === "light" ? (disableDarkMode(), uncheckBox = !0) :
  // Nếu chưa có biến currentScheme
  window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches ? enableDarkMode() : 
  
  
  // Có thể bỏ dấu , và thêm dấu ; để thay thế
  // Đoạn dưới này có ý nghĩa thứ tự như sau:
  // 1. Chạy hàm: disableDarkMode()
  // 2. Gán uncheckBox = !0 (giá trị là true)
  // 3. Đăng ký một sự kiện:DOMContentLoaded và xử lý:
  //    - Tìm checkbox có class c-scheme-switch_input
  //    - Đăng ký sự kiện change cho checkbox tìm được và xử lý sự kiện đó: t.checked là true), hàm enableDarkMode() được gọi. Nếu không, hàm disableDarkMode() được gọi.  
  //    - Gán giá trị ngược lại cho t.checked: Kiểm tra biến uncheckBox và gán giá trị cho t.checked tương ứng.   
  (disableDarkMode(), uncheckBox = !0), addEventListener("DOMContentLoaded", e => {
      const t = document.querySelector('input[type="checkbox"].c-scheme-switch_input');
      t.addEventListener("change", () => {
          t.checked ? enableDarkMode() : disableDarkMode()
      }), uncheckBox ? t.checked = !1 : t.checked = !0
  })
</script>
<!-- end Xử lý nút bật tắt chế độ tối -->
```

Add thêm scss của nút này vào file `_default.scss` luôn cho đơn giản, lưu ý đường dẫn tấm hình `/dust-texture.png`

```scss
// Thêm css cho nút thay đổi theme
[type=checkbox] {
 box-shadow: none;
}


.icon {
 display: inline-block;
 block-size: 1em;
 inline-size: 1em;
 fill: currentColor;
 line-height: 1;
 vertical-align: middle;
}

.c-scheme-switch {
 position: relative;

 &_slider {
  position: relative;
  display: flex;
  flex-wrap: nowrap;
  align-items: center;
  cursor: pointer;
  gap: 1ch;
  padding: 0;
  color: #1c1c19;
  color: var(--foreground-color);
  font-family: courier prime, monospace;
  font-family: var(--font-family-code);

  & .icon {
   transition: 250ms;
  }

  & .moon-icon {
   opacity: 0.2;
  }

  & .sun-icon {
   opacity: 1;
  }
 }

 &_slider-track {
  $offset: 3px;
  $diameter: 0.9em;
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: space-around;
  box-sizing: content-box;
  block-size: calc(#{$diameter} + #{$offset} * 2);
  inline-size: calc(#{$diameter} * 2 + #{$offset} * 2);
  border: 2px solid #1c1c19;
  border: 2px solid var(--foreground-color);
  border-radius: 1e5px;
  border-radius: var(--radius-round);
  transition: 250ms;

  &::before {
   content: "";
   position: absolute;
   inset-block-start: 50%;
   inset-inline-start: $offset;
   z-index: 2;
   z-index: var(--layer-2);
   box-sizing: border-box;
   block-size: $diameter;
   inline-size: $diameter;
   border-radius: 1e5px;
   border-radius: var(--radius-round);
   background-color: #1c1c19;
   background-color: var(--foreground-color);
   transform: translate(0, -50%);
   will-change: transform;
   transition: inherit;
  }
 }

 @media (min-width: 768px) {
  &_slider-track {
   $diameter: 1em;
   -webkit-mask-image: url(/dust-texture.png);
   mask-image: url(/dust-texture.png);
   -webkit-mask-size: 960px 450px;
   mask-size: 960px 450px;
  }
 }

 &_input {
  position: absolute;
  inset: 0;
  background: 0 0;
  border: none;
  z-index: 1;
  z-index: var(--layer-1);
  cursor: pointer;

  &:focus {
   background: 0 0;
   border: none;
   box-shadow: none;
  }

  &:focus + .c-scheme-switch_slider .c-scheme-switch_slider-track {
   
   box-shadow: 0 0 0 2px var(--foreground-muted-color);
  }

  &:checked + .c-scheme-switch_slider .moon-icon {
   opacity: 1;
  }

  &:checked + .c-scheme-switch_slider .sun-icon {
   opacity: 0.2;
  }

  &:checked + .c-scheme-switch_slider .c-scheme-switch_slider-track::before {
   transform: translate(100%, -50%);
  }
 }
}


.visually-hidden {
 position: absolute;
 block-size: auto;
 inline-size: 1px;
 margin: 0;
 padding: 0;
 overflow: hidden;
 white-space: nowrap;
 border: 0;
 clip: rect(0, 0, 0, 0);
 &:focus {
  display: block;
  block-size: auto;
  inline-size: auto;
  clip: auto;
  z-index: 2147483647;
  z-index: var(--layer-important);
 }
}

$color_1: #1c1c19;
$color_2: var(--foreground-color);

input {
 padding: .75rem 1rem;
 padding: var(--size-3)var(--size-4);
 color: $color_1;
 color: $color_2;
 background: #fafaf9;
 background: var(--input-background);
 border: 2px solid #1c1c19;
 border: 2px solid var(--border-color);
 border-radius: .375rem;
 border-radius: var(--radius);
 font: inherit;
 -webkit-appearance: none;
 -moz-appearance: none;
 appearance: none;
}
button {
 padding: .75rem 1rem;
 padding: var(--size-3)var(--size-4);
 color: $color_1;
 color: $color_2;
 background: #fafaf9;
 background: var(--input-background);
 border: 2px solid #1c1c19;
 border: 2px solid var(--border-color);
 border-radius: .375rem;
 border-radius: var(--radius);
 font: inherit;
 -webkit-appearance: none;
 -moz-appearance: none;
 appearance: none;
}
textarea {
 padding: .75rem 1rem;
 padding: var(--size-3)var(--size-4);
 color: $color_1;
 color: $color_2;
 background: #fafaf9;
 background: var(--input-background);
 border: 2px solid #1c1c19;
 border: 2px solid var(--border-color);
 border-radius: .375rem;
 border-radius: var(--radius);
 font: inherit;
 -webkit-appearance: none;
 -moz-appearance: none;
 appearance: none;
}
select {
 padding: .75rem 1rem;
 padding: var(--size-3)var(--size-4);
 color: $color_1;
 color: $color_2;
 background: #fafaf9;
 background: var(--input-background);
 border: 2px solid #1c1c19;
 border: 2px solid var(--border-color);
 border-radius: .375rem;
 border-radius: var(--radius);
 font: inherit;
 -webkit-appearance: none;
 -moz-appearance: none;
 appearance: none;
}



label {
 >input {
  
  margin-block-start: var(--size-1);
 }
 >textarea {
  
  margin-block-start: var(--size-1);
 }
 >select {
  
  margin-block-start: var(--size-1);
 }
}

```

Đến đây nút chuyển chế độ đã hiển thị đẹp, click vào đã xử lý được biến local và thay đổi thuộc tính cho `html` data-scheme="light" thay đổi thành data-scheme="dark"

Đã thử thêm vào `:root {` biến `--background-color: #fff ;` và `[data-scheme=dark] {` biến `--background-color: #000000 ;` rồi sử dụng biến này kiểu ghi đè ở

```scss
//Thêm vào từ trang kia
:root {
  
   --background-color: #fff ;
  background-color:  var(--background-color); // định nghĩa này áp dụng cho toàn bộ html
}   

// Thêm đoạn này để xử lý darkmode
[data-scheme=dark] {
 --background-color: #000000 ;
   // Thêm vào từ trang kia
   --foreground-muted-color: var(--color-gray-300);
}
```
