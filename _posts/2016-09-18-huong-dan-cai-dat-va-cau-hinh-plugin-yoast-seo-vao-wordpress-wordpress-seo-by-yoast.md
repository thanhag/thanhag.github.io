---
title: "Hướng dẫn cài đặt và cấu hình plugin Yoast SEO vào wordpress (WordPress SEO by Yoast)"
date: "2016-09-18"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "plugin"
  - "wordpress"
  - "wordpress-co-ban"
  - "yoast-seo"
header:
  image: /assets/images/Yoast-Logo-Icon.png
  teaser: /assets/images/Yoast-Logo-Icon.png
toc: true
breadcrumbs: true
---

Khi nói đến các kỹ thuật SEO trong WordPress, chúng ta không thể nói đến một plugin miễn phí rất thông dụng để hỗ trợ bạn dễ dàng tối ưu lại tiêu đề & description của các thành phần trong website tên là **Yoast SEO** (tên cũ là WordPress SEO by Yoast). Ngoài ra, plugin này còn có rất nhiều tính năng khác cũng có liên quan tới SEO để bạn sử dụng.

Tuy nhiên, bạn nên biết rằng đây chỉ là plugin giúp bạn dễ dàng tinh chỉnh các thông tin về meta tag để tối ưu SEO chứ không phải cài vào là website sẽ có thứ hạng tốt.

![Thiết lập SEO by Yoast linh hoạt hơn với biến dữ liệu](/assets/images/Yoast-Logo-Icon.png)

## Tải và cài đặt plugin WordPress SEO

Đầu tiên thì bạn tải và cài đặt plugin trước nhé, nếu bạn chưa biết cách cài đặt thì có thể ghé qua xem bài viết hướng dẫn plugin WordPress. Bạn có thể cài đặt plugin thông qua bảng điều khiển hoặc tải bản cài đặt về máy tính rồi sau đó upload lên hosting thông qua phần mềm FTP.

Và bạn hãy nhớ tên của plugin này là **Yoast SEO** nó được viết bởi **Joost de Valk**.

Bây giờ thì bạn nhìn sang menu chính của bảng điều khiển bên phía tay trái thì bạn sẽ thấy một menu con với cái tên là **SEO**, bạn hãy nhấn vào menu này để chuyển sang khung Dashboard của plugin WordPress SEO.

![yoast-seo-01](/assets/images/yoast-seo-01.png) Khu vực thao tác plugin Yoast SEO

## Các tính năng trong WordPress SEO by Yoast

### Dashboard

Phần này là bảng thông tin chung về plugin Yoast SEO. Tại đây bạn có thể theo dõi các thông tin mới nhất từ nhà phát triển Yoast SEO và các thông tin khác liên quan đến website của bạn. Trong phần này có các phần nhỏ như:

- **Dashboard** Khu vực hiển thị các thông tin đưa ra các tư vấn về tối ưu website của bạn. Ví dụ nếu bạn đặt cấu trúc permalink chưa chuẩn, hoặc chưa thiết lập tagline cho website thì ở đây sẽ hiển thị ghi chú để bạn cải thiện.
- **General** Khu vực này hiện chưa có nhiều chức năng cho lắm, chỉ có một chức năng duy nhất là khôi phục các thiết lập mặc định.
- **Your Info** Thiết lập tên website và tên hiển thị metadata trên Google’s Knowledge Graph.
- **Webmaster Tools** Chỗ này để bạn điền các mã xác thực của các công cụ hỗ trợ khai báo website với máy tìm kiếm. Nếu bạn có chèn mã xác thực thì nên chèn vào đây vì nó sẽ không mất khi bạn đổi theme, nhưng tắt plugin này thì nó sẽ mất.
- **Security** Phần này hiện có một chức năng duy nhất là bật tính năng thiết lập SEO nâng cao ở khung meta box trong các bài viết.

### Titles & Metas

Mục này khá quan trọng, được sử dụng để tuỳ chỉnh cấu trúc title và thẻ meta description. Nên nhớ ở đây chỉ là nơi sửa cấu trúc thôi nhé, và bạn có thể đặt title và description cho trang chủ. Còn nếu bạn muốn đặt title và description cho post, page, category, tag,..thì bạn phải sửa thông tin của các phần đó để thêm.

#### General

Phần này là thiết lập chung liên quan đến tiêu đề và các thẻ meta, nó bao gồm các tùy chọn sau:

- Title Separator Thiết lập ký tự ngăn cách giữa tên website và tiêu đề của trang. Ví dụ: _Hướng dẫn Yoast SEO – Thach Pham Blog._ Trong đó, ký tự `-` là ký tự ngăn cách.
- Enabled analysis Ở đây để bật các chức năng phân tích trong Yoast SEO. Hiện tại nó hỗ trợ 2 tính năng phân tích là Readability analysis (Phân tích khả năng dễ đọc) và Keyword analysis (phân tích từ khóa) của nội dung trong trang.

#### Homepage

Phần này là nơi để thiết lập tiêu đề và mô tả của trang chủ. Nếu bạn sử dụng một Page (Trang) làm trang chủ thì nó sẽ nhắc nhở bạn vào page đó mà sửa tiêu đề và mô tả.

### Post Types

Khu vực này để bạn thiết lập lại cấu trúc tiêu đề và mô tả mặc định của các post types bên trong website (bao gồm Trang, Bài viết hoặc các post type khác có trong website) nếu bạn không nhập các thông tin này riêng. Trong phần này họ sử dụng các biến được thiết lập sẵn để đại diện một thành phần nào đó, ví dụ như %%title%% đại diện cho tiêu đề của trang.

Để hiểu hết về các biến trong Yoast SEO, bạn vui lòng tham khảo [**bài viết này**](http://sofsog.com/2016/09/19/thiet-lap-seo-yoast-linh-hoat-hon-voi-bien-du-lieu/).

Ngoài ra, ở đây bạn còn có các tùy chọn như thiết lập lại Meta Robots của post type, nếu bạn chưa hiểu Meta Robots là gì thì nên để mặc định.

### Taxonomies

Phần này cũng giống với Post Types nhưng nó áp dụng cho các taxonomies trong website (Category, Tag,…).

### Archives

Cũng giống như Post Types và Taxonomies, phần này để thiết lập cấu trúc tiêu đề và mô tả của các trang lưu trữ.

### Others

Các thiết lập khác liên quan đến tiêu đề và mô tả sẽ có tại đây, trong đây hiện tại có 3 chức năng chính:

- Subpages of archives Thiết lập noindex hoặc index các trang con ở các trang lưu trữ. Các trang con là những trang thứ 2 trở đi. Mình khuyên nên chọn là Noindex để tránh tình trạng trùng lặp tiêu đề và mô tả.
- Use meta keywords tag? Hiện tại Google đã không còn đánh giá cao thẻ meta tag trong website nên Yoast SEO mặc định sẽ không hiển thị phần nhập tag cho các trang. Nếu bạn muốn bật tính năng nhập tag cho trang thì phải bật tính năng này lên.
- Force noodp meta robots tag sitewide Thiết lập sử dụng thẻ meta noodp trên toàn trang của website.

## Social

![seo-by-yoast-social-2](/assets/images/seo-by-yoast-social-2.jpg)

Khu vực này giúp bạn điền các thông tin về tài khoản mạng xã hội có liên quan tới website của bạn như đường dẫn tới fanpage của Facebook, thêm tài khoản quản trị Facebook, thêm link đến Google+, Twitter,…với mục đích thông báo đầy đủ các thông tin về mạng xã hội để có tác động tới kết quả tìm kiếm hoặc khi chia sẻ liên kết lên mạng xã hội.

XML Sitemaps

![seo-by-yoast-sitemap-3](/assets/images/seo-by-yoast-sitemap-3.jpg)

Ở đây là nơi tuỳ chỉnh thiết lập chức năng tạo XML Sitemap cho website để bạn submit sitemap lên Google. Đường dẫn sitemap của bạn sau khi cài plugin này vào là `http://domain.com/sitemap_index.xml`.

Tại đây, bạn có thể tuỳ chỉnh các thành phần muốn đưa vào sitemap như category, tag hoặc post type nào đó.

## Advanced

Ở đây là các chức năng thêm mà bạn không bắt buộc để sử dụng.

### Breadcrumbs

Phần này sẽ thiết lập bật/tắt chức năng thanh điều hướng có hỗ trợ schema data. Sau khi bật lên, muốn thanh điều hướng hiển thị ở đâu thì chèn code này vào giao diện:

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td class="gutter"><div class="line number1 index0 alt2">01</div><div class="line number2 index1 alt1">02</div><div class="line number3 index2 alt2">03</div><div class="line number4 index3 alt1">04</div><div class="line number5 index4 alt2">05</div><div class="line number6 index5 alt1">06</div></td><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="php plain">&lt;!--?php &lt;br ?--&gt; </code><code class="php keyword">if</code> <code class="php plain">( function_exists(</code><code class="php string">'yoast_breadcrumb'</code><code class="php plain">) ) {</code></div><div class="line number2 index1 alt1"><code class="php plain">yoast_breadcrumb('</code></div><div class="line number3 index2 alt2"><code class="php plain">&lt;p id=</code><code class="php string">"breadcrumbs"</code><code class="php plain">&gt;</code><code class="php string">','</code><code class="php plain">&lt;/p&gt;</code></div><div class="line number4 index3 alt1"><code class="php plain">');</code></div><div class="line number5 index4 alt2"><code class="php plain">}</code></div><div class="line number6 index5 alt1"><code class="php plain">?&gt;</code></div></div></td></tr></tbody></table>

### Permalinks

- Phần này sẽ có các thiết lập phụ liên quan đến đường dẫn tĩnh.Strip the category base (usually /category/) from the category URL. Tùy chọn loại bỏ `/category/` trên đường dẫn các trang danh mục bài viết.
- Redirect attachment URLs to parent post URL. Tự động chuyển hướng trang của các tập tin đính kèm về trang bài viết mà nó được đính kèm.
- Stop words in slugs. Tự loại bỏ một số từ khóa thông dụng nhưng không cần thiết để đưa lên đường dẫn. Ví dụ như các từ `on`, `a`,`as`, `be`,…danh sách xem [tại đây](http://www.ranks.nl/stopwords).
- Remove the ?replytocom variables. Tự động loại bỏ tham số `?replytocom` trên các đường dẫn trả lời bình luận để tránh bị trùng tiêu đề và mô tả.
- Redirect ugly URLs to clean permalinks. (Not recommended in many cases!) Tự động chuyển hướng các đường dẫn có chứa các tham số về đường dẫn nguyên bản. Tuy nhiên tính năng này bạn không nên bật vì đôi khi dùng đường dẫn có chứa tham số hỗ trợ theo dõi trên website sẽ không làm việc chính xác cho lắm.

### RSS

Chức năng này sẽ cho phép bạn tự thêm một đoạn văn bản tùy thích vào trong đầu và cuối nội dung ở trang RSS Feed. Trang RSS Feed của bạn sẽ có đường dẫn là domain.com/feed.

## Tools

![seo-by-yoast-tools-4](/assets/images/seo-by-yoast-tools-4.jpg)

Đây là một số tính năng quản trị nhanh trong website, bao gồm:

- **Bulk Editor**: Sửa title và metas nhanh ở nhiều post hoặc page khác nhau.
- **File Editor**: Sửa file robots.txt và .htaccess trên host (Apache).
- **Import and Export:** Xuất và nhập các thiết lập trong SEO by Yoast của bạn.

## Search Console

Phần này sẽ hỗ trợ bạn kết nối website với tài khoản Google Webmaster Tools (Search Console) để theo dõi các liên kết truy cập vào website bị lỗi. Xem chi tiết với video bên dưới:

<iframe width="300" height="150" class="arve-inner fitvidsignore" src="https://www.youtube-nocookie.com/embed/UbrhOn8KXuE?wmode=transparent&amp;iv_load_policy=1&amp;modestbranding=0&amp;rel=0&amp;autohide=0&amp;v=UbrhOn8KXuE&amp;autoplay=0" frameborder="0" allowfullscreen="allowfullscreen" data-mce-fragment="1"></iframe>

## Cách dùng SEO by Yoast

### Tối ưu SEO cho Post/Page

Khi bạn vào sửa hoặc thêm mới một Post hoặc Page thì bạn sẽ thấy phần meta box cho phép nhập các thông tin liên quan đến tối ưu SEO bao gồm title, description, thông tin hiển thị ở mạng xã hội hoặc tối ưu nâng cao.

![yoast-seo-05](/assets/images/yoast-seo-05.png)

Để thiết lập tiêu đề và mô tả, bạn nhấp vào Edit snippet và điền mô tả, tiêu đề phù hợp với trang hiện tại mà tối ưu tốt hơn.

Nếu bạn muốn plugin tự phân tích khả năng SEO cho từ khóa trong bài, hãy nhập từ khóa cần phân tích vào phần Focus keyword để nó tiến hành phân tích.

### Tối ưu SEO cho taxonomy (tag, category,…)

Giống như các trang Post và Page, khi tiến hành sửa một Category hoặc Tag bạn sẽ thấy phần nhập thông tin tối ưu SEO để bạn tối ưu lại tiêu đề, mô tả hoặc tùy chỉnh các thẻ meta data.

## Kết luận

Bạn vừa xem xong bài viết hướng dẫn cài đặt và cấu hình plugin WordPress SEO by Yoast hoàn chỉnh nhất, có cả video và hình ảnh cho bạn tham khảo. Nhưng có một điều quan trọng ở đây là cho dù plugin có tốt tới đâu, nếu như bạn là người quản lý và viết nội dung mà bạn không có chút kiến thức nào về SEO thì coi như mọi cố gắng cũng trở nên vô ích.

Có những chỗ bạn không nhất thiết là phải cài đặt theo Sáu hướng dẫn, nhưng đây là những bước cài đặt hoàn thiện nhất và được nhiều người cấu hình giống vậy, họ đã làm và thành công, còn bạn thì sao bạn có nên cấu hình theo như thế này hay không? Hãy cùng gửi bình luận bên dưới để thảo luận cùng mọi người bạn nhé.

Nguồn: Thạch Phạm Blog
