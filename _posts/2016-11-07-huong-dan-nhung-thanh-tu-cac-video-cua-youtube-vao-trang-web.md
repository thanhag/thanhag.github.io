---
title: "Hướng dẫn nhúng âm thanh từ các Video của youtube vào trang web."
date: "2016-11-07"
categories: 
  - "thiet-ke-web"
tags: 
  - "am-thanh-youtube"
  - "audio-youtube"
  - "how-to-embed-youtube"
  - "huong-dan-nhung-am-thanh-tu-cac-video-cua-youtube"
  - "thiet-ke-web"
---

Làm cách nào để nhúng một phần âm thanh của bất kì video youtube nào và trang web của bạn. Có một cách dễ dàng là bạn có thể chuyển đổi video của youtube sang file mp3 rồi upload nó lên một trang web lưu trữ âm thanh, sau đó nhúng vào web của mình. Cách này dễ dàng nhưng sẽ dính vấn đề bản quyền với youtube.

Có một phương pháp cũng đơn giản nhưng có sử dụng các API chính thức của YouTube và không yêu cầu chuyển đổi tập tin.

Bạn có thể nhúng bất kỳ video YouTube  vào trang web của bạn và khách truy cập vào trang web của bạn sẽ có thể play và pause các video âm thanh với một nhấp chuột đơn giản. Với kỹ thuật này, bạn cũng có thể sử dụng một video YouTube như âm thanh nền chạy trong một vòng lặp.

#### Các bạn xem demo:

<script src="https://www.youtube.com/iframe_api"></script>

<script src="http://sofsog.com/wp-content/uploads/2016/11/yt.js"></script>

**Cách làm như sau:**

Mở Video youtube mà bạn muốn lấy âm thanh để nhúng vào web. Để ý đường link của video, bạn sẽ thấy ID\_Video (11 ký tự cuối, sau dấu "=")

Ví dụ: **https://www.youtube.com/watch?v=j\_\_Q13iAxNk**  --> 11 ký tự màu đỏ là ID\_Video của youtube (hãy copy nó)

Copy đoạn mã bên dưới, thay  ID\_Video thành **11 ký tự mà bạn vừa copy được** (ở ví dụ này là: j\_\_Q13iAxNk). Paste vào bất kỳ chỗ nào trên trang web mà bạn muốn nhúng âm thanh vào.

```html
<div data-video="ID\_Video"  
         data-autoplay="0"         
         data-loop="1"             
         id="youtube-audio">
  </div>
  <script src="https://www.youtube.com/iframe\_api"></script>
  <script src="http://sofsog.com/wp-content/uploads/2016/11/yt.js"></script>

```

Bạn có thể thay đổi một số thông số trong đoạn code trên theo nhu cầu, ví dụ như: data-autoplay="1" âm thanh sẽ tự chạy khi tải trang web, data-loop="0" âm thanh sẽ không lập lại khi chạy hết bài...

Bạn có thể tải file **yt.js** về để chỉnh sửa theo ý thích và up lên website của bạn luôn.

Nội dung file yt.js:

```javascript
/* 
  Web: http://sofsog.com/
*/
function onYouTubeIframeAPIReady() {
    var e = document.getElementById("youtube-audio"),
        t = document.createElement("img");
    t.setAttribute("id", "youtube-icon"), t.style.cssText = "cursor:pointer;cursor:hand", e.appendChild(t);
    var a = document.createElement("div");
    a.setAttribute("id", "youtube-player"), e.appendChild(a);
    var o = function(e) {
        var a = e ? "Button-Pause-blue.ico" : "Button-Play-blue.ico"; 
        t.setAttribute("src", "http://sofsog.com/wp-content/uploads/2016/11/" + a) /* Thêm vào hai dấu nháy trống đường link của 2 file ảnh, nếu nằm ở thư mục khác */
    };
    e.onclick = function() {
        r.getPlayerState() === YT.PlayerState.PLAYING || r.getPlayerState() === YT.PlayerState.BUFFERING ? (r.pauseVideo(), o(!1)) : (r.playVideo(), o(!0))
    };
    var r = new YT.Player("youtube-player", {
        height: "0",
        width: "0",
        videoId: e.dataset.video,
        playerVars: {
            autoplay: e.dataset.autoplay,
            loop: e.dataset.loop
        },
        events: {
            onReady: function(e) {
                r.setPlaybackQuality("small"), o(r.getPlayerState() !== YT.PlayerState.CUED)
            },
            onStateChange: function(e) {
                e.data === YT.PlayerState.ENDED && o(!1)
            }
        }
    })
}
```

Trong đó bạn để ý đường link: **http://sofsog.com/wp-content/uploads/2016/11/**, là nơi chứa 2 file ảnh **"Button-Pause-blue.ico"** và "**Button-Play-blue.ico" ,** bạn có thể thay đổi 2 ảnh này theo nhu cầu của mình.

**Kết luận:**

Bằng cách này chúng ta có thể nhúng âm thanh của Video của youtube sử dụng API của chính Youtube, do đó bạn không phải lo về vấn đề bản quyền. Các bạn thử xem, nếu có vướng mắt chỗ nào hãy comment bên dưới nhé.
