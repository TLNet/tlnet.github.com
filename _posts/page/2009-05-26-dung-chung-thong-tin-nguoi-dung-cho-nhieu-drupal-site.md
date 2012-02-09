---
layout    : post
permalink : /su-dung-chung-thong-tin-nguoi-dung-cho-nhieu-drupal-site
title     : Dùng chung thông tin người dùng cho nhiều Drupal site
comments  : true
author    : thehong
file      : ./_posts/page/2009-05-26-dung-chung-thong-tin-nguoi-dung-cho-nhieu-drupal-site.md
tags      : ['Drupal', 'Multisite']
category  : Drupal
---
{% include JB/setup %}
Bạn có nhiêu drupal site khác nhau, nhưng muốn người dùng của website này cũng có thể sử dụng cùng thông tin đăng nhập ở các website khác, thông tin thay đổi ở site này, kéo theo thông tin ở các site khác cũng thay đổi, ... Tôi có một kinh nghiệm nhỏ của tôi ở project gần đây để xử lý việc này khá đơn giản.

###Giả sử###

i. Các webstie chạy chung trên một server.
ii. Các website sử dụng chung một mã nguồn (chỉ một thực thể).
iii. Mỗi website chạy một database khác nhau.
iv. Các website đó, thí dụ là:
  iv.i. http://website-1.com/
  iv.ii. http://website-2.net/

Cấu trúc thư mục của drupal lúc này:

{% highlight ini %}
  /sites/
        /all/
            /modules/
                    /singlesignon
        /website-1.com/
                      /files/
                      /...
                      /settings.php
        /website-1.net/
                      /files/
                      /...
                      /settings.php
{% endhighlight %}

###Các databases###

* drupal_website1: sử dụng cho website-1.com
* drupal_website2: sử dụng cho website-2.net
* drupal_share: sử dụng cho các thông tin về người dùng ở 2 website trên

###Cấu hình kết nối CSDL###
* cho website-1.com (sites/website-1.com/settings.php)

{% highlight php linenos startinline %}
// ...

$db_url = 'mysql://username:password@localhost/drupal_website1';
$db_prefix = array(
  'default'     => 'w1_',
  'users'       => 'drupal_share.',
  'users_roles' => 'drupal_share.',
  'sessions'    => 'drupal_share.',
  'role'        => 'drupal_share.',
  'authmap'     => 'drupal_share.',
);

// ...
{% endhighlight %}

* cho website-2.net (sites/website-2.net/settings.php)

{% highlight php linenos startinline %}
// ...

$db_url = 'mysql://username:password@localhost/drupal_website2';
$db_prefix = array(
  'default'     => 'w2_',
  'users'       => 'drupal_share.',
  'users_roles' => 'drupal_share.',
  'sessions'    => 'drupal_share.',
  'role'        => 'drupal_share.',
  'authmap'     => 'drupal_share.',
);

// ...
{% endhighlight %}

Với cấu hình thế này, thông tin người dùng ở (mạng lưới) các site của chúng ta sẽ tự động đồng bộ với nhau.

Thế Hồng