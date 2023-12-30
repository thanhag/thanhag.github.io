## Việt hoá, cấu hình, Google analytic, bình luận file `_config.yml`

- Tạo bình luận bằng staticman không thành công vì dự án hình như đã lỗi thời
- Chốt cuối tạo bình luận bằng Facebook
-

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

<<<<<<< HEAD
=======

## Sửa lỗi menu trên android không đè lên nút `Theo dõi` trên android

- Đã tạo [discussions](https://github.com/mmistakes/minimal-mistakes/discussions/4602) trên repo [mmistakes](https://github.com/mmistakes) nhưng chưa được ai quan tâm.
- Loading ...

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
