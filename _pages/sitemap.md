---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: false
---

Danh sách tất cả các bài viết và trang được tìm thấy trên trang web. Đối với các bạn, robot hiện có sẵn [phiên bản XML]({{ '/sitemap.xml' |relal_url }}) để xử lý.

<h2>Danh sách các trang</h2>
{% for post in site.pages %}
  {% include archive-single.html %}
{% endfor %}

<h2>Danh sách các bài viết</h2>
{% for post in site.posts %}
  {% include archive-single.html %}
{% endfor %}

{% capture written_label %}'None'{% endcapture %}

{% for collection in site.collections %}
{% unless collection.output == false or collection.label == "posts" %}
  {% capture label %}{{ collection.label }}{% endcapture %}
  {% if label != written_label %}
  <h2>{{ label }}</h2>
  {% capture written_label %}{{ label }}{% endcapture %}
  {% endif %}
{% endunless %}
{% for post in collection.docs %}
  {% unless collection.output == false or collection.label == "posts" %}
  {% include archive-single.html %}
  {% endunless %}
{% endfor %}
{% endfor %}