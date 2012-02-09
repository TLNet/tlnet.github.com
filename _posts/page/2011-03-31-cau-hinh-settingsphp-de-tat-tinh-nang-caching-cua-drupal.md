---
layout    : post
permalink : /node/3677
title     : Cấu hình settings.php để tắt tính năng caching của Drupal
comments  : false
author    : thehong
file      : ./_posts/page/2011-03-31-cau-hinh-settingsphp-de-tat-tinh-nang-caching-cua-drupal.md
category  : Drupal
tags      : ['Drupal', 'cache']
---
{% include JB/setup %}
Drupal hỗ trợ tính năng caching đối với người dùng chưa đăng nhập, giúp giảm bớt việc truy xuất đến cơ sở dữ liệu. Tuy nhiên ở một số trang chúng ta cần tắt tính năng này, thí dụ bạn có một trang cho người dùng xem IP của họ, hay một trang upload files, ...

Với cấu hình đơn giản như sau, ở file settings.php, bạn có thể thực hiện điều này:

{% highlight php linenos startinline %}

if ($_GET['q'] === 'my-ip-address') {
  $conf['cache']
      = $conf['preprocess_css']
      = $conf['preprocess_js']
      = $conf['block_cache']
      = $conf['page_compression']
      = $conf['cache']
      = FALSE;
}

{% endhighlight %}
