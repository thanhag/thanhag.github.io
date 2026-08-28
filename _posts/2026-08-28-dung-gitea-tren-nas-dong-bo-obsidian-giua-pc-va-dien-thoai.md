---
published: true
title: Dựng Gitea trên NAS - "GitHub riêng" để đồng bộ Obsidian giữa PC và điện thoại
date: '2026-08-28'
categories:
  - server
  - thu-thuat-chung
tags:
  - Gitea
  - NAS
  - Synology
  - Obsidian
  - Tailscale
  - Git
header:
  teaser: >-
    /assets/images/2026/2026-08-28-dung-gitea-tren-nas-sofsog.com01.png
  overlay_image: >-
    /assets/images/2026/2026-08-28-dung-gitea-tren-nas-sofsog.com01.png
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)"
excerpt: >-
  Vault Obsidian của mình có **986 ghi chú** và mình sửa chúng trên ba thiết bị.
  Synology Drive đẻ file conflict liên tục nên mình thay nó bằng **Gitea** chạy
  ngay trên NAS, đi qua **Tailscale**, mirror ngược lên GitHub và GitLab.
toc: true
breadcrumbs: true
permalink: /server/dung-gitea-tren-nas-dong-bo-obsidian-giua-pc-va-dien-thoai
---

Vault Obsidian của mình có 986 ghi chú và mình sửa chúng trên ba thiết bị: PC nhà, PC công ty, điện thoại. Suốt một thời gian dài mình để Synology Drive lo việc đồng bộ, và suốt thời gian đó mình phải đi dọn file conflict.

Bài này kể lại cách mình thay Synology Drive bằng một máy chủ Git riêng — **Gitea** — chạy ngay trên con NAS ở nhà, truy cập qua **Tailscale** nên không phải mở port nào ra Internet, và tự đẩy bản sao lên GitHub với GitLab để phòng NAS chết.

## Vì sao Synology Drive không hợp với Obsidian

Synology Drive đồng bộ ở **mức file**. Khi nó thấy cùng một file có hai bản khác nhau ở hai máy, nó không hợp nhất — nó giữ cả hai và đặt tên bản thứ hai thành *conflict copy*. Với ảnh hay file Word thì cách xử lý đó hợp lý. Với vault Obsidian thì không.

Lý do là cách mình dùng Obsidian: mở note trên điện thoại lúc đang đi, về nhà mở lại đúng note đó trên PC, hôm sau sửa tiếp ở công ty. Ba thiết bị chạm vào cùng một file `.md` trong vài giờ là chuyện bình thường. Mỗi lần như vậy Synology Drive lại đẻ thêm một bản sao, và mình phải tự mở hai file ra so từng dòng để biết giữ bản nào.

Git thì hợp nhất ở **mức dòng**. Hai thiết bị sửa hai đoạn khác nhau trong cùng một ghi chú, git gộp lại thành một file duy nhất, không hỏi han gì cả. Chỉ khi hai bên sửa đúng cùng một dòng nó mới báo conflict — và lúc đó nó đánh dấu ngay trong file bằng `<<<<<<<`, `=======`, `>>>>>>>` để mình sửa tại chỗ, thay vì bắt mình đi tìm file thứ hai nằm ở đâu.

Đây là lý do duy nhất mình chuyển. Không phải vì Synology Drive chậm hay tốn tài nguyên — nó chạy tốt. Nó chỉ được thiết kế cho loại dữ liệu khác.

## Kiến trúc mình đang chạy

```text
PC nhà     ──┐
PC công ty ──┼──⇄── Gitea (NAS, qua Tailscale) ──→ GitHub (mirror)
Điện thoại ──┘      http://100.107.72.33:8418   └─→ GitLab (mirror)
```

Ba điều quan trọng trong sơ đồ này:

**Gitea là trung tâm duy nhất.** Mọi thiết bị chỉ pull và push với Gitea. GitHub và GitLab là bản sao một chiều, không thiết bị nào được push thẳng lên đó. Nếu bạn lỡ push thẳng lên GitHub, thay đổi đó sẽ không bao giờ quay ngược về Gitea, và lần mirror kế tiếp sẽ đè mất nó.

**Địa chỉ `100.107.72.33` là IP Tailscale, không phải IP mạng nhà.** NAS không mở một port nào ra Internet. Thiết bị nào nằm trong tailnet thì thấy NAS, thiết bị khác thì không thấy gì cả — kể cả khi mình ngồi ở quán cà phê hay ở công ty.

**Mỗi thiết bị chỉ được có một công cụ đồng bộ.** PC dùng plugin Git trong Obsidian, điện thoại dùng app GitSync. Bật hai cái cùng lúc trên một máy là hỏng.

Con NAS chạy Gitea của mình là một chiếc HPE ProLiant MicroServer Gen10, CPU AMD Opteron X3421 bốn nhân, 3,4 GiB RAM, cài DSM 7.2.2-72806. Phần cứng khiêm tốn. Gitea vẫn chạy thoải mái trên đó — tại thời điểm mình viết bài này tiến trình đã chạy liên tục 20 ngày 23 giờ mà chưa phải khởi động lại lần nào.

## Điều kiện cần trước khi bắt đầu

Gói Gitea của SynoCommunity yêu cầu **DSM từ 7.1-42661 trở lên** và tự kéo theo gói `git` phiên bản 2 trở lên. File `INFO` của gói liệt kê 22 nền tảng phần cứng được hỗ trợ, từ `avoton`, `bromolow` cũ tới `epyc7002`, `v1000` — NAS Synology đời gần đây gần như chắc chắn nằm trong danh sách.

Ngoài ra bạn cần Tailscale cài trên NAS và trên mọi thiết bị sẽ đồng bộ, Git cài sẵn trên PC, và một tài khoản GitHub hoặc GitLab nếu muốn có bản sao ngoài nhà.

Nếu chưa dùng Tailscale bao giờ thì cứ cài trước, đăng nhập cùng một tài khoản trên tất cả các máy là xong — không cần cấu hình gì thêm cho bài này.

## Bước 1: Cài Gitea từ Package Center

Gitea không có trong kho chính thức của Synology, phải thêm nguồn của SynoCommunity trước.

Vào **Package Center → Settings → Package Sources → Add**, đặt tên tùy ý và điền địa chỉ:

```text
https://packages.synocommunity.com/
```

Vẫn trong Settings, chuyển sang tab **General** và đổi **Trust Level** thành *Any publisher*. Không đổi mục này thì DSM sẽ từ chối cài, vì gói của SynoCommunity không có chữ ký của Synology.

Quay ra tab **Community**, tìm **Gitea** và bấm cài. Gói do `wkobiela` đóng gói, và tại thời điểm mình viết bài thì gói này đã có 3.611 lượt tải.

![Hình gói Gitea của SynoCommunity trong Package Center của DSM sofsog.com](/assets/images/2026/2026-08-28-dung-gitea-tren-nas-sofsog.com02.png)

Ảnh trên chụp đúng máy mình, và nó cho thấy luôn một chuyện đáng nói: bản mình đang chạy là `1.25.0-26` trong khi bản mới nhất đã là `1.27.2-30`, kèm dòng ghi chú *"Security update for CVE-2026-60004"*. Gói này cập nhật khá đều, và bạn nên bấm Update mỗi khi thấy chữ **Update Available** thay vì để dồn như mình.

Trong lúc cài, DSM sẽ hỏi bạn chọn một thư mục chia sẻ để chứa dữ liệu. Mình chọn `gitea-share`, và sau khi cài xong thư mục đó có hai thư mục con:

```text
/volume1/gitea-share/gitea-repositories/   ← repo nằm ở đây
/volume1/gitea-share/lfs/                  ← cho file lớn, mình không dùng
```

Phần còn lại — cơ sở dữ liệu, log, avatar — nằm ở `/volume1/@appdata/gitea/`. Đáng chú ý là gói này dùng **SQLite** chứ không cần MariaDB hay PostgreSQL. Nguyên cơ sở dữ liệu của mình sau 642 commit chỉ là một file `gitea.db` nặng 2,6 MB. Với vault cá nhân thì SQLite thừa sức, và nó tiết kiệm được cả một gói cơ sở dữ liệu chạy nền trên máy chỉ có 3,4 GiB RAM.

Cài xong, Gitea nghe ở **cổng 8418**. Mở trình duyệt vào `http://<IP-NAS>:8418`, bạn sẽ thấy màn hình cài đặt lần đầu. Cứ để nguyên các giá trị mặc định, chỉ tạo tài khoản quản trị. Tài khoản đầu tiên tạo ra chính là tài khoản admin.

![Hình trang chủ Gitea chạy trên NAS truy cập qua địa chỉ Tailscale sofsog.com](/assets/images/2026/2026-08-28-dung-gitea-tren-nas-sofsog.com01.png)

Thấy tách trà này là xong phần nặng nhất. Để ý thanh địa chỉ: Chrome báo **Not secure** vì đây là `http://` — mình sẽ nói về chuyện đó ở cuối bài.

## Bước 2: Tạo repo và token cho vault

Đăng nhập Gitea, bấm **+ → New Repository**, đặt tên trùng tên thư mục vault cho dễ nhớ. Repo của mình tên `Ghi-chu-markdown`, để chế độ **Private**. Không tick "Initialize repository" — vault của bạn đã có sẵn nội dung, để repo rỗng thì bước đẩy lên đơn giản hơn.

Tiếp theo tạo token. Gitea không cho dùng mật khẩu tài khoản để clone qua HTTP nữa, phải dùng token:

Bấm avatar → **Settings → Applications**, đặt một cái tên gợi nhớ gắn với máy sẽ dùng token đó, chọn quyền **repository: Read and Write**, rồi bấm tạo.

**Copy token ngay lúc đó.** Gitea chỉ hiện đúng một lần, đóng trang là mất, phải tạo cái khác.

Mỗi thiết bị một token riêng. Làm vậy khi mất điện thoại bạn chỉ cần thu hồi đúng token của nó mà không ảnh hưởng máy nào khác.

## Bước 3: Đẩy vault hiện có lên Gitea

Trước khi làm bước này, **tắt Synology Drive cho thư mục vault**. Cả FreeFileSync, GoodSync hay bất cứ công cụ đồng bộ file nào khác cũng vậy. Chúng sẽ chép đè thư mục ẩn `.git` giữa các máy và phá nát lịch sử — đây là bài học mình phải trả giá trước khi chốt lại kiến trúc hiện tại.

Mở terminal tại thư mục vault:

```bash
git init
git branch -M main
git remote add origin http://100.107.72.33:8418/thanh_gitea/Ghi-chu-markdown.git
```

Trước khi commit lần đầu, đặt danh tính. Thiếu bước này git sẽ từ chối commit:

```bash
git config user.name "thanh_gitea"
git config user.email "email-cua-ban@example.com"
```

Tạo file `.gitignore` trong thư mục vault. Đây là file của mình, và mỗi dòng trong đó đều là một nguyên nhân gây conflict mà mình đã gặp:

```gitignore
# Trạng thái giao diện Obsidian - thay đổi liên tục trên mỗi thiết bị, gây conflict
.obsidian/workspace.json
.obsidian/workspace-mobile.json

# Thùng rác của Obsidian
.trash/

# File rác hệ thống
Thumbs.db
.DS_Store
desktop.ini

# Database của FreeFileSync
*.ffs_db
```

Hai dòng đầu là quan trọng nhất. `workspace.json` ghi lại bạn đang mở tab nào, panel rộng bao nhiêu — nó đổi mỗi lần bạn bấm chuột. Không loại nó ra thì mỗi lần đồng bộ đều đụng độ, và nội dung đụng độ hoàn toàn vô nghĩa.

Đẩy lên:

```bash
git add -A
git commit -m "Initial commit"
git push -u origin main
```

Git sẽ hỏi tài khoản: điền tên đăng nhập Gitea, còn mật khẩu thì **dán token** chứ không phải mật khẩu thật.

Lần push đầu chậm. Vault của mình có 1.905 file, thư mục `.git` dưới máy chiếm 248 MB, và Gitea báo repo trên NAS nặng 351 MiB. Nếu bạn thấy dòng "compressing objects" đứng yên khá lâu thì đó là NAS đang nén lịch sử, cứ để nó chạy.

## Bước 4: Bật mirror sang GitHub và GitLab

NAS ở nhà mình. Nhà cháy thì vault cháy theo. Gitea có sẵn tính năng **push mirror** để tự đẩy bản sao lên nơi khác sau mỗi lần bạn push.

Tạo trước một repo rỗng và một access token trên GitHub (quyền `repo`), làm tương tự trên GitLab nếu muốn hai lớp.

Trong Gitea, vào repo vault → **Settings → Repository → Mirror Settings → Add Push Mirror**, điền URL repo đích, tên đăng nhập, dán token vào ô mật khẩu, và đặt chu kỳ đồng bộ.

![Hình mục Mirror Settings của Gitea với hai push mirror sang GitHub và GitLab sofsog.com](/assets/images/2026/2026-08-28-dung-gitea-tren-nas-sofsog.com03.png)

Mình đang chạy hai mirror song song, một sang `github.com` và một sang `gitlab.com`, chu kỳ 8 tiếng. Chọn hai nhà cung cấp khác nhau là có chủ ý — tài khoản bị khóa vì lý do gì đó thì vẫn còn đường lấy dữ liệu về.

Bạn để ý dòng thứ hai trong ảnh: nó có badge **Error** màu đỏ. Mình phát hiện ra đúng lúc chụp ảnh minh hoạ cho bài này. Mirror GitHub chạy lúc 14:43:37 thì bình thường, mirror GitLab chạy sau đó 55 giây thì hỏng, và trước khi mở trang này ra mình hoàn toàn không biết.

Đó chính là điều mình muốn bạn nhớ: **mirror hỏng không báo cho bạn**. Không có email, không có thông báo trên điện thoại. Chỗ duy nhất nói cho bạn biết là dòng chữ đỏ trong đúng trang này. Token GitHub và GitLab đều có hạn — của mình hết hạn khoảng tháng 7/2027 — và khi chúng hết hạn thì mọi thứ vẫn trông như đang chạy tốt. Đặt lịch mỗi tháng mở trang Mirror Settings ra liếc một cái, đừng tin là nó tự lo được.

## Bước 5: Cấu hình plugin Git trên PC

Trong Obsidian, cài plugin cộng đồng tên **Git**, rồi vào phần Automatic trong cài đặt của nó.

![Hình cấu hình plugin Git trong Obsidian với ba mốc thời gian tự động sofsog.com](/assets/images/2026/2026-08-28-dung-gitea-tren-nas-sofsog.com04.png)

Cấu hình mình đang dùng, đúng như trong ảnh:

```text
Split timers for automatic commit and sync: bật
Auto commit interval:  3 phút
Auto push interval:    3 phút
Auto pull interval:    5 phút
Pull on startup: bật
Pull before push: bật
Merge strategy: merge
Commit message: vault backup: {{date}}
```

Công tắc **Split timers for automatic commit and sync** ở trên cùng phải bật trước, nếu không plugin chỉ cho bạn đặt một mốc thời gian chung cho cả commit lẫn push.

Ba con số đầu là thứ đáng cân nhắc nhất. Commit quá dày thì lịch sử ngập rác, quá thưa thì lúc mở máy khác lại thiếu bài vừa gõ. Ba phút là con số mình chốt lại: đủ nhanh để chuyển máy là có ngay, đủ chậm để một lần ngồi gõ note không sinh ra năm commit.

**Pull before push** thì bắt buộc bật. Không bật thì mỗi lần hai máy cùng có thay đổi, push sẽ bị từ chối và bạn phải tự vào gỡ.

Con số commit của mình nói khá rõ về nhịp sử dụng thật: 207 commit trong tháng 5/2026, 101 trong tháng 6, 219 trong tháng 7. Tổng 642 commit tính tới ngày 25/08/2026. Đó là lịch sử phiên bản của từng ghi chú, tự động, không phải làm gì cả.

## Bước 6: Cấu hình GitSync trên điện thoại Android

Đây là phần nhiều bẫy nhất, và cũng là phần Synology Drive từng làm tốt hơn — trên điện thoại, git không hề trong suốt như đồng bộ file.

Cài **Tailscale**, **GitSync** và **Obsidian**. Bật Tailscale, rồi mở trình duyệt vào `http://100.107.72.33:8418` để chắc chắn điện thoại thấy được Gitea đã. Không thấy thì đừng làm tiếp, xử lý Tailscale trước.

Mở GitSync và **điền Author name với email trước khi làm bất cứ việc gì khác**. Thiếu hai trường này, GitSync vẫn chạy, vẫn báo sync xong, nhưng commit thất bại âm thầm — trong log chỉ có một dòng `empty name or email`. Mình mất kha khá thời gian cho đúng chỗ này.

Clone repo trong GitSync với **Shallow Depth = 1**, **Bare Clone = tắt**, chọn một thư mục trống hoàn toàn mới. Shallow depth 1 nghĩa là chỉ tải bản mới nhất, bỏ qua toàn bộ lịch sử. Với repo 351 MiB thì đây là khác biệt giữa vài giây và vài phút chờ trên mạng di động.

Bật auto-sync: **App Sync Settings → chọn Obsidian → cấp quyền Trợ năng**. Android sẽ hiện cảnh báo nghe khá đáng sợ về quyền này; đó là cảnh báo mặc định cho mọi app dùng Accessibility, cứ đồng ý.

Chống hệ điều hành giết app: bật **Autostart** và đặt chế độ pin **Không hạn chế** cho cả GitSync lẫn Tailscale, rồi ghim GitSync trong màn hình đa nhiệm.

Cuối cùng, mở Obsidian → **Open folder as vault** → chọn thư mục GitSync vừa clone → vào **Settings → Git** và bật **"Disable on this device"**. Tùy chọn này chỉ tắt plugin trên máy hiện tại, PC không bị ảnh hưởng. Không tắt thì plugin Git và GitSync sẽ giẫm chân nhau.

Thói quen hàng ngày trên điện thoại: bật Tailscale, mở Obsidian, **đợi vài giây cho GitSync pull xong rồi mới sửa**. Sửa xong thì **thoát hẳn app** để nó push. Đây chính là cái giá phải trả so với Synology Drive, và mình sẽ nói rõ hơn ở cuối bài.

## Kiểm tra xem đã chạy chưa

Sửa một note trên điện thoại, thoát hẳn app, rồi mở Gitea trên trình duyệt xem có commit mới không. Làm ngược lại: sửa trên PC, đợi ba phút, mở Obsidian trên điện thoại xem thay đổi đã về chưa.

Kiểm tra mirror bằng cách vào GitHub xem commit mới nhất có khớp với commit trên Gitea không. Khớp là toàn bộ chuỗi đã thông.

Trên NAS, nếu bạn bật SSH thì đếm nhanh được số commit:

```bash
/var/packages/git/target/bin/git \
  --git-dir=/volume1/gitea-share/gitea-repositories/<user>/<repo>.git \
  rev-list --count HEAD
```

Lệnh `git` trần không chạy được trên DSM vì nó không nằm trong `PATH` mặc định — phải gọi bằng đường dẫn đầy đủ tới gói.

## Những cái bẫy mình đã dẫm phải

**Lỗi "Filename too long" khi merge trên Windows.** Git trên Windows chặn đường dẫn dài quá 260 ký tự, mà ghi chú tiếng Việt có dấu thì tên file dài rất nhanh. Chạy một lần trong thư mục vault:

```bash
git config core.longpaths true
```

Phải chạy trên **từng máy Windows**, vì đây là cấu hình cục bộ, không đi theo repo. Mình đã bật trên PC nhà và vẫn quên mất mấy máy khác cho tới khi chúng báo lỗi.

**Điện thoại Xiaomi tự tắt quyền Trợ năng.** HyperOS thu hồi quyền Accessibility của app lâu ngày không mở. Tự dưng hết auto-sync mà Tailscale vẫn bình thường thì vào Cài đặt → Trợ năng bật lại cho GitSync.

**Branch báo "diverged".** Thấy chữ này đừng hoảng, nó không phải hỏng. Hai thiết bị cùng commit trong lúc chưa kịp đồng bộ là ra vậy. Bấm Pull trong Obsidian là git tự gộp.

**File kẹt không chịu commit trên GitSync.** Sửa thêm một ký tự vào ghi chú bất kỳ rồi sync lại. Vẫn kẹt thì mở log GitSync tìm hai chuỗi `empty name or email` và `index.lock` — gần như lần nào cũng là một trong hai.

## Những gì cách này không làm được

**Không có mã hóa HTTPS giữa thiết bị và Gitea.** URL là `http://`, không phải `https://`. Cái giữ cho nó an toàn là lớp mã hóa WireGuard của Tailscale chứ không phải TLS. Nghĩa là ai vào được tailnet của bạn thì vào được Gitea. Với vault cá nhân mình thấy đủ; nếu bạn định cho đồng nghiệp dùng chung thì nên dựng thêm reverse proxy có chứng chỉ.

**Git giữ mọi phiên bản của mọi file, vĩnh viễn.** Vault của mình 986 file `.md` nhưng thư mục `.git` đã 248 MB, và tổng vault là 415 MB. Thủ phạm là ảnh dán vào ghi chú. Xóa ảnh khỏi note không làm repo nhỏ lại, vì bản cũ vẫn nằm trong lịch sử. Hạn chế dán video và ảnh lớn ngay từ đầu, GitHub cũng chặn file trên 100 MB.

**Trên điện thoại, đồng bộ không tự động hoàn toàn.** Bạn phải nhớ đợi pull xong mới sửa và thoát app để push. Synology Drive không bắt bạn nhớ gì cả. Đây là điểm trừ thật, và nếu bạn chủ yếu dùng Obsidian trên điện thoại thì hãy cân nhắc kỹ chỗ này.

**Conflict vẫn xảy ra, chỉ đổi hình dạng.** Sửa cùng một dòng trong cùng một ghi chú trên hai máy trong vài phút thì git vẫn bó tay, và bạn sẽ thấy `<<<<<<<` xuất hiện giữa bài viết. Khác biệt là bạn sửa ngay trong file thay vì đi tìm bản sao thứ hai.

**Cả hệ thống phụ thuộc NAS còn sống.** Bù lại, mỗi PC đều giữ một bản clone đầy đủ có toàn bộ lịch sử, nên NAS chết cũng không mất dữ liệu — chỉ là các máy tạm thời không nói chuyện được với nhau. Riêng điện thoại thì không, vì clone shallow depth 1 không có lịch sử.

**Máy yếu thì phải cân nhắc.** NAS của mình 3,4 GiB RAM và đang chạy thêm Plex, Jellyfin, Navidrome, Tailscale, Synology Drive. Lúc mình kiểm tra, RAM còn trống 141 MB và swap đã dùng 2,8 trên 4 GiB. Gitea không phải nguyên nhân chính — nó nhẹ — nhưng nếu NAS bạn đang đầy như vậy thì đừng nghĩ nó là gói cuối cùng bạn cài được.

## Vậy có nên làm không

Nên, nếu bạn sửa ghi chú trên từ hai thiết bị trở lên và đã từng phải dọn file conflict. Lợi ích lớn nhất không phải là miễn phí — Obsidian Sync chính chủ cũng không đắt — mà là **hợp nhất ở mức dòng** và **lịch sử phiên bản của từng ghi chú**. 642 commit của mình là 642 mốc thời gian có thể quay lại được cho bất kỳ ghi chú nào, thứ mà không công cụ đồng bộ file nào cho bạn.

Không nên, nếu bạn chỉ dùng một máy, hoặc dùng điện thoại là chính. Một máy thì không có gì để hợp nhất. Điện thoại là chính thì cái nhịp "đợi pull, sửa, thoát app" sẽ làm bạn khó chịu mỗi ngày, và sớm muộn bạn cũng quên một lần rồi ngồi gỡ conflict.

Riêng phần cứng thì đừng lo. Con MicroServer Gen10 đời cũ của mình cõng được Gitea không hề vất vả, và gói SynoCommunity thì cài bằng vài cú bấm trong Package Center chứ không cần đụng tới Docker.

Chúc các bạn thành công.

## Link tham khảo

[https://synocommunity.com/package/gitea](https://synocommunity.com/package/gitea)

[https://docs.gitea.com/administration/repo-mirror](https://docs.gitea.com/administration/repo-mirror)

[https://tailscale.com/kb/1131/synology](https://tailscale.com/kb/1131/synology)

[https://github.com/Vinzent03/obsidian-git](https://github.com/Vinzent03/obsidian-git)

[https://github.com/ViscousPot/GitSync](https://github.com/ViscousPot/GitSync)
