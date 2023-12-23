---
title: "Plugin tăng tốc cho Wordpress"
date: "2016-10-03"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "plugin"
  - "seo"
  - "tang-toc-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
---

_WordPress_ vốn là một nền tảng blog nhỏ gọn và đã được tối ưu hóa để có thể ít chiếm tài nguyên nhân nhất có thể. Nhưng đó chỉ là “viễn cảnh” nếu bạn đang sử dụng blog WordPress mà không cài thêm cứ bất kỳ plugin hay theme nào, còn nếu bạn đã tiến hành cài đặt một số plugin mà bạn thích và sử dụng những themes có nhiều chi tiết phức tạp sẽ khiến blog bạn ngày càng trở nên chậm chạp như thể nó đang già nua đi mỗi ngày.

![plugin-tang-toc-wordpress](http://sofsog.com/wp-content/uploads/2016/10/Plugin-tang-toc-Wordpress.svg)

Tạm gác lại phương án chuyển hosting, bạn nên áp dụng một số phương thức **tăng tốc  WordPress** khác để cải thiện tốc độ của blog. Một trong những phương án đơn giản nhất dành riêng cho WordPress là sử dụng các plugin có sẵn trong thư viện WordPress để hạn chế tối đa việc tinh chỉnh thủ công.

Với **hàng chục plugin hỗ trợ tăng tốc** thì việc lựa chọn một plugin theo đúng nhu cầu của mỗi người là một quá trình dài hơi. Như vậy để tiện lợi hơn cho việc chọn plugin cho mọi người, mình xin liệt kê danh sách các plugin tốt nhất dùng để tăng tốc blog WordPress và theo mình nghĩ bạn chỉ cần một vài trong số 8 plugin này là đủ.

#### Tạo cache cho trang với WP Super Cache

Nếu như bạn muốn cải thiện tốc độ của blog mà không sử dụng bộ nhớ đệm (cache) thì là điều hơi thiếu sót. Các bản lưu cache sẽ rút ngắn thời gian tải trang thông qua việc sao lưu một bản nội dung tĩnh lên máy chủ, và khi có người truy cập vào thì bản lưu đó sẽ được thực thi. Như vậy thì chúng ta sẽ tiết kiệm được khâu gửi reuqest đến máy chủ thông qua các lệnh thi hành PHP và cơ sở dữ liệu.

Một plugin mà luôn nằm trong danh sách bắt buộc phải có trong WordPress với riêng mình là WP Super Cache. Với ưu điểm dễ sử dụng, không cần cấu hình nhiều mà vẫn hỗ trợ rất nhiều chức năng cần thiết, mình tin rằng đây luôn là sự lựa chọn tối ưu nhất cho những người không am hiểu nhiều về kỹ thuật.

![W3 Total Cache](/assets/images/33_8015047187_6ca712f586_o.jpg "Plugin tạo cache nâng cao để tăng tốc blog WordPress")

Ngoài ra còn một plugin có cùng chức năng nhưng có phần hơi khó sử dụng đó là W3 Total Cache. Tuy nhiên nếu bạn cần một plugin có nhiều chức năng hơn và cấu hình nâng cao hơn thì đây cũng là một sự lựa chọn tốt.

#### Giảm tải Javascript với [jsDelivr WordPress CDN Plugin](http://wordpress.org/extend/plugins/jsdelivr-wordpress-cdn-plugin/ "Plugin chuyển các file javascript ra máy chủ ngoài")

![%image_alt%](/assets/images/8015084944_b8b5be3d99_o.png "Áp dụng công nghệ CDN cho các file Javascript để tăng tốc blog WordPress")

Đây là một plugin mới được giới sử dụng WordPress biết tới khoảng hơn 1 tháng nay. Plugin này sẽ tự động chuyển các file Javascript (.js) ra máy chủ công cộng bên ngoài nhằm cải thiện tối thiểu thời gian tải trang, đồng thời tiết kiệm băng thông vì không sử dụng trực tiếp các file Javascript trên host mình.

Plugin này cũng được tích hợp với _WP Super Cache_ và _W3 Total Cache_, lời khuyên của mình là dù host bạn yếu cỡ nào đi chăng nữa thì cũng đừng quên sử dụng plugin này.

#### Load ảnh thông minh với [BJ Lazyload](http://wordpress.org/extend/plugins/bj-lazy-load/ "Kích hoạt lazyload cho hình ảnh để tăng tốc blog")

Một trong những lý do “kinh điển” làm blog của bạn trở nên chậm chạp đó là sử dụng quá nhiều hình ảnh. Sau khi kích hoạt plugin này, các hình ảnh có trong blog của bạn sẽ không load một lượt mà chỉ load hình ảnh chỉ khi nào bạn cần xem (đi đến khu vực hiển thị hình ảnh). Nếu bạn vẫn chưa hiểu plugin này làm việc ra sao thì xem demo LazyLoad  [tại đây](http://davidwalsh.name/demo/lazyload-2.0.php "lazyload demo").

### Sử dụng [Use Google Libraries](http://wordpress.org/extend/plugins/use-google-libraries/) để tiết kiệm băng thông

Tương tự như với plugin jsDevilery, plugin này sẽ giúp bạn thay thế các file javascript thông dụng có trên host để sử dụng các file đó trên [thư viện Javascript của Google](https://developers.google.com/speed/libraries/ "Thư viện plugin Javascript của Google") nhằm tiết kiệm băng thông và giảm CPU load cho máy chủ.

### Tối ưu hình ảnh to với Hammy

![%image_alt%](/assets/images/2_8015220006_c53bbe14a1_o.jpg "Tự động giảm kích thước hình ảnh theo từng trình duyệt")

Nếu bạn đã từng truy cập vào một số website có nhiều hình ảnh bằng trình duyệt trên các thiết bị di động thì sẽ thấy điều đó đáng sợ đến chừng nào. Các hình ảnh có kích thước to sẽ gây ra tình trạng tải ì ạch trên các trình duyệt di động vì khả năng xử lý của các thiết bị di động có giới hạn. Vì vậy muốn giải quyết vấn đề này, chúng ta phải tiến hành giảm kích cỡ hình ảnh xuống cho từng trình duyệt để thích hợp hơn với các thiết bị đó, và đó chính là tính năng của plugin này.

### Bảo mật và tăng tốc với CloudFlare

![%image_alt%](/assets/images/33_8015142697_7ca62d77f4_o.png)

Dịch vụ này đã được mình nhắc tới trong bài viết giới thiệu công nghệ CDN. Về bản chất thực sự của nó thì đây là dịch vụ miễn phí để kích hoạt tính năng CDN cho website để tăng tốc blog, đồng thời tối ưu hóa và bảo mật blog bạn tránh khỏi các nguy cơ tấn công và spam, một điều tuyệt vời hơn nữa là CloudFlare hiện nay còn cho phép sử dụng SSL miễn phí để bảo mật website tốt hơn.

### Phân tích tốc độ blog với [Plugin Performance Profile](http://wordpress.org/extend/plugins/p3-profiler/ "Phân tích tác nhân làm chậm blog WordPress")

![Plugin Performance Profile](/assets/images/8015092405_b91e90d3e9_o.png "Phân tích tác nhân làm chậm blog WordPress")

Nếu như bạn chưa rõ vì sao blog mình trở nên chậm chạp thì có thể dùng plugin này để phân tích. Các báo cáo chi tiết sẽ cho bạn thấy được phần nào trong blog chiếm tài nguyên nhiều nhất, từ đó bạn có thể tối ưu hóa cho từng phần đó để giảm tải gánh nặng cho máy chủ.

### Sử dụng [Async Social Sharing](http://wordpress.org/extend/plugins/async-social-sharing/ "Tạo các nút chia sẻ bài viết với các file javascript đã được tối ưu") để chèn nút mạng xã hội tối ưu

![%image_alt%](/assets/images/37_8015162403_3ba536a423_o.jpg)

Bạn có chèn các nút chia sẻ bài viết lên mạng xã hội vào blog không? Vậy bạn có nhận ra điều gì từ những nút chia sẻ đó? Chẳng có điều gì khác ngoài việc blog bạn trở nên hơi chậm một chút vì phải load thêm các file Javascript đi kèm nó. Thế thì hãy sử dụng plugin này ngay, Async Social Sharing sẽ tiến hành tải các file javascript sau khi toàn bộ nội dung trên blog đã được tải xong. Vì sao lại phải tải các nút này sau cùng? Bởi vì nội dung trên blog của bạn quan trọng hơn, người ta chỉ bấm vào nút Like hay +1 chỉ khi thấy nội dung của bạn thật sự tốt, như vậy thì cớ gì phải để các file javascript của các nút này tải cùng lúc với nội dung của bạn?

### Tối ưu điểm PageSpeed với [Speed Booster Pack](https://wordpress.org/plugins/speed-booster-pack/)

Cài đặt và kích hoạt mà không cần chỉnh gì cả để có điểm Google PageSpeed cao hơn, tại sao không? Thích hợp cho các bạn nào thích theo đuổi chỉ số điểm Google Pagespeed chứ bản thân mình thì không dùng.

Nguồn: Thạch phạm Blog
