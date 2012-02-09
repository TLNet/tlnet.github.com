---
layout    : post
permalink : /content/drupal-va-sub-domain.html
title     : Drupal và sub-domain
comments  : true
author    : thehong
file      : ./_posts/page/2008-02-21-drupal-va-sub-domain.md
tags      : ['Drupal', 'Apache', 'mode_rewrite', 'htaccess']
category  : Drupal
---
{% include JB/setup %}
Đối với những site có rất nhiều nội dung, có lẽ chúng ta cần tạo những URL đơn giản, gọn gàng để người dùng dễ nhớ để truy cập lại sau này. Thí dụ, <code>toila.net/thehong</code> thì đẹp hơn <code>toila.net/index.php?q=user/1</code>, <code>web.com/thongbao</code> sẽ dễ nhớ hơn <code>web.com/index.php?q=taxonomy/term/1+2+3</code> rất nhiều hay là <code>thehong.yeublog.com</code> sẽ chuyên nghiệp hơn là <code>yeublog.com/index.php?module=blog&action=frontpage</code>, ... Đối với sub-domain dạng sub folder thì vấn đề được giải quyết rất đơn giản, nhưng đối với sub-domain dạng <code>*subdomain.domain.com*</code> thì có một số trở ngại. Bài viết này nêu lên một số trở ngại và cách giải quyết.

##Yêu cầu hệ thống##

- Apache/server hỗ trợ mod_rewrite, cấu hình trên từng thư mục bằng tập tin <code>.htaccess</code>.
- Có cài đặt module rewrite.
- Host phải hỗ trợ chức năng subdomain wildcard -- subdomain ảo. Khi chức năng subdomain wildcard này
được kích hoạt, các request đến server dưới dạng <code>*http://foo.domainname.com/bar*</code> sẽ được 
server hiểu là <code>*http://domainname.com/bar*</code>. Khi đó, các request đến Drupal site đều quy 
về một mối -- các request dạng <code>http://foo.domainname.com/node/1</code>, server sẽ gọi Drupal 
site của bạn với URL có dạng <code>http://domainname.com/index.php?q=node/1</code>

##Cookie##
Việc tạo tên SESSION trong Drupal phụ thuộc vào domain (và sub domain) được request, cho nên, cũng là một người truy cập, nhưng khi bạn truy cập <code>http://domainname.com</code> và khi bạn truy cập <code>http://foo.domainame.com</code>, thì đối với Drupal, bạn là hai người khác nhau. Tham khảo hàm config_init(). Để giải quyết trở ngại này, chúng ta phải đồng bộ tên SESSION khi sử dụng các domain/sub-domain. Mở tập tin <code>sites/settings/settings.php</code>, thêm (bỏ comment) dòng:

{% highlight php linenos startinline %}
  $cookie_domain = domainname.com';
{% endhighlight %}

Vấn đề còn lại giờ, chúng ta hải chỉnh lại tập tin .htaccess để Drupal hiểu được chính xác các yêu cầu của người dùng ứng với các domain/sub-domain:-  http://foo.domainname.com/ => http://domainname.com/index.php?q=foo-  http://bar.domainname.com/baz/blah => http://domainname.com/index.php?q=baz/blah


##Rewrite##
Apply [patch này](http://toila.net/sites/toila.net/files/code/patch/subdomain-drupal5-7.patch) (áp
dụng cho drupal 5.7) để điều chỉnh lại tập tin <code>.htaccess</code>. Khi đó, <code>.htaccess</code> 
của drupal sẽ có dạng sau:

{% highlight ini linenos startinline %}
#
# Apache/PHP/Drupal settings:
#

# Protect files and directories from prying eyes.
<FilesMatch "\.(engine|inc|info|install|module|profile|po|sh|.*sql|theme|tpl(\.php)?|xtmpl)$|^(code-style\.pl|Entries.*|Repository|Root|Tag|Template)$">
  Order allow,deny
</FilesMatch>

# Don't show directory listings for URLs which map to a directory.
Options -Indexes

# Follow symbolic links in this directory.
Options +FollowSymLinks

# Customized Error messages.
ErrorDocument 404 /index.php

# Set the default handler.
DirectoryIndex index.php

# Override php settings. More in sites/default/settings.php
# but the following cannot be changed at runtime.

# php 5, Apache 1 and 2.
<IfModule mod_php5.c>
  php_value magic_quotes_gpc                0
  php_value register_globals                0
  php_value session.auto_start              0
  php_value mbstring.http_input             pass
  php_value mbstring.http_output            pass
  php_value mbstring.encoding_translation   0
</IfModule>

# Requires mod_expires to be enabled.
<IfModule mod_expires.c>
  # Enable expirations.
  ExpiresActive On
  # cache all files for 2 weeks after access (A).
  ExpiresDefault A1209600
  # Do not cache dynamically generated pages.
  ExpiresByType text/html A1
</IfModule>

# Various rewrite rules.
<IfModule mod_rewrite.c>
  RewriteEngine on

  # If your site can be accessed both with and without the 'www.' prefix, you
  # can use one of the following settings to redirect users to your preferred
  # URL, either WITH or WITHOUT the 'www.' prefix. Choose ONLY one option:
  #
  # To redirect all users to access the site WITH the 'www.' prefix,
  # (http://example.com/... will be redirected to http://www.example.com/...)
  # adapt and uncomment the following:
  RewriteCond %{HTTP_HOST} ^example\.com$ [NC]
  RewriteRule ^(.*)$ http://www.example.com/$1 [L,R=301]
  #
  # To redirect all users to access the site WITHOUT the 'www.' prefix,
  # (http://www.example.com/... will be redirected to http://example.com/...)
  # uncomment and adapt the following:
  # RewriteCond %{HTTP_HOST} ^www\.example\.com$ [NC]
  # RewriteRule ^(.*)$ http://example.com/$1 [L,R=301]

  # Modify the RewriteBase if you are using drupal in a subdirectory or in a
  # VirtualDocumentRoot and the rewrite rules are not working properly.
  # For example if your site is at http://example.com/drupal uncomment and
  # modify the following line:
  # RewriteBase /drupal
  #
  # If your site is running in a VirtualDocumentRoot at http://example.com/,
  # uncomment the following line:
  # RewriteBase /

  # Rewrite old-style URLs of the form 'node.php?id=x'.
  #RewriteCond %{REQUEST_FILENAME} !-f
  #RewriteCond %{REQUEST_FILENAME} !-d
  #RewriteCond %{QUERY_STRING} ^id=([^&]+)$
  #RewriteRule node.php index.php?q=node/view/%1 [L]

  # Rewrite old-style URLs of the form 'module.php?mod=x'.
  #RewriteCond %{REQUEST_FILENAME} !-f
  #RewriteCond %{REQUEST_FILENAME} !-d
  #RewriteCond %{QUERY_STRING} ^mod=([^&]+)$
  #RewriteRule module.php index.php?q=%1 [L]

  # Rewrite current-style URLs of the form 'index.php?q=x'.
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_URI} ^/.+$
  RewriteRule ^(.*)$ index.php?q=$1 [L,QSA]
  
  # Rewrite subdomain.example.com to example.com/index.php?q=subdomain
  RewriteCond %{REQUEST_URI} ^/$
  RewriteCond %{HTTP_HOST} ^(.+)\.example\.com$ [NC]
  RewriteRule ^.*$ index.php?q=%1 [L,QSA]
</IfModule>

# $Id: .htaccess,v 1.81.2.4 2008/01/22 09:01:39 drumm Exp $
{% endhighlight %}

##Ứng dụng##
Chúng ta có thể áp dụng chức năng sub-domain cho các trường hợp sau:- Multi blogger sites - Mỗi user blog có một sub-domain.- Site bán hàng - Mỗi site, mỗi shop có một domain name riêng biệt.- Các tờ báo lớn, ...- Kết hợp với module path của drupal để tạo các path tùy biến.- Kết hợp với module pathauto để hệ thống tự sinh ra các path đẹp cho: các node, hồ sơ người dùng, ...

Thế Hồng

##Tham khảo##

-  root drupal 5's .htaccess file
-  Apache document: http://httpd.apache.org/docs/1.3/mod/mod_rewrite.html

##Update #1 (2008/Dec/26)##
New custom rewrite rule, which removes domain hardcode.

{% highlight ini linenos startinline %}
<IfModule mod_rewrite.c>
  RewriteEngine on

  # Rewrite current-style URLs of the form 'index.php?q=x'.
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_URI} ^/.+$
  RewriteRule ^(.*)$ index.php?q=$1 [L,QSA]

  ###
  # Rewrite subdomain.example.com to example.com/index.php?q=subdomain
  ###

  ## Only rewrite on root level:
  ### true: foo.example.com
  ### false: foo.example.com/bar
    RewriteCond %{REQUEST_URI} ^/$

  ## is not www.example.com
    RewriteCond %{HTTP_HOST} !^(www\.){,1}([^\.]+\.(com|info|net|org))$ [NC]

  ## is something.example.com
    RewriteCond %{HTTP_HOST} ^([^\.]+)\.([^\.]+)\.(com|info|net|org)$ [NC]

  ## rewrite to example.com/index.php?q=something
    RewriteRule ^.*$ index.php?q=%1 [L,QSA]

</IfModule>
{% endhighlight %}
