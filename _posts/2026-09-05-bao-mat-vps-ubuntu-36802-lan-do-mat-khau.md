---
published: true
title: 'Bảo mật VPS Ubuntu: 36.802 lần bị dò mật khẩu trong 4 ngày'
date: '2026-09-05'
categories:
  - server
  - ubuntu
tags:
  - VPS
  - Vultr
  - Ubuntu
  - SSH
  - ufw
  - bao-mat
excerpt: >-
  Cuối năm 2023 mình viết bài hướng dẫn tạo VPS trên Vultr, và bài đó bảo người đọc đặt
  **`PermitRootLogin yes`** rồi kết thúc. Hôm nay mình mở log của chính con VPS dựng theo
  hướng dẫn đó: **36.802 lần đăng nhập thất bại trong bốn ngày**, từ 449 địa chỉ IP. Đây là
  phần mình đã viết thiếu.
toc: true
breadcrumbs: true
permalink: /server/bao-mat-vps-ubuntu-36802-lan-do-mat-khau
---

Cuối năm 2023 mình viết [bài hướng dẫn tạo VPS trên Vultr](/thu-thuat-chung/he-dieu-hanh/ubuntu/huong-dan-tao-vps-tren-vultr-chi-tiet-nhat). Bài đó dừng lại đúng chỗ nguy hiểm nhất: nó chỉ người đọc mở đăng nhập root qua SSH, rồi hết bài.

Hôm nay mình mở log của chính con VPS dựng theo hướng dẫn đó ra xem.

## Con số làm mình phải viết bài này

Ubuntu ghi mọi lần đăng nhập thất bại vào `/var/log/btmp`. Đọc nó bằng lệnh `lastb`:

```bash
sudo lastb -f /var/log/btmp | wc -l
```

Máy mình trả về **36.802**. Tệp `btmp` được xoay vòng hằng tháng, tệp hiện tại bắt đầu lúc `2026-09-01 00:00:01`, nên đó là số lần trong **bốn ngày chín tiếng**. Trung bình khoảng 350 lần một giờ, tức là cứ mười giây lại có một lần gõ cửa.

Chúng đến từ 449 địa chỉ IP khác nhau:

```bash
sudo lastb | grep "ssh:notty" | awk '{print $3}' | sort -u | wc -l
```

Và đây là tên tài khoản chúng thử nhiều nhất:

```
  14943 root
   1692 admin
   1194 user
    704 ubuntu
    476 debian
    474 test
    414 deploy
    254 postgres
    252 ftpuser
```

Lệnh sinh ra bảng đó:

```bash
sudo lastb | awk '{print $1}' | sort | uniq -c | sort -rn | head -12
```

Nhìn danh sách này thì rõ một điều: **gần một nửa số lần thử là nhắm vào `root`**. Đó không phải là ai đó ghét mình. Đó là các bot quét dải IP của mọi nhà cung cấp VPS, và `root` là cái tên duy nhất chắc chắn tồn tại trên mọi máy Linux. Cho phép đăng nhập root bằng mật khẩu qua SSH là tự tay bỏ đi một nửa bài toán của kẻ tấn công — chúng chỉ còn phải đoán mật khẩu.

Máy mình chưa bị chiếm. Nhưng "chưa bị" không phải là một chiến lược.

## Kiểm tra máy của bạn trước đã

Trước khi sửa gì, hãy xem máy bạn thật sự đang chạy với cấu hình nào. Đây là chỗ mình từng nhầm, và mình nghĩ nhiều người cũng nhầm.

Đừng đọc `/etc/ssh/sshd_config` rồi tin vào đó. Hãy hỏi thẳng OpenSSH:

```bash
sudo sshd -T | grep -E '^port|permitrootlogin|passwordauthentication|pubkeyauthentication'
```

Máy mình trả về:

```
port 22
permitrootlogin yes
passwordauthentication yes
pubkeyauthentication yes
```

`sshd -T` in ra **giá trị đang thực sự có hiệu lực** sau khi đã gộp hết mọi tệp cấu hình. Khác biệt giữa nó và nội dung tệp bạn vừa sửa là chỗ nhiều hướng dẫn trên mạng làm sai.

### Cái bẫy thứ tự tệp cấu hình

Ubuntu từ bản 22.04 tách cấu hình SSH thành nhiều mảnh. Tệp chính `/etc/ssh/sshd_config` có một dòng gọi thư mục con vào:

```
Include /etc/ssh/sshd_config.d/*.conf
```

Quy tắc của OpenSSH là **giá trị đọc được đầu tiên sẽ thắng**, không phải giá trị cuối cùng. Đây là điều ngược với trực giác của gần như mọi người từng sửa tệp cấu hình.

Trên máy mình, dòng `Include` nằm ở **dòng 15**. Còn dòng `PermitRootLogin yes` — đúng cái dòng bài 2023 của mình bảo người đọc thêm vào — nằm ở **dòng 2**. Nó đứng trước, nên nó thắng tất cả. Bạn có tạo bao nhiêu tệp trong `sshd_config.d/` để tắt root cũng vô ích.

Ngược lại, `PasswordAuthentication` không hề xuất hiện trong tệp chính. Giá trị `yes` đang có hiệu lực đến từ một tệp do trình cài đặt của nhà cung cấp sinh ra:

```bash
cat /etc/ssh/sshd_config.d/50-cloud-init.conf
```

```
PasswordAuthentication yes
```

Hệ quả thực tế: một tệp drop-in đặt tên `99-hardening.conf` sẽ **không** sửa được gì, vì `99` sắp sau `50` theo thứ tự chữ cái, mà giá trị đầu tiên mới thắng. Muốn đè lên tệp cloud-init thì tệp của bạn phải sắp **trước** nó.

## Việc 1: Tắt đăng nhập bằng mật khẩu

Đây là việc quan trọng nhất trong bài. Làm xong việc này thì 36.802 lần thử kia trở thành tiếng ồn vô hại, vì không có mật khẩu nào để đoán nữa.

Điều kiện bắt buộc: **bạn phải đăng nhập được bằng khoá SSH trước đã**. Làm ngược thứ tự là tự khoá mình ở ngoài. Trên máy của bạn:

```bash
ssh-keygen -t ed25519 -C "ten-may-cua-ban"
ssh-copy-id root@dia-chi-vps
```

Rồi mở một cửa sổ terminal mới và thử đăng nhập. Nó phải vào thẳng, không hỏi mật khẩu. Kiểm tra khoá đã nằm đúng chỗ:

```bash
grep -c "^ssh-" ~/.ssh/authorized_keys
```

Máy mình trả về `7`. Con số đó hơi nhiều so với nhu cầu — mình sẽ nói ở cuối bài.

Vào được bằng khoá rồi thì tạo tệp drop-in, đặt tên bắt đầu bằng `10-` để nó sắp trước `50-cloud-init.conf`:

```bash
sudo tee /etc/ssh/sshd_config.d/10-bao-mat.conf > /dev/null <<'EOF'
PasswordAuthentication no
KbdInteractiveAuthentication no
PubkeyAuthentication yes
EOF
```

`KbdInteractiveAuthentication` là con đường vòng: tắt mật khẩu mà quên tắt nó thì OpenSSH vẫn có thể hỏi mật khẩu qua cơ chế hỏi đáp của PAM.

**Đừng khởi động lại dịch vụ ngay.** Kiểm tra cú pháp trước:

```bash
sudo sshd -t
```

Lệnh này không in gì nếu tệp cấu hình hợp lệ. Có lỗi thì nó chỉ đúng tệp và số dòng. Sai cú pháp mà cứ khởi động lại thì `sshd` không lên được, và cách duy nhất để cứu là vào bảng điều khiển noVNC của Vultr.

Hợp lệ rồi thì nạp lại cấu hình:

```bash
sudo systemctl reload ssh
```

Dùng `reload` chứ không phải `restart`: `reload` không cắt các phiên SSH đang mở. Nếu có gì sai, bạn vẫn còn cửa sổ hiện tại để sửa lại.

Xác minh:

```bash
sudo sshd -T | grep passwordauthentication
```

Phải ra `passwordauthentication no`.

Và **mở một cửa sổ terminal thứ hai để thử đăng nhập lại**, trong khi cửa sổ cũ vẫn giữ nguyên. Đây là bước nhiều người bỏ qua. Vào được thì mới đóng cửa sổ cũ.

## Việc 2: Cấm root đăng nhập thẳng

Vì `PermitRootLogin yes` nằm ở dòng 2 của tệp chính, tệp drop-in không đè được. Phải sửa thẳng tệp chính:

```bash
sudo sed -i 's/^PermitRootLogin yes/PermitRootLogin prohibit-password/' /etc/ssh/sshd_config
sudo sshd -t && sudo systemctl reload ssh
sudo sshd -T | grep permitrootlogin
```

`prohibit-password` cho phép root vào bằng khoá nhưng cấm bằng mật khẩu. Nó là mức mặc định của Ubuntu và là lựa chọn mình dùng, vì các script quản trị của mình đang chạy dưới root qua khoá.

Chặt hơn nữa là `PermitRootLogin no`, buộc mọi người vào bằng user thường rồi `sudo` lên. Đúng bài hơn về nguyên tắc. Nhưng nó chỉ có ý nghĩa thật khi bạn đã có sẵn một user thường vào được bằng khoá và có quyền `sudo` — chưa có mà đặt `no` là tự khoá mình ra ngoài.

Kiểm tra tài khoản nào trên máy còn đặt mật khẩu:

```bash
sudo passwd -S root
```

Chữ cái thứ hai trong kết quả là thứ cần nhìn: `P` nghĩa là tài khoản có mật khẩu dùng được, `L` là đã khoá, `NP` là không có mật khẩu. Máy mình ra `P` — root có mật khẩu, và trong bốn ngày qua có 14.943 lần người ta thử đoán đúng nó.

## Việc 3: Tường lửa chỉ mở đúng cổng cần

Ubuntu có sẵn `ufw`. Thứ tự lệnh ở đây quan trọng hơn bản thân các lệnh:

```bash
sudo ufw allow 22/tcp
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
```

**Câu `allow 22/tcp` phải chạy trước `enable`.** Bật tường lửa với chính sách chặn hết mà chưa mở cổng SSH thì phiên của bạn rớt ngay lập tức, và lại phải vào noVNC.

Khi chạy `ufw enable` nó sẽ hỏi:

```
Command may disrupt existing ssh connections. Proceed with operation (y|n)?
```

Đã mở cổng 22 ở bước trên thì cứ `y`.

Xem kết quả:

```bash
sudo ufw status verbose
```

```
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
```

Đúng một cổng mở, và mở cho cả IPv4 lẫn IPv6. Dòng `(v6)` đáng để ý: VPS Vultr có địa chỉ IPv6, và một tường lửa chỉ chặn IPv4 là một tường lửa có cửa sau.

Sau này cài thêm dịch vụ gì thì mở thêm cổng đó, mỗi lần một cổng, và ghi lại lý do. Cách chắc chắn nhất để một máy chủ trở nên hở là mở cổng lúc thử nghiệm rồi quên đóng.

Đổi cổng SSH sang một số lạ thì sao? Nó cắt được gần hết log rác, vì bot quét cổng 22 là chính. Mình không làm, vì nó không thêm bảo mật thật một khi đã tắt mật khẩu — nó chỉ làm log sạch hơn, đổi lại mọi công cụ và mọi người trong nhóm phải nhớ thêm một con số.

## Việc 4: Swapfile cho máy 4 GB

Việc này không liên quan tới bảo mật, nhưng nó là thứ thứ hai làm hỏng một VPS mới, sau việc bị chiếm. Máy hết RAM thì nhân Linux giết tiến trình ngốn nhiều nhất, thường đúng là thứ bạn đang chạy.

Máy mình có 2 nhân CPU, đĩa 75 GB, và bộ nhớ như sau:

```
               total        used        free      shared  buff/cache   available
Mem:            3910        2213         352         0        1637        1696
Swap:           2399         323        2076
```

RAM còn trống chỉ 352 MB, nhưng cột `available` là 1.696 MB — phần lớn chỗ "đã dùng" là bộ đệm đĩa, nhân sẽ trả lại khi cần. **Cột đáng nhìn là `available`, không phải `free`.**

Swap đang dùng 323 MB trên 2.399 MB. Có dùng, nhưng chưa sâu. Máy mình có sẵn swapfile 2,3 GB; nếu máy bạn chưa có thì tạo như sau:

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile swap swap defaults 0 0' | sudo tee -a /etc/fstab
```

`chmod 600` là bắt buộc. Swapfile chứa nội dung bộ nhớ đã bị đẩy ra đĩa, trong đó có thể có mật khẩu và khoá; để nó cho mọi user đọc được là hỏng. Dòng thêm vào `/etc/fstab` để swap tự bật lại sau khi khởi động.

Kiểm tra:

```bash
swapon --show
```

```
NAME      TYPE SIZE   USED PRIO
/swapfile file 2.3G 323.7M   -2
```

Còn một tham số nữa nên chỉnh:

```bash
cat /proc/sys/vm/swappiness
```

Mặc định của Ubuntu là `60`. Máy mình là `10`, đặt trong `/etc/sysctl.conf` dòng 65. Số này quyết định nhân sốt sắng đến mức nào trong việc đẩy dữ liệu ra swap: `60` nghĩa là nó đẩy khá sớm, `10` nghĩa là chỉ đẩy khi thật sự cần. Trên máy ảo có đĩa chậm hơn RAM rất nhiều, `10` cho cảm giác mượt hơn hẳn. Đặt cố định:

```bash
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

Swap là lưới an toàn, không phải RAM giá rẻ. Máy phải dùng swap thường xuyên là máy cần thêm RAM.

## Việc 5: Bật cập nhật bảo mật tự động

Ubuntu Server cài sẵn `unattended-upgrades`, nhưng nên xác nhận nó đang bật:

```bash
cat /etc/apt/apt.conf.d/20auto-upgrades
```

```
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
```

Hai dòng, cùng giá trị `1`, là đủ. Thiếu tệp này hoặc giá trị `0` thì bật bằng:

```bash
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

Xem thử nó sẽ làm gì mà chưa cài gì cả:

```bash
sudo unattended-upgrades --dry-run --debug
```

Và đây là chỗ mình bị hớ. Cập nhật tự động **cài** gói mới, nhưng nó không khởi động lại máy. Với bản vá nhân Linux, không khởi động lại thì nhân cũ vẫn đang chạy — tức là bản vá chưa có tác dụng gì cả:

```bash
uname -r
cat /var/run/reboot-required.pkgs
```

```
6.8.0-137-generic
linux-image-6.8.0-138-generic
linux-base
linux-image-6.8.0-139-generic
linux-base
```

Máy mình đang chạy nhân `137` trong khi `138` và `139` đã cài xong từ lúc nào không rõ. Chậm hai phiên bản nhân, trên một máy mà mình vẫn đinh ninh là "đã bật cập nhật tự động rồi".

Tệp `/var/run/reboot-required` tồn tại là dấu hiệu cần khởi động lại. Kiểm tra nhanh mỗi khi SSH vào:

```bash
[ -f /var/run/reboot-required ] && echo "CAN KHOI DONG LAI"
```

Muốn máy tự khởi động lại vào giờ vắng thì sửa `/etc/apt/apt.conf.d/50unattended-upgrades`:

```
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-Time "04:00";
```

Mình chưa bật cái này, vì máy đang chạy một dịch vụ mà mình muốn tự tay canh lúc nó khởi động lại. Đó là một lựa chọn có giá của nó: đổi lấy quyền kiểm soát bằng việc phải nhớ, và mình vừa chứng minh là mình quên.

## Còn fail2ban thì sao

Máy mình không cài `fail2ban`. Nói rõ để bạn không tưởng là mình bỏ sót.

`fail2ban` đọc log, thấy một IP thất bại nhiều lần thì chặn IP đó một khoảng thời gian. Nó hữu ích thật, nhưng hãy nhìn đúng vị trí của nó: **khi đã tắt đăng nhập bằng mật khẩu, 36.802 lần thử kia không còn cơ hội nào cả.** Chúng chỉ tốn một ít CPU và làm log phình ra — tệp `auth.log` của mình đã 23 MB cho sáu ngày.

Nên `fail2ban` với mình là việc dọn dẹp, không phải việc bảo mật, và nó xếp sau năm việc trên. Ai muốn cài thì trên Ubuntu 24.04:

```bash
sudo apt install fail2ban
```

Cấu hình đặt trong `/etc/fail2ban/jail.local` chứ đừng sửa `jail.conf`, vì tệp đó bị ghi đè mỗi lần nâng cấp gói.

## Tự chấm điểm máy mình

Đây là hiện trạng con VPS của mình lúc viết bài, chưa sửa gì:

| Việc | Trạng thái | Mức nguy hiểm |
|---|---|---|
| Tường lửa chỉ mở cổng 22 | Đã làm | — |
| Swapfile và `swappiness` | Đã làm | — |
| Cập nhật tự động đang bật | Đã làm | — |
| Đăng nhập bằng mật khẩu | **Vẫn bật** | Cao |
| Root đăng nhập thẳng, có mật khẩu | **Vẫn bật** | Cao |
| Khởi động lại sau vá nhân | **Chậm 2 phiên bản** | Vừa |
| 7 khoá trong `authorized_keys` | Chưa rà lại | Vừa |

Ba dòng đầu là những việc mình làm đúng ngay từ đầu và quên mất là mình đã làm. Bốn dòng dưới là những việc mình tưởng đã xong.

Cái mình thấy đáng nói nhất là dòng cuối. Bảy khoá công khai trong `authorized_keys`, tích tụ qua nhiều năm, mỗi lần mua máy mới lại thêm một cái. Mình không còn nhớ chắc từng khoá thuộc máy nào, và trong số đó gần như chắc chắn có khoá của máy mình đã bán hoặc cài lại từ lâu. Tắt mật khẩu xong thì `authorized_keys` trở thành cánh cửa duy nhất — mà mình lại chưa từng kiểm kê nó lần nào.

Rà bằng lệnh này, phần ghi chú cuối mỗi dòng khoá thường là tên máy lúc tạo:

```bash
awk '{print $NF}' ~/.ssh/authorized_keys
```

Khoá nào không nhận ra thì xoá. Xoá nhầm khoá của máy đang dùng thì phiên SSH hiện tại vẫn sống, nên hãy giữ nguyên cửa sổ đó cho tới khi thử đăng nhập lại thành công từ cửa sổ khác.

## Cập nhật cùng ngày: mình đã sửa hai dòng đỏ

Viết xong bài thì không còn lý do gì để bảng trên giữ hai dòng "Vẫn bật". Mình làm đúng Việc 1 và Việc 2, và phần đáng kể lại nhất là cách tự bảo hiểm.

Trước khi đụng vào gì, sao lưu tệp cấu hình rồi cài một cái chốt tự phục hồi. Ý tưởng đơn giản: nếu sau năm phút mình không tạo được tệp đánh dấu `/root/.ssh_ok` — nghĩa là mình đã tự khoá mình ở ngoài — thì máy tự khôi phục cấu hình cũ:

```bash
cp -a /etc/ssh/sshd_config /root/sshd_config.bak
rm -f /root/.ssh_ok
nohup bash -c 'sleep 300; [ -f /root/.ssh_ok ] || {   cp -a /root/sshd_config.bak /etc/ssh/sshd_config;   rm -f /etc/ssh/sshd_config.d/10-bao-mat.conf;   systemctl reload ssh; }' >/dev/null 2>&1 &
```

Sửa xong và xác minh vào được thì tháo chốt:

```bash
touch /root/.ssh_ok
```

Cái chốt này đã cứu mình thật, ngay trong lần chạy đầu. Một bước ở giữa bị hỏng, và đúng năm phút sau máy tự trả về nguyên trạng, không mất gì và không cần mình can thiệp. Nếu bạn chỉ lấy một thứ từ bài này, hãy lấy đoạn trên: **mọi thay đổi cấu hình SSH từ xa đều nên có đường lùi tự động.**

Lần chạy thứ hai trót lọt. `sshd -T` sau khi nạp lại:

```
permitrootlogin without-password
pubkeyauthentication yes
passwordauthentication no
kbdinteractiveauthentication no
```

`without-password` là tên cũ của `prohibit-password`. OpenSSH in ra tên cũ, ý nghĩa y hệt.

Rồi tự tấn công máy mình để kiểm chứng, ép client chỉ được phép dùng mật khẩu:

```bash
ssh -o PubkeyAuthentication=no -o PreferredAuthentications=password root@dia-chi-vps
```

```
root@dia-chi-vps: Permission denied (publickey).
```

Máy chỉ còn chào đúng một phương thức. Đừng bỏ bước này: `sshd -T` cho biết cấu hình **nói** gì, còn lệnh trên cho biết máy chủ **làm** gì. Hai thứ đó lệch nhau thường xuyên hơn bạn tưởng — cả bài này sinh ra từ một lần lệch như vậy.

Hai dòng còn lại trong bảng thì vẫn còn nguyên đó. Nhân vẫn chậm hai phiên bản vì mình chưa chọn được lúc khởi động lại, và bảy cái khoá vẫn chưa rà. Ghi ra đây để lần sau mở bài này còn thấy mình nợ cái gì.

## Thứ tự nên làm

Nếu bạn chỉ có mười lăm phút, làm theo đúng thứ tự này:

Đưa khoá SSH lên và **xác minh vào được bằng khoá**. Rồi tắt `PasswordAuthentication`. Rồi đặt `PermitRootLogin prohibit-password`. Ba việc đó xử lý gần hết rủi ro thực tế. Tường lửa và swapfile làm sau cũng được, còn `fail2ban` thì lúc nào rảnh.

Bài hướng dẫn năm 2023 của mình sai ở chỗ nó coi việc dựng được máy là xong. Dựng xong mới là lúc máy bắt đầu bị quét, và trong bốn ngày nó hứng 36.802 lần gõ cửa mà mình không hề biết cho tới hôm nay.

Chúc các bạn thành công.

## Link tham khảo

[https://man.openbsd.org/sshd_config](https://man.openbsd.org/sshd_config)

[https://help.ubuntu.com/community/UFW](https://help.ubuntu.com/community/UFW)

[https://wiki.debian.org/UnattendedUpgrades](https://wiki.debian.org/UnattendedUpgrades)
