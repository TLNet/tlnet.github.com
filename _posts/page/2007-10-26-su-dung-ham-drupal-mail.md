---
layout    : post
permalink : /content/su-dung-ham-drupalmail.html
title     : Sử dụng hàm drupal_mail ()
comments  : true
author    : thehong
file      : ./_posts/page/2007-10-26-su-dung-ham-drupal-mail.md
tags      : ['Drupal']
category  : Drupal
---
{% include JB/setup %}

Thí dụ đơn giản gửi một mail có nội dung HTML sử dụng hàm drupal_mail ()

{% highlight php linenos startinline %}

  drupal_mail(
    'mail-test', // khóa, tiện để hệ thống theo dõi các mail gửi đi
    'thehongtt@gmail.com', // gửi đến
    'Tiêu đề email', // tiêu đề của email
    // Nội dung chúng ta gửi đi lúc này là một HTML table...
    theme (
      'table', 
      array('Col1', 'Col2', 'Col3'), 
      array(
        array ('1.1', '1.2', '1.3'),
        array ('2.1', '2.2', '2.3'),
        array ('3.1', '3.2', '32.3'),
      ), 
      array ('style' => 'border: 1px #f00 dashed'),
      'Nội dung của email'
    ),
    // !-- nội dung email

    null, 

   // Header của email, cần xác định thuộc tính text/html ...
    array (
      'Content-type' => 'text/html; charset=UTF-8; format=flowed',
      'From' => 'VNSupperMark Info <info@vnsuppermark.com>'
    )
  );

{% endhighlight %}
