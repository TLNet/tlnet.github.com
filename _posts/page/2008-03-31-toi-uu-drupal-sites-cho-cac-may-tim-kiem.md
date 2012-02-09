---
layout    : post
permalink : /content/toi-uu-drupal-sites-va-cac-may-tim-kiem.html
title     : Tối ưu Drupal sites cho các máy tìm kiếm
comments  : true
author    : thehong
file      : ./_posts/page/2008-03-31-toi-uu-drupal-sites-cho-cac-may-tim-kiem.md
tags      : ['Drupal', 'Modules', 'SEO']
category  : Drupal
---
{% include JB/setup %}
Tối ưu Drupal sites và các máy tìm kiếm, tiếng Anh người ta thường gọi là SEO, *Search Engines 
Optimization*, là vấn đề cực kỳ quan trọng đối với mọi site. Tôi xin giới thiệu các module hỗ trợ 
SEO:

- **pathauto:** tự động tạo alias cho các trang node, taxonomy term, user, blog, ... Vì các search 
engine ngoài việc tìm nội dung ở trong trang web, thì cũng tìm kiếm ở URL của trang web nữa, và độ 
ưu tiên này rất cao.
- **nodewords:** hỗ trợ tạo thẻ meta keyword, description cho từng node.
- **xmlsitemap:** tạo chỉ mục nội dung để các SE có thể truy cập, đồng thời, module này cũng thường 
xuyên submit sitemap đến SE để chúng khỏi quên.
- **ping (core module):** thông báo đến một số site 
quan trọng để biết rằng, site bạn đang sống.
