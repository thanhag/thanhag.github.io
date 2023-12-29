---
title: "Backup WordPress tự động với BackWPUP"
date: "2016-09-26"
categories: 
  - "wordpress"
tags: 
  - "huong-dan-wordpress"
  - "wordpress"
  - "wordpress-co-ban"
header:
  overlay_image: /assets/images/home_cloud.png
  caption: "Nguồn ảnh: [**sofsog**](https://sofsog.com)" 
  teaser: /assets/images/home_cloud.png
toc: true
breadcrumbs: true
---

Nếu bạn cảm thấy việc [tự backup dữ liệu WordPress thủ công](http://sofsog.com/2016/09/26/huong-dan-backup-du-lieu-wordpress/ "Cách backup (sao lưu) dữ liệu WordPress thủ công") quá mất thời gian của bạn mỗi ngày thì điều đó cũng đúng thôi, bởi mỗi lần như vậy bạn lại phải mất công vào host nén mã nguồn, export file .sql và tải về máy.

Do đó, việc tìm các giải pháp tự động backup định kỳ là điều hiển nhiên, và rất may mắn là trên WordPress không thiếu các giải pháp như vậy. Trong bài này, mình sẽ giới thiệu và hướng dẫn các bạn cách thiết lập cho website tự động backup dữ liệu định kỳ, các dữ liệu đó sẽ bao gồm cả mã nguồn và database (hoặc bạn có thể chọn 1 trong 2) và được lưu trên host hoặc lưu ở một số dịch vụ đám mây như Dropbox chẳng hạn – plugin này tên là BackWPUp, một plugin hoàn toàn miễn phí.

![home_cloud](/assets/images/home_cloud.png)

### Giới thiệu BackWPUp

[**BackWPUp**](https://wordpress.org/plugins/backwpup/ "BackWPUp") là một plugin miễn phí hỗ trợ tự động sao lưu dữ liệu website WordPress thông dụng nhất hiện nay, với số lượng download mỗi ngày gần 2000 lượt.

Sở dĩ plugin này được nhiều người sử dụng như vậy là bởi vì nó vừa dễ sử dụng, tốn ít tài nguyên và hỗ trợ tự động upload dữ liệu được backup qua host khác thông qua FTP, hoặc các dịch vụ lưu trữ đám mây như Dropbox và Amazon S3.

Mặc dù BackWPUp không hỗ trợ tính năng khôi phục dữ liệu nhanh chóng nhưng khi đã có file backup rồi, bạn có thể thực hiện khôi phục dữ liệu thủ công.

#### Các tính năng của BackWPUp gồm

- Backup database
- Backup mã nguồn của website trên host
- Tùy chỉnh thư mục không cần backup
- [Tối ưu database](#) khi backup
- Kiểm tra và sửa lỗi database khi backup
- Lưu danh sách plugin lại thành file text .txt
- Nén dữ liệu lại thành .zip, .tar, .gz,…
- Tùy chỉnh thư mục lưu dữ liệu backup trên host
- Gửi file backup qua FTP của host khác, Dropbox, Amazon S3, RackSpace, Google Drive, Amazon Glacier, SugarSync,…
- Gửi email thông báo kèm file log.

#### Cấu hình host để dùng BackWPUp

Để sử dụng plugin BackWPUp tốt nhất, host của bạn phải cài các phần mềm với cấu hình như sau:

- WordPress 3.4 trở lên.
- PHP 5.3 trở lên.
- Có hỗ trợ mysqli, cURL, nén gz, zip.

Ngoài ra, hãy chắc chắn là thư mục **/wp-content/uploads/** trên host của bạn đang được CHMOD là 755.

#### Cách sử dụng BackWPUp

Sau khi cài plugin và kích hoạt BackWPUp xong, bạn sẽ thấy trên Dashboard có một menu tên BackWPUp ở cột tay trái.

![backwpup-menu-1](/assets/images/backwpup-menu-1.jpg)

Trong đó:

- **Dashboard**: Khu vực chứa các thông tin chung về tiến trình backup trên website.
- **Jobs**: Danh sách các tiến trình backup tự động, mỗi job là một tiến trình backup.
- **Add new Job**: Thêm một tiến trình backup mới.
- **Logs**: Xem nội dung các file log của mỗi lần backup.
- **Backups**: Xem danh sách các file backup trên website.
- **Settings**: Thiết lập plugin.
- **About**: Giới thiệu tổng quan plugin BackWPUp.

Để chắc chắn là cấu hình host của bạn phù hợp với BackWPUp, bạn nên vào phần **BackWPUp -> Settings -> Information** để xem thông tin cấu hình host, ở đó bạn sẽ xem được các phiên bản của từng phần mềm đang chạy trên host.

![backwpup-information-2](/assets/images/backwpup-information-2.jpg)

#### Tạo một job mới

Để tạo một job backup mới, hãy vào **BackWPUp -> Add new Job.**

Tại đây, bạn khai báo các thông tin về tiến trình tự động backup. Phần **Job Destination** là thiết lập nơi cần lưu dữ liệu backup, nếu bạn mới sử dụng thì nên chọn Backup to Folder để nó lưu dữ liệu backup lên host.

Dưới đây là cách thiết lập thông dụng nhất:

![backwpup-newjob-3](/assets/images/backwpup-newjob-3.jpg)

Kế tiếp là chuyển qua tab Schedule để thiết lập lịch backup tự động, bạn hãy chọn **With WordPress cron** và chọn là daily nếu muốn job này chạy mỗi ngày.

![backwpup-schedule-4](/assets/images/backwpup-schedule-4.jpg)

Tới bước này thì bạn đã có thể backup được rồi, nên hãy ấn Save Changes lại. Nếu muốn bạn có thể tự tìm hiểu thêm các chức năng còn lại.

Bây giờ để chạy thử Job, hãy vào BackWPUp -> Jobs -> ấn nút Run now của cái job vừa tạo để nó bắt đầu backup xem có lỗi gì xảy ra không.

![backwpup-runjob-5](/assets/images/backwpup-runjob-5.jpg)

Và nó sẽ bắt đầu backup kèm tiến trình để bạn xem.

![backwpup-running-6](/assets/images/backwpup-running-6.jpg)

Bạn có thể ấn vào nút **Display working log** để xem nó làm việc tới đâu và có lỗi gì màu đỏ không. Nếu nó chạy hết 100%, bạn có thể vào **BackWPUp -> Backup**s để xem file chứa dữ liệu backup của bạn, bạn có thể tải về máy.

![backwpup-backups-7](/assets/images/backwpup-backups-7.jpg)

Trong file dữ liệu backup này sẽ bao gồm mã nguồn website của bạn và file .sql chứa database, bạn có thể [khôi phục bằng cách thủ công](http://sofsog.com/2016/09/26/huong-dan-phuc-hoi-du-lieu-wordpress-thu-cong-restore-wordpress/ "Cách restore (phục hồi) dữ liệu WordPress thủ công") khi cần thiết.

Chúc các bạn thành công!

Nguồn: Thạch Phạm Blog
