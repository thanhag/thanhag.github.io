---
title: "Hướng dẫn cài đặt Google Analytics cho website của bạn"
date: "2017-08-31"
categories: 
  - "seo"
  - "thiet-ke-web"
  - "wordpress"
tags: 
  - "cai-dat-google-analytics"
  - "google-analytics"
  - "huong-dan-cai-dat-google-analytics"
  - "su-dung-google-analytics"
  - "tao-thong-ke-trang-web"
  - "thiet-ke-web"
  - "thong-ke-trang-web"
  - "wordpress"
  - "wordpress-co-ban"
header:
  image: /assets/images/1314.jpg
  teaser: /assets/images/1314.jpg
toc: true
breadcrumbs: true
---

Trong bài này Sofsog xin **_h__ướng dẫn cài đặt Google Analytics_** và đọc một số báo cáo cơ bản của Google Analytics cho website của bạn một cách chi tiết nhất.

# **1\. Trước tiên Google Analytics là gì?**

Đúng như tên gọi Analytics, **Google Analytics** (GA) là công cụ thống kê dữ liệu số mạnh nhất cho người quản trị web. GA chủ yếu phân tích số lượng người truy cập website của bạn, phân loại và theo dõi số lượng người đó theo hành vi, độ tuổi, ngôn ngữ, thiết bị máy vi tính, điện thoại, từ khóa… Google Analytics là một phần không thể thiếu với người làm SEO.

# **2\. Hướng dẫn cài đặt Google Analytics:**

## **Bước 1: Đăng ký Google Analytics**

Để đăng ký Google Analytics, bạn truy cập vào trang chủ [Google Analytics](http://www.google.com/analytics/ "Trang chủ Google Analytics").

Bấm nút **SIGN IN** ở góc phải phía trên, như trong hình, bấm tiếp [Analytics](http://www.google.com/analytics/ "Trang chủ Google Analytics").

![hướng dẫn cài đặt google analytics](/assets/images/hướng-dẫn-cài-đặt-google-analytics.png)

Đăng nhập bằng tài khoản Gmail của bạn. Nếu chưa có thì tạo ngay 1 cái nhá

Đăng nhập xong bạn sẽ thấy một ô nhỏ nhỏ có hình như sau, nếu Gmail đăng ký là là tiếng Việt:

![Hướng dẫn cài đặt google analytics](/assets/images/hướng-dẫn-cài-đặt-google-analytics-2.png)

Bấm nút **Đăng ký**, đương nhiên rồi, điền các thông tin cần thiết vào, tham khảo hình dưới:

![Hướng dẫn cài đặt google analytics](/assets/images/hướng-dẫn-cài-đặt-google-analytics-3.png)

Lưu ý: ở ô **URL của trang web,** các bạn chọn đúng **<http://>** và **<https://>**, có **www** hay không ?

Xong thì bấm nút "**Nhận ID theo dõi**" màu xanh bên dưới cùng. Chọn "**Chấp nhận**" điều khoản của Google.

Đối với các bạn đã có sẳn tài khoản **Google Analytics** từ trước, có thể thêm website khác vào **Google Analytics,** trong tài khoản bạn chọn "**Quản trị**" (biểu tượng bánh răng), trong ô "**Tài khoản**", click vào đó chọn "**Tạo tài khoản mới**", xem hình:

![Hướng dẫn cài đặt google analytics (5)](/assets/images/hướng-dẫn-cài-đặt-google-analytics-5.png)

Điền thông tin giống như các bước tạo tài khoản mới hồi nảy.

## **Bước 2: Thêm mã theo dõi vào trang web của bạn**

Khi làm xong bước 1 bên trên, bạn sẽ được đưa sang một trang như trong hình:

![hướng dẫn cài đặt google analytics (4)](/assets/images/hướng-dẫn-cài-đặt-google-analytics-4.png)

Bạn để ý ô **màu đỏ** (hình chữ nhật to) ở trong hình bên trên, đây chính là **mã theo dõi**, bạn phải sao chép và dán **mã theo dõi** này vào trang web của bạn.

Trường hợp không thấy mã, bên trong tài khoản bạn chọn "**Quản trị**" (biểu tượng bánh răng), ở phần "**Thuôc tính**" (nằm giữa màn hình), chọn đúng tên trang web của bạn, chọn tiếp "**Thông tin theo dõi**", chọn "**Mã theo dõi**", sẽ hiện ra giống hình bên trên.

**Thêm mã theo dõi vào website:**

Google Analytics đo đạc và lấy thông tin từ website của bạn thông qua một đoạn mã Javascript (còn gọi là Mã theo dõi). Đó chính là đoạn **mã theo dõi** mà mình gới thiệu bên trên.

Các bạn nên chèn **mã theo dõi** bên trên vào thẻ **Header** của trang web của bạn là tối ưu nhất.

Ở đây mình hướng dẫn chèn **mã theo dõi** vào trang web trên nền tảng Wordpress, phổ biến nhất, các nền tảng khác (Blogger, Magento, Drupal…) các bạn search Google, vì dụ "thêm code vào header Drupal", để thực hiện nhá.

Đối với Wordpress, các bạn có thể tự thêm code vào **Header** thủ công (nếu bạn rành code một chút), còn không thì mình khuyên bạn nên sử dụng Plugin [Insert Headers and Footers](https://wordpress.org/plugins/insert-headers-and-footers/) là dễ dàng và an toàn nhất.

Trong Dashboard của WordPress, bạn chọn **Plugins/Add New**. Sau đó search từ khóa “**Insert Headers and Footers**", chọn kết quả đúng nhất (hình như đầu tiên thì phải), chọn **cài đặt** rồi chọn **kích hoạt** Plugin (phần này dễ các bạn tự làm nhá)

Cài và kích hoạt xong Plugin, các bạn thêm mã theo dõi **Google Analytics** bằng cách: Trong Dashboard của WordPress, bạn chọn **Setting/Insert Headers and Footers** , dán đoạn mã theo dõi vào ô bên trên (ô **Scripts in Header**) như hình:

![hướng dẫn cài đặt google analytics (6)](/assets/images/hướng-dẫn-cài-đặt-google-analytics-6.png)

Xong thì nhớ bấm nút **Save** nhá.

Vậy là bạn đã cài đặt **Google Analytics** cho WordPress thành công, tuy nhiên bạn phải chờ 18-24 tiếng mới có những báo cáo đầu tiên.

# **3\. Hướng dẫn sử dụng Google Analytics:**

Các báo cáo trong Google Analytics được liệt kê trong thanh điều hướng bên trái của trang. Nếu bạn là người mới bắt đầu, bạn cần quan tâm đến những báo cáo sau:

### 3.1. Thời gian thực (Real time)

Cho bạn biết những gì đang diễn ra ở thời điểm hiện tại.

![](/assets/images/1314.jpg)

Báo cáo thời gian thực là 1 công cụ rất tiện ích, cho phép bạn theo dõi được lượng truy cập trong 1 thời điểm thực tế: Những ai đang truy cập, họ đến từ đâu và họ đang xem ở trang nào, bài nào ngay tại thời điểm đó. Để xem được, bạn vào Báo cáo tổng quan hoặc có thể tìm hiểu sâu hơn các thông tin bằng cách click vào những báo cáo chi tiết dưới đó: Vị trí, nguồn lưu lượng, nội dung, sự kiện, chuyển đổi.

Tính năng này đặc biệt quan trọng trong việc kiểm định tác động trực tiếp tới lưu lượng truy cập của các chiến dịch quảng cáo, email marketing…

Ví dụ như bạn đang chạy quảng cáo trên Facebook, ngoài việc bạn có thể theo dõi tổng bao nhiêu người đang truy cập trang web của bạn mà bạn còn biết được có bao nhiêu lượt truy cập từ Facebook trong thời điểm hiện tại. Qua việc giám sát này, bạn sẽ có sự đánh giá hiệu quả của chiến dịch này, có thu hút lượt click hay không, trang nào, bài viết nào được người tiêu dùng quan tâm…

### 3.2. Đối tương (Audience)

Thống kê chi tiết thành phần, số liệu cụ thể của khách hàng, người truy cập website.

![](/assets/images/1313.png)

Báo cáo này giúp bạn nắm được những thông tin cơ bản của khách hàng về nhân khẩu học như giới tính, ngôn ngữ, địa điểm, thậm chí còn có thể biết được họ truy cập website của bạn nhờ sản phẩm công nghệ nào (điện thoại hay PC…), hệ điều hành gì (Mac, window, iOS, Android…), mạng nào (FPT, 3G, Viettel…)

Trong phần Tổng quan đối tượng bao gồm các thông tin:

- Phiên: Khoảng thời gian mà 1 người dùng truy cập website
- Người sử dụng: Tổng số người truy cập vào website bao gồm cả người dùng cũ và người dùng mới
- Số lần xem trang: Tổng số trang đã được xem. Số lần xem lặp lại của 1 trang vẫn được tính
- Số trang/phiên: Cho bạn biết trung bình 1 phiên truy cập đọc bao nhiêu trang trên website
- Thời gian trung bình của phiên: Thời gian trung bình mỗi lần truy cập
- Tỷ lệ thoát: Được tính là tỷ lệ % lượng truy cập vào website và thoát ra mà không có thao tác nào trong khoảng thời gian 30s.
- % phiên mới: Tỷ lệ % lượng khách hàng mới so với tổng số người truy cập website.

Những thông tin trên giúp bạn nắm rõ được tình hình phát triển của website. Một trang web thành công là 1 trang web có lượng truy cập cao, số phiên, số người sử dụng, lần xem trang, số trang phiên, thời gian trung bình của phiên càng lớn càng tốt, riêng tỷ lệ thoát cần phải giảm tối đa. Chỉ số % tỷ lệ mới cao hay thấp là tốt thì còn phụ thuộc vào chiến lược website. Ví dụ như website của bạn mới được thành lập thì cần phải đẩy mạnh % người dùng mới này. Còn khi website đã đi vào quỹ đạo ổn định, đạt lượng truy cập nhất định, việc bạn cần làm là giữ chân những lượt truy cập cũ bằng cách thường xuyên cập nhật nội dung hữu ích cho họ.

Các thông tin về nhân khẩu học như giới tính, vị trí… nói cho bạn biết khoanh vùng đối tượng để bạn có kế hoạch tiếp cận với những khách hàng tiềm năng với ngành nghề, quy mô của bạn.

### 3.3.  Sức thu hút (Acquisition)

Thể hiện cách thức khách hàng đến với website của bạn và quản lý được tiến trình của các chiến dịch quảng cáo trả phí, từ khóa,…

![](/assets/images/1312.png)

Báo cáo này rất quan trọng bởi nó cung cấp cho bạn đầy đủ thông tin về cách thức khách hàng tìm đến website của bạn và cách họ truy cập trang như thế nào. Google Analytics sẽ cung cấp cho bạn tỷ lệ những kênh mà thông qua đó người dùng đến với website của bạn, ví dụ như Google search, mạng xã hội hay vào trực tiếp trang… Chi tiết hơn, bạn cũng biết được kênh nào thu hút được nhiều khách ghé thăm, kênh nào mang lại nhiều tương tác nhất hay kênh nào mang đến nhiều doanh thu nhất… Từ việc nắm được phương thức, kênh hiệu quả hay không có thể giúp bạn định hướng và đầu tư hiệu quả để chiến dịch tiếp cận khách hàng tối ưu nhất.

Ngoài ra, báo cáo này cũng giúp bạn biết được những trang hoặc những domain đang có đường liên kết với website và lượng truy cập từ các kênh đó để bạn lựa chọn cơ hội quảng bá website hiệu quả.

### 3.4.  Hành vi (Behavior)

Giúp bạn thống kê những tương tác của người truy cập đối với website.

![](/assets/images/1311.png)

Báo cáo hành vi bao gồm tất cả thông tin về nội dung từng trang, tốc độ và thời gian tải trang, phản ứng của người truy cập khi vào website của bạn. Từ đó, bạn sẽ có kế hoạch cải thiện nội dung hoặc kĩ thuật tốt hơn cho website của mình để tạo ra những trải nghiệm thú vị hơn dành cho khách hàng và làm gia tăng tỷ lệ chuyển đổi.

# **3. Lời kết:**

Đối với các bạn mới sử dụng lần đầu, mình nghĩ **_hướng dẫn cài đặt google analytics_** cùng với hướng dẫn sử dụng các báo cáo như trên là quá tốt, sau một thời gian sử dụng bạn có thể tìm hiểu thêm các [tính năng nâng cao của Google Analytics](https://www.google.com.vn/intl/vi_ALL/analytics/features/index.html)  . Ngoài ra theo mình các tính năng cơ bản như bài viết này là đủ.

Trong quá trình cài đặt và sử dụng nếu các bạn gặp khó khăn vấn đề gì có thể để lại comment bên dưới, Sofsog xin hỗ trợ hết mức có thể.
