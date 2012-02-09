---
layout    : post
permalink : /content/tat-nong-cac-module-su-dung-phpmyadmin.html
title     : Tắt nóng các module sử dụng PHPMyAdmin
comments  : true
author    : thehong
file      : ./_posts/page/2008-02-20-tat-nong-cac-module-su-dung-phpmyadmin.md
tags      : ['Drupal', 'PHPMyAdmin']
category  : Drupal
---
{% include JB/setup %}
Đối với một số server cung cấp giới hạn bộ nhớ PHP/MySQL khá ít, có lúc chúng ta sẽ gặp phải tình 
trạng site không thể hoạt động: hoặc hiện ra trang trắng, hoặc luôn báo lỗi Page not found, hoặc có 
Fatal error đại khái: 

> Fatal error: Allowed memory size of 8388608 bytes exhausted (tried to allocate 302882 bytes) 
> in /var/hsphere/local/home/user/domain/includes/database.inc on line 199

Đến lúc này, chúng ta đành phải giảm bớt lại chức năng sử dụng, để site có thể tạm thời hoạt động, 
nhưng, việc tắt bớt các module đến lúc này không phải lúc nào cũng dễ dàng, vì bộ nhớ PHP/MySQL đã 
quá tải. Chúng ta cũng có thể tắt bớt các module bằng giao diện PHPMyAdmin như sau:

- Thực hiện câu truy vấn:
> SELECT *
> FROM system
> WHERE type = 'module' AND status = 1 
> ORDER BY name LIMIT 0, 300;
-  Bảng kết quả là danh sách các module hiện có trong hệ thống
-  Click chọn sửa status của module muốn tắt thành 0.
