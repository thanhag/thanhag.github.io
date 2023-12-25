---
title: "Giới thiệu những công cụ cơ bản trong GIMP - Phần mềm chỉnh sửa ảnh mã nguồn mở"
date: "2017-05-15"
categories: 
  - "kali-linux"
  - "phan-mem"
  - "thu-thuat-chung"
tags: 
  - "chinh-sua-anh-tren-linux"
  - "cong-cu-co-ban-cua-gimp"
  - "gimp"
  - "gioi-thieu-ve-gimp"
  - "phan-mem"
  - "thu-thuat-chung"
header:
  
  teaser: /assets/images/G.png

breadcrumbs: true
permalink: /thu-thuat-chung/nhung-cong-cu-co-ban-trong-gimp
---

**GIMP là phần mềm xử lý ảnh nguồn mở mạnh mẽ và hoàn toàn miễn phí. Muốn làm chủ GIMP, trước hết bạn cần tìm hiểu qua về những công cụ cơ bản của GIMP.**

![Phần mềm chỉnh sửa ảnh GIMP](/assets/images/G.png)

Trước tiên, cài đặt **GIMP** trên **linux**, bạn gõ vào **Terminal**:

```terminal
apt-get install gimp
```

Lưu ý: Cài đặt trên window các bạn Google nhá.

_Giao diện chính của **GIMP** được chia thành ba phần chính:_ Bảng **_Toolbox_** chứa các công cụ xử lý ảnh, kèm theo đó là bảng tùy chọn nằm ngay bên dưới (tương ứng với mỗi công cụ sẽ có một bảng tùy chọn riêng), bảng _**Layers**, **Channels**, **Paths**, **Undo**_ chứa các thông số liên quan đến lớp, kênh màu,… Cuối cùng là bảng **_GNU Image Manipulation Program_** hiển thị ảnh đang xử lý. Để xử lý một ảnh có sẵn, trước hết bạn vào menu **_File > Open_**, duyệt đến file ảnh cần xử lý và nhấn Open. Trong bài này, chúng ta tìm hiểu một số công cụ cơ bản trong **GIMP** như: _**Scale Tool,** **Crop Tool,** **Paths Tool, Flip Tool, Rotate Tool.**_

**Scale Tool:** Kéo giãn đối tượng mà không làm “méo” chi tiết Sử dụng công cụ **_Scale Tool_**, bạn dễ dàng thay đổi kích thước các đối tượng trong ảnh. Tại bảng **_Toolbox_**, bạn chọn công cụ _**Scale Tool**_ (biểu tượng ![](/assets/images/710F72705C6C4DC6869ECA9943C93C67.jpg)), chọn đối tượng cần xử lý từ bảng **_Layer_**, nhấp chuột lên vùng hiển thị ảnh. Hộp thoại **_Scale_** sẽ tự động xuất hiện.

![](/assets/images/0A4D619791C8F05751535F70B26C3D27.jpg)

Để kéo giãn đối tượng, bạn chỉ việc rê chuột đến các điểm neo xung quanh đối tượng đó, nhấn giữ và rê chuột theo hướng cần thu nhỏ hoặc phóng to. Xong, nhấn **_Enter_**. Ngoài ra, nếu muốn việc kéo giãn đối tượng không làm “móp méo” các chi tiết (gây hiện tượng “lùn” hình, “hẹp” hình,…), bạn chỉ việc nhấn biểu tượng ![](/assets/images/48B1DAD2C633E21FD8A3E38EE17580F2.jpg) từ hộp thoại **_Scale_**, rồi kéo giãn đối tượng thoải mái mà không sợ bị “méo”, vì **GIMP** sẽ tự động điều chỉnh chiều ngang và chiều dọc của ảnh theo đúng tỷ lệ ban đầu. Trong trường hợp không muốn thực hiện thủ công, bạn có thể nhập trực tiếp kích thước muốn thay đổi trên đối tượng theo chiều ngang (mục **_Width_**) hoặc chiều dọc (mục **_Height_**) từ hộp thoại **_Scale_**.

![](/assets/images/6CB106641AE2DCA643C5F846B48F17CD.jpg)

Sau khi thay đổi kích thước đối tượng, ảnh thường bị thừa vùng trong suốt xung quanh đối tượng. Để kích thước ảnh khớp với kích thước đối tượng, bạn vào menu _**Image** > **Fit Canvas to Layers**._

**![](/assets/images/C820EAEB3D3483D06BD70EB93310EBBA.jpg)**

**Crop Tool: Xén ảnh** Về cơ bản, **_Crop Tool_** là công cụ cải tiến từ **_Scale Tool_**. Sử dụng **_Crop Tool_** nghĩa là bạn đang kết hợp **_Scale Tool_** (thay đổi kích thước đối tượng trong ảnh) và **_Fit Canvas to Layers_** (lấy kích thước đối tượng làm kích thước ảnh). Rất đơn giản, bạn chỉ việc chọn công cụ **_Crop Tool_** (biểu tượng ![](/assets/images/975F2027BBC90C6F1AF558E3D2B9B847.jpg)) từ bảng **_Toolbox_**, sau đó nhấn giữ và rê chuột trên ảnh để tạo vùng ảnh cần “xén” và nhấn **_Enter_**.

**![](/assets/images/89FAFB17FE0CC5CC5AA4460BEBCB247E.jpg)**

**Paths Tools: Xén ảnh để loại bỏ màu nền** Với công cụ **_Crop Tool_**, bạn chỉ có thể “xén” ảnh theo hình chữ nhật, do đó vẫn bị “dính” màu nền bên dưới. Muốn “xén” ảnh theo sát viền đối tượng để loại bỏ màu nền, bạn nên nhờ vậy công cụ **_Paths Tool_**. Trước hết, bạn chọn công cụ **_Paths Tool_** (biểu tượng ![](/assets/images/B9E814B014C59C577233822AD894C2E0.jpg)) từ bảng **_Toolbox_**, lần lượt nhấp chuột quanh viền đối tượng, sao cho điểm đầu và điểm cuối trùng nhau, tạo thành một vùng kín. Xong, nhấn **_Enter_** để tạo vùng chọn cho đối tượng, nhấn tiếp **_Ctrl+I_** để đảo ngược vùng chọn (lúc này, vùng chọn là phần nền nằm phủ kín quanh đối tượng), rồi nhấn **_Delete_** để xóa nền.

**Flip Tool và Rotate Tool: Lật ảnh** Để lật ảnh theo phương ngang, bạn chọn công cụ **_Flip Tool_** (biểu tượng ![](/assets/images/D3ECEB7CCE61493663BDE317667A94D9.jpg)) từ bảng **_Toolbox_**, sau đó nhấn chuột lên ảnh. Muốn lật ảnh theo góc độ tùy thích, bạn chọn công cụ **_Rotate Tool_** (biểu tượng ![](/assets/images/13FB54DB33788D556199EE3429563B72.jpg)) từ bảng **_Toolbox_**, nhấp chuột lên đối tượng cần xoay. Trong hộp thoại **_Rotate_** xuất hiện, muốn xoay đối tượng theo góc độ nào, bạn chỉ việc di chuyển thanh trượt hoặc gõ giá trị góc vào khung **_Angle_** từ hộp thoại **_Rotate_** và nhấn **_Enter_**.

![](/assets/images/CF3FA4FBC216AD1D07572012509D397C.jpg)

Một ebook tiếng việt để bạn nào cần tìm hiều thêm về Gimp nhé:

**Linkdownload:** [Ebook Gimp cơ bản Tiếng việt](https://drive.google.com/open?id=1y5ZQamsJkKCE9bZWLADNOvsQaYT3Qach)

Sofsog.com chúc các bạn thành công !

Nguồn <http://thegioitinhoc.vn>
