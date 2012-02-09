---
layout    : post
permalink : /hack-de-cai-dat-drupal-tren-server-voi-register_global-on
title     : Hack để cài đặt Drupal trên server với register_global = ON
comments  : true
author    : thehong
file      : ./_posts/page/2008-08-12-hack-de-cai-dat-drupal-tren-server-voi-register-global-on.md
tags      : ['Drupal']
category  : Drupal
---
{% include JB/setup %}
Bạn không thể cài đặt Drupal nếu như server thiết lập tính năng register_globals thành ON. Năn nỉ 
hoài mà quản lý server không chịu cấu hình lại server => Đành phải hack code.

Mở file /modules/system/system.install, tìm hàm system_requirements(), tìm dòng:
{% highlight php linenos startinline %}
  if (!empty($register_globals) && strtolower($register_globals) != 'off') {
{% endhighlight %}

Sửa thành:
{% highlight php linenos startinline %}
  if (
    FALSE // toila.net's HACK: !empty($register_globals)
    && strtolower($register_globals) != 'off'
  ) {
{% endhighlight %}

Sử dụng hack này cực kỳ rủi ro nhé, google thử sẽ ra
một vài thí dụ.