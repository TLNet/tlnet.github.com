---
layout    : post
permalink : /doi-pho-voi-cache-trong-drupal-6
title     : Đối phó với Cache trong Drupal 6
comments  : true
author    : thehong
file      : ./_posts/page/2008-08-02-doi-pho-voi-cache-trong-drupal-6.md
tags      : ['Drupal', 'Drupal 6', 'cache']
category  : Drupal
---
{% include JB/setup %}
Để tối ưu cho việc thực thi và tải trang, Drupal 6 có cung cấp sẵn một số công cụ hữu ích: nén các tập tin CSS, nén các tập tin Javascript, nén trang tải về, đưa các hàm giao diện vào registry, đệm menu, đệm block, ...

Các tính năng này thật sự hữu ích khi site đã chính thức đi vào hoạt động. Tuy nhiên, đối với hệ thống đang được phát triển thì có lẽ việc đệm nội dung là không cần thiết, lắm khi là phiền toái.

Có một vài cách để đối phó:

###1. Sử dụng module cache_disable###
Module này chỉ làm nhiệm vụ là clear cache sau mỗi request được thực hiện.

###2. Sử dụng API:###

Có thể sử dụng các hàm sau để xoá nội dung đệm

* drupal_rebuild_theme_registry(): Xoá theme registry
* cache_clear_all(): Xóa các nội dung quá hạn ra khỏi đệm. Nếu hàm được gọi không có tham số truyền vào các mục quá hạn từ bảng cache_page và cache_block sẽ được xoá.
* menu_rebuild(): (Re)populate the database tables used by various menu functions.
* drupal_flush_all_caches(): Xóa đệm CSS, xoá đệm Javascript, xoá theme registry, xây dựng lại bảng menu, xây dựng lại các thông số của các node type, kết hợp hook_flush_caches của các  module xóa các dữ liệu đệm khác.
