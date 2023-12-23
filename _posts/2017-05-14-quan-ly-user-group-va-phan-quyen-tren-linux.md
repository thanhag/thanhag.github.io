---
title: "Quản lý User, group và phân quyền trên linux"
date: "2017-05-14"
categories: 
  - "he-dieu-hanh"
  - "kali-linux"
  - "thu-thuat-chung"
tags: 
  - "group-va-phan-quyen-tren-linux"
  - "kali-linux"
  - "linux"
  - "quan-ly-user"
  - "user-trong-linux"
header:
  image: /assets/images/mode.png
  teaser: /assets/images/mode.png
toc: true
breadcrumbs: true
---

**1.** **User**

User là người có thể truy cập đến hệ thống.

User có **username** và **[password](http://www.gocit.vn/bai-viet/tag/password/ "Posts tagged with Password")**.

Có hai loại user: **super user** và **regular user**.

Mỗi user còn có một định danh riêng gọi là **UID**.

Định danh của người dùng bình thường sử dụng giá trị bắt đầu từ 500.

**2.** **Group**

Group là **tập hợp nhiều user** lại.

Mỗi user luôn là thành viên của một group.

Khi **tạo một user thì mặc định một group được tạo ra**.

Mỗi group còn có một định danh riêng gọi là **GID**.

Định danh của group thường sử dụng giá trị bắt đầu từ 500.

**3.** **Tập lệnh quản lý User và Group**

- Tạo User:

**Cú pháp:** #useradd \[option\] <username> -c “Thông tin người dùng” -d <Thư mục cá nhân> -m : Tạo thư mục cá nhân nếu chưa tồn tại -g <nhóm của người dùng> **Ví dụ:** #**useradd** –c “Nguyen Van A – Server Admin” –g serveradmin vana

- Thay đổi thông tin cá nhân:

**Cú pháp:** #**usermod** \[option\] <username>

Những option tương tự **Useradd**

**Ví dụ:** #usermod –g kinhdoanh vana  _//chuyển vana từ nhóm server admin sang nhóm kinh doanh._

- Xóa người dùng

  **Cúpháp** : #**userdel** \[option\] <username>

**Vídụ :**  #userdel  –r  vana

- Khóa/Mở khóa người dùng

**passwd –l <username>**  **/**  **passwd –u <username>**

**usermod –L <username>** /  **usermod –U <username>**

Trong /etc/shadow có thể khóa tài khoản bằng cách thay từ khóa x bằng từ khóa \*.

- Tạo nhóm:

**Cú pháp:** #**groupadd** <groupname>

**Ví dụ:** #groupadd serveradmin

- Xóa nhóm

**Cú pháp:** #**groupdel** <groupname>

**Ví dụ:** #groupdel <serveradmin>

- Xem thông tin về User và Group

**Cú pháp:** #**id** <option> <username>

**Ví dụ:** #id -g vana //xem GroupID của user vana

**Cú pháp:** #**groups** <username>

**Ví dụ:** #groups vana //xem tên nhóm của user vana

**4.  Những file liên quan đến User và Group**

_**#/etc/passwd**_

Mỗi dòng trong tập tin gồm có 7 trường, được phân cách bởi dấu hai chấm.

_**#/etc/group**_

Mỗi dòng trong tập tin gồm có 4 trường, được phân cách bởi dấu hai chấm.

_**#/etc/shadow**_

Lưu mật khẩu đã được mã hóa và chỉ có user [root](http://www.gocit.vn/bai-viet/tag/root/ "Posts tagged with Root") mới được quyền đọc.

**5.  Quyền hạn**

![Quyen han user trong linux](/assets/images/mode.png)

Trong Linux có 3 dạng đối tượng :

- Owner (người sở hữu).
- Group owner (nhóm sở hữu).
- Other users (những người khác).

Các quyền hạn :

- Read – r – 4  : cho phép đọc nội dung.
- Write – w – 2  : dùng để tạo, thay đổi hay xóa.
- Execute – x – 1  : thực thi chương trình.

Vídụ : Với lệnh ls –l ta thấy :

\[root@task ~\]# ls -l
total 32
-rw-------. 1 root root  1416 Jan 10 14:06 anaconda-ks.cfg
-rw-r--r--. 1 root root 15522 Jan 10 14:06 install.log
-rw-r--r--. 1 root root  5337 Jan 10 14:06 install.log.syslog
drwxr-xr-x  6 root root  4096 Feb  9 10:02 softs

Ngoài ra, chúng ta có thể dùng số.

Vídụ : quyền r, w, x : 4+2+1 = 7

_Tổ hợp 3 quyền trên có giá trị từ 0 đến 7._

 **Các lệnh liên quan đến quyền hạn**

- **Lệnh** _**Chmod**_ : dùng để cấp quyền hạn.

Cú pháp : #**chmod**  <specification> <file>

_Ví dụ:_ #**chmod** 644 baitap.txt   _//cấp quyền cho owner có thể ghi các nhóm các chỉ có quyền đọc với file taptin.txt_

- _**Lệnh Chown :**_ dùng thay đổi người sở hữu.

 Cú pháp : #**chown**  <owner>  <filename>

- **_Lệnh Chgrp_** : dùng thay đổi nhóm sở hữu.

Cú pháp : #**chgrp**  <group>  <filename>

\*  _**Quyền hạn**_1\. Sơ lựơc về quyềnTrên Linux, quyền trên files hoặc thư mục được ghi vào trong inode của file hoặc thư mục đó. Để dễ quản lý, Linux xem mọi thứ như là file. Để xem quyền, chúng ta có thể sử dụng lệnh “ls -l” như trong hình sau:![Image](https://dacchieu.files.wordpress.com/2012/12/quyenhan1.gif?w=360&h=185)Cột đầu tiên trong kết quả của lệnh ls -l thể hiện cho quyền hạn. Phần này bao gồm 10 bit:– bit 1: thể hiện kiểu file (vd: “-” file thường, “d” thư mục,…) – 9 bit còn lại chia làm 3 nhóm, mỗi nhóm có 3 bit: +owner: Quyền của user mà owner của file này. +group: Quyền của những users thuộc group mà owner của file này. +other: Quyền của tất cả các user khác trên máy.Trong mỗi nhóm (3 bit) thể hiện cho các quyền đọc (r), ghi (w), thực thi (x). Nếu nơi nào không có quyền sẽ được ghi là denied (-).

<table border="0"><tbody><tr><td>Ký hiệu</td><td>file</td><td>thư mục</td></tr><tr><td>–</td><td>Không có quyền</td><td>Không có quyền</td></tr><tr><td>r</td><td>Có thể đọc file, ví dụ dùng lệnh cat, more, ….</td><td>Có thể xem nội dung trong thư mục, ví dụ dùng lệnh ls.</td></tr><tr><td>w</td><td>Có thể thêm, bớt nội dung trong file.</td><td>Có thể tạo thêm hoặc xóa đi file hoặc thư mục con của thư mục này.</td></tr><tr><td>x</td><td>Có thể thực thi file này, chỉ dùng trong trường hợp đây là program hoặc script.</td><td>Có thể “đứng” trong thư mục được, vi dụ cd vào thư mục này.</td></tr></tbody></table>

**Thay đổi quyền**

Chỉ có user có quyền root, hoặc user là owner của file mới có thể thay đổi quyền của file đó. Lệnh chuyển quyền:

chmod mode file

Trong đó “mode” có thể được viết theo 2 cách: symbolic hoặc octal mode

a. symbolic mode

![Image](https://dacchieu.files.wordpress.com/2012/12/quyenhan2.gif?w=453&h=292)

Trong mode này chúng ta có thể thêm (+), bớt (-), gán (=) các quyền (r w x) cho từng nhóm (u g o) hoặc cho cả 3 nhóm (a). Ưu điểm của mode này là chúng ta có thể kế thừa quyền củ.

vd: chmod g-w myfile <=bỏ quyền write trên group. chmod u+x,go+r <=thêm quyền thực thi cho owner, quyền đọc cho group và other.

b. octal mode

Trong mode này, mổi quyền được thể hiện bằng 1 số tương ứng:

– : 0 x : 1 w : 2 r : 4

Quyền sẽ được tính tổng trên từng nhóm, vd: r(4)+w(2)+x(1)=7. Khi gán quyền phải gán cho cả 3 nhóm.

ví dụ quyền và số octal tương ứng:

644 rw-r–r– 751 rwxr-x–x 775 rwxrwxr-x 777 rwxrwxrwx

Dùng lệnh: chmod

chmod 644 myfile <=gán quyền 644 trên file.

Với cách sử dụng như trên, khi dùng octal mode chúng ta không kế thừa được quyền củ, nhưng bù lại chúng ngắn gọn dễ xài. ![:D](/assets/images/02.gif " ")

**Quyền mặc định**

Khi chúng ta tạo ra file hoặc thư mục, mặc nhiên hệ thống sẽ gán cho 1 quyền mặc định, trong đó:

File: 666 (rw-rw-rw-) Thư mục: 777 (rwxrwxrwx)

Để thay đổi quyền mặc định khi tạo file và thư mục, hệ thống cung cấp cho chúng ta một công cụ đó là umask. Như vậy, khi tạo ra file hoặc thư mục, thì quyền mặc định được tính như sau:

File: 666 – umask Thư mục: 777 – umask

Ví dụ, nếu umask=022 thì quyền mặc định trên file và thư mục sẽ là (644) và (755)

![Image](https://dacchieu.files.wordpress.com/2012/12/quyenhan3.gif?w=226&h=259)

Lưu ý: ví dụ như umask=123, thì quyền mặc định cho file sẽ là (644) chứ không phải (543) nhé. Lý do vì sao bạn thử tìm hiểu xem

Chúng có thể xem hoặc thay đổi giá trị umask như trong ví dụ sau:

$ umask
022
$ umask 027
$ umask
027

**Thay đổi Owner**

Chúng ta có thể thay đổi chủ sở hữu của file (owner) bằng lệnh sau:

chown -R \[user.group\] files

\-R : đổi tất cả files và thư mục con.

Lệnh này cũng cho phép thay đổi owner chỉ riêng user hoặc group hoặc cả hai.

vd:

\# ls -l
total 0
-rw-r–r– 1 nhsang nhsang 0 Nov 23 16:46 file1
-rw-r–r– 1 nhsang nhsang 0 Nov 23 16:46 file2
-rw-r–r– 1 nhsang nhsang 0 Nov 23 16:46 file3

# chown oravn file1 <=đổi user owner

# chown .dba file2 <=đổi group owner

# chown oravn.dba file3 <=đổi cả user và group owner

# ls -l

total 0
-rw-r–r– 1 oravn nhsang 0 Nov 23 16:46 file1
-rw-r–r– 1 nhsang dba 0 Nov 23 16:46 file2
-rw-r–r– 1 oravn dba 0 Nov 23 16:46 file3

#

Lưu ý là bạn chỉ có thể dùng lệnh này khi bạn là user mà owner của file này hoặc user có quyền root.

Liên quan đến phần quyền hạn, chúng ta còn 3 quyền đặc biệt là SUID, SGID và Sticky bit. Các bạn vui lòng tham khảo thêm trong các tài liệu tiếng Anh nhé.

IV. Tạo Links

Mục đích của links trên Linux là tạo ra nhiều tên hoặc alias cho file và thư mục. Có 2 loại links: hard link và soft link (symbolic link) Để tạo link chúng ta sử dụng lệnh sau:

ln \[-s\] filename linkname

\-s : tạo softlink

**6.Hard link**

Nhằm tạo ra nhiều file hoặc thư mục có cùng sử dụng chung 1 inode. Do đó các files hoặc thư mục này phải cùng nằm chung trên 1 partition (chung bảng inode). Tuy nhiên, chúng ta không thể dùng lệnh để tạo thêm hard link cho thư mục!

Ví dụ sau tạo thêm 1 file (hardlink) “hrdoravn.txt” cùng dùng chung inode (3074178) với file “oravn.txt”. Các bạn để ý con số hardlink-count từ 1 đã tăng lên 2 trong lệnh “ls -i” (con số đứng sau chuổi quyền hạn).

$ ls -i
3074178 oravn.txt
$ ls -li
total 4
3074178 -rw-rw-r– 1 nhsang nhsang 1 Nov 23 15:54 oravn.txt
$ ln oravn.txt hrdoravn.txt
$ ls -li
total 8
3074178 -rw-rw-r– 2 nhsang nhsang 1 Nov 23 15:54 hrdoravn.txt
3074178 -rw-rw-r– 2 nhsang nhsang 1 Nov 23 15:54 oravn.txt
$

**2\. Soft link**

Nhằm tạo alias tới tên file hiện có, gần giống như shortcut trên MS Windows. Do đó bạn có thể link tới bất kỳ file nào trên cây thư mục. Điểm khác nhau cơ bản giữa softlink và shortcut chính là trong softlink tới thư mục bạn có thể “nhảy” vào đó đứng được, hay nói cách khác là có thể cd vào “thư mục” link được. Lưu ý khi tạo softlink, bạn nên ghi đường dẫn tuyệt đối cho tên source-file. Điều này sẽ giúp bạn khi bị lổi khi di chuyển file hoặc link đi nới khác.

Ví dụ sau tạo 1 softlink tới file và một softlink tới thư mục, sau đó cd vào trong softlink của thư mục.

$ ln -s /home/nhsang/oravn/oravn.txt sftoravn.txt
$ ls -li
total 8
3074178 -rw-rw-r– 2 nhsang nhsang 1 Nov 23 15:54 hrdoravn.txt
3074178 -rw-rw-r– 2 nhsang nhsang 1 Nov 23 15:54 oravn.txt
3074179 lrwxrwxrwx 1 nhsang nhsang 28 Nov 23 16:11 sftoravn.txt –Image /home/nhsang/oravn/oravn.txt

$ mkdir mydir
$ ln -s /home/nhsang/oravn/mydir sftmydir
$ cd sftmydir/
$ pwd
/home/nhsang/oravn/sftmydir
$
