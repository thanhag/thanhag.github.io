---
published: false
date: 2023-12-30T00:00:00.000Z
categories:
  - ubuntu
  - thu-thuat-chung
tags:
  - ubuntu
  - vps
  - vultr
header:
  teaser: /assets/images/Hướng-dẫn-tạo-VPS-trên-VULTR-chi-tiết-nhất.jpg
  overlay_image: /assets/images/phong-canh-vietnam.jpg
  caption: 'Nguồn ảnh: [**sofsog**](https://sofsog.com)'
excerpt: >-
  Để tải file lên **Google Drive** từ **Ubuntu**, bạn có thể sử dụng giao thức
  cơ bản **WebDAV** hoặc sử dụng các công cụ dòng lệnh như **gdrive** hoặc
  **rclone**.
toc: true
breadcrumbs: true
permalink: /ubuntu/huong-dan-tao-vps-tren-vultr-chi-tiet-nhat
---
Để tải file lên **Google Drive** từ **Ubuntu**, bạn có thể sử dụng giao thức cơ bản **WebDAV** hoặc sử dụng các công cụ dòng lệnh như **gdrive** hoặc **rclone**. 

Hướng dẫn này mình sẽ  thực hiện sao chép một thư mục và tất cả các thư mục con của nó lên **Google Drive** đơn giản nhất sử dụng công cụ dòng lệnh **rclone**. Mình thực hiện từ một **máy tính windows cá nhân** sử dụng giao thức **ssh** kết nối với **Ubuntu server**. Dưới đây là các bước để thực hiện:

## 1. Cài đặt rclone bằng cách thực hiện các bước sau:

Kết nối vào **Ubuntu** của bạn thông qua ssh. Sau đó chạy lệnh:

```terminal
curl https://rclone.org/install.sh | sudo bash
```
## 2. Tiếp theo, thực hiện xác thực bằng cách chạy lệnh sau và làm theo các hướng dẫn trên màn hình:

```terminal
rclone config
```

Màn hình sẽ hiển thị như dưới đây, gõ `n` để chọn `New remote` rồi gõ `Enter`, đặt tên remote, mình đặt là `thanhag`, tiếp tục `Enter`

```terminal
No remotes found, make a new one?
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
Enter name for new remote.
name> thanhag
```

Màn hình sẽ hiển thị một hàng dài để bạn lựa chọn kho lưu trữ mà bạn muốn kết nối, trong hướng dẫn này mình chọn `Google Drive`, bấm số `18` rồi `enter`

```terminal
...
13 / Dropbox
   \ (dropbox)
14 / Encrypt/Decrypt a remote
   \ (crypt)
15 / Enterprise File Fabric
   \ (filefabric)
16 / FTP
   \ (ftp)
17 / Google Cloud Storage (this is not Google Drive)
   \ (google cloud storage)
18 / Google Drive
   \ (drive)
19 / Google Photos
   \ (google photos)
20 / HTTP
   \ (http)
21 / Hadoop distributed file system
   \ (hdfs)
22 / HiDrive
   \ (hidrive)
23 / ImageKit.io
   \ (imagekit)
24 / In memory object storage system.
   \ (memory)
25 / Internet Archive
   \ (internetarchive)
26 / Jottacloud
   \ (jottacloud)
27 / Koofr, Digi Storage and other Koofr-compatible storage providers
   \ (koofr)
28 / Linkbox
   \ (linkbox)
29 / Local Disk
   \ (local)
...
Storage> 18

```

Chương trình sẽ hỏi tiếp về `client_id>` và `client_secret>` cứ `enter` để bỏ qua. Chương trình tiếp tục hỏi về `Phạm vi tùy chọn`, bạn chọn `1` rồi `enter`

```terminal
Option scope.
Comma separated list of scopes that rclone should use when requesting access from drive.
Choose a number from below, or type in your own value.
Press Enter to leave empty.
 1 / Full access all files, excluding Application Data Folder.
   \ (drive)
 2 / Read-only access to file metadata and file contents.
   \ (drive.readonly)
   / Access to files created by rclone only.
 3 | These are visible in the drive website.
   | File authorization is revoked when the user deauthorizes the app.
   \ (drive.file)
   / Allows read and write access to the Application Data folder.
 4 | This is not visible in the drive website.
   \ (drive.appfolder)
   / Allows read-only access to file metadata but
 5 | does not allow any access to read or download file content.
   \ (drive.metadata.readonly)
scope> 1

```

Chương trình lại hỏi `Chỉnh sửa cấu hình nâng cao?` cứ `enter`để bỏ qua

```terminal
Option service_account_file.
Service Account Credentials JSON file path.
Leave blank normally.
Needed only if you want use SA instead of interactive login.
Leading `~` will be expanded in the file name as will environment variables such                                                        as `${RCLONE_CONFIG_DIR}`.
Enter a value. Press Enter to leave empty.
service_account_file>

Edit advanced config?
y) Yes
n) No (default)
y/n>
```

Đến đây là **bước quan trọng**:
- Nếu bạn đang chạy  ứng dụng **rclone** này trên ubuntu có trình duyệt web, thì bạn bấm `y` 
- Nếu bạn đang thực hiện bằng cách sử dụng giao thức **ssh** như đầu bài viết có nói thì bạn bấm `n`. Trong hướng dẫn này **mình thực hiện ssh từ máy tính windows kết nối với Ubuntu server thông qua ssh **, đo đó mình chọn `n`

```terminal
Use web browser to automatically authenticate rclone with remote?
 * Say Y if the machine running rclone has a web browser you can use
 * Say N if running rclone on a (remote) machine without web browser access
If not sure try Y. If Y failed, try N.

y) Yes (default)
n) No
y/n> n
```
Đến bước xác thực, để làm việc này, bạn sẽ cần **rclone** có sẵn trên máy có sẵn trình duyệt web. 

Các bạn để ý màn hình hiển thị có dòng lệnh tương tự như bên dưới: `rclone authorize "drive" "eyJzY29w1hgINyh8aXZlIn0"`, sẽ cần để thực hiện bước tiếp theo. 

```
Option config_token.
For this to work, you will need rclone available on a machine that has a web browser available.
For more help and alternate methods see: https://rclone.org/remote_setup/
Execute the following on the machine with the web browser (same clone version recommended):
        rclone authorize "drive" "eyJzY29w1hgINyh8aXZlIn0"
Then paste the result.
Enter a value.
config_token> 
```
Cứ để y nguyên màn hình dòng lệnh như thế và trở về **máy tính windows cá nhân** để thực hiện bước tiếp theo

## 3. Trên máy windows:

Bạn vào link: [download rclone](https://rclone.org/downloads/) để tải ứng dụng `rclone` về, các bạn lựa chọn đúng hệ điều hành của mình, ở đây mình chọn `Intel/AMD - 64 Bit` dành cho `Windows`

chèn hình

Tải về giải nén ra, ta được như mục như hình:

Chèn hình

Vào thư mục này, giữ phím `Shift` và `click phải chuột` vào vùng trống rồi chọn một chương trình dòng lệnh như `Command Prompt (cmd)` hoặc  `PowerShell`,  trong hướng dẫn này mình chạy bằng `cmd`

Trở lại **ubuntu** để xem cái dòng lệnh cần chạy, nó tương tự như vầy `rclone authorize "drive" "eyJzY29w1hgINyh8aXZlIn0"`

Copy dòng lệnh đó và chạy trên `cmd` của **windows**, chương trình sẽ tự động mở trình duyệt của bạn để bắt đầu xác thực, nếu nó không tự động mở, bạn có thể tự mở bằng cách copy dòng hiển thị trên màn hình dòng lệnh `cmd`tương tự như vầy `http://127.0.0.1:53682/auth?state=XI4vj...` rồi dán vào trình duyệt, gõ `enter`.

Nếu bạn đã đăng nhập sẵn tài khoản `Google Drive` thì chỉ cần chọn đúng tài khoản và chấp nhận cho `rclone` truy cập vào là xong. Ngược lại, thì bạn cần đăng nhập vào tài khoản `Google Drive`của mình để tiếp tục việc xác thực, khi xác thực xong, màn hình `cmd` sẽ hiển thị như hình dưới đây:

Chèn hình

Copy `token`  được đánh dấu trong hình trên, **lưu ý cách copy trên cmd thường tự động ngắt dòng**, tốt nhất là copy rồi dán vào file txt sau đó điều chỉnh sao cho nó chỉ ở trên 1 dòng rồi copy lại.

## 4. Trở lại máy Ubuntu

Lúc này màn hình dòng lệnh trên máy **Ubuntu** đang hiển thị như bên dưới để chờ bạn dán `token` vào

```terminal
config_token> 
```
Dán đoạn `token` vừa copy từ máy tính **windows** vào đó để nó xác thực. Nếu thành công nó sẽ tiếp tục hỏi `Định cấu hình đây là Bộ nhớ dùng chung (Drive nhóm)?` gõ `enter` để bỏ qua, tiếp tục được hỏi `Keep this "thanhag" remote?`, lại `enter` để bỏ qua. Sau đó gõ `q` để thoát khỏi chế độ cài đặt.

```terminal
Configure this as a Shared Drive (Team Drive)?
y) Yes
n) No (default)
y/n>

Configuration complete.
Keep this "thanhag" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d>
Current remotes:
Name                 Type
====                 ====
thanhag              drive
e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q
```
Công cụ dòng lệnh của bạn hiển thị tương tự như trên là cài đặt thành công

## 5. Bắt đầu copy dữ liệu

Sau khi hoàn tất cấu hình, bạn có thể sử dụng lệnh sau để sao chép thư mục và tất cả các thư mục con lên `Google Drive`:

```terminal
rclone copy /path/to/source/folder thanhag:/destination/folder
```

Trong đó: 
- `/path/to/source/folder` là đường dẫn tới thư mục nguồn bạn muốn sao chép.
- `thanhag` là tên cấu hình bạn đã đặt trong bước 2.
- `/destination/folder` là đường dẫn đến thư mục đích trên `Google Drive`. Nếu thư mục đích không tồn tại, **rclone** sẽ tự động tạo nó.

Ví dụ, để sao chép thư mục `/home/user/documents` và tất cả các thư mục con lên Google Drive, bạn có thể chạy lệnh sau:

```terminal
rclone copy /home/user/documents thanhag:/backup/documents
```
Để copy ngược lại, một thư mục từ Google Drive về Ubuntu của bạn, chạy lệnh:

```terminal
rclone copy thanhag:/source/folder /path/to/destination/folder
```

Trong đó:
- `thanhag` là tên cấu hình bạn đã đặt trong bước 2.
- `/source/folder` là đường dẫn đến thư mục nguồn trên Google Drive.
- `/path/to/destination/folder` là đường dẫn đến thư mục đích trên Ubuntu của bạn. Nếu thư mục đích không tồn tại, **rclone** sẽ tự động tạo nó.

Ví dụ, để sao chép thư mục `/backup/documents` từ Google Drive về thư mục `/home/user/documents` trên máy tính, bạn có thể chạy lệnh sau:

```
rclone copy thanhag:/backup/documents /home/user/documents
```

Lưu ý rằng quá trình sao chép có thể mất thời gian, phụ thuộc vào kích thước và số lượng file trong thư mục và các thư mục con.
