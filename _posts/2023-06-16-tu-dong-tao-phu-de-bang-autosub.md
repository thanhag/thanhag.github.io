---
title: "Hướng dẫn tạo phụ đề tự động cho Video bằng phần mềm Autosub"
date: "2023-06-16"
categories: 
  - "kiem-tien"
  - "thu-thuat-chung"
tags: 
  - "api-google"
  - "autosub"
  - "kiem-tien-bang-youtube"
  - "python"
  - "subtitle-edit"
  - "thu-thuat-chung"
  - "tu-dong-dich-phu-de"
  - "tu-dong-tao-phu-de"
header:
  image: /assets/images/Tao-phu-de-tu-dong-bang-AutoSub.jpg
  teaser: /assets/images/Tao-phu-de-tu-dong-bang-AutoSub.jpg
toc: true
breadcrumbs: true
permalink: /thu-thuat-chung/tu-dong-tao-phu-de-bang-autosub
---

Mình sẽ hướng dẫn chi tiết nhất cách để _tạo phụ đề tự động_ từ một Video hoặc file âm thanh bằng phần mềm Autosub. Có thể tạo phụ đề từ bất cứ ngôn ngữ nào. Trong bài này mình chỉ ví dụ từ một video tiếng anh chưa có phụ đề, sẽ tự động tạo phụ đề tiếng anh và tự động dịch sang tiếng việt.

**UPDATE 2023 KÉO XUỐNG CUỐI BÀI VIẾT, CÓ DÒNG CHỮ MÀU ĐỎ "Một cách đơn giản hơn", DÀNH CHO BẠN NÀO KHÔNG RÀNH CÔNG NGHỆ.**

![Tạo phụ đề tự động](/assets/images/Tao-phu-de-tu-dong-bang-AutoSub.jpg) Tạo phụ đề tự động

## Ok, bây giờ giới thiệu một chút về tiện ích **[Autosub](https://github.com/agermanidis/autosub) :**

Nó là một tiện ích nhận dạng giọng nói tự động và tạo phụ đề. Tiện ích này lấy một Video hoặc một file âm thanh làm nguồn đầu vào, nó sẽ tự tìm các vùng hội thoại, sau đó nó tạo ra các yêu cầu cho Google Speech API tạo các bản ghi cho các vùng hội thoại đó, tự động tạo phụ đề và lưu về máy tính dưới dạng file .srt

## CÀI ĐẶT

[Sofsog](http://sofsog.com) chỉ hướng dẫn các bạn cài đặt trên nền tảng Window, nếu có nhiều quan tâm từ các bạn, mình sẽ hướng dẫn ở các nền tảng khác:

### 1\. Cài đặt Python

Vì [Autosub](https://github.com/agermanidis/autosub) được viết bằng ngôn ngữ [Python](https://www.python.org/) nên trước tiên bạn phải cài đặt nó trước đã. (nếu đã cài trước rồi thì bỏ qua bước này)

Các bạn vào [trang chủ của Python](https://www.python.org/) chọn phiên bản 2.x.x hoặc bấm [vào đây để download Python](https://www.python.org/ftp/python/2.7.13/python-2.7.13.msi)

Mở file vừa tải về lên và cài đặt bình thường

![python](/assets/images/c3d84166-6389-11e6-9cda-2144e2c98ade.png)

**Lưu ý: Chọn Add Python.exe to Path như trong hình nhá.**

Nếu quên chọn như hình thì sau khi cài xong có thể thêm 2 đường dẫn C:\\Python27  và C:\\Python27\\scripts  vào biến môi trường nhá (mình sẽ hướng dẫn ở bước cài đặt [ffmpeg](https://www.ffmpeg.org/))

### 2\. Cài đặt FFmpeg

Tải FFmpeg tại đường link sau: [Download FFmpeg](https://ffmpeg.zeranoe.com/builds/)

Chọn phiên bản 32bit hay 64bit tùy máy của bạn.

Giải nén file vừa tải về, copy thư mục qua ổ C, cần thiết thì đổi tên thư mục cho gọn như vầy: C:\\ffmpeg  chú ý để cấu trúc file như hình.

![Capture](https://huwng.files.wordpress.com/2016/05/capture1.png?w=444)

Copy file **ffmpeg.exe** (nằm trong thu mục C:\\ffmpeg\\bin ) vào thư mục C:\\Python27

Thêm các thư mục C:\\ffmpeg\\bin  vào biến môi trường: Chuột phải **My Computer** chọn **Properties** chọn **Advanced System Settings** ở tab **Advanced** chọn **Environments Variables…**ở ô **System variables** (bên dưới) tìm đến **Path** chọn **Edit**, thêm vào thư mục: C:\\ffmpeg\\bin  bấm **OK.**

Ở bước trên mình có nói thêm 2 thư mục C:\\Python27  và C:\\Python27\\scripts  vào biến môi trường đó, bạn kiểm tra nếu chưa thêm thì thêm vào luôn nha, làm xong sẽ như hình:

![Hướng dẫn tạo phụ đề tiếng việt tự động cho Video bằng phần mềm Autosub](/assets/images/Hướng-dẫn-tạo-phụ-đề-tiếng-việt-tự-động-cho-Video-bằng-phần-mềm-Autosub.png)

### 3\. Cài đặt Autosub (em này tạo phụ đề tự động đây)

- Các bạn mở cmd bằng quyền Administrator
- Gõ lệnh: pip install autosub
- Vào thư mục C:\\Python27\\scripts  đổi tên file **autosub** thành **autosub\_app.py**
- Dùng Notepad.exe hoặc Notepad++ mở file **autosub\_app.py** bên trên: Bấm **Ctrl+F** tìm kiếm dòng  _**temp = tempfile.NamedTemporaryFile(suffix='.flac')**_  thay đổi thành temp = tempfile.NamedTemporaryFile(suffix='.flac', delete=False) _._Tiếp tục tìm kiếm dòng: exe\_file = os.path.join(path, program)  thay đổi thành: exe\_file = os.path.join(path, program + ".exe") .  Hoặc các bạn có thể tài file của mình về tại link này: [File autosub\_app.py](https://drive.google.com/open?id=0B3FpmWUmd-t4ZkhHNHNXNjFER1k) và copy đè lên file của các bạn, khỏi chỉnh sửa.

Ok giờ các bạn mở cmd bằng quyền Administrator gõ vào: C:\\Python27\\scripts\\autosub\_app.py -h  . Nếu hiện ra tương tự như hình dưới này là ok:

![Hướng dẫn tạo phụ đề tiếng việt tự động cho Video bằng phần mềm Autosub 2](/assets/images/Hướng-dẫn-tạo-phụ-đề-tiếng-việt-tự-động-cho-Video-bằng-phần-mềm-Autosub-2.png)

- Xong phần cài đặt.

## HƯỚNG DẪN SỬ DỤNG

##  1. Tạo phụ đề Tiếng Anh

- Ví dụ mình có 1 Video tiếng anh ở đường dẫn như sau: D:\\VideoTiengAnh.mp4
- Để tạo phụ đề bạn mở cmd bằng quyền Administrator gõ lệnh: C:\\Python27\\scripts\\autosub\_app.py "D:\\VideoTiengAnh.mp4" . Xong chờ chút để chương trình làm việc, thời gian chờ phụ thuộc file dài hay ngắn, tốc độ mạng, ...Nói chung cũng khá nhanh:

![Hướng dẫn tạo phụ đề tiếng việt tự động cho Video bằng phần mềm Autosub 3](/assets/images/Hướng-dẫn-tạo-phụ-đề-tiếng-việt-tự-động-cho-Video-bằng-phần-mềm-Autosub-3.png)

- Nếu không có dính lỗi gì thì file phụ đề sẽ được tạo cùng thư mục với file video.

**Lưu ý:** Công thức cụ thể, chi tiết  để nhận dạng các ngôn ngữ như sau:

- File nguồn nói **tiếng Anh** và bạn muốn tạo phụ đề **tiếng Anh,** các bạn gõ lệnh sau:

C:\\Python27\\python.exe C:\\Python27\\scripts\\autosub\_app.py -S en -D en ĐườngDẫnVideoNguồn.mp4

- File nguồn nói **tiếng Tây Ban Nha (Spanish)** và bạn muốn tạo phụ đề **Spanish,** các bạn gõ lệnh:

C:\\Python27\\python.exe C:\\Python27\\scripts\\autosub\_app.py -S es -D es ĐườngDẫnVideoNguồn.mp4

- File nguồn nói **tiếng Nhật (Japanese)** và bạn muốn tạo phụ đề **tiếng Nhật,** các bạn gõ lệnh:

C:\\Python27\\python.exe C:\\Python27\\scripts\\autosub\_app.py -S ja -D ja ĐườngDẫnVideoNguồn.mp4

- Các ngôn ngữ khác các bạn tự tìm hiểu thêm bằng cách gõ:

C:\\Python27\\scripts\\autosub\_app.py --list-languages

## 2\. Tạo phụ đề tự động nhanh chóng, chỉ 1 click

Như bên trên, mỗi lần tạo phụ đề lại phải đánh đường dẫn lằng nhằng, mất thời gian. Mình có thể đơn giản hóa thao tác bên trên bằng một cú click, như sau:

- Dùng Notepad.exe hoặc Notepad++ tạo một file có đuôi **\*.dat** , trong hướng dẫn này mình tạo file tên là **autosub\_app.bat** . Nội dung trong file như sau:

 C:\\Python27\\python.exe C:\\Python27\\scripts\\autosub\_app.py %1

_(đoạn mã trên áp dụng cho file video **Tiếng Anh** nha các bạn)_

- Vào **Start --> Run**, gõ hoặc copy đoạn này vào: %APPDATA%\\Microsoft\\Windows\\SendTo

![Huong dan tao phu de tu dong](/assets/images/Huong-dan-tao-phu-de-tu-dong.png)

- Bấm **OK** sẽ xuất hiện một thư mục **SendTo**, Copy file **autosub\_app.bat** đã tạo bên trên vào thư mục này, các bạn xem hình, lưu ý 2 vòng màu đỏ:

![Huong dan tao phu de tu dong 1](/assets/images/Huong-dan-tao-phu-de-tu-dong-1.png)

- Xong. Từ giờ trở đi khi muốn tạo phụ đề cho video nào, bạn chỉ việc **click phải vào video** đó, chọn **Send to**, chọn tiếp **autosub\_app.bat,** và ngồi chờ một tý là có phụ đề tiếng anh ngay

![Huong dan tao phu de tu dong 2](/assets/images/Huong-dan-tao-phu-de-tu-dong-2.png)

## 3\. Tự động dịch phụ đề sang tiếng Việt

Để tự động dịch phụ đề sang tiếng Việt chúng ta có nhiều cách, Sofsog.com sẽ hướng dẫn 1 cách đơn giản là dùng phần mềm miễn phí **Subtitle Edit** :

- Tải phần mềm về bằng link này: [Subtitle Edit](https://github.com/SubtitleEdit/subtitleedit/releases) .Hoặc link này (bản Portable): [Subtitle Edit Portable](https://drive.google.com/open?id=0B3FpmWUmd-t4Qy1QRC1YcEdMSzA)
- Cài đặt **Subtitle Edit** hoặc giải nén file tải về tùy phiên bản cài đặt hay portable
- Chạy chương trình, mở file **SubtitleEdit.exe**
- Mở file phụ đề tiếng anh cần dịch (ví dụ: phudetienganh.srt)
- Nhìn trên thanh menu, chọn **Auto-translate**, chọn tiếp **Translate (powered by Google)** . Hoặc bấm phím tắt **Ctrl+Shift+G**

![Huong dan tu dong dich phu de sang tieng viet](/assets/images/Huong-dan-tu-dong-dich-phu-de-sang-tieng-viet.png)

- Trong ô **From** (ngôn ngữ nguồn) chọn **English**, ô **To** (ngôn ngữ đích), chọn **Vietnamese.** Bấm nút **Translate,** save lại, mặc định chương trình sẽ save với tên **phudetienganh.vi.srt** (theo ví dụ ban đầu) nằm cùng thư mục với phụ đề tiếng Anh.
- Xong, mở video lên và thưởng thức thành quả thôi.

## Một cách khác đơn giản hơn

Dành cho bạn nào không rành về vi tính, bạn Thành Phạm ở trang web [Daynhauhoc.com](https://daynhauhoc.com/t/autogensubgui-v3-tao-phu-de-tu-dong-bang-autosub-khong-can-cai-dat-tren-windows/45651/73) đã buid lại autosub thành 1 tool rất dễ sử dụng:

Trước tiên các bạn download tool của bạn ấy về ở 1 trong các link sau: (Link update 6/2023)

[](https://drive.google.com/file/d/1xANc_sw2DPcJ4fxgbNm06pgwbI43Mj6u/view?usp=drive_link)

Password giải nén (nếu có): sofsog.com

Tải về xong giải nén, mở file **autosub\_gui.exe** , chọn ngôn ngữ nguồn **(From)**, và ngôn ngữ đích muốn làm phụ đề **(To)** (Update: Chọn "From" và "To" giống nhau, vì chức năng dịch không còn miễn phí, chỉ tạo phụ đề đúng ngôn ngữ của Video thôi) sau đó kéo (drap) và thả (drop) video (hoặc file âm thanh) vào vùng màu trắng là xong, chờ vài giây, phụ đề sẽ được tự động tạo ra ở cùng đường dẫn với file video (hoặc âm thanh).

Khi đã có phụ đề, muốn dịch phụ đề đó sang ngôn ngữ khác, hãy vào link: <https://translatesubtitles.co/>

## LỜI KẾT

[Autosub](https://github.com/agermanidis/autosub) và [Subtitle Edit](https://github.com/SubtitleEdit/subtitleedit/releases) đều sử dụng API của Google. Mình nhận thấy Autosub nhận dạng giọng nói tiếng anh cực tốt, **tạo phụ đề tự động** với độ chính xác cao. Tuy nhiên [Subtitle Edit](https://github.com/SubtitleEdit/subtitleedit/releases)  dịch lại phụ đề từ tiếng Anh sang tiếng Việt thì hơi củ chuối, giống như google translate vậy thôi. Do đó để phụ đề tiếng Việt được chuẩn hơn, sau khi sử dụng tự động dịch, các bạn chỉnh sửa lại một chút thì sẽ hay hơn nhiều, mặc dù vậy nếu sử dụng luôn thì các bạn vẫn sẽ hiểu nội dung đoạn hội thoại (nếu bạn chỉ cần hiểu mà không up cho người khác xem).

Hướng dẫn của sofsog.com cũng khá chi tiết rồi, nhưng cũng không tránh khỏi những thiếu xót, nếu trong quá trình cài đặt, sử dụng các bạn gặp lỗi gì có thể để lại một comment, sofsog.com nhất định sẽ hỗ trợ hết mức có thể.

Cám ơn bạn đã đọc đến đây, chúc bạn thành công.
