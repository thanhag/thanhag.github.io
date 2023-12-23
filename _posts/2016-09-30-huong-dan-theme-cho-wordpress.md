---
title: "Hướng dẫn cài đặt theme cho Wordpress"
date: "2016-09-30"
categories: 
  - "wordpress"
tags: 
  - "cai-dat-theme"
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/upload-theme_thumb.jpg
  teaser: /assets/images/upload-theme_thumb.jpg
toc: true
breadcrumbs: true
---

Ở  bài này, mình sẽ hướng dẫn bạn cách cài theme **thông qua ba cách** đó là cài theme miễn phí thông qua thư viện theme của WordPress.Org, cài bằng cách upload gói theme trong Dashboard và cách cuối cùng là copy thư mục theme vào thư mục **/wp-content/themes/** trên localhost hoặc host đang chứa website WordPress của bạn.

### 3 cách cài theme WordPress

#### Tìm và cài đặt theme từ thư viện

Nếu bạn là người mới học WordPress, **mình khuyến khích bạn chỉ nên cài các theme miễn phí** có sẵn trong thư viện của WordPress.Org để nắm rõ cách sử dụng và thiết lập một theme vì các theme ở đó đa phần đều dễ sử dụng đúng chuẩn của WordPress và nhất là an toàn – không chứa mã độc.

Để cài theme mới cho WordPress, bạn vào **Appearance –> Themes** và ấn Add New.

![cai-theme-wordpress](/assets/images/cai-theme-wordpress_thumb.jpg "cai-theme-wordpress")

Lúc này bạn sẽ thấy danh sách các theme có trong thư viện WordPress.Org, hãy ghi nhớ là thư viện này **có hơn 2000 theme**s khác nhau lận đấy. Bạn có thể sử dụng các bộ lọc để tìm ra một theme phù hợp với sở thích/nhu cầu của mình.

![bo-loc-theme](/assets/images/bo-loc-theme_thumb.jpg "bo-loc-theme")

Sau khi tìm ra một theme ưng ý, hãy ấn vào theme đó để xem thông tin và xem trước theme. Hãy lưu ý rằng, tính năng xem trước này chỉ có ý nghĩa tượng trưng chứ đôi lúc nó sẽ không hiển thị chính xác và đầy đủ các tính năng có trong theme đó.

![xem-thong-tin-theme](/assets/images/xem-thong-tin-theme_thumb.jpg "xem-thong-tin-theme")

Nếu bạn thấy ưng ý thì ấn nút **Install** để cài đặt.

![cai-dat-theme](/assets/images/cai-dat-theme_thumb.jpg "cai-dat-theme")

Và ấn vào nút **Activate** lên để kích hoạt chứ cài xong nó chỉ nằm trên thư mục **/wp-content/themes** mà thôi chứ chưa được kích hoạt.

![kich-hoat-theme](/assets/images/kich-hoat-theme_thumb.jpg "kich-hoat-theme")

Sau khi kích hoạt xong, hãy vào **Appearance –> Menus** để thiết lập menu và **Apperance –> Widgets** để thêm một vài widget vào sidebar để theme hiển thị tốt nhất. Đồng thời, nhiều theme sẽ có thêm mục khu vực tùy chỉnh riêng được hiển thị trên menu bên tay trái của Dashboard mà ta thường gọi đó là **Theme Options**, nếu có thì hãy truy cập vào đó tùy chỉnh.

#### Cài theme bằng cách upload từ máy tính lên website

Giả sử bạn đang có một theme trên máy tính thì bạn hãy nén nó lại thành file **.zip**. Lưu ý rằng, bạn phải nén thư mục của theme đó chứ không nén luôn thư mục lồng vào nó.

Ví dụ, khi giải nén ra thì theme của bạn phải có cấu trúc là /tên-theme/style.css((File style.css luôn nằm ở thư mục gốc của theme)) thì mới chính xác chứ nếu giải nén nó ra mà nó thành /tên-thư-mục/tên-theme/style.csslà sai, và bạn phải nén nó thành định dạng .zip chứ các đuôi khác như .rar, .tar đều sai.

Sau khi có file nén .zip của theme, bạn vào **Appearance –> Themes –> Add New –> Upload Theme**.

![upload-theme](/assets/images/upload-theme_thumb.jpg "upload-theme")

Sau đó bạn upload file .zip của theme lên và kích hoạt như thông thường. Nếu nó báo lỗi missing style.css thì là do bạn nén với cấu trúc sai, hãy giải nén ra và nén lại cho đúng như mình nói ở trên.

#### Cài theme bằng cách upload trực tiếp vào host/localhost

Cách này dùng để làm khi bạn bị giới hạn dung lượng upload do theme quá nặng, đó là hãy giải nén ra và upload thư mục theme vào thư mục /wp-content/themes/, nhớ là thư mục theme cũng phải có dạng /tên-theme/style.css chứ không phải /tên-thư-mục/tên-theme/style.css.

Sau khi upload xong, bạn vào **Appearance –> Themes** rồi kích hoạt vì lúc này theme mà bạn vừa upload đã hiển thị trong đó.

### Nói thêm về việc cài theme

Khi bạn xem demo (bản xem thử) của một theme nào đó thì điều đó không có nghĩa là bạn cài vào là nó hiển thị giống y hệt như vậy. Bạn phải biết, mỗi theme đều có một cách cài khác nhau và muốn giống như demo bạn cũng phải tùy chỉnh nhiều (thông qua các tùy chọn sẵn có). Do vậy, bạn nên tập cài các theme miễn phí trong thư viện vì có nhiều theme cũng khá khó cài nên đó là nguồn bạn thực hành tốt nhất, dần dần bạn sẽ cảm thấy cài một theme như demo không hề quá khó.

### Lời kết

Vậy là hết bài này, bạn đã biết cách thay đổi giao diện cho website của mình nhờ vào việc tìm hiểu cách cài một theme mới vào website thông qua nhiều cách khác nhau. Cũng từ đó, mình đã có nói qua một số lưu ý khi cài theme nên mình hy vọng bạn có thể nhớ nó và tập cách cài cho thuần thục.

Nguồn: Thạch Phạm Blog
