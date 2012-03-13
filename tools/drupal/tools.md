---
layout: page
title: Drupal Tools
gist: https://gist.github.com/gists/afc175e6624a8aec7945/edit
---
{% include JB/setup %}

**Drupal là nền tảng cực kỳ tốt để bạn có thể dựa vào đó và phát triển các ứng dụng web của mình. 
Tuy nhiên, để trở thành một drupal developer giỏi, bạn cần nhiều thời gian học hỏi và không sử dụng
thành thạo các công cụ hỗ trơ. Ở đây, Xeko Magazine xin giới thiệu với bạn những công cụ mà chúng tôi
biết được trong thời gian dài sử dụng Drupal.**

![](http://static.v3k.net/sites/default/files/styles/article_large/public/content-files/72/4f/68/dojo_poster_sm.jpg "Đồ nghề cho Drupal Developer")

### Hệ điều hành
- [Virtualbox](http://www.virtualbox.org/) Phần mềm miễn phí của Oracle, hỗ trợ thiết lập các máy 
    vi tính ảo trên hệ điều hành bạn đang sử dụng. Hỗ trợ Windows, Mac OS X và nhiều dòng Linux. Bạn
    có thể cài đặt và chạy Windows XP trên Ubuntu, Fedora Core trên Mac Lion, ...
- [Barracuda](http://drupal.org/project/barracuda) Cài đặt một hosting với đầy đủ công cụ cho việc 
    chạy Drupal là công việc không quá đơn giản và đòi hỏi bạn khá nhiều thời gian. Chỉ với một bash
    script nhỏ gọn, Barracuda giúp bạn nhanh chóng xây dựng được một web hosting hoàn hảo, với đầy 
    đủ đồ nghề: nginx, mariadb (fork of mysql), php-fpm, apc, memcached, aegir, ...

### Webserver
- [nginX](/taxonomy/term/65 "nginx article on Xeko Magazine") là một máy chủ web (web server), proxy
    ngược (reserve proxy) và e-mail proxy (IMAP/POP3) nhẹ, hiệu năng cao, sử dụng giấy phép mở BSD.
    Nginx có thể chạy trên UNIX, Linux, các dòng BSD, Mac OS X, Solaris và Microsoft Windows. Theo 
    thống kê của Netcraft, trong số 1 triệu website lớn nhất thế giới, có 6,52% sử dụng nginx. Tại 
    Nga, quê hương của nginx, có đến 46,9% sử dụng máy chủ này. Nginx chỉ đứng sau Apache và IIS
    (của Microsoft).
- [Apache Httpd](http://httpd.apache.org/ "Apache Official web") Máy chủ web phổ biến nhất thế giới
    hiện nay, cũng là web server được hỗ trợ nhiệt tình nhất trên drupal.org. Thời gian đã thay đổi,
    hiện nay Apache trở nên ì ạch, chậm chạp hơn những người anh em sinh sau đẻ muộn.

### Benchmark
- [ab](http://httpd.apache.org/docs/2.0/programs/ab.html "Apache Benchmark") là công cụ đi kèm với 
    Apache httpd, là công cụ phổ biến giúp người dùng đo đạc tốc độ tải web.
- [siege](http://www.joedog.org/index/siege-home) nếu không sử dụng Apache, bạn có thể tìm đến với 
    **siege**, công cụ này có hỗ trợ một số tính năng khá hay: đo tốc độ tải của các URL được định 
    trong một file, gửi chèn header tuỳ chỉnh, ...

### Editors, IDE
- [VIM](http://www.vim.org/) Editor mạnh mẽ trên môi trường dòng lệnh.
- [Netbeans](http://netbeans.org/) IDE nổi tiếng của Orcale, hỗ trợ hoàn hảo cho việc viết chương 
    trình Drupal (PHP, HTML, CSS, Javascript)
- [Notepad++](http://notepad-plus.sourceforge.net/) Editor cực kỳ gọn nhẹ cho người dùng Windows.
- [TextWrangler](http://www.barebones.com/products/TextWrangler/) Editor miễn phí, tiện dùng cho 
    người dùng Mac OS X.

### Browsers
- **All**
  - [CanIUse](http://caniuse.com/ "canIuse.com") Trang tham khảo các tính năng cho các loại browsers khác nhau.
- **Microsoft Internet Explorer** IE là browser được phân phối mặc định trên các hệ điều hành Windows. Các công cụ hỗ trợ bạn phát triển web trên họ browser này:
  - [Firebug Lite](http://getfirebug.com/firebuglite) Phiên bản nhỏ gọn của Firebug để nhúng vào một trang web, do đó, có thể chạy được trên mọi trình duyệt có hỗ trợ javascript.
  - [Multiple Internet Explorer versions](http://tredosoft.com/Multiple_IE)
  - [IETester](http://www.my-debugbar.com/wiki/IETester/HomePage) Công cụ tuyệt vời giúp bạn có thể chạy cùng lúc nhiều phiên bản IE.
- **[Mozilla Firefox](/browser/firefox "Articles about Firefox on Xeko Magazine")** Trình duyệt mã nguồn mở tuyệt vời từ Mozilla, cung cấp rất nhiều extension hữu ích cho người phát triển web:
  - [Web Developer](http://chrispederick.com/work/web-developer/) Là một trong những extension đồ sộ nhất cho web developer trên Firefox -- hỗ trợ validate HTML, CSS, sửa nhanh CSS, xem thuộc tính thẻ, ...
  - [Firebug](http://getfirebug.com/) Có thể nói, ai không biết Firebug, người đó không phải là người... phát triển web. Đây là extension cực kỳ hiệu quả giúp bạn debug javascript, xem cấu trúc html, sửa nhanh css, theo dõi request, ...
  - [FireFTP](https://addons.mozilla.org/en-US/firefox/addon/fireftp/) Extension giúp upload/download file qua giao thức FTP ngay trên trình duyệt Firefox.
  - [YSlow](http://developer.yahoo.com/yslow/) Công cụ đo đạt tốc độ web từ Yahoo.
  - [Page Speed](http://code.google.com/speed/page-speed/) công cụ từ Google, tương tự như YSlow.

### Modules
- [Cài đặt Cywin cho người Windows](http://www.lullabot.com/node/280/play "by Lullabot")
    Windows là hệ điều hành tốt, tuy nhiên, nó không tiện lợi lắm cho công việc lập trình. Nhưng 
    không  lo, cywin là môi trường giả lập unix cho bạn.
- [Drush -- Drupal SH](http://drupal.org/project/drush "Drush project homepage on drupal.org")
    Nếu bạn đã quen thuộc với môi trường dòng lệnh, và ước ao được tương tác với Drupal qua môi 
        trường này, đây chính là công cụ bạn cần.
- [Tự xây dựng trang tham khảo Drupal API](http://groups.drupal.org/node/5334 "article by thehong on groups.drupal.org")
    Viết code trên Drupal, người lập trình phải vào http://api.drupal.org để tra cứu các hàm, 
    các thí dụ mẫu. Trường hợp, máy tính của mạng không nối mạng, hoặc mạng chậm, hoặc A.D.O có trở
    ngại thì công việc sẽ bị ngưng trệ.
- [Coder module](http://drupal.org/project/coder "Coder project homagepage on drupal.org")
    Coder module là module hỗ trợ bạn kiểm tra mã Drupal được viết có hợp chuẩn chung hay không. Ngoài ra,
    coder module cũng hỗ trợ bạn nâng cấp module/theme lên phiên bản Drupal mới hơn.
- [Module Builder](http://drupal.org/project/module_builder "Module builder homepage on drupal.org")
    Đây là công cụ tiện lợi giúp bạn tạo nhanh drupal module, với tính năng generate hooks, docs, ...
- [Devel module](http://drupal.org/project/devel "Devel project homepage on drupal.org")
    Devel hầu như là một module không thể thiếu cho các lập trình viên Drupal. Nó hỗ trợ bạn debug
    chương trình, trình bày các câu truy vấn trong trang, memory sử dụng, generate dummy content,
    kiểm tra quyền truy cập, ....
- [Entity API](http://drupal.org/project/entity)
    Module cung cấp tính năng mở rộng cho Entity API của core (Drupal 7). Những tính năng được cung
    cấp: entity CRUD controller, data wrappers API, admin UI, tích hợp Rules, ...

### Base theme
- [Fusion](http://drupal.org/project/fusion)
- [AdaptiveTheme](http://drupal.org/project/adaptivetheme)
- [Omega](http://drupal.org/project/omega)
- [Zen](http://drupal.org/project/zen)
- [Boron HTML5 Base Theme](http://drupal.org/project/boron)
- [BoilderPlate](http://drupal.org/project/boilerplate)

### Durpal & HTML5
- [HTML5 Base](http://drupal.org/project/html5_base)
- [HTML5 Tools](http://drupal.org/project/html5_tools)
- [HTML5 Group](http://groups.drupal.org/html5)
- [Adaptive HTML5 Base Theme](http://drupal.org/project/adaptivetheme)
- [HMLT5 Specification](http://developers.whatwg.org/)
- [HTMLDoctor](http://html5doctor.com/)
- [Modernizr.js](http://www.modernizr.com/)
- [YepNope.js](http://yepnopejs.com/)

### Cộng đồng
- [Drupal.org](http://drupal.org/) Đại bản doanh của Drupal
- [Drupal.stackexchange.com](http://drupal.stackexchange.com) Chuyên trang hỏi-đáp cho Drupal
- [DrupalModules.com](http://drupalmodules.com/) Tìm kiếm, đánh giá chất lượng các modules trên drupal.org
- [DrupalVietnam.org](http://drupalvietnam.org) Cộng đồng người Việt Nam sử dụng Drupal

Danh sách này sẽ được thường xuyên cập nhật (Last Update: 2012 Feb 17)

_Web Developer @ Xeko.vn_