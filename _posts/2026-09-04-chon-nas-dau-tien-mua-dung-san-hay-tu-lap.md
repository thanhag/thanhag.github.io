---
published: true
title: Chọn NAS đầu tiên - mua hộp dựng sẵn hay tự lắp từ máy chủ cũ
date: '2026-09-04'
categories:
  - server
  - thu-thuat-chung
tags:
  - NAS
  - phần cứng
  - RAID
  - HPE MicroServer
  - TrueNAS
series: "Tự dựng server tại nhà"
series_thu_tu: 4
cap_do: "Cơ bản"
excerpt: >-
  Người mua NAS lần đầu thường so kè **CPU** và **dung lượng ổ cứng**. Máy của mình
  chạy liên tục 27 ngày cho thấy thứ hết trước lại là **RAM** — CPU vẫn nhàn rỗi
  trong khi bộ nhớ chỉ còn trống hơn 500 MB.
toc: true
breadcrumbs: true
permalink: /server/chon-nas-dau-tien-mua-dung-san-hay-tu-lap
---

Ba bài trước của series này đều bắt đầu bằng câu "bạn cần một con NAS". Bài này trả lời câu hỏi đứng trước tất cả: nên mua hộp dựng sẵn hay tự lắp từ máy chủ cũ.

{% include series-nav.html %}

Mình sẽ không dẫn giá, vì giá phần cứng thay đổi liên tục và giá mình mua vài năm trước không còn nói lên điều gì. Thay vào đó là số liệu thật từ máy đang chạy, và một kết luận đi ngược với thứ hầu hết người mua lần đầu quan tâm.

## Hai đường đi

**Mua hộp dựng sẵn** nghĩa là mua một thiết bị đóng hộp của Synology, QNAP hay Asustor. Cắm điện, cắm mạng, mở trình duyệt là dùng được. Phần mềm do hãng làm sẵn, có kho ứng dụng, có bảo hành, có nơi để gọi khi hỏng.

**Tự lắp** nghĩa là mua một máy chủ nhỏ cũ hoặc dựng máy từ linh kiện, rồi cài hệ điều hành lưu trữ lên. Cùng số tiền, bạn được nhiều RAM hơn, CPU khoẻ hơn và nhiều khay ổ hơn. Đổi lại bạn tự lo mọi thứ, và không có bộ phận hỗ trợ nào.

Khác biệt thật không nằm ở tiền. Nó nằm ở chỗ **bạn muốn tiêu thời gian vào việc gì**. Hộp dựng sẵn bán cho bạn thời gian. Tự lắp bán cho bạn phần cứng.

## Máy của mình là gì

Một con **HPE ProLiant MicroServer Gen10**, CPU AMD Opteron X3421 bốn nhân, ba ổ cứng. Đây là dòng máy chủ nhỏ cho văn phòng, mua lại được với giá dễ chịu vì doanh nghiệp thải ra khá nhiều.

Nói thẳng một chuyện để bạn khỏi hiểu nhầm khi đọc các bài khác trong series: máy của mình đang chạy **DSM**, hệ điều hành của Synology, trên phần cứng không phải Synology. Cách này chạy được và nhiều người làm, nhưng nó **trái với điều khoản giấy phép của Synology**, nên mình không hướng dẫn ở đây và cũng không khuyên bạn làm theo.

Nếu bạn tự lắp, đường chính thống là các hệ điều hành sinh ra cho việc đó: **TrueNAS**, **OpenMediaVault**, hoặc **Unraid**. Cả ba đều chạy Docker, tức là mọi thứ mình viết trong series này — Gitea, Vaultwarden, Tailscale — đều dùng được.

## Thứ hết trước không phải CPU

Đây là phần đáng giá nhất của bài, và nó đến từ một máy chạy liên tục chứ không phải từ bảng thông số.

Máy của mình đã chạy **27 ngày không nghỉ**, phục vụ hơn chục container. Tải trung bình:

```
load average: 0.25, 0.31, 0.50   (trên 4 nhân)
```

Bốn nhân mà tải chỉ 0,25. CPU gần như ngồi chơi.

Còn bộ nhớ:

```
              total        used        free      available
Mem:          3.4Gi       2.6Gi       143Mi         547Mi
```

Tổng 3,4 GB, còn trống **547 MB**. Đây mới là chỗ sắp nghẹt.

Nhìn vào các tiến trình ngốn nhất thì hiểu vì sao:

| Dịch vụ | RAM |
|---|---|
| AdGuard Home | 437 MB |
| Java (ứng dụng của DSM) | 379 MB |
| Jellyfin | 169 MB |
| Node | 110 MB |
| Gitea | 90 MB |

Không dịch vụ nào bắt CPU làm việc quá vài giây, nhưng mỗi dịch vụ đều chiếm một phần bộ nhớ **và giữ nguyên phần đó suốt thời gian chạy**. Thêm một container là thêm vài trăm MB nằm đó vĩnh viễn, trong khi CPU chỉ bận vài giây rồi lại rảnh.

Kết luận cho người sắp mua: **đừng so kè CPU, hãy nhìn RAM tối đa mà máy đó hỗ trợ và giá nâng RAM**. Một con NAS hai khe RAM nâng được lên nhiều sẽ sống lâu hơn hẳn một con CPU mạnh mà hàn chết 2 GB.

## Ổ cứng và thứ RAID không làm được

Mình dùng ba ổ **Seagate IronWolf 2 TB**, loại chuyên cho NAS. Ổ chuyên NAS khác ổ máy bàn ở chỗ nó được thiết kế để quay liên tục và để chịu rung khi nhiều ổ nằm sát nhau trong cùng một khay.

Ba ổ đó chạy **RAID 5**, cho ra 3,5 TB dùng được. RAID 5 chịu được **một ổ chết**: rút ổ hỏng ra, cắm ổ mới vào, dữ liệu tự dựng lại.

Nhưng RAID không phải backup, và chỗ này mình đã viết kỹ trong [bài về lưu trữ chứng từ kế toán](/ke-toan/luu-tru-chung-tu-ke-toan-10-nam). Tóm tắt lại: RAID chép mọi thao tác sang mọi ổ ngay lập tức, kể cả thao tác xoá nhầm. Nó chống ổ hỏng, không chống bạn, không chống mã độc, và không chống cháy.

Vì vậy khi tính tiền mua NAS, hãy cộng luôn tiền cho một ổ cứng ngoài để backup. Nó không phải phần tuỳ chọn.

## Bao nhiêu dung lượng là đủ

Chỗ này người ta hay mua thừa nhất.

3,5 TB của mình hiện dùng **53%**, sau nhiều năm chứa ảnh, phim, dữ liệu Docker của hơn chục dịch vụ, và bản sao lưu của mấy máy tính trong nhà.

Không lưu phim thì nhu cầu nhỏ hơn nhiều. Nhớ lại con số ở bài trước: mười năm chứng từ kế toán của một doanh nghiệp nhỏ chỉ khoảng 150–250 GB, còn kho mật khẩu Vaultwarden của mình vỏn vẹn 8,4 MB.

Cách tính hợp lý là ước lượng nhu cầu hiện tại rồi nhân đôi, đừng nhân mười. Ổ cứng năm sau vừa rẻ hơn vừa lớn hơn, và một con NAS còn khay trống thì nâng lúc nào cũng được.

## Vậy nên mua gì

Mình không né câu này bằng cách nói mỗi lựa chọn đều có cái hay riêng.

Chọn **hộp dựng sẵn** nếu đây là lần đầu bạn tự dựng thứ gì, hoặc nếu con NAS sẽ giữ dữ liệu mà người khác trong nhà hay trong công ty phụ thuộc vào. Khi hỏng lúc nửa đêm, việc có một nơi để gọi và một giao diện đã được kiểm thử kỹ đáng giá hơn số tiền tiết kiệm được.

**Tự lắp từ máy chủ cũ** nếu bạn thấy việc mày mò là phần vui chứ không phải phần phiền, và chấp nhận rằng mọi sự cố là việc của mình. Cùng số tiền bạn được nhiều RAM và nhiều khay ổ hơn hẳn — mà RAM lại đúng là thứ hết trước.

Điều mình khuyên cả hai nhóm giống nhau: **mua ổ chuyên NAS**, và **đừng mua con rẻ nhất chỉ có một khe RAM**.

## Nếu làm lại

Thứ mình làm khác là mua nhiều RAM hơn ngay từ đầu.

Lúc chọn máy, mình nhìn số nhân CPU và số khay ổ, rồi nghĩ 4 GB là thoải mái. Hai năm sau, CPU vẫn rảnh còn bộ nhớ chỉ còn 547 MB, và mỗi lần muốn thêm một dịch vụ mình lại phải cân nhắc xem có đủ RAM không. Nâng RAM sau vẫn được, nhưng phải tắt máy, tháo ra, và mua đúng loại máy đó nhận.

Đó là thứ không có trong bảng thông số nào, chỉ hiện ra sau vài trăm ngày chạy thật.

Chúc các bạn thành công.

## Link tham khảo

[https://www.truenas.com/](https://www.truenas.com/)

[https://www.openmediavault.org/](https://www.openmediavault.org/)

[https://www.snapraid.it/faq#raidvsbackup](https://www.snapraid.it/faq#raidvsbackup)
