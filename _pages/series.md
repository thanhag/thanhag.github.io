---
title: "Series"
excerpt: "Các bài hướng dẫn được gom thành series, sắp theo thứ tự từ nền tảng tới nâng cao. Vào đây nếu bạn muốn đọc có đầu có đuôi thay vì nhặt từng bài rời."
permalink: /series/
author_profile: true
---

Blog này có những bài đứng riêng, nhưng phần lớn nội dung kỹ thuật đi theo mạch. Một bài
dựng dịch vụ sẽ cần bài trước đó nói về hạ tầng, và mở đường cho bài sau. Gom lại thành
series để bạn đọc theo thứ tự thay vì đoán xem nên đọc gì trước.

{% assign nhom = site.posts | where_exp: "p", "p.series" | group_by: "series" | sort: "name" %}
{% if nhom.size == 0 %}

Chưa có series nào.

{% else %}
<div class="series-ds">
{% for g in nhom %}
{% assign bai = g.items | sort: "series_thu_tu" %}
{% assign dau_tien = bai | first %}
{% assign moi_nhat = g.items | sort: "date" | last %}
  <section class="series-the">
    <p class="series-the__nhan">{% if dau_tien.cap_do %}<span class="series-box__cap">{{ dau_tien.cap_do }}</span>{% endif %}{% if dau_tien.categories[0] %} <span class="series-the__muc">{{ dau_tien.categories[0] }}</span>{% endif %}</p>
    <h2 class="series-the__ten">{{ g.name }}</h2>
    <p class="series-the__so">{{ g.items | size }} bài &middot; cập nhật {{ moi_nhat.date | date: "%d/%m/%Y" }}</p>
    <ol class="series-the__ds">
      {% for b in bai %}<li><a href="{{ b.url | relative_url }}">{{ b.title }}</a></li>{% endfor %}
    </ol>
  </section>
{% endfor %}
</div>
{% endif %}

Series nào chưa đủ bài là do mình đang viết dở. Thứ tự trong danh sách là thứ tự nên đọc,
không phải thứ tự đăng.
