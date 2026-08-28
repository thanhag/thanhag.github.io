---
published: true
title: Từ Staticman sang giscus - làm lại hệ thống bình luận cho blog Jekyll
date: '2026-08-28'
categories:
  - thiet-ke-web
  - thu-thuat-chung
tags:
  - blog
  - Jekyll
  - giscus
  - Staticman
  - Comments
  - github-discussions
header:
  teaser: >-
    /assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com01.jpg
  overlay_image: >-
    /assets/images/2024/2024-01-08-them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman-sofsog.com01.jpg
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)"
excerpt: >-
  Hai năm trước mình dựng hệ thống bình luận bằng **Staticman** trên một máy chủ
  riêng. Giờ nó chết hẳn. Bài này kể lại vì sao nó chết, và cách làm lại bằng
  **giscus** trong khoảng 15 phút mà không cần nuôi server nào cả.
toc: true
breadcrumbs: true
permalink: /thiet-ke-web/tu-staticman-sang-giscus-lam-lai-he-thong-binh-luan-blog-Jekyll
---

Đầu năm 2024 mình có viết bài [Thêm hệ thống bình luận vào blog Jekyll bằng Staticman](/thiet-ke-web/them-he-thong-binh-luan-vao-blog-Jekyll-bang-Staticman). Nó chạy được, mình khá tự hào, và rồi... nó chết.

Bài này là phần kết của câu chuyện đó: **vì sao Staticman chết**, những cái bẫy mà lúc dựng mình không nhìn ra, và cách làm lại hệ thống bình luận bằng **giscus** — lần này không phải nuôi máy chủ nào cả.

Nếu bạn đang định dựng Staticman theo bài cũ của mình, mình khuyên bạn đọc hết bài này trước đã.

## Chuyện gì đã xảy ra với Staticman

Kiến trúc của Staticman rất hay trên giấy: người đọc gửi bình luận, một API do bạn tự chạy nhận lấy, nó dùng token GitHub tạo `pull request` chứa file `.yml`, bạn duyệt, và bình luận trở thành file tĩnh nằm ngay trong repo blog. Không cần cơ sở dữ liệu, không phụ thuộc dịch vụ bên thứ ba, dữ liệu hoàn toàn của mình.

Cái giá của nó là **bạn phải nuôi một máy chủ chạy 24/7**. Và đó chính là chỗ mọi thứ đổ vỡ.

### Máy chủ tắt là hệ thống chết

Mình chạy Staticman trên một con **Windows Server 2012** sẵn có, trỏ tên miền `staticman.sofsog.com` qua Cloudflare. Đến một lúc mình không dùng con máy chủ đó nữa và tắt nó đi. Bản ghi DNS vẫn còn trên Cloudflare, tên miền vẫn phân giải ra IP bình thường, nhưng phía sau không còn gì cả:

```bash
curl -sI -m 10 https://staticman.sofsog.com/
# không trả về gì, timeout
```

Khung bình luận trên blog vẫn hiện ra như thường. Người đọc vẫn gõ được, vẫn bấm gửi được. Chỉ là bình luận của họ bay vào hư vô. **Lỗi kiểu này không ai báo cho bạn biết** — mình chỉ phát hiện khi ngồi kiểm tra lại toàn bộ blog.

### Bản dự phòng miễn phí cũng không cứu được

Trước đó mình có dựng sẵn một bản Staticman thứ hai trên **Render** gói miễn phí, kiểu để dự phòng. Hôm rồi mình thử gọi lại nó:

```bash
curl -s -o /dev/null -w "status=%{http_code} time=%{time_total}\n" \
     -m 240 https://staticman-ek71.onrender.com/
# status=000 time=240.013528
```

Kết nối TCP và TLS đều thành công, request gửi đi được, nhưng **240 giây không nhận về một byte nào**. Để chắc chắn không phải lỗi mạng nhà mình, thử luôn một tên miền Render không hề tồn tại:

```bash
curl -sI -m 20 https://khong-ton-tai-abc123xyz.onrender.com/
# HTTP/1.1 404 Not Found
# x-render-routing: no-server
```

Tên miền không tồn tại thì trả `404` ngay lập tức. Nghĩa là dịch vụ của mình **vẫn còn trong tài khoản Render**, Render vẫn định tuyến tới nó, nhưng cái instance đó không bao giờ dậy nữa.

Đây là bản chất của mọi gói hosting miễn phí: máy chủ ngủ sau một thời gian không có ai truy cập. Kể cả khi nó còn sống, người đọc bấm "Gửi bình luận" sẽ phải chờ gần một phút để máy chủ thức dậy, và thường là timeout trước khi kịp.

### Cái bẫy khoá RSA

Đây là cái mình muốn cảnh báo nhất, vì nó không hề hiển nhiên.

Trong `staticman.yml`, khoá bí mật của reCaptcha được lưu ở dạng đã mã hoá:

```yaml
reCaptcha:
  enabled: true
  siteKey: "6Lfgx2oUAAAAAAZJmldPnrBPme8OwqgyedPSuIfE"
  secret: "i1fL9gAbWPC0fItzKJUfmuGb9arCVuV6+hQukBEoz7876Bav8d0br..."
```

Chuỗi `secret` đó được mã hoá bằng **`rsaPrivateKey` của đúng cái instance Staticman đã tạo ra nó**. Đổi sang một instance khác, dù là máy chủ mới, VPS mới, Render hay Fly.io, thì instance mới **không giải mã nổi chuỗi này**, và mọi bình luận gửi lên đều bị từ chối.

Nghĩa là khi máy chủ cũ chết mà bạn không còn giữ `config.production.json`, bạn mất luôn khả năng khôi phục cấu hình. Muốn chuyển nhà thì phải mã hoá lại secret gốc qua endpoint `/v2/encrypt/` của instance mới, hoặc tắt hẳn reCaptcha đi.

Cộng thêm một chuyện nữa: GitHub token dạng `classic` mà Staticman dùng, dù bạn đặt `No expiration`, vẫn có thể bị GitHub thu hồi khi lâu không hoạt động. Đến lúc khôi phục là phải làm lại từ `Bước 1` của bài cũ.

### Và 76 bình luận rác

Phần này thì đúng ra lại là tin tốt.

Mình để `moderation: true`, nên mỗi bình luận gửi lên sẽ nằm chờ trong một nhánh riêng dạng `staticman_<uuid>` cho tới khi mình duyệt. Lúc dọn dẹp, repo của mình còn **65 nhánh như vậy với 76 bình luận chưa duyệt**. Đếm theo tên người gửi:

```
10  ppu-prof_Et
 9  Thành          <- mình tự test
 4  ppu-prof_RoG
 4  Trealdlig
 4  Ejeje
 ...
```

Gần như toàn bộ là spam SEO tiếng Nga (một tên miền quảng cáo dịch vụ cách nhiệt xuất hiện 14 lần), xen lẫn spam casino. Trừ các bình luận test của chính mình ra thì **số bình luận thật của người đọc đếm chưa hết một bàn tay**.

Con số này nói lên hai điều. Một là chế độ kiểm duyệt của Staticman hoạt động tốt, không có rác nào lọt lên blog. Hai là mình đã nuôi một máy chủ 24/7 suốt hai năm để phục vụ vài bình luận thật mỗi năm. **Không đáng.**

## giscus khác Staticman ở chỗ nào

**giscus** lưu bình luận vào **GitHub Discussions** của chính repo blog. Mỗi bài viết tương ứng một discussion, khung bình luận nhúng vào trang qua một `iframe`.

| | Staticman | giscus |
|---|---|---|
| Máy chủ phải nuôi | Có, chạy 24/7 | Không |
| Nơi lưu bình luận | File `.yml` trong repo | GitHub Discussions |
| Người đọc cần tài khoản | Không | **Có, phải có GitHub** |
| Kiểm duyệt | Qua pull request | Ẩn/xoá trực tiếp trên GitHub |
| Chống spam | reCaptcha, tự cấu hình | GitHub lo |
| Build lại blog mỗi bình luận | Có | Không |
| Thời gian dựng | Vài buổi tối | Khoảng 15 phút |

Điểm đánh đổi lớn nhất nằm ở dòng in đậm, mình sẽ nói kỹ ở cuối bài.

Một điểm cộng ít người để ý: với Staticman, **mỗi bình luận mới là một commit**, và mỗi commit làm GitHub Pages build lại toàn bộ blog. Bài nào đông bình luận thì lịch sử commit của repo loãng hẳn. giscus không đụng gì tới repo cả.

## Điều kiện cần trước khi bắt đầu

Ba thứ, thiếu một là không chạy:

- **Repo phải là public.** giscus không hoạt động với repo riêng tư.
- **Repo phải bật Discussions.**
- **Phải cài GitHub App giscus** cho repo đó.

Nếu blog của bạn dùng theme **Minimal Mistakes** như mình thì không cần đụng gì tới code của theme, nó đã hỗ trợ sẵn giscus, chỉ cần khai báo trong `_config.yml`.

## Bước 1: Bật Discussions cho repo

Vào repo blog trên GitHub, chọn `Settings`, kéo xuống mục `Features`, tick vào ô **`Discussions`**.

![Hình bật Discussions cho repo trên GitHub sofsog.com](/assets/images/2026/2026-08-28-tu-staticman-sang-giscus-sofsog.com01.png)

Xong bước này, repo của bạn sẽ có thêm tab `Discussions` ở thanh trên cùng, kèm sáu nhóm mặc định: `Announcements`, `General`, `Ideas`, `Polls`, `Q&A`, `Show and tell`.

Mình dùng nhóm **`Announcements`** cho bình luận, vì nhóm này chỉ chủ repo mới tạo được discussion mới. Đúng như ta muốn, vì discussion sẽ do giscus tự tạo chứ không phải ai muốn tạo cũng được.

## Bước 2: Cài GitHub App giscus

Truy cập [github.com/apps/giscus](https://github.com/apps/giscus), bấm `Install`, chọn **`Only select repositories`** và chỉ chọn đúng repo blog.

![Hình cài GitHub App giscus chỉ cho một repo sofsog.com](/assets/images/2026/2026-08-28-tu-staticman-sang-giscus-sofsog.com02.png)

Đừng chọn `All repositories`. Không có lý do gì để cấp quyền ghi vào toàn bộ repo của bạn cho một ứng dụng chỉ phục vụ một cái blog.

## Bước 3: Lấy `repo_id` và `category_id`

giscus không nhận tên repo dạng chữ, nó cần **ID nội bộ** của GitHub. Có hai cách lấy.

**Cách phổ thông:** vào trang cấu hình chính chủ tại [giscus.app](https://giscus.app/vi), điền tên repo, chọn nhóm `Announcements`, rồi kéo xuống dưới cùng. Trang sẽ sinh ra sẵn đoạn mã nhúng có chứa hai ID đó.

**Cách nhanh hơn nếu bạn quen dòng lệnh**, chỉ hai câu lệnh, không cần mở trình duyệt.

Lấy `repo_id` (chính là `node_id` của repo, API công khai, không cần token):

```bash
curl -s https://api.github.com/repos/thanhag/thanhag.github.io | grep '"node_id"' | head -1
```

```
"node_id": "R_kgDOK84I7w",
```

Lấy `category_id`:

```bash
curl -s "https://giscus.app/api/discussions/categories?repo=thanhag/thanhag.github.io"
```

Kết quả trả về:

```json
{"repositoryId":"R_kgDOK84I7w","categories":[
  {"id":"DIC_kwDOK84I784DEXEi","name":"Announcements"},
  {"id":"DIC_kwDOK84I784DEXEj","name":"General"}
]}
```

Nhớ thay `thanhag/thanhag.github.io` bằng repo của bạn. Một mẹo nhỏ: nếu `categories` trả về mảng rỗng thì nghĩa là bạn **chưa bật Discussions** ở Bước 1.

## Bước 4: Khai báo trong `_config.yml`

Trong bài Staticman cũ, khối cấu hình của mình là:

```yaml
comments:
  provider  : "staticman_v2"
  staticman:
    branch    : "master"
    endpoint  : https://staticman.sofsog.com/v2/entry/
```

Giờ thay bằng:

```yaml
repository  : "thanhag/thanhag.github.io"

comments:
  provider  : "giscus"
  giscus:
    repo_id           : "R_kgDOK84I7w"
    category_name     : "Announcements"
    category_id       : "DIC_kwDOK84I784DEXEi"
    discussion_term   : "pathname"
    strict            : "1"
    reactions_enabled : "1"
    input_position    : "bottom"
    emit_metadata     : "0"
    theme             : "light"
    lang              : "vi"
    lazy              : true
```

Lưu ý dòng `repository` ở trên: Minimal Mistakes lấy đúng giá trị này làm `data-repo` cho giscus, nên nó phải có và phải đúng.

Vài tham số đáng giải thích:

- **`discussion_term: "pathname"`** là cách giscus ghép một trang với một discussion. Dùng `pathname` (đường dẫn bài viết) là hợp lý nhất. Đừng dùng `title`, vì hễ bạn sửa tiêu đề bài là mất hết bình luận cũ của bài đó.
- **`strict: "1"`** bắt giscus khớp chính xác thay vì tìm discussion nào có tiêu đề *chứa* đường dẫn. Không bật cái này thì bài `/vps` và bài `/vps-nang-cao` có thể bị gán nhầm vào chung một discussion.
- **`lang: "vi"`** cho giao diện khung bình luận bằng tiếng Việt.
- **`lazy: true`** chỉ tải khung bình luận khi người đọc cuộn xuống tới. Nên bật, vì `iframe` của giscus khá nặng mà phần lớn người đọc không cuộn xuống tới cuối bài.
- **`theme`** nếu blog bạn có chế độ tối thì đổi thành `preferred_color_scheme` để khung bình luận đổi màu theo.

## Bước 5: Dọn tàn dư của Staticman

Chuyển xong thì mấy thứ này thành rác, dọn luôn cho gọn.

**Khối `reCaptcha` trong `_config.yml`.** giscus không dùng tới, mà cái `secret` trong đó lại đang được mã hoá bằng khoá của instance đã chết, giữ cũng vô nghĩa. Xoá.

**File `staticman.yml` ở gốc repo.** Không còn được đọc tới nữa. Xoá được, nhưng mình giữ lại để đối chiếu khi viết bài này.

**Các nhánh `staticman_*`.** Của mình là 65 nhánh. Trước khi xoá, nên dump nội dung ra một file để phòng xa, vì trong đó có thể lẫn bình luận thật chưa kịp duyệt:

```bash
for b in $(git branch -r | grep staticman_ | sed 's|origin/||'); do
  base=$(git merge-base master "origin/$b")
  for f in $(git diff --name-only --diff-filter=AM "$base" "origin/$b" -- _data/comments/); do
    echo "### $f (nhanh $b)" >> binh-luan-chua-duyet.md
    git show "origin/$b:$f" >> binh-luan-chua-duyet.md
  done
done
```

Xem lại file vừa tạo, thấy không tiếc gì thì xoá hàng loạt:

```bash
git push origin --delete $(git branch -r | grep staticman_ | sed 's|  origin/||' | tr '\n' ' ')
```

**Thư mục `_data/comments/`** chứa các bình luận đã duyệt trước đây. giscus không đọc tới nên chúng sẽ không còn hiển thị, nhưng file vẫn nằm nguyên trong repo. Mình giữ lại, không mất gì cả.

## Kiểm tra xem đã chạy chưa

`Commit` và `push`, chờ GitHub Pages build khoảng một hai phút, rồi kiểm tra bằng dòng lệnh xem đoạn mã giscus đã được sinh ra đúng chưa:

```bash
curl -s https://sofsog.com/bai-viet-nao-do/ | grep -o "data-[a-z-]*', '[^']*'"
```

Kết quả phải ra đầy đủ như thế này:

```
data-repo = thanhag/thanhag.github.io
data-repo-id = R_kgDOK84I7w
data-category = Announcements
data-category-id = DIC_kwDOK84I784DEXEi
data-mapping = pathname
data-strict = 1
```

Nếu `data-repo-id` hoặc `data-category-id` trống thì xem lại `_config.yml`.

![Hình khung bình luận giscus tiếng Việt trên blog sofsog.com](/assets/images/2026/2026-08-28-tu-staticman-sang-giscus-sofsog.com03.png)

Cuối cùng, **tự vào blog bình luận thử một câu**. Đây là bước duy nhất xác nhận được GitHub App ở Bước 2 đã cài đúng, từ bên ngoài không có cách nào kiểm tra chuyện đó. Bình luận gửi thành công thì vào tab `Discussions` của repo, bạn sẽ thấy giscus đã tự tạo một discussion mới mang tên đường dẫn bài viết.

![Hình discussion do giscus tự tạo trên GitHub sofsog.com](/assets/images/2026/2026-08-28-tu-staticman-sang-giscus-sofsog.com04.png)

## Những gì giscus không làm được

Đổi lại sự nhẹ nhàng, bạn mất mấy thứ. Nói thẳng để bạn cân nhắc trước khi làm theo:

**Người bình luận bắt buộc phải có tài khoản GitHub.** Đây là hạn chế lớn nhất và không có cách nào lách. Nếu blog bạn viết cho dân lập trình thì gần như không ảnh hưởng. Nhưng nếu độc giả của bạn là người dùng phổ thông thì đây là một bức tường: rất ít người chịu đăng ký GitHub chỉ để gõ một câu "cảm ơn bạn". Trường hợp đó thì Staticman, hoặc Disqus, Cusdis, vẫn hợp lý hơn.

**Bình luận cũ không tự chuyển sang được.** Chúng nằm dưới dạng file `.yml`, còn giscus đọc từ GitHub Discussions. Muốn giữ thì phải đăng lại thủ công, và tên người bình luận sẽ thành tên bạn chứ không phải người viết gốc. Của mình thì 8/9 bình luận cũ là tin nhắn test của chính mình nên mình bỏ luôn.

**Repo phải public.** Blog GitHub Pages cá nhân thì thường public sẵn, nhưng nếu bạn để repo riêng tư thì phải chọn: hoặc mở public, hoặc dùng giải pháp khác.

**Phụ thuộc hoàn toàn vào GitHub.** GitHub sập thì mất khung bình luận. Đổi lại, xác suất GitHub sập thấp hơn nhiều so với xác suất bạn quên gia hạn VPS.

## Vậy có nên chuyển không

Kinh nghiệm của mình sau hai năm, gói lại thế này:

- Blog kỹ thuật, độc giả là dân IT, muốn xong trong một buổi tối và không phải bận tâm gì nữa thì chọn **giscus**.
- Muốn ai cũng bình luận được không cần tài khoản, và bạn thực sự có sẵn một máy chủ đang chạy cho việc khác, thì **Staticman** vẫn tốt. Nhưng hãy nhớ giữ `config.production.json` ở chỗ an toàn, và đặt lịch kiểm tra định kỳ xem cái endpoint còn sống không.

Cá nhân mình, thứ khiến mình dứt khoát chuyển không phải vì Staticman dở. Nó là một ý tưởng đẹp. Vấn đề là **nó chết âm thầm**: khung bình luận vẫn hiện, người đọc vẫn gõ, vẫn bấm gửi, và không ai, kể cả mình, biết là dữ liệu đang rơi vào hư không. Không biết bao nhiêu bình luận thật đã mất theo cách đó trước khi mình phát hiện.

Một hệ thống hỏng mà báo lỗi thì còn sửa được. Một hệ thống hỏng mà vẫn trông như đang chạy thì tệ hơn nhiều.

Chúc các bạn thành công.

## Link tham khảo

[https://giscus.app/vi](https://giscus.app/vi)

[https://github.com/giscus/giscus](https://github.com/giscus/giscus)

[https://mmistakes.github.io/minimal-mistakes/docs/configuration/#comments](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#comments)

[https://docs.github.com/en/discussions](https://docs.github.com/en/discussions)
