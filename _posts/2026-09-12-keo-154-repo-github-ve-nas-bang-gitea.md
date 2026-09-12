---
published: true
title: 'Kéo 154 repo GitHub về NAS: mirror tự cập nhật bằng Gitea'
date: '2026-09-12'
categories:
  - server
  - thu-thuat-chung
tags:
  - Gitea
  - GitHub
  - NAS
  - backup
  - mirror
  - API
series: "Tự dựng server tại nhà"
series_thu_tu: 9
cap_do: "Nâng cao"
header:
  teaser: >-
    /assets/images/2026/2026-09-12-gitea-mirror-sofsog.com01.jpg
  overlay_image: >-
    /assets/images/2026/2026-09-12-gitea-mirror-sofsog.com01.jpg
  og_image: >-
    /assets/images/2026/2026-09-12-gitea-mirror-sofsog.com01.jpg
  caption: "Ảnh minh hoạ — chu kỳ đồng bộ thật là 8 tiếng, không phải tức thời. [**sofsog**](https://sofsog.com)"
excerpt: >-
  Toàn bộ 154 repo của mình nằm trên một tài khoản GitHub duy nhất. Bài này là cách
  dùng **Pull Mirror** của Gitea kéo hết về NAS làm bản sao tự cập nhật — kèm script
  chạy hàng loạt, và cái bẫy token khiến repo private trả về **404** mà không báo lỗi gì.
toc: true
breadcrumbs: true
permalink: /server/keo-154-repo-github-ve-nas-bang-gitea
---

Mình có 154 repo trên GitHub, tất cả nằm dưới một tài khoản duy nhất. Mất tài khoản đó là mất sạch.

Không cần tới chuyện bị khoá tài khoản mới thành vấn đề — đổi chính sách, mất khoá xác thực hai lớp, hay đơn giản là một hôm nào đó không đăng nhập được, hậu quả đều giống nhau.

{% include series-nav.html %}

Bài này là cách mình kéo toàn bộ số repo đó về con NAS ở nhà, tự động cập nhật, kèm script chạy hàng loạt và cái bẫy token đã làm mình mất một buổi.

## Push mirror hay pull mirror — nhầm chiều là hỏng

Gitea có hai thứ tên gần giống nhau mà chiều dữ liệu ngược hẳn. Phải phân biệt trước khi bấm bất cứ nút nào.

| | Push mirror | Pull mirror |
|---|---|---|
| Chiều dữ liệu | Gitea → GitHub | GitHub → Gitea |
| Ai là bản gốc | Gitea | GitHub |
| Repo bên Gitea | ghi bình thường | **chỉ đọc** — chặn push, chặn sửa trên web |

Bài này dùng **pull mirror**: GitHub là bản gốc, Gitea chỉ hứng về.

Ở đây có một cái bẫy đáng nói. Vault Obsidian của mình đang chạy **ngược lại** — [Gitea trên NAS là hub](/server/dung-gitea-tren-nas-dong-bo-obsidian-giua-pc-va-dien-thoai), máy tính và điện thoại push vào đó rồi Gitea mới đẩy tiếp lên GitHub. Nếu mình lỡ tay bật pull mirror cho cái repo vault đó thì nó thành chỉ đọc, và **mọi commit từ máy sẽ bị chặn**.

Nên việc đầu tiên là ghi tên repo đó vào danh sách loại trừ, trước khi chạy script. Mình sẽ nói ở bước 4.

## Điều kiện cần

Một Gitea đang chạy — mình dùng bản cài dạng gói trên DSM, [đã viết ở bài đầu series](/server/dung-gitea-tren-nas-dong-bo-obsidian-giua-pc-va-dien-thoai). Một tài khoản GitHub. Và quyền SSH vào NAS để chạy script.

Dung lượng thì cứ tính rộng tay: 154 repo của mình về tới nơi không nặng, nhưng nếu bạn có repo chứa ảnh hay dữ liệu lớn thì cộng lại nhanh hơn tưởng.

## Bước 1: Tạo token GitHub, và cái bẫy ở đây

Đây là chỗ mình vấp, và triệu chứng của nó rất khó chịu vì **không có thông báo lỗi nào cả**.

Vào GitHub → Settings → Developer settings → Personal access tokens → **Fine-grained tokens** → Generate new token. Cần đúng **hai** thứ, thiếu một là hỏng:

1. **Repository access** đặt thành `All repositories`
2. **Permissions → Repository permissions**: `Contents` để `Read-only`, và `Metadata` để `Read-only`

Cái bẫy nằm ở chỗ: **nếu bạn để phần Permissions trống, GitHub âm thầm đưa Repository access về `Public repositories` mỗi lần lưu.** Bấm Update bao nhiêu lần cũng vô ích, quay lại vẫn thấy nó nhảy về Public.

Lý do thì hợp lý khi hiểu ra: loại token này đọc được repo công khai sẵn rồi, nên chọn "All repositories" mà không cấp quyền nào thì chẳng có nghĩa gì. Chỉ là GitHub không nói ra.

Hệ quả nếu để lọt: **script chạy trơn tru, không lỗi, thấy đủ repo công khai — nhưng mọi repo private trả về HTTP 404 như thể không tồn tại.** Mình đã tạo xong 100 mirror rồi mới phát hiện thiếu mất 52 cái.

Kiểm tra nhanh bằng một lệnh, thay tên tài khoản và tên một repo private của bạn:

```bash
curl -sS -o /dev/null -w "%{http_code}\n" \
  -H "Authorization: Bearer <token-github>" \
  https://api.github.com/repos/<tài-khoản>/<repo-private>
```

Ra `200` là ổn. Ra `404` là token chưa đủ quyền — repo vẫn ở đó, chỉ là token không nhìn thấy.

Một điểm tiện: nếu bạn sửa quyền của **token cũ** thì chuỗi token không đổi, không phải nạp lại vào NAS. Chỉ khi tạo token mới mới phải cập nhật.

## Bước 2: Tạo token Gitea

Script cần gọi API của cả hai bên, nên cũng cần một token của chính Gitea.

Trên Gitea: bấm avatar → **Settings** → **Applications** → Generate Token, cấp quyền `repository: Read and Write`.

Copy ngay, vì Gitea chỉ hiện một lần.

## Bước 3: Thử một repo bằng giao diện web trước

Đừng chạy script ngay. Làm tay một repo để biết mọi thứ đúng chưa.

Trên Gitea bấm dấu **+** → **New Migration** → chọn **GitHub**:

- **Clone From URL**: `https://github.com/<tài-khoản>/<repo>.git`
- **Access Token**: dán token GitHub ở bước 1
- Tick **This repository will be a mirror** — đây chính là công tắc biến nó thành pull mirror
- **Mirror Interval**: `8h`. Tối thiểu Gitea cho phép là `10m`; để trống nghĩa là chỉ đồng bộ khi bấm tay
- Tick **Private**

Mấy ô Issues, Pull Requests, Labels, Milestones thì nên biết trước: **pull mirror chỉ đồng bộ định kỳ phần git** — nhánh, thẻ, wiki. Những thứ kia nếu tick thì chỉ được sao chép đúng một lần lúc tạo, sau đó đứng im mãi mãi.

Tạo xong, vào repo đó → Settings → **Mirror Settings** để đổi chu kỳ, bấm **Synchronize Now** đồng bộ ngay, hoặc cập nhật token khi hết hạn. Ở đó cũng có nút **Convert to Regular Repository** để gỡ trạng thái mirror — nút này **một chiều, không hoàn tác được**.

## Bước 4: Script mirror hàng loạt

Làm tay 154 lần thì không ai làm nổi. Đây là script mình đang chạy thật trên NAS, đặt ở `~/scripts/gitea-mirror-all.sh` với quyền `700`.

Cách nó hoạt động: gọi `/user/repos` của GitHub có phân trang để lấy toàn bộ repo mình sở hữu, rồi với từng repo gọi `POST /api/v1/repos/migrate` của Gitea kèm `"mirror": true`. Repo đã tồn tại bên Gitea sẽ trả về **409** và bị bỏ qua — nên **chạy lại bao nhiêu lần cũng an toàn**.

```bash
#!/usr/bin/env bash
# Dong bo pull mirror tu GitHub ve Gitea tren NAS.
#   bash gitea-mirror-all.sh          -> quet GitHub va tao mirror cho repo moi
#   bash gitea-mirror-all.sh --check  -> chi kiem tra token + dem repo, khong tao gi
set -u
export PATH=/usr/bin:/bin:/usr/local/bin:$PATH

GITEA_URL="${GITEA_URL:-http://<địa-chỉ-nas>:8418}"
GITEA_OWNER="${GITEA_OWNER:-<tài-khoản-gitea>}"
MIRROR_INTERVAL="${MIRROR_INTERVAL:-8h}"

BASE="$(cd "$(dirname "$0")" && pwd)"
ENV_FILE="${ENV_FILE:-$BASE/.gitea-mirror.env}"
SKIP_FILE="$BASE/skip.txt"
LIST_FILE="$BASE/logs/repos.txt"
LOG="$BASE/logs/gitea-mirror.log"
mkdir -p "$BASE/logs"

log() { m="$(date '+%F %T') $*"; echo "$m"; echo "$m" >> "$LOG"; }

exec 9>"$BASE/logs/.lock"
flock -n 9 || { log "Bo qua: dang co tien trinh khac chay"; exit 0; }

[ -f "$ENV_FILE" ] || { log "LOI: thieu file token $ENV_FILE"; exit 1; }
. "$ENV_FILE"
if [ -z "${GH_TOKEN:-}" ] || [ -z "${GITEA_TOKEN:-}" ]; then
  log "LOI: $ENV_FILE chua co GH_TOKEN / GITEA_TOKEN"; exit 1
fi

pick() { grep -o "\"$1\"[[:space:]]*:[[:space:]]*\"[^\"]*\"" | sed 's/.*"\([^"]*\)"$/\1/'; }

gh_user=$(curl -sS --max-time 30 -H "Authorization: Bearer $GH_TOKEN" \
  https://api.github.com/user | pick login)
[ -n "$gh_user" ] || { log "LOI: token GitHub khong hop le hoac het han"; exit 1; }
gt_user=$(curl -sS --max-time 30 -H "Authorization: token $GITEA_TOKEN" \
  "$GITEA_URL/api/v1/user" | pick login)
[ -n "$gt_user" ] || { log "LOI: token Gitea khong hop le hoac het han"; exit 1; }
log "=== Bat dau: GitHub=$gh_user -> Gitea=$gt_user ==="

: > "$LIST_FILE"; page=1
while :; do
  names=$(curl -sS --max-time 60 -H "Authorization: Bearer $GH_TOKEN" \
    "https://api.github.com/user/repos?per_page=100&affiliation=owner&page=$page" | pick full_name)
  [ -z "$names" ] && break
  printf '%s\n' "$names" >> "$LIST_FILE"
  page=$((page + 1))
done
sort -u -o "$LIST_FILE" "$LIST_FILE"
total=$(grep -c . "$LIST_FILE" || true)
log "GitHub dang co $total repo (danh sach: $LIST_FILE)"

if [ "${1:-}" = "--check" ]; then log "=== Che do --check, khong tao gi ==="; exit 0; fi

tmp=$(mktemp); ok=0; skip=0; err=0
while IFS= read -r full; do
  case "$full" in ''|'#'*) continue ;; esac
  if [ -f "$SKIP_FILE" ] && grep -qxF "$full" "$SKIP_FILE" 2>/dev/null; then
    skip=$((skip + 1)); continue
  fi
  name="${full##*/}"
  code=$(curl -sS -o "$tmp" -w '%{http_code}' --max-time 1800 \
    -X POST "$GITEA_URL/api/v1/repos/migrate" \
    -H "Authorization: token $GITEA_TOKEN" -H "Content-Type: application/json" \
    -d "{\"clone_addr\":\"https://github.com/$full.git\",\"auth_token\":\"$GH_TOKEN\",\"repo_owner\":\"$GITEA_OWNER\",\"repo_name\":\"$name\",\"service\":\"github\",\"mirror\":true,\"mirror_interval\":\"$MIRROR_INTERVAL\",\"private\":true,\"wiki\":true,\"description\":\"Pull mirror: $full\"}")
  case "$code" in
    201) ok=$((ok + 1)); log "TAO MOI  $full" ;;
    409) skip=$((skip + 1)) ;;
    *)   err=$((err + 1)); log "LOI $code  $full : $(head -c 200 "$tmp" | tr -d '\n')" ;;
  esac
done < "$LIST_FILE"
rm -f "$tmp"

log "=== Xong: tao moi=$ok, da co/bo qua=$skip, loi=$err ==="
if [ "$(wc -l < "$LOG")" -gt 5000 ]; then tail -2000 "$LOG" > "$LOG.tmp" && mv "$LOG.tmp" "$LOG"; fi
exit 0
```

Vài chỗ trong script đáng giải thích:

**`flock -n 9`** khoá không cho hai lần chạy chồng lên nhau. Chạy theo lịch định kỳ mà lần trước còn đang tải dở thì lần sau tự thoát, không đánh nhau.

**`--max-time 1800`** cho lệnh migrate là ba mươi phút cho mỗi repo. Nghe dài, nhưng Gitea clone repo lớn có thể lâu và cắt sớm thì hỏng dở dang.

**`affiliation=owner`** giới hạn ở repo mình sở hữu, không kéo về những repo mình chỉ được mời cộng tác.

**Mã trả về** là toàn bộ logic: `201` là tạo mới, `409` là đã có nên bỏ qua, còn lại là lỗi và được ghi log kèm 200 ký tự đầu của phản hồi.

Script đọc token từ file riêng, không nhúng trong mã. Tạo file đó **trên NAS**, bằng cách gõ vào chứ đừng để token nằm trong lịch sử lệnh:

```bash
read -rsp "GitHub token: " G; echo
read -rsp "Gitea token : " T; echo
umask 077
printf 'export GH_TOKEN=%s\nexport GITEA_TOKEN=%s\n' "$G" "$T" > ~/scripts/.gitea-mirror.env
chmod 600 ~/scripts/.gitea-mirror.env
```

Rồi tạo danh sách loại trừ — **đây là bước bảo vệ repo vault nói ở đầu bài**, mỗi dòng một `tài-khoản/repo`:

```bash
echo "<tài-khoản>/<repo-vault>" >> ~/scripts/skip.txt
```

Chạy thử ở chế độ kiểm tra trước, nó chỉ xác thực token và đếm repo chứ không tạo gì:

```bash
bash ~/scripts/gitea-mirror-all.sh --check
```

Thấy đúng số repo mình có thì chạy thật:

```bash
bash ~/scripts/gitea-mirror-all.sh
```

## Bước 5: Đặt lịch chạy hàng tuần

Đây là chỗ nhiều người bỏ sót. **Gitea không có chức năng mirror cả một tài khoản.** Mỗi mirror là một repo được tạo riêng. Repo bạn tạo mới trên GitHub ngày mai sẽ không tự về NAS — phải chạy lại script.

Mình đặt **hàng tuần**. Hàng tháng cũng chạy được, nhưng một repo mới có thể nằm ngoài bản sao tới ba mươi ngày, mà chi phí chạy thêm gần như bằng không: lần chạy khi không có repo mới chỉ mất hơn một phút và không tạo ra gì.

Trên DSM: **Control Panel → Task Scheduler → Create → Scheduled Task → User-defined script**

| Trường | Giá trị |
|---|---|
| Task name | `Gitea mirror GitHub` |
| User | tài khoản có thư mục `scripts` |
| Schedule → Date | Repeat **Weekly**, chọn một ngày cố định trong tuần |
| First run time | `03:00` |
| Run command | `/bin/bash /var/services/homes/<user>/scripts/gitea-mirror-all.sh` |

Dùng Task Scheduler của DSM chứ **đừng viết vào `/etc/crontab`** — DSM có thể ghi đè tệp đó khi cập nhật hệ thống, và bạn sẽ mất lịch mà không biết.

## Kiểm tra bằng cơ sở dữ liệu của Gitea

Giao diện web không có chỗ nào xem được toàn bộ mirror cùng lúc. Nhưng Gitea dùng SQLite nên đọc thẳng được. Luôn thêm `-readonly`, đừng ghi vào đó.

Đếm nhanh — bảng `mirror` là pull mirror, `push_mirror` là push mirror:

```bash
sqlite3 -readonly /volume1/@appdata/gitea/data/gitea.db \
  "SELECT count(*) FROM mirror; SELECT count(*) FROM push_mirror;"
```

Xem chu kỳ và lần đồng bộ gần nhất của từng cái:

```bash
sqlite3 -readonly -header -column /volume1/@appdata/gitea/data/gitea.db \
  "SELECT r.owner_name||'/'||r.name AS repo,
          (m.interval/3600000000000)||'h' AS chu_ky,
          datetime(m.updated_unix,'unixepoch','localtime') AS lan_cuoi,
          datetime(m.next_update_unix,'unixepoch','localtime') AS lan_toi
   FROM mirror m JOIN repository r ON r.id = m.repo_id;"
```

Cột `interval` lưu bằng nanô giây, nên phải chia cho 3.600.000.000.000 mới ra giờ.

Và câu truy vấn mình thấy hữu ích nhất — tìm repo nằm trên Gitea nhưng **không phải mirror**, tức là sẽ không bao giờ tự cập nhật:

```bash
sqlite3 -readonly /volume1/@appdata/gitea/data/gitea.db \
  "SELECT r.name FROM repository r
   LEFT JOIN mirror m ON m.repo_id = r.id
   WHERE m.id IS NULL;"
```

Chính câu này chỉ ra cho mình một repo mình từng clone tay từ lâu. Vì nó trùng tên với repo trên GitHub nên script luôn nhận `409` và bỏ qua, nghĩa là nó nằm đó như một bản chụp chết cứng từ nhiều tháng trước mà mình cứ tưởng đang được cập nhật. Đó đúng là loại sai lầm mà [bài quy tắc 3-2-1](/server/quy-tac-3-2-1-lam-cho-that) nói tới: có bản sao không bằng có bản sao còn sống.

Log của Gitea ở `/volume1/@appdata/gitea/gitea.log` nếu cần đào sâu hơn.

## Những gì cách này không làm được

**Không phải tức thời.** Mỗi mirror đặt chu kỳ 8 tiếng. Gitea có một cron nội bộ tên `update_mirrors` chạy mười phút một lần, quét xem mirror nào tới hạn thì `git fetch --prune`. Nên commit mới trên GitHub về tới NAS chậm nhất sau tám tiếng.

**Đây là polling, không phải webhook.** GitHub hoàn toàn không biết con NAS tồn tại. Muốn gần như tức thời bằng webhook thì không làm được, vì NAS nằm sau [Tailscale](/server/tailscale-vao-nas-tu-xa-khong-mo-port) và GitHub không gọi vào được. Đây là cái giá phải trả cho việc không mở cổng nào ra Internet, và mình thấy đổi vậy là đáng.

**NAS phải đang bật.** Tắt máy đúng lúc tới hạn thì lần đó bị lỡ, chạy bù sau khi bật lại.

**Chỉ có phần git.** Issue, pull request, nhãn, mốc — không đồng bộ định kỳ. Nếu chúng quan trọng với bạn thì đây không phải giải pháp đủ.

**Xoá bên GitHub là xoá bên này.** `git fetch --prune` nghĩa là nhánh bị xoá trên GitHub cũng biến mất khỏi bản mirror. Nó là bản sao trung thực, **không phải bản lưu trữ chống xoá nhầm**. Muốn chống xoá nhầm thì cần snapshot theo thời điểm, là chuyện khác.

## Kết quả

GitHub của mình lúc thiết lập có **101 repo công khai và 53 repo riêng tư, tổng 154**.

Đợt chạy đầu tạo được 100 mirror — đúng lúc token còn chưa nhìn thấy repo private. Sửa quyền token rồi chạy lại, đợt hai tạo thêm 52 cái, **hết 11 phút, không lỗi nào**.

Đếm lại trên Gitea hôm nay: **152 pull mirror**, cộng repo vault đang chạy push mirror theo chiều ngược lại, cộng một repo thường — vừa đúng 154, khớp 1:1 với GitHub.

Từ giờ mỗi tuần script tự chạy một lần để hứng repo mới, còn repo cũ thì tự cập nhật mỗi tám tiếng. Mình không phải làm gì nữa.

Chúc các bạn thành công.

## Link tham khảo

[https://docs.gitea.com/usage/repo-mirror](https://docs.gitea.com/usage/repo-mirror)

[https://docs.gitea.com/api/1.20/](https://docs.gitea.com/api/1.20/)

[https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
