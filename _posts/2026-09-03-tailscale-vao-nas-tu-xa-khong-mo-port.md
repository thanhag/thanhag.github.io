---
published: true
title: Tailscale - vào NAS từ bất cứ đâu mà không mở port trên router
date: '2026-09-03'
categories:
  - server
  - thu-thuat-chung
tags:
  - Tailscale
  - NAS
  - Synology
  - VPN
  - WireGuard
series: "Tự dựng server tại nhà"
series_thu_tu: 2
cap_do: "Cơ bản"
header:
  teaser: >-
    /assets/images/2026/2026-09-03-tailscale-vao-nas-sofsog.com01.png
  overlay_image: >-
    /assets/images/2026/2026-09-03-tailscale-vao-nas-sofsog.com01.png
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)"
excerpt: >-
  Điện thoại ra khỏi nhà là mất kết nối với NAS. Cách quen thuộc là mở port trên
  router rồi trỏ **DDNS** vào, nhưng làm vậy là phơi cả con NAS ra Internet.
  **Tailscale** giải bài này mà không cần mở thêm cổng nào.
toc: true
breadcrumbs: true
permalink: /server/tailscale-vao-nas-tu-xa-khong-mo-port
---

Điện thoại của mình đang ở quán cà phê và cần kéo vault Obsidian về từ Gitea chạy trên con NAS ở nhà. Cách quen thuộc là mở một cổng trên router rồi trỏ DDNS vào đó. Mình không làm vậy, và đây là cách mình vào được NAS từ bất cứ đâu trong khi router không mở thêm cổng nào.

{% include series-nav.html %}

## Vì sao mình không mở port

Mở một cổng ra Internet nghĩa là bất kỳ ai trên thế giới cũng gõ được vào đó. Con NAS của mình chạy giao diện web DSM, có SSH, có hơn chục container Docker. Mỗi thứ là một bề mặt tấn công, và mình không muốn cái nào trong số đó nằm ngoài đường.

Còn chuyện thứ hai: IP nhà thay đổi. Giải pháp thường thấy là DDNS, tự cập nhật tên miền mỗi lần IP đổi. Nó chạy được, nhưng thêm một mắt xích nữa để hỏng, mà vẫn không giải quyết chuyện phơi cổng.

Bài trước mình [dựng Gitea trên NAS để đồng bộ vault Obsidian](/server/dung-gitea-tren-nas-dong-bo-obsidian-giua-pc-va-dien-thoai). Gitea đó chỉ lắng nghe trong mạng nội bộ, nên điện thoại ra khỏi nhà là hết đồng bộ. Đó là bài toán cụ thể mình cần giải.

## Tailscale làm gì

Tailscale dựng một mạng riêng trên nền WireGuard. Mọi thiết bị đăng nhập vào cùng một tài khoản sẽ nhận một địa chỉ trong dải `100.x.x.x`, và địa chỉ đó gắn với thiết bị chứ không gắn với mạng nó đang nối vào. Máy ở nhà, ở công ty hay đang dùng 4G thì vẫn một địa chỉ ấy.

Hai máy trong mạng đó nói chuyện với nhau như đang chung một mạng LAN. Router không phải mở cổng, vì kết nối luôn được thiết lập từ trong ra ngoài.

## Điều kiện cần

Một tài khoản để đăng nhập — Tailscale dùng Google, GitHub hoặc Microsoft chứ không bắt tạo tài khoản riêng. Quyền cài gói trên DSM. Và mỗi thiết bị bạn muốn nối đều phải đăng nhập cùng tài khoản đó.

## Bước 1: Cài Tailscale lên NAS

Vào `Package Center` của DSM và tìm `Tailscale`. Gói này do chính hãng phát hành chứ không phải bản cộng đồng, kiểm chứng được sau khi cài:

```bash
grep -E "^(package|version|maintainer)=" /var/packages/Tailscale/INFO
```

```
package="Tailscale"
version="1.58.2-700058002"
maintainer="Tailscale, Inc."
```

![Hình tìm gói Tailscale trong Package Center của DSM sofsog.com](/assets/images/2026/2026-09-03-tailscale-vao-nas-sofsog.com02.png)

Không thấy trong Package Center thì tải file `.spk` từ trang tải của Tailscale rồi dùng nút `Manual Install`.

Một chi tiết mất thời gian nếu không biết trước: sau khi cài, lệnh `tailscale` **không** nằm trong `PATH`. Đường dẫn đầy đủ là:

```bash
/var/packages/Tailscale/target/bin/tailscale
```

Mình đặt alias cho khỏi phải gõ lại mỗi lần.

## Bước 2: Đăng nhập và lấy địa chỉ

Mở Tailscale trong DSM rồi bấm đăng nhập. Nó đưa ra một liên kết, mở liên kết đó trên trình duyệt bất kỳ, đăng nhập xong là con NAS được ghép vào tài khoản.

![Hình bảng điều khiển Tailscale trong DSM sau khi đăng nhập sofsog.com](/assets/images/2026/2026-09-03-tailscale-vao-nas-sofsog.com03.png)

Lấy địa chỉ vừa được cấp:

```bash
tailscale ip -4
```

```
100.107.72.33
```

Ghi lại con số này. Từ giờ mọi thứ trỏ vào NAS đều dùng nó.

## Bước 3: Cài lên các thiết bị còn lại

Windows và macOS tải ứng dụng từ trang chủ. Android và iOS cài từ cửa hàng ứng dụng. Đăng nhập cùng tài khoản, xong là các máy thấy nhau, không phải khai báo địa chỉ hay khoá gì thêm.

Vào `console.tailscale.com` sẽ thấy toàn bộ thiết bị đã ghép, kèm phiên bản và lần cuối online. Tài khoản và tên thiết bị trong các ảnh của bài này mình đã thay bằng giá trị giả.

## Bước 4: Đổi mọi địa chỉ sang dải 100.x

Đây là bước hay bị bỏ sót. Remote git của vault đổi thành:

```
http://100.107.72.33:8418/thanh_gitea/Ghi-chu-markdown.git
```

Alias SSH trong `~/.ssh/config`:

```
Host my-nas
    HostName 100.107.72.33
    User thanh
```

Nếu bạn để nguyên IP nội bộ `192.168.x.x` thì ở nhà vẫn chạy ngon, ra khỏi nhà mới đứng — và lúc đó rất dễ đổ lỗi cho Tailscale. Đổi hết sang `100.x` thì cả trong nhà lẫn ngoài đường đều dùng chung một địa chỉ.

## Kiểm tra xem đã chạy chưa

```bash
tailscale status
```

```
100.107.72.33   nas-nha   linux   -
100.103.75.74   dt-1      android offline
100.125.204.118 dt-2      android offline
100.81.9.26     pc-nha    windows active; direct 192.168.1.4:41641, tx 154507132 rx 167670448
100.79.71.53    pc-cty    windows active; relay "sin", tx 227624576 rx 622359232
100.80.203.37   wsl-pc    linux   -
100.92.69.123   dt-3      android idle, tx 155648 rx 36096
```

![Hình kết quả lệnh tailscale status trên NAS sofsog.com](/assets/images/2026/2026-09-03-tailscale-vao-nas-sofsog.com04.png)

Tên thiết bị và tài khoản mình đã thay bằng giá trị giả, các số còn lại giữ nguyên. Phần đáng nhìn nằm ở cột cuối: một máy ghi `direct`, một máy ghi `relay`.

## Trực tiếp hay đi qua relay

Chỗ này quyết định tốc độ, và cũng là chỗ hay bị hiểu nhầm thành "Tailscale chậm".

Dòng `direct 192.168.1.4:41641` là PC ở nhà. Nó chung mạng LAN với NAS nên hai máy bắt tay thẳng, gói tin không đi đâu vòng vèo.

Dòng `relay "sin"` là PC ở công ty. Máy đó nằm sau NAT của công ty, con NAS nằm sau NAT của nhà mạng, hai bên không đục được lỗ để gặp nhau nên Tailscale chuyển sang dùng máy chủ trung chuyển gần nhất. `sin` là Singapore.

Vì sao không đục được lỗ thì lệnh `netcheck` nói khá rõ:

```
Report:
	* UDP: true
	* IPv4: yes, 103.xxx.xxx.xxx:25064
	* IPv6: no, but OS has support
	* MappingVariesByDestIP: true
	* HairPinning: false
	* PortMapping:
	* Nearest DERP: Singapore
	* DERP latency:
		- sin: 56.5ms  (Singapore)
		- hkg: 90.7ms  (Hong Kong)
		- blr: 93.7ms  (Bengaluru)
		- tok: 122ms   (Tokyo)
		- fra: 205ms   (Frankfurt)
```

IP công cộng mình che đi, còn lại là số thật.

`MappingVariesByDestIP: true` nghĩa là router nhà mình cấp cổng khác nhau cho mỗi đích đến. Đây là kiểu NAT khó chịu nhất, vì không có cách nào báo trước cổng cho đầu bên kia. Dòng `PortMapping` bỏ trống nghĩa là router không bật UPnP hay NAT-PMP để Tailscale tự xin cổng. Hai thứ cộng lại là lý do máy công ty phải đi vòng qua Singapore.

Đi qua relay thì độ trễ tăng, nhưng dữ liệu vẫn được mã hoá đầu cuối. Máy trung chuyển chỉ đẩy gói đi tiếp, nó không có khoá để đọc.

Muốn nhiều máy nối trực tiếp hơn thì bật UPnP trên router là hướng đầu tiên nên thử. Mình chưa bật nên không kể như đã kiểm chứng.

## Những gì Tailscale không làm được

Quên bật trên điện thoại là mọi thứ đứng im. Trong sổ tay đồng bộ của mình có hẳn một dòng "sync không chạy thì kiểm tra Tailscale trước tiên", viết ra sau khi đã mất thời gian đi tìm lỗi ở chỗ khác.

Bạn phụ thuộc vào máy chủ điều phối của Tailscale. Nó lo việc giới thiệu các máy với nhau và giữ danh sách khoá công khai. Dịch vụ đó gặp sự cố thì các kết nối đang chạy vẫn chạy, nhưng thiết bị mới sẽ không vào được mạng. Đó là cái giá của việc không phải tự dựng gì cả.

Gói cá nhân miễn phí giới hạn số thiết bị và số người dùng. Con số này Tailscale có thay đổi theo thời gian nên mình không dẫn ra đây, bạn xem trang giá của họ cho chắc.

## Vậy có nên dùng không

Nên, nếu bạn muốn vào máy ở nhà từ bên ngoài mà không muốn học cách cấu hình NAT và tường lửa. Cả bốn thiết bị của mình cài xong trong khoảng mười lăm phút, và không phải sửa một dòng nào trên router.

Không nên, nếu bạn có nguyên tắc không để dịch vụ bên thứ ba dính vào hạ tầng của mình. Trường hợp đó thì tự dựng WireGuard là hướng đúng, vì bạn giữ toàn bộ khoá và tự lo việc ghép nối. Mình chưa tự dựng WireGuard nên không kể như trải nghiệm — đây là nhận định dựa trên cách hai thứ hoạt động, không phải kết luận sau khi dùng cả hai.

Chúc các bạn thành công.

## Link tham khảo

[https://tailscale.com/kb/1131/synology](https://tailscale.com/kb/1131/synology)

[https://tailscale.com/kb/1257/connection-types](https://tailscale.com/kb/1257/connection-types)

[https://tailscale.com/kb/1232/derp-servers](https://tailscale.com/kb/1232/derp-servers)

[https://tailscale.com/download](https://tailscale.com/download)
