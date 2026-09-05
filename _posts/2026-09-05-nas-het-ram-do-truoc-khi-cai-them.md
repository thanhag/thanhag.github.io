---
published: true
title: 'NAS hết RAM: zram đầy 100%, gần 1 GB tràn xuống ổ cứng'
date: '2026-09-05'
categories:
  - server
  - thu-thuat-chung
tags:
  - NAS
  - RAM
  - swap
  - zram
  - Docker
  - Synology
series: "Tự dựng server tại nhà"
series_thu_tu: 8
cap_do: "Cơ bản"
excerpt: >-
  Mình định cài thêm một dịch vụ nữa lên NAS. Đo trước cho chắc, và phát hiện máy đã
  hết chỗ từ lâu: **zram đầy 99,9%**, gần 1 GB tràn xuống ổ cứng, và nhân đang đọc
  swap **285 KB/s** ngay lúc máy gần như rảnh. Bài này là ba lệnh để tự đo, và cách
  đọc kết quả cho đúng.
toc: true
breadcrumbs: true
permalink: /server/nas-het-ram-do-truoc-khi-cai-them
---

Mình định cài thêm một dịch vụ nữa lên NAS. Trước khi cài thì đo một lượt cho chắc, và số đo cho thấy máy đã hết chỗ từ lâu rồi.

{% include series-nav.html %}

Bài này là ba lệnh để tự đo, cách đọc kết quả cho đúng, và một chuyện khó nói hơn: phần lớn RAM của mình đang bị chiếm bởi những thứ mình không còn dùng.

## Ba con số

Con NAS 4 GB của mình, uptime 28 ngày 17 giờ, đang trong tình trạng này:

```
              total        used        free      shared  buff/cache   available
Mem:           3458        2679         132          54         646         487
Swap:          4121        3028        1093
```

**RAM còn thật sự dùng được: 487 MB.** Không phải cột `free` (132 MB) — cột đó luôn thấp và không nói lên điều gì, vì nhân giữ bộ đệm đĩa ở `buff/cache` và sẽ trả lại khi cần. Cột đáng nhìn là `available`.

**Swap đã dùng 3.028 MB trên 4.121 MB.** Nhưng con số này một mình vẫn chưa kết luận được gì, và đó là chỗ mình sẽ nói kỹ bên dưới.

**Nhân đang đọc swap 285 KB/s** trong lúc máy gần như rảnh. Đây mới là con số làm mình dừng tay.

## Lệnh 1: xem swap nằm ở đâu

Đây là lệnh mà mình nghĩ nhiều người bỏ qua. `free` gộp tất cả swap vào một dòng, nhưng swap có thể nằm ở hai chỗ rất khác nhau về hậu quả:

```bash
cat /proc/swaps
```

```
Filename                Type            Size      Used    Priority
/dev/md1                partition       2096124   977612  -1
/dev/zram0              partition       2124796   2122532  1
```

Hai dòng, hai câu chuyện khác hẳn.

`/dev/zram0` là **swap nằm trong chính RAM**, dữ liệu được nén lại. Đẩy trang vào đây tốn CPU để nén, nhưng không hề chạm vào ổ cứng, nên nhanh. Nó đang dùng 2.122.532 trên 2.124.796 KB — **đầy 99,9%**.

`/dev/md1` là swap **trên đĩa thật**, nằm trên chính mảng ổ cứng chứa dữ liệu của bạn. Nó đang giữ 977.612 KB, tức gần 1 GB.

Cột `Priority` giải thích thứ tự: zram có ưu tiên `1`, cao hơn `-1` của đĩa, nên nhân dùng zram trước. Gần 1 GB nằm trên đĩa nghĩa là **zram đã đầy tới mức nhân buộc phải tràn xuống ổ cứng**. Đó không còn là chuyện tối ưu nữa.

## Lệnh 2: đo xem swap có đang bị đọc ghi liên tục không

Đây là phép đo quan trọng nhất trong bài, và cũng là thứ hầu như không hướng dẫn nào nhắc.

**Swap có dữ liệu không đồng nghĩa với máy đang chậm.** Nhân đẩy các trang nguội — thứ nạp lúc khởi động rồi không đụng tới nữa — ra swap là hành vi đúng, nó giải phóng RAM cho việc có ích. Một máy có 3 GB swap toàn trang nguội vẫn chạy mượt.

Vấn đề chỉ xuất hiện khi nhân phải **đọc đi đọc lại** swap, vì thứ nằm trong đó vẫn đang được dùng. Muốn biết thì phải đo tốc độ, không phải đo dung lượng.

DSM không có `vmstat`, nhưng bộ đếm nằm sẵn trong nhân. Lấy hai mẫu cách nhau 15 giây rồi chia ra:

```bash
a=$(grep -E "^pswpin|^pswpout" /proc/vmstat); sleep 15
b=$(grep -E "^pswpin|^pswpout" /proc/vmstat)
echo "$a"; echo "$b"
```

Mỗi trang là 4 KB, nên lấy hiệu số nhân 4 rồi chia cho 15 là ra KB/s. Máy mình trong 15 giây đó:

```
doc tu swap  (swap-in) : 1069 trang -> 285 KB/s
ghi ra swap (swap-out):  327 trang ->  87 KB/s
```

Máy đang **đọc từ swap 285 KB/s liên tục** trong lúc không ai dùng gì. Nghĩa là dữ liệu nằm trong swap không phải trang nguội — nó là thứ các tiến trình vẫn cần, và nhân phải lôi ra vào suốt.

Con số cộng dồn từ lúc khởi động còn rõ hơn:

```bash
grep -E "^pswpin|^pswpout" /proc/vmstat
```

```
pswpin 13294756
pswpout 11598748
```

Nhân 4 KB: **53 GB đã đọc ra từ swap và 46 GB đã ghi vào swap** trong 28 ngày. Phần rơi xuống `/dev/md1` là ghi thật lên ổ cứng.

Nếu máy bạn đo ra vài KB/s hoặc bằng không thì swap đầy tới đâu cũng không sao. Nếu ra hàng trăm KB/s như của mình thì máy đang bù RAM bằng đĩa, và mọi thứ chậm đi một cách khó chỉ mặt đặt tên.

## Lệnh 3: ai đang ăn RAM

```bash
ps -eo rss,args --sort=-rss | head -15
```

Máy mình, đơn vị KB:

| RSS (KB) | Tiến trình |
|---|---|
| 428.324 | AdGuard Home (lọc quảng cáo DNS) |
| 355.016 | một trình quản lý tải file chạy trên Java |
| 148.672 | Jellyfin (máy chủ phim) |
| 103.720 | một dịch vụ Node |
| 80.920 | Gitea |
| 51.508 | `synoelasticd` — bộ đánh chỉ mục tìm kiếm của DSM |
| 35.608 | `dockerd` |
| 34.380 | `Xvnc` — máy chủ màn hình từ xa |
| 29.128 | tiến trình đồng bộ của Synology Drive |
| 24.744 | `tailscaled` |

Một lưu ý phải nói kẻo bạn cộng nhầm: **RSS đếm cả phần bộ nhớ dùng chung**, nên cộng cả cột lại sẽ ra số lớn hơn lượng RAM thật đang bị chiếm. Dùng nó để xếp hạng ai nặng ai nhẹ thì đúng, dùng để tính tổng thì sai.

Còn một cách nhìn khác, gọn hơn:

```bash
grep Committed_AS /proc/meminfo
```

```
Committed_AS:   11060624 kB
```

Tổng bộ nhớ mà nhân đã **hứa** cấp cho các tiến trình là 10,5 GB, trên một cái máy có 3,4 GB. Nhân cho phép hứa vượt vì phần lớn chương trình xin nhiều hơn mức thật sự đụng tới. Nhưng tỷ lệ hứa gấp ba lần thực có là dấu hiệu máy đang gánh nhiều hơn khả năng của nó.

## Chỗ khó nói: mình cài rồi không dùng

Nhìn lại bảng trên và tự hỏi từng dòng "tuần vừa rồi mình có mở nó không", kết quả không đẹp.

Cái ăn nhiều thứ hai, 355 MB, là một trình quản lý tải file mình cài từ rất lâu và gần như không còn mở tới. Nó là ứng dụng Java, mà JVM thì giữ chặt vùng heap đã xin kể cả lúc ngồi không. `Xvnc` chiếm thêm 34 MB cho một màn hình từ xa mình chưa dùng lần nào trong tháng. Jellyfin 148 MB trong khi nhà mình xem phim bằng thứ khác. `synoelasticd` 51 MB là bộ đánh chỉ mục tìm kiếm của DSM, chạy để phục vụ một ô tìm kiếm mình gần như không gõ vào.

Cộng riêng bốn thứ đó đã khoảng **590 MB**, hơn cả lượng RAM còn trống của cả máy.

Trong khi đó những dịch vụ mình thật sự dùng hằng ngày lại rất nhẹ: Gitea 80 MB, Tailscale 24 MB, Vaultwarden và PrivateBin thậm chí không lọt nổi vào bảng. **Cái làm NAS hết RAM không phải là những thứ mình dựng có chủ đích, mà là những thứ mình cài thử rồi quên.**

Đây là kiểu tích tụ rất dễ xảy ra với NAS, vì cài một gói chỉ mất vài cú bấm và không có gì nhắc bạn rằng nó vẫn đang chạy sau đó hai năm.

## Về `swappiness` trên NAS

```bash
cat /proc/sys/vm/swappiness
```

Máy mình trả về `60`, là mặc định. Con [VPS mình vừa gia cố tuần này](/server/bao-mat-vps-ubuntu-36802-lan-do-mat-khau) đặt `10`.

Khác biệt đó có lý do. Trên VPS không có zram, swap nằm thẳng trên đĩa, nên đẩy ra swap là chậm thật và để `10` là hợp lý. Trên NAS có zram, swap ưu tiên nằm trong RAM nén, nên nhân sốt sắng đẩy ra một chút cũng không hại gì — `60` không phải con số sai.

Nhưng nó chỉ đúng **khi zram còn chỗ**. Zram của mình đã đầy 99,9%, nên bây giờ mỗi lần nhân quyết định đẩy một trang ra swap, chỗ duy nhất còn nhận là ổ cứng. Hạ `swappiness` xuống lúc này chỉ là bịt triệu chứng. Cái sai không nằm ở tham số, mà ở chỗ máy đang chạy nhiều hơn mức RAM cho phép.

## Vậy mình làm gì

Mình **không cài thêm dịch vụ mới**, dù đã lên kế hoạch viết bài về nó. Cài một ứng dụng Node vào lúc này là đẩy máy tràn xuống đĩa sâu hơn và làm chậm mọi thứ đang chạy, đổi lấy một bài viết. Không đáng.

Thứ tự mình sẽ làm là gỡ trước, nâng sau. Gỡ hẳn những gói không còn dùng — gỡ chứ không chỉ tắt, vì gói đã tắt vẫn có thể tự bật lại sau khi cập nhật DSM. Ước tính thu về khoảng 500–600 MB, đủ để zram thôi đầy và máy thôi ghi swap xuống đĩa.

Nhưng phải nói thẳng: **dọn dẹp chỉ mua thêm thời gian.** Nó đưa máy về trạng thái lành mạnh với đúng số dịch vụ hiện tại, chứ không tạo ra chỗ cho dịch vụ mới. Muốn chạy thêm thì phải nâng RAM, không có đường tắt nào khác.

Và đây là bài học vòng lại [bài chọn NAS đầu tiên](/server/chon-nas-dau-tien-mua-dung-san-hay-tu-lap): lúc mua, 4 GB nghe rất thoải mái cho "một cái ổ cứng mạng". Nó chỉ chật khi bạn bắt đầu tự host thật, và lúc đó thì khe RAM còn trống hay không đã được quyết định từ lâu rồi. Nếu bạn đang chọn máy, đây là lý do mình khuyên nhìn khả năng nâng RAM trước khi nhìn số khay ổ cứng.

## Đo lại sau khi dọn

Đừng tin cảm giác "hình như nhanh hơn". Ghi lại ba con số trước khi dọn, dọn xong đo lại đúng ba con số đó:

```bash
free -m | head -3
cat /proc/swaps
grep -E "^pswpin|^pswpout" /proc/vmstat
```

Hai chỉ số cần thay đổi là **`available` tăng lên** và **tốc độ swap-in tụt về gần 0**. Riêng dòng `/dev/md1` trong `/proc/swaps` sẽ không tự giảm ngay, vì nhân không chủ động kéo trang từ đĩa về khi RAM vừa trống ra. Muốn dọn sạch phần đó thì tắt bật lại swap, và chỉ làm khi RAM đã đủ trống để nhận hết:

```bash
sudo swapoff -a && sudo swapon -a
```

Làm lệnh này lúc RAM còn chật là cách nhanh nhất để máy bị nhân giết tiến trình. Đo trước, chắc chắn `available` đã lớn hơn lượng swap đang dùng, rồi mới chạy.

Chúc các bạn thành công.

## Link tham khảo

[https://www.kernel.org/doc/Documentation/blockdev/zram.txt](https://www.kernel.org/doc/Documentation/blockdev/zram.txt)

[https://docs.kernel.org/filesystems/proc.html](https://docs.kernel.org/filesystems/proc.html)
