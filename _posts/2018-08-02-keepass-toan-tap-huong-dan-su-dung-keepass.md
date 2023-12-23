---
title: "KeePass toàn tập - Hướng dẫn sử dụng KeePass từ a đến z"
date: "2018-08-02"
categories: 
  - "phan-mem"
  - "thu-thuat-chung"
tags: 
  - "ckp-keepass-integration-for-chrome"
  - "huong-dan-su-dung-keepass"
  - "huong-dan-su-dung-keepass-tu-a-den-z"
  - "keepass"
  - "keepass-toan-tap"
  - "keepass-tu-a-den-z"
  - "keepass-tusk"
  - "lastpass"
header:
  image: /assets/images/1.-huong-dan-su-dung-keepass-sofsog.com_.jpg
  teaser: /assets/images/1.-huong-dan-su-dung-keepass-sofsog.com_.jpg
toc: true
breadcrumbs: true
---

Trong thời đại công nghệ hiện nay, việc nhớ các loại password, mật khẩu, thông tin đăng nhập là một cực hình đối với hầu hết mọi người thường xuyên tiếp xúc với internet. Như vậy, một câu hỏi đặt ra là có cách nào để quản lý tất cả các thông tin đăng nhập, password mật khẩu, ... một cách bảo mật, an toàn.

Tất nhiên, có nhiều phần mềm hỗ trợ việc này, trả phí có, miễn phí cũng có. Đơn cử như một phần mềm khá nổi tiếng là **Lastpass** , phần mềm này khá hay, có thể đồng bộ giữ máy tính để bàn, điện thoại (android, ios). Mình sử dụng phần mềm này khá lâu rồi, chỉ dùng bản miễn phí thôi, nói chung mọi thứ đều ổn. Nhưng có 1 vấn đề, mặc dù nhà phát hành nói, mọi thông tin đều được bảo mật hoàn toàn vì được mã hóa bằng mật khẩu chính, nhưng ai mà biết được ... (^\_^). Có lẽ mình hơi đa nghi một tý.

Vậy, lại đặt ra câu hỏi là, có phần mềm nào mã nguồn mở (có thể kiểm tra mã nguồn), đáp ứng được những điều đã nói ở trên hay không ? Và bên dưới là câu trả lời.

## **GIỚI THIỆU KEEPASS**

**KeePass** là một phần mềm mã nguồn mở miễn phí giúp lưu trữ tất cả mật khẩu, thông tin cá nhân. Chương trình này lưu trữ password của bạn trong một file cơ sở dữ liệu (CSDL) được mã hóa ở mức cao.

![Huong dan su dung keepass sofsog.com](/assets/images/1.-huong-dan-su-dung-keepass-sofsog.com_.jpg)

Chương trình cũng cho phép bạn in danh sách mật khẩu hoặc cửa sổ hiện hành. Menu ngữ cảnh của danh sách password cho phép bạn copy nhanh password hoặc user name vào bộ nhớ của Windows. Bạn cũng có thể thực hiện thao tác tìm kiếm trên chương trình.

Vì **Keepass** là mã nguồn mở nên nó đã được nhiều lập trình viên kiểm tra, và có thể nói nó đảm bảo hơn cái thằng **lastpass** đã nói ở trên về độ an toàn thông tin.

## HƯỚNG DẪN SỬ DỤNG KEEPASS TRÊN WINDOW

### Bước 1: Download **keepass**

Trang chủ **[KeePass](http://keepass.info/download.html) hoặc link trực tiếp  [Keepass](https://sourceforge.net/projects/keepass/files/KeePass%202.x/2.39.1/KeePass-2.39.1.zip/download)**

![Hướng dẫn sử dụng KeePass Sofsog.com](/assets/images/2.-Hướng-dẫn-sử-dụng-KeePass-Sofsog.com_.jpg)

Các bạn có thể download bản cài đặt, hoặc bản portable đều được, mình thì thích bản portable hơn.

Tải về xong giải nén, cài đặt như bình thường. Đối với bản portable thì chỉ cần giải nén là sài được.

### **Bước 2:** Tạo mới một CSDL

Khởi động chương trình lên

![Hướng dẫn sử dụng KeePass Sofsog.com](/assets/images/3.-Hướng-dẫn-sử-dụng-KeePass-Sofsog.com_.jpg)

Chọn lệnh **File > New (hoặc Ctrl+N)** , màn hình **Create New Database** hiện ra

![Hướng dẫn sử dụng KeePass Sofsog.com](/assets/images/4.-Hướng-dẫn-sử-dụng-KeePass-Sofsog.com_.jpg)

Chọn đường dẫn cần lưu trữ và đặt tên Database trong ô **File Name ,** ví dụ tên file mình đặt là : **SofsogPass.kdbx** , phần mở rộng là .kdbx mặc định của nó, đừng quan tâm, cứ để y nguyên.

**Lưu ý quan trọng:** Để sử dụng _**KeePass**_ một cách hiệu quả trên cả PC, Smartphones Bạn nên lưu file này ở thư mục mà bạn dùng để đồng bộ hóa lên các dịch vụ lưu trữ đám mây như Dropbox, Google Drive, ... (Ví dụ trong bài viết mình sử dụng Dropbox).

Click nút save, cửa sổ **Create Composite Master key** hiện ra.

![Hướng dẫn sử dụng KeePass Sofsog.com](/assets/images/5.-Hướng-dẫn-sử-dụng-KeePass-Sofsog.com_.jpg)

### **Bước 3:** Đặt mật khẩu (quan trọng)

Trong bảng **Create Composite Master Key** hiện ra, có 3 hình thức để bạn đặt mật khẩu cho CSDL của mình:

- **Master Password:** Đăng nhập bằng mật khẩu mình khuyến khích các bạn dùng lựa chọn này (Master Password) để dễ sử dụng. Lần đầu tiên này bạn phải đặt mật khẩu cho file CSDL, bạn gõ 02 lần giống nhau vào tương ứng 02 ô **Master Password** và **Repeat password** sau đó bấm nút OK.
- **Key file/Provider:** Tạo một file làm chìa khóa để đăng nhập, nói cách khác, thay vì nhập mật khẩu, bạn có thể mở file này lên là vào được.
- **Windows user account:** Dùng chính tài khoản đăng nhập Windows để làm tài khoản đăng nhập KeePass.

Mình thì chọn **Master Password,** các bạn phải nhớ kỹ **Master Password** này, và chỉ cần nhớ một mính nó, vì các **Password và thông tin** sau này bạn lưu trữ bằng **keepass** đều được mã hóa thông qua **Master Password.** Khi bạn muốn sử dụng các thông tin và mật khấu được lưu trữ đó, thì bắt buộc phải nhớ **Master Password** , để đăng nhập vào file **SofsogPass.kdbx** (file lưu trữ thông tin).

Sau khi gõ **Master Password** 2 lần xong thì nhấn **OK**

Cửa sổ **Database Settings** hiện ra cho phép bạn cấu hình các thông số của CSDL. Bạn có thể bỏ qua bước này bằng cách bấm nút **OK**. Lúc này giao diện chính của chương trình hiện ra.

### **Bước 4:** Tổ chức quản lý và lưu trữ thông tin tài khoản

Vùng cửa sổ bên trái cho phép bạn tạo ra các danh mục để việc quản lý được dễ dàng hơn (cấu trúc cây thư mục trong Windows). Các danh mục được gọi là Group. Mặc định hệ thống tạo sẵn cho bạn 06 danh mục bao gồm:

\+ **General**:     Tổng hợp +  **Windows**: Các tài khoản liên quan đến Windows. + **Network**:     Các tài khoản liên quan đến việc truy cập vào các hê thống mạng + **Internet**:      Các tài khoản đăng nhập khi lướt web. + **eMail**:          Các tài khoản email + **Homebanking**: Các thông tin tài khoản ngân hàng.

![Hướng dẫn sử dụng KeePass Sofsog.com](/assets/images/6.-Hướng-dẫn-sử-dụng-KeePass-Sofsog.com_.jpg)

Để tạo một danh mục mới, bạn bấm phải chuột lên 1 vị trí cần tạo và chọn lệnh **Add Group** từ menu hiện ra hoặc click phải chọn **Add Group**.

![Hướng dẫn sử dụng KeePass Sofsog.com](/assets/images/7.-Hướng-dẫn-sử-dụng-KeePass-Sofsog.com_.jpg)

Để xóa một danh mục, bạn bấm phải chuột lênh danh mục đó và chọn lệnh **Delete Group** từ menu hiện ra. Nếu muốn chỉnh sửa thì chọn lệnh Edit Group hoặc click phải vào tên group đó và chọn Delete Group.

Vùng cửa sổ bên phải là nơi chứa danh sách các tài khoản bạn cần lưu trữ tương ứng của danh mục được chọn từ bên trái, mỗi một dòng lưu trữ được gọi là một mục (entry).

![Hướng dẫn sử dụng KeePass Sofsog.com](/assets/images/8.-Hướng-dẫn-sử-dụng-KeePass-Sofsog.com_.jpg)

Để thêm mới một entry, bạn bấm phải chuột lên vùng này và chọn lệnh **_Add Entry_** từ menu hiện ra. Cửa sổ Add entry hiện ra cho phép bạn nhập thông tin tài khoản cần lưu trữ.

![Hướng dẫn sử dụng KeePass Sofsog.com](/assets/images/9.-Hướng-dẫn-sử-dụng-KeePass-Sofsog.com_.jpg)

- **Title:** Đặt tên cho tài khoản cần lưu trữ.
- **User name:** Tên đăng nhập.
- **Password:** Mật khẩu, nếu bạn muốn nhìn thấy mật khẩu thì bạn bấm vào nút ba chấm (…) ở cuối ô.
- **Repeat:** Gõ xác nhận lại mật khẩu. (phía sau trường này có 1 nút để bạn Generator một password ngẫu nhiên)
- **Quality:** Thanh trạng thái cho biết mức độ bảo mật của mật khẩu bạn đặt là mạnh hay yếu.
- **URL:** Địa chỉ/đường dẫn của trang web cần đăng nhập với mật khẩu này.
- **Notes:**Các ghi chú.

## **SỬ DỤNG KEEPASS TRÊN TRÌNH DUYỆT CHROME**

Làm thế nào để mỗi lần cần đăng nhập vào 1 trang web nào đó trên trình duyệt chrome, mình không cần phải copy và paste thông tin đăng nhập, password từ keepass vào trang web, mà nó tự điền luôn (tất nhiên trước đó mình đã cung cấp **Master Password** rồi.

### **Keepass Tusk** là một extension đáp ứng được điều đó

Cài extension **Keepass Tusk** vào chrome bằng đường dẫn: [Keepass Tusk](https://chrome.google.com/webstore/detail/keepass-tusk-password-acc/fmhmiaejopepamlcjkncpgpdjichnecm/related)

Sau khi thêm **Keepass Tusk** vào chrome, ckick vào biểu tượng **Keepass Tusk** trên góc phải phía trên của chrome (hình con voi).

Chọn **Add a Keepass database file**

Chọn **CLOUD STORAGE SETUP**

Bật nút chọn ở **Dropbox** (các bạn lưu trữ file **.kdbx** ở đám mây nào  thì chọn cái đó) chọn Allow (nếu trình duyệt có hỏi).

Đăng nhập tài khoản **Dropbox** vào cửa sổ vừa hiện ra.

Sau khi đăng nhập xong bấm vào nút cho phép **Keepass Tusk.**

**Keepass Tusk** sẽ tự động tìm đến file   **.kdbx** mà mình đã lưu. (vì dụ của mình: **SofsogPass.kdbx)**

Tiếp tục click vào biểu tượng **Keepass Tusk** trên góc phải phía trên của chrome.

Lúc này sẽ thấy file **SofsogPass.kdbx,** click vào file đó

Gõ **Master Password** của bạn.

**Lưu ý:** _bạn có thể lấy trực tiếp file **SofsogPass.kdbx** từ máy tính của mình, không cần phải thông qua dropbox. Ở đây mình ví dụ lấy file qua Dropbox để phòng trường hợp bạn tạo file **.kdbx** ở máy tính 1 (có đồng bộ lên Dropbox) , sau đó sử dụng trên máy tính 2 (không có file **.kdbx)** . Ví dụ máy 1 ở nhà, máy 2 ở công ty chẳng hạn._

Kéo thanh trượt, để chọn thời gian phải gõ **Master Password** lại (mình chọn luôn cuối cùng: mỗi khi đóng trình duyệt, mở lại thì mới gõ pass. Còn mặc định của nó là mỗi lần sử dụng mỗi lần gõ, hơi mệt)

Chọn tiếp **Unlock Database**

Giờ khi muốn đăng nhập vào trang web nào thì click vào biểu tượng, chọn tài khoản cho đúng, rồi nhấn auto fill là được.

### Extension khác

Ngoài **Keepass Tusk** , còn có 1 extension khác tương tự là **CKP - KeePass integration for Chrome** , chức năng cũng tương tự như **Keepass Tusk** , và cách sử dụng cũng tương tụ, các bạn tự tìm hiểu thêm nhé.

## **SỬ DỤNG KEEPASS TRÊN IOS (Iphone, Ipad, ... )**

### **MiniKeePass**

Cách sử dụng từng bước như sau:

Ở đây giã sử Iphone Ipad của bạn  đã cài đặt và sử dụng **Dropbox** rồi nhé.

Vào **App Store**

Tìm, tải và cài đặt app tên là: [**MiniKeePass**](https://itunes.apple.com/app/id451661808)

Xong, thì mở **Dropbox**

Tìm đến file **SofsogPass.kdbx** của bạn đã tạo ở hướng dẫn bên trên và Mở file này lên

Nhấn vào biểu tượng góc trên bên phải , chọn **Export**

Chọn tiếp **Open In ...**

Chọn tiếp **Copy to MiniKeebase**

Giờ thì file **.kdbx** của bạn đã được link đến chương trình **MiniKeePass**

Bạn mở **MiniKeePass**

Sẽ thấy file **.kdbx** chọn vào đó, và nhấn **Master Password** của bạn để giải mã nó.

Hiệu chỉnh một chút cho dễ sử dụng:

Nhấn vào biểu tượng bánh răng ở góc dưới bên trái

Chỗ REMEMBER DATABASE PASSWORD, enabled nó lên để khỏi phải nhấn **Master Password** mỗi lần sử dụng.

Tiếp tục bật  PIN Enabled hoặc TOUCH ID để mỗi lẫn sử dụng chỉ cần nhấn mã pin hoặc vân tay, tùy thói quen sử dụng của các bạn.

OK, cơ bản là vậy thôi, các bạn tìm hiểu sâu thêm nhé

### Ngoài ra, các bạn có thể sử dụng các app khác trong danh sách bên dưới

Cách sử dụng cũng tương tự, mình không hướng dẫn phần này, các bạn tự tìm hiểu

![iPod](/assets/images/menuipod.gif) ![iKeePass](https://itunes.apple.com/app/id299697688) (for iPhone / iPad) ![iPod](/assets/images/menuipod.gif) ![Passwordix](https://itunes.apple.com/app/id488134069) (for iPhone / iPad) ![iPod](/assets/images/menuipod.gif) ![SyncPass](https://itunes.apple.com/app/id533858341) (for iPhone / iPad) ![iPod](/assets/images/menuipod.gif) ![MyKeePass](https://mykeepass.blogspot.com/) (for iPhone / iPad) ![iPod](/assets/images/menuipod.gif) ![PassDrop](http://passdrop.rudism.com/) (for iPhone / iPad) ![1.x Yes](/assets/images/plg1xyes.png) ![iPod](/assets/images/menuipod.gif) [KyPass](https://www.kyuran.be/kypass/) (for iPhone / iPad)

## **SỬ DỤNG KEEPASS TRÊN ANDROID**

Các bạn tìm và tải một trong các ứng dụng sau để cài đặt vào smarphone android của mình

![KeePassDroid](/assets/images/menukpdroid.png) ![KeePassDroid](https://play.google.com/store/apps/details?id=com.android.keepass) (for Android) ![KeePass2Android](/assets/images/menukp2android.png) ![KeePass2Android](https://play.google.com/store/apps/details?id=keepass2android.keepass2android) (for Android) ![KeepShare](/assets/images/menukeepshare.png) [KeepShare](https://play.google.com/store/apps/details?id=com.hanhuy.android.keepshare) (for Android)

## KẾT LUẬN

Như vậy bạn đã có 1 file lưu tất cả mọi thông tin đăng nhập, mật khẩu, ... có tên là **SofsogPass.kdbx** (theo ví dụ của mình). Do công nghệ điện toán đám mây, tất cả thay đổi  thêm, xóa, mật khẩu trên Iphone, trên máy tính ở nhà, hoặc máy tính ở công ty, ... sẽ được lưu trên file

**SofsogPass.kdbx** sẽ được tự động cập nhật và từ giờ trở đi, cho dù có hàng trăm mật khẩu khác nhau, bạn cũng không cần phải mất chất xám để nhớ.

Bạn chưa thực hiện được phần nào, hoặc muốn mình cải thiện hơn về bài viết, vui lòng để lại một vài lời bình luận để mình biết nhé

Sofsog.com chúc các bạn thành công !
