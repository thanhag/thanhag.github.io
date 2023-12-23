---
title: "Thiết lập SEO by Yoast linh hoạt hơn với biến dữ liệu"
date: "2016-09-19"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "plugin"
  - "wordpress"
  - "wordpress-co-ban"
  - "yoast-seo"
header:
  
  teaser: /assets/images/Yoast-Logo-Icon.png
toc: true
breadcrumbs: true
---

Khi thiết lập plugin SEO by Yoast, chắc bạn cũng có biết là cấu trúc tiêu đề và description của các post type và taxonomy sẽ được hiển thị dựa vào thiết lập các biến dữ liệu đặc biệt mà plugin này cung cấp sẵn. Ví dụ nếu ở phần Title của Post bạn thiết lập là thế này:

![yoast-variables](/assets/images/yoast-variables.jpg)

Thì điều này có nghĩa là Post của bạn sẽ được hiển thị thẻ <title> với cấu trúc “_Tên của post – Tên website_” ở mặc định. Vậy chúng ta có thể gọi, %%title%% là biến dữ liệu để in tiêu đề của post type và biến`%%sitename%%` để in tên của website. Các biến này đều được nằm trong giữa 4 ký tự phần trăm (%).

Lưu ý rằng, title chỉ hiển thị theo cấu trúc này nếu bạn không đánh dấu vào mục “**Force rewrite titles**” ở **SEO-> Titles & Metas -> General**. Còn nếu đánh dấu vào, nó sẽ hiển thị những gì mà bạn đã nhập trong phần thiết lập SEO Title trong mỗi post type hoặc taxonomy.

Vậy thì ngoài hai biến ví dụ ở trên, Yoast còn có biến nào nữa để giúp chúng ta có thể hiển thị title và description linh hoạt hơn? Rất nhiều nhé, mà ở bài này mình sẽ liệt kê ra toàn bộ các biến dữ liệu mà hiện tại plugin WordPress SEO by Yoast đang hỗ trợ.

### Các biến dữ liệu cơ bản

Các biến dữ liệu cơ bản của plugin WordPress SEO by Yoast là những biến dễ sử dụng và cũng thường xuyên được sử dụng nhất.

<table><tbody><tr><th>Tên biến</th><td><strong>Giải thích</strong></td></tr><tr><th>%%date%%</th><td>Hiển thị ngày tháng đăng post/page.</td></tr><tr><th>%%title%%</th><td>Hiển thị tiêu đề của post/page.</td></tr><tr><th>%%sitename%%</th><td>Hiển thị tên website.</td></tr><tr><th>%%sitedesc%%</th><td>Hiển thị mô tả của website thiết lập trong Settings -&gt; General.</td></tr><tr><th>%%excerpt%%</th><td>Hiển thị excerpt của post/page.</td></tr><tr><th>%%excerpt_only%%</th><td>Hiển thị excerpt của post/page nhưng không tự tạo ra nếu không có.</td></tr><tr><th>%%tag%%</th><td>Hiển thị tên (các) tag của post.</td></tr><tr><th>%%category%%</th><td>Hiển thị tên (các) category của post.</td></tr><tr><th>%%category_description%%</th><td>Hiển thị mô tả của category.</td></tr><tr><th>%%tag_description%%</th><td>Hiển thị mô tả của tag.</td></tr><tr><th>%%term_description%%</th><td>Hiển thị mô tả của một term ((Term ở đây bạn có thể hiểu là một đối tượng trong một taxonomy. Ví dụ trong category bạn có category tên A, và A đó chính là term của category)) trong một taxonomy mà post đang sử dụng.</td></tr><tr><th>%%term_title%%</th><td>Hiển thị tiêu đề của term mà post đang sử dụng.</td></tr><tr><th>%%searchphrase%%</th><td>Hiển thị từ khóa tìm kiếm mà người dùng đang tìm.</td></tr><tr><th>%%sep%%</th><td>Hiển thị ký tự phân cách mà bạn có thể thiết lập trong SEO -&gt; Titles &amp; Metas -&gt; General.</td></tr></tbody></table>

### Các biến dữ liệu nâng cao

Nếu các biến ở trên không đủ nhu cầu của bạn thì bạn có thể sử dụng các biến dưới đây. Đặc biệt là nếu bạn làm việc với custom taxonomy và custom post type sẽ thấy nó có hiệu quả hơn.

<table><tbody><tr><th><strong>Tên biến</strong></th><td><strong>Giải thích</strong></td></tr><tr><th>%%pt_single%%</th><td>Hiển thị Single Label của post type</td></tr><tr><th>%%pt_plural%%</th><td>Hiển thị Singular Label của post type</td></tr><tr><th>%%modified%%</th><td>Hiển thị thời gian cập nhật lần cuối cùng của post type</td></tr><tr><th>%%id%%</th><td>Hiển thị ID của post hiện tại</td></tr><tr><th>%%name%%</th><td>Hiển thị tên tác giả của post</td></tr><tr><th>%%userid%%</th><td>Hiển thị ID tác giả giả của post</td></tr><tr><th>%%currenttime%%</th><td>Hiển thị giờ hiện tại</td></tr><tr><th>%%currentdate%%</th><td>Hiển thị ngày tháng năm hiện tại</td></tr><tr><th>%%currentday%%</th><td>Hiển thị ngày hôm nay</td></tr><tr><th>%%currentmonth%%</th><td>Hiển thị tháng hiện tại</td></tr><tr><th>%%currentyear%%</th><td>Hiển thị năm hiện tại</td></tr><tr><th>%%page%%</th><td>Hiển thị số trang hiện tại (kiểu Trang 2/10)</td></tr><tr><th>%%pagetotal%%</th><td>Hiển thị tổng số trang</td></tr><tr><th>%%pagenumber%%</th><td>Hiển thị số trang hiện tại</td></tr><tr><th>%%caption%%</th><td>Hiển thị caption của tập tin media đính kèm</td></tr><tr><th>%%focuskw%%</th><td>Hiển thị từ khóa đang focus vào bài</td></tr><tr><th>%%term404%%</th><td>Hiển thị slug của trang 404</td></tr><tr><th>%%cf_&lt;custom-field-name&gt;%%</th><td>Hiển thị giá trị của một custom post field đang sử dụng trong post. Ví dụ: %%cf_tinhthanh%%</td></tr><tr><th>%%ct_&lt;custom-tax-name&gt;%%</th><td>Hiển thị term của custom taxonomy.</td></tr><tr><th>%%ct_desc_&lt;custom-tax-name&gt;%%</th><td>Hiển thị description của custom taxonomy.</td></tr></tbody></table>

Thật tuyệt vời phải không nào. Bây giờ bạn có thể áp dụng các giá trị này vào việc tối ưu SEO cho website với plugin WordPress SEO by Yoast cho phù hợp nhất với nhu cầu của bạn nhé.

Nguồn: Thạch phạm Blog
