---
title: "Hướng dẫn sử dụng CloudFlare"
date: "2017-05-15"
categories: 
  - "thiet-ke-web"
  - "thu-thuat-chung"
  - "wordpress"
tags: 
  - "cloudflare"
  - "dns"
  - "dns-mien-phi"
  - "dns-trung-gian"
  - "huong-dan-su-dung-cloudflare"
header:
  overlay_image: /assets/images/cloudflare-example-960x480.png
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)" 
  teaser: /assets/images/cloudflare-example-960x480.png
toc: true
breadcrumbs: true
---

**CloudFlare** là một dịch vụ DNS trung gian rất nổi tiếng trên thế giới. Nhiều người, trong đó có mình sử dụng CloudFlare bởi những chức năng đặc biệt mà không nhà cung cấp DNS nào khác có được.

Ngoài chức năng DNS thông thường, khi sử dụng CloudFlare bạn còn được xài CDN, tường lửa hạn chế DDoS + Spam, SSL, Forward Domain và nhiều chức năng khác nữa. Tất nhiên, miễn phí hết nhé.

CloudFlare có [mạng lưới máy chủ toàn cầu](https://www.cloudflare.com/network/) phục vụ cho DNS nên lúc nào cũng đảm bảo thời gian look-up cực nhanh khi truy cập từ mọi nơi trên thế giới. Hơn nữa, tốc độ cập nhật DNS ở đây gần như là ngay lập tức luôn, rất sướng.

![](/assets/images/cloudflare-example-960x480.png)

## I. Đăng ký tài khoản CloudFlare

Để dùng được CloudFlare, bạn cần phải có một tài khoản. Thủ tục đăng ký rất nhanh gọn.

– Đầu tiên bạn truy cập vào [https://www.cloudflare.com](https://www.cloudflare.com/), click _Sign up now!_

– Thông tin đăng ký chỉ cần nhập Email và Password là xong.

– Đăng ký xong, bạn hãy Login để sử dụng.

## II. Thêm Website vào CloudFlare

### 1\. Add Site

– Đầu tiên bạn click link _Add Site_ để thêm website mới vào hệ thống CloudFlare. Nhập tên miền rồi click _Begin Scan_.

![huong dan su dung Cloudflare 3-min](/assets/images/huong-dan-su-dung-Cloudflare-1-min.png)

– Bạn có thể thêm nhiều tên miền cùng một lúc, mỗi tên miền cách nhau bởi dấu phẩy ,

– Đợi khoảng 1 phút để CloudFlare scan toàn bộ các bản ghi hiện có. Đây là một chức năng rất hay, bạn không cần tốn thời gian để chuyển các bản ghi DNS cũ sang nữa.

– Tiếp theo, nhấn nút _Continue_ để tiếp tục.

### 2\. Xác nhận các bản ghi cho tên miền

– Nếu tên miền đang hoạt động, toàn bộ các bản ghi sẽ được CloudFlare quét và hiển thị bên dưới, hầu hết đều chuẩn nên bạn chỉ cần duyệt qua mà thôi.

– Có thể xuất hiện trường hợp không có bản ghi nào cả, nếu tên miền vừa được đăng ký xong.

![huong dan su dung Cloudflare 3-min](/assets/images/huong-dan-su-dung-Cloudflare-2-min.png)

Bạn có thể cập nhật các bản ghi ngay bây giờ hoặc cập nhật sau.

Nhấn nút _Continue_ để tiếp tục.

### 3\. Lựa chọn Plan

CloudFlare có khá nhiều plan với các chức năng cao cấp, tuy nhiên chúng ta chỉ cần dùng Free Plan là đủ rồi.

Chọn _Free Website_ rồi nhấn _Continue_.

![huong dan su dung Cloudflare 3-min](/assets/images/huong-dan-su-dung-Cloudflare-3-min.png)

### 4\. Trỏ Name servers về CloudFlare

Cuối cùng, CloudFlare cung cấp 2 bản ghi Name servers, hãy trỏ tên miền về Name servers mới này. Nhấn _Continue_ để hoàn tất.

![](/assets/images/huong-dan-su-dung-Cloudflare-4-min.png)

Đợi một lúc chờ tên miền cập nhật Name servers xong thì CloudFlare sẽ tự động gửi một email thông báo hoàn tất. Tên miền đã xuất hiện trong tài khoản của bạn và có Status là Active.

![](/assets/images/huong-dan-su-dung-Cloudflare-5-min.png)

Vậy là xong, website hoạt động rồi đó.

![](/assets/images/huong-dan-su-dung-Cloudflare-7.png)

Giới thiệu các tính năng cho các bạn tự nghiên cứu thêm

### Overview

Mục này bạn sẽ xem được tổng quan thiết lập của website trên CloudFlare và nơi để bạn chỉnh lại trạng thái của website hay nâng cấp lên CloudFlare trả phí. Thường thì chúng ta sẽ không dùng nhiều tính năng ở đây.

Để chuyển trạng thái của CloudFlare,bạn chọn nút Quick Actions. Nếu website của bạn đang bị tấn công, bạn có thể chuyển trạng thái thiết lập CloudFlare sang Under Attacked Mode để nó tự cấu hình bảo mật tối đa cho bạn. Nếu webite bạn đang trong giai đoạn phát triển, đang chỉnh sửa các tập tin CSS hay JS thì nên chuyển về trạng thái Development Mode để nó không lưu cache.

### Analytics

Nếu bạn cần xem thống kê lượng băng thông của website đã sử dụng hoặc các thống kê khác liên quan đến bảo mật thì có thể xem tại trang này. Ở đây bạn sẽ thấy các thống kê rất chi tiết dù là tài khoản miễn phí, nhưng khi nâng cấp trả phí bạn sẽ sử dụng được nhiều hơn.

### DNS

Nơi quản lý và sửa đổi các bản ghi DNS của tên miền. Khi bạn trỏ tên miền về CloudFlare thì khi có nhu cầu trỏ tên miền về máy chủ khác, bạn sẽ thực hiện sửa trong đây.

### Crypto

Ở trang này bạn sẽ thấy được các tùy chọn bật những tính năng liên quan đến việc mã hóa của website như SSL, HSTS, TLS,…Tài khoản miễn phí sẽ bị giới hạn một số tính năng. Và nếu bạn không có ý định cài SSL miễn phí cho CloudFlare thì đừng sửa thiết lập phần này.

### Firewall

Mục này sẽ cần đụng tới nếu bạn cần sửa các thiết lập liên quan tới tường lửa trên website như bật tắt tường lửa, theo dõi IP truy cập vào website,….

Security Level: Chọn mức độ bảo vệ.

Challenge Passage: Chọn thời gian lưu lại thử thách với các lượt truy cập nghi vấn tấn công/spam. Thử thách ở đây là các lượt truy cập đó sẽ phải nhập một mã captcha khi vào website bạn.

IP Firewall: tại đây bạn có thể xem danh sách các IP đã truy cập vào website. Nếu bạn cảm thấy IP nào nghi vấn, bạn có thể ấn vào nút Whitelist và chọn CAPTCHA hoặc BLOCK hoặc Javascript Challenge.

Bạn có thể bật captcha cho tất cả lượt truy cập từ quốc gia nào đó, rất tiếc là không thể chặn.

### Speed

Nơi chứa các thiết lập liên quan đến việc tăng tốc độ cho website sử dụng CloudFlare như bật tắt các tính năng nén Javascript/CSS/HTML, bật tính năng RocketLoader (sử dụng kỹ thuật tải async cho Javascript),…

- **Auto Minify**: Bật chức năng nén Javascript, CSS và HTML. Lưu ý một vài giao diện website sẽ không thể hoạt động tốt sau khi bật chức năng nén CSS hoặc Javascript.
- **Polish**: Tính năng tự động tối ưu dung lượng hình ảnh trên website để tăng tốc tốt hơn. Chỉ có ở gói Pro.
- **Railgun**: Sử dụng công nghệ Railgun để nén dữ liệu gửi từ server đến CloudFlare nhằm giảm thời gian tải trang tốt hơn. Chỉ có ở gói Business.
- **Mirage**: Giảm thời gian tải hình ảnh trên các thiết bị di động. Chỉ có ở gói Pro.
- **Rocket Loader**: Giảm thời gian tải trang bằng cách tải các tập tin Javascript ở dạng không đồng bộ.
- **Mobile Redirect**: Chuyển hướng qua một sub-domain khác khi truy cập bằng diện thoại di động. Bạn phải thêm bản ghi cho subdomain tại mục DNS mới dùng được tính năng này.

### Caching

Tùy chỉnh và bật tắt các tính năng lưu bộ nhớ đệm cho website để hỗ trợ tăng tốc và tiết kiệm băng thông.

- **Purge Cache**: Xóa bản lưu cache của website, bạn có thể xóa cache của một tập tin riêng hoặc cache toàn bộ website.
- **Cache Level**: Cấp độ lưu bộ nhớ đệm. Ấn phần Help để xem họ giải thích ý nghĩa của từng thiết lập, nếu bạn chưa rõ thì chọn Standard.
- **Browser Cache Expiration**: Chọn thời gian lưu bộ nhớ đệm của các tập tin trên website. Nếu website bạn có ít thay đổi về mã nguồn thì hãy chọn càng lâu càng tốt.
- **Development Mode**: Nếu website bạn đang tiến hành sửa code bên trong, tốt nhất nên bật chế độ Development Mode để CloudFlare không lưu lại cache.

### Page Rules

Tính năng này chỉ có ở gói Pro, nhưng nó sẽ rất có ích nếu như bạn muốn thiết lập CloudFlare riêng cho từng trang. Ví dụ ở trang chủ chúng ta thiết lập bảo vệ mạnh nhưng các trang khác thì không. Hoặc nếu một subdomain của bạn bị lỗi khi bật Minify thì có thể dùng tính năng này để tắt Minify ở subdomain đó.

### Network

Phần này chúng ta cũng ít khi đụng tới vì nó sẽ có một số tính năng để cấu hình như bật tắt hỗ trợ IPv6, bật tính năng IP Geolocation và một số tính năng nâng cao chỉ có ở tài khoản Pro hoặc Business.

HTTP/2 + SPDY: Sử dụng giao thức SPDY và HTTP/2 để kết nối vào website hỗ trợ SSL nhanh hơn, tính năng này có thể cấu hình khi cài đặt SSL cho domain tại CloudFlare.

IPv6 Compatibility: Hỗ trợ tính năng phân giải IPv6 nếu host của bạn có hỗ trợ IPv6.

Websockets: Cho phép websockets của CloudFlare kết nối với máy chủ của website bạn nhanh hơn. Và tuy theo gói bạn đang sử dụng, khả năng kết nối của websocket cũng khác.

**IP Geolocation**: bật tính năng xác định quốc gia của người dùng thông qua IP của họ. Đây là tính năng bạn sẽ cần nếu như bạn cần xác định quốc gia của khách hàng do website sử dụng CloudFlare đều pass lượt truy cập qua proxy nên thông tin thu thập từ server cũng khác. Sau khi bật tính năng này, bạn sử dụng code của họ để lấy IP của khách theo [hướng dẫn này](https://support.cloudflare.com/hc/en-us/articles/200168236-What-does-CloudFlare-IP-Geolocation-do-).

Maximum Upload Size: Dung lượng tập tin upload tối đa của người truy cập vào website cho mỗi request gửi đi. Mặc định gói miễn phí bạn bị giới hạn 100MB.

### Traffic

Theo dõi các lượt truy cập vào website đã bị chặn hoặc áp đặt thử thách.

###  Customize

Một tính năng thú vị khi sử dụng gói Pro trở lên, đó là bạn có thể tùy biến lại các trang thông báo lỗi của CloudFlare.

### App

Một cái hay của CloudFlare là bạn có thể dễ dàng tích hợp các dịch vụ thứ ba vào, và bạn sẽ kích hoạt nó ở phần này. Ví dụ bạn có thể tích hợp Google Analytics vào website thông qua CloudFlare mà không cần chèn mã theo dõi vào website.

## Một số vấn đề khi sử dụng CloudFlare

Mỗi khi bạn muốn sửa nội dung file CSS hay Javascript, bạn nên kích hoạt chế độ Development Mode để nó không lưu cache các file tĩnh và như vậy bạn mới thấy sự thay đổi. Chế độ này sẽ tự động bỏ đi sau 3 giờ.

![cloudflare-devmode](/assets/images/cloudflare-devmode.jpg)

Ngoài ra bạn cũng nên biết là sau này nếu có chuyển host, bạn hãy vào CloudFlare để đổi lại IP của host mới chứ đừng đụng chạm gì đến việc sửa lại Nameserver của tên miền.

### Lấy IP gốc visitor

**Với Shared Hosting**, các bạn không có quyền can thiệp nhiều vào hệ thống. Để lấy IP gốc của visitor thay vì IP proxy của CloudFlare, chỉ có duy nhất cách cài plugin tương ứng với hệ thống CMS đang sử dụng bên dưới:

- [WordPress Plugin](http://blog.cloudflare.com/introducing-the-cloudflare-wordpress-plugin): hiển trị IP thật của người dùng khi truy cập, ngoài ra plugin này còn hỗ trợ optimize database và trực tiếp report spam users từ blog.
- [Joomla Extension](http://blog.cloudflare.com/introducing-the-cloudflare-joomla-extension): hiển trị IP thật của người dùng khi truy cập, ngoài ra không có thêm chức năng nào khác.
- [Drupal Extension](http://blog.cloudflare.com/the-cloudflare-drupal-extension): hiển trị IP thật của người dùng khi truy cập, ngoài ra không có thêm chức năng nào khác.

Trong quá trình sử dụng CloudFlare, nếu gặp bất kỳ vấn đề gì bạn hãy để lại comment bên dưới, mình sẽ support hỗ trợ.

## Lời kết

Ở trên là cách thiết lập của CloudFlare, về cơ bản thì bạn chỉ cần làm vậy thôi là website bạn đã hoạt động tốt rồi. Nếu bạn muốn thì có thể vào phần thiết lập của từng tên miền trong CloudFlare để sửa lại các tùy chỉnh về tối ưu tốc độ và bảo mật, đừng quên xem qua phần [https://www.cloudflare.com/app-signup](https://www.cloudflare.com/app-signup) để sử dụng thêm một số apps được tích hợp sẵn vào CloudFlare chẳng hạn như tích hợp Google Analytics chẳng hạn.

Sofsog.com chúc các bạn thành công!

Nguồn: Canhme.com, thachpham.com
