---
layout    : post
permalink : /book/drupal/chuan-lap-trinh-drupal-001--to-chuc-tap-tin-va-thu-muc
title     : Drupal Coding Standard
tagline   : Organize your files
comments  : true
author    : thehong
file      : ./_posts/page/2008-08-30-chuan-lap-trinh-drupal-phan-1-to-chuc-tap-tin-va-thu-muc.md
tags      : ['PHP', 'CSS', 'JQuery', 'SQL', 'Javascript']
category  : Drupal
---
{% include JB/setup %}
"Chín người, mười ý", làm sao có thể cùng làm việc chung với nhau? Chỉ có một cách là đặt ra một quy
ước chung, gọi là chuẩn, và mọi người trong cùng project đó *buộc* phải tuân thủ. Chuẩn chỉ là quy 
ước chung, không phải là cái tốt nhất, do đó, chuẩn có thể sẽ thay đổi để tốt hơn, phù hợp hơn với 
nhóm làm việc. 

Chuẩn trong lập trình có các mục:

1. Tổ chức thư mục và tập tin
2. Chuẩn viết mã PHP
3. Chuẩn viết mã SQL
4. Chuẩn viết mã CSS
5. Chuẩn viết mã Javascript

Ở phần đầu tiên này, tôi xin đề cập đến "Tổ chức thư mục và tập tin".

Đối với trường hợp của Drupal phiên bản 5.x, cho đến thời điểm bài viết này, đã có 10 lần thay đổi. 
Mỗi lần có phiên bản mới được công bố trong nhánh 5.x, chúng ta đều thấy có vá các lỗi bảo mật; và 
để đảm bảo an toàn cho các hệ thống của chúng ta, chúng ta phải nhanh chóng nâng cấp. Việc nâng cấp 
sẽ rất khó khăn, nếu như chúng ta sửa đổi nhiều nơi trong mã nguồn của nhân (core hacks), có nhiều 
module mở rộng phụ thuộc vào core hacks, ... Hiểu rõ cấu trúc thư mục và tập của Drupal, chúng ta 
sẽ tổ chức mã nguồn của chúng ta tốt hơn, dẫn đến việc bảo trì hệ thống cũng tốt hơn.

Xin chú ý là nội dung của mục này là chuẩn của tôi tự đặt ra sau vài năm làm việc với Drupal, tôi 
đặt ra theo tiêu chí:
1. Ý nghĩa rõ ràng.
2. Dễ nâng cấp.
3. Khả năng mở rộng tốt.

Khi giải nén mã nguồn nhân Drupal, chúng ta sẽ thấy cấu trúc sau:

{% highlight ini linenos %}

(i) /includes/*
(ii) /misc/*
(iii) /modules/*/*
(iv)  /profiles/*
(v) /scripts/*
(vi) /sites/all/*
(vii) /sites/default/*
(viii) /themes/*
(ix) /*.*

{% endhighlight %}

(i) Chứa các hàm chung hệ thống có thể sử dụng. Ngoại trừ trường hợp chúng ta muốn mở rộng thư viện
làm việc với cơ sở dữ liệu, thư viện xử lý ảnh, thư viện cache, thì chúng ta không nên thay đổi bất 
cứ phần nào trong thư mục này.

(ii) Chứa các tập tin hình ảnh, Javascript, CSS chung mà các module hệ thống có thể sử dụng. Việc 
thay đổi nội dung trong thư mục này cũng hết sức hạn chế, chỉ nên thay đổi trong trường hợp bất khả 
kháng -- không thể giải quyết thông qua các module mở rộng, định nghĩa các hàm quá tải giao diện.

(iii) Chứa các module của nhân. Không nên có bất kỳ thay đổi nào ở thư mục này. Xem thêm mục (vi + vii)

(iv) Chứa các hồ sơ cài đặt. Chúng ta có thể định nghĩa thêm các hồ sơ cài đặt bằng cách thêm các 
thư mục tương ứng. Thí dụ, nếu chúng ta muốn tạo một hồ sơ cài đặt "vietnamese": tạo thư mục 
/profiles/vietnamese/, tạo tập tin /profiles/vietnamese/vietnamese.profile

Như vậy, chúng ta có thể thêm profile, nhưng mã nguồn ban đầu được cung cấp bởi nhân Drupal vẫn được
giữ nguyên.

(v) Chứa các kịch bản chỉ có thể thực thi từ phía server (máy phục vụ). Đối với  các tác vụ bình 
thường thì chúng ta chưa cần sử dụng tới. Trong trường hợp cần xây dựng các kịch bản mở rộng, 
chúng ta cần định vị chúng trong các thư mục con, để tiện cho việc nâng cấp mã nguồn Drupal sau này.

(vi + vii) Trong một bài viết trước đây,  tôi có đề cập đến vấn đề sử dụng một mã nguồn Drupal để 
chạy cùng lúc nhiều site. Sở dĩ có thể thực hiện được điều này là nhờ cơ chế tìm thông tin cấu hinh
/modules/themes uyển chuyển của Drupal. Đối với thư mục /sites/all chúng ta nên chứa các giao diện 
và module với phiên bản mới nhất. Các site cụ thể, nếu muốn sử dụng phiên bản cũ hơn, 
thì có thể đặt modules/themes vào thư mục tương ứng của nó. Tổ chức tập tin theo cách này, chúng ta có thể nâng cấp nhanh chóng các modules/themes nhiều site cùng lúc.

(viii) /themes/* chứa các giao diện của hệ thống và bộ máy giao diện PHPTemplate được hệ thống cung cấp sẵn. Cũng như (iii), chúng ta không nên có thay đổi nào ở thư mục này. Trường hợp chúng ta phát triển một bộ máy giao diện mới, chúng ta cũng thể tạo thư mục mới trong /themes/engines/ vào chứa mã nguồn mở rộng của  chúng ta ở đó. Xem thêm (vi + vii).

(ix) Ở thư mục gốc, ngoài các tập tin .htaccess, robots.txt thì chúng ta không nên có thay đổi nào.