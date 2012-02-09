---
layout    : post
permalink : /content/fckeditor-va-encode-tieng-viet.html
title     : FCKEditor và Encode tiếng Việt
comments  : true
author    : thehong
file      : ./_posts/page/2007-11-01-fckeditor-va-encode-tieng-viet.md
tags      : ['Drupal']
category  : Drupal
---
{% include JB/setup %}
Lâu quá không tham gia [Group](http://groups.drupal.org/vietnam), có mánh nhỏ mà hay.

Tác giả * hỏi:
> Hi,
> 
> Không biết có bà con nào gặp trường hợp này chưa, tôi mới dùng FCK và thấy text bị encode sang dạng sau:
> 
> > Kh&ocirc;ng cần chạy đ&ocirc;n chạy đ&aacute;o khắp các trung t&acirc;m để mong t&igrave;m được một c&ocirc;ng việc l&agrave;m th&ecirc;m tăng thu nhập, chẳng cần phải gật đầu với những c&ocirc;ng việc nằm ngo&agrave;i v&ugrave;ng chuy&ecirc;n m&ocirc;n như gia sự, b&aacute;n h&agrave;ng, tiếp thị&hellip; Giới sinh vi&ecirc;n IT c&oacute; v&ocirc; v&agrave;n những c&ocirc;ng việc kiếm tiền thật từ thế giới ảo.
> 
> Mặc dù đoạn text này vẫn được trình duyệt hiển thị đúng nhưng trong html code bị như thế, nhìn không thích một chút nào cả hơn nữa có thể gây ra dư thừa dữ liệu (not sure).
> Lỗi này chỉ gặp khi sử dung FCK để input data thôi.

Tác giả tự trả lời:
> Thì ra là chú này, thêm vào file config là xong.
> 
> FCKConfig.ProcessHTMLEntities = false ;</pre>
> 
> Hêh, FCK vẫn ngon hơn TinyMCE :D

* Tác giả: [dohoangnguyen.com](http://dohoangnguyen.com/)
