---
layout    : post
permalink : /drupal-6-views-2-and-its-concepts
title     : Views 2 và các khái niệm
comments  : true
author    : thehong
file      : ./_posts/page/2008-07-07-views-2-va-cac-khai-niem.md
tags      : ['Drupal', 'Modules', 'Views']
category  : Drupal
---
{% include JB/setup %}
Update 1: Add sponsor link.

Sử dụng thuần thục hệ thống Drupal, với các khái niệm node, node type, taxonomy, user, roles, 
roles's permission, chúng ta đã có thể áp dụng được Drupal vào các nhu cầu thực tế. Tuy nhiên, xét 
về khả năng trình bày nội dung, bản thân Drupal chưa đưa ra được các khả năng cần thiết. Thí dụ, 
chúng ta sẽ thực hiện những thao tác nào để tìm ra:

- Người dùng tích cực nhất từ thời điểm t đến  thời điểm t + t'?
- Vocabulary nào có nhiều nội dung nhất, và những term được người dùng đọc nhiều nhất.
- Top 10 người dùng mới nhất của site.
- Những node có kiểu nội dung C, thuộc vocab V, có term T của người dùng thuộc role R.
- Top 10 chủ đề mới nhất/nóng nhất từ diễn đàn D...
- Top 10 node có liên kết trở về node N.- ...

Không chỉ đáp ứng được những tính năng kể trên, views 2 sẽ còn mạnh mẽ hơn rất nhiều. Sử dụng views 
2 không khó, nhưng bạn cần phải thông một số khái niệm.

###1. View###
Module views 2 định nghĩa nhiều view. Mỗi view sẽ có những cấu hình khác nhau, tuỳ thuộc vào người 
quản trị, để trình những kết quả khác nhau phù hợp với nhu cầu của thực tế.

###2. Type###
views có thể lấy nội dung từ nhiều kiểu nội dung khác nhau. Để định nghĩa một view, trước tiên, 
chúng ta cần xác định, kiểu nội dung chúng ta cần lấy về là gì. Mặc định, views 2 có cung cấp các 
kiểu nội dung sau: node, vocabulary, term, user, roles, files, comment. Trường hợp hệ thống của chúng
ta có sử dụng các module khác để mở rộng views 2, có thể danh sách các kiểu nội dung sẽ nhiều hơn.

###3. Display###
Views cần biết được thuộc tính Display của mỗi view để xác định vị trí mà kết quả của view tương ứng
được hiển thị. Mỗi view có thể có nhiều display, mỗi display lại có thể có những thiết lập riêng để 
tuỳ chỉnh kết quả trình bày. Nói về Display, mặc định, Views cung cấp một số Display type được liệt 
kê như sau. Nếu hệ thống của chúng ta có sử dụng các module khác để mở rộng views 2, lúc đó, có thể 
hệ thống sẽ có nhiều dislay type hơn, thí dụ JSON.

####3.1 Default display####
Default display, là display chính của mỗi view, được dùng để lưu trữ các thiết lập của view. Default 
display không thật sự được sử dụng ở bất kỳ nơi nào, ngoại trừ bên trong hệ thống Views 2.

####3.2 Page display####
Mỗi page display có thiết lập **path** và các tùy chọn thiết lập về **menu**. Khi trình bày một view
ở dạng page display, kết quả của view sẽ được trình bày như nội dung chính của một trang, nghĩa là,
kết quả của view sẽ được trình bày ở khu vực trình bày nội dung chính khi bạn truy cập vào URL ứng 
với **path** đã thiết lập cho page display.

Page display, nếu có các thiết lập về argument, sẽ nạp vào nó các argument từ URL. Chúng ta có thể 
nhúng các argument vào URL bằng cách sử dụng ký hiệu %. Thí dụ. thiết lập URL của chúng ta là 
'node/%/foo', ứng với trường hợp display/view tương ứng có các thiết lập về argument, khi đó, page 
display sẽ được sử dụng, khi người dùng truy cập vào URL 'node/1/foo', và tham số đầu tiên sẽ là '1'.

####3.3 Block display####
Nếu một view có định nghĩa một/nhiều block display, nó đồng thời cũng sẽ định nghĩa các block trong 
hệ thống Drupal với nội dung tương ứng với các thiết lập của block display.

Chú ý: block display không chấp nhận argument như các dạng view display khác. Trong trường hợp, 
chúng ta cần sử dụng argument cho các block display, để mở rộng khả năng trình bày, chúng ta buộc 
phải truyền argument vào ở dạng **argument mặc định**; Cách thực hiện: cấu hình view tương ứng > 
chọn display tương ứng > xem mục Arguments > nhấp chọn argument tương ứng > xem mục "Action to take 
if argument is not present" vừa hiện ra > chọn "Provide default argument" > xem mục "Default argument
type" vừa hiện ra. Nếu chọn "PHP Code" có thể nhập đoạn php code tương tự như sau (không cần cặp thẻ
đóng mở php):

{% highlight php linenos startinline %}
if (arg(0) == 'node' && is_numeric(arg(1))) {
  return arg(1);
}
{% endhighlight %}

####3.4 Attachment display####
Attachment display là các display có thể được đính kèm vào các display khác ở cùng view. Khi một 
display được gọi, thì đồng thời các attachment display được kèm theo với display đó cũng được gọi,
và kết quả của các attachment display có thể được định vị ở trước hoặc sau hoặc cả trước và sau kết 
quả của display chính của view. Có thể sử dụng attachment display để trình bày bảng danh mục (glossary)
cho các view. Xem view "glossary" được cung cấp mặc định bởi view như một thí dụ cho việc sử dụng 
Attachment display.

####3.5 Feed display####
Feed display cho phép chúng ta đính kèm RSS feed vào một view.

###4. Override###
Như đã biết ở mục 3, mỗi view có thể có một default display và có thể định nghĩa thêm một hoặc nhiều
các display khác, với các dislay type tùy thích mà view cung cấp. Theo mặc định, các display, khác
default display, sẽ sử dụng các thiết lập của default display cho việc tạo kết quả trình bày của 
chúng. Do đó, nếu chúng ta chỉnh sửa các thiết lập của một display, thì các display khác ở cùng một
view cũng sẽ bị ảnh hưởng. Giải quyết trở ngại này, views 2 có đưa ra khả năng "override", giúp cho
các display, ngoài việc sử dụng các thiết lập từ default display, có thể có những thiết lập riêng cho
nó, các thiết lập này, nếu được chỉnh sửa, thì không ảnh hưởng đến các display khác ở cùng view.

###5. Output style (view style)###

View phát sinh ra kết quả, hệ thống style giúp chúng ta có thể tuỳ chỉnh cách trình bày kết quả được 
phát sinh đó. Về cơ bản, mỗi output style là một khuôn mẫu giao diện thông minh, xử lý kết quả quả của 
view và xuất kết quả đó ra. Tất cả các style trong Views 2 đều có thể được quá tải bằng cách đặt bản 
các bản sao chép của style tương ứng vào thư mục giao diện mà hệ thống đang sử dụng, sau đó, chỉnh 
sửa chúng. Mỗi display của view có cung cấp một mục "theme: information", nhấp chọn vào mục đó, 
views 2 sẽ đề xuất cho chúng ta các khuôn mẫu giao diện có thể được sử dụng đê quá tải lên các thành
phần kết quả của view.

Các output style được views 2 cung cấp sẵn:- 5.1 Grid: Trình bày kết quả ở dạng ô.- 5.2 List: Trình 
bày kết quả ở dạng danh sách- 5.3 Table: Trình kết quả ở dạng bảng- 5.4 Unformatted: Trình bày kết 
quả ở đơn giản, mỗi dòng kết quả chỉ được bao quanh bởi cặp thẻ  với một số DOM class, dựa vào các 
class đơn giản này, quản trị viên có thể sử dụng CSS để định dạng lại kết quả trình bày.

Trường hợp các output style được cung cấp sẵn này không đáp ứng đủ nhu cầu thực tế, chúng ta có thể 
xây dựng module mở rộng views 2 để định nghĩa thêm các output style khác.

###6. Field (trường dữ liệu)###
Đối với một số output style, thí dụ table, chúng ta cần xác định cụ thể trường dữ liệu nào được 
trình bày trong kết quả trình bày. Tùy thuộc và trường dữ liệu được xác định, chúng ta có thể có 
những thiết lập riêng cho chúng.

###7. Sort criteria###
Các dòng kết quả được phát sinh bởi view có thể được sắp xếp thứ tự theo một hoặc nhiều tiêu chí. 
Tuỳ thuộc vào view type (và các relationship), mỗi view sẽ có những tùy chọn sắp xếp thứ tự kết quả
trình khác nhau.

###8. Filter###
Filter, hay bộ lọc nội dung, là một tính năng chủ chốt của views 2, giúp người điều hành có thể lọc 
nội dung theo những tiêu chí nhất định. Không như các tính năng liệt kê node của nhân Drupal, 
/node/, chỉ liệt kê được các node được thiết lập thuộc tính "promoted to frontpage" (được quảng bá 
ở trang chủ) là true, /taxonomy/term/x/, chỉ liệt kê được các node có gán từ liệu là x, ... views 
với tính năng filter, cung cấp khả năng trình bày nội dung của hệ thống rất sinh động. Với views 2, 
bây giờ, chúng ta có thể trình bày các node được tạo bởi một người dùng nhất định, ở (các) term 
nhất định, vào thời khoảng nhất định, ...

###9. Argument###
Tính năng filter của Views 2 mạnh, tuy nhiên nó cũng có mổt trở ngại nhỏ: filter không động theo 
từng view. Thí dụ, chúng ta định nghĩa một view V1 để trình bày các node có node type là NT1, có 
thể truy cập view này qua URL /content/foo. Sau một thời gian, theo nhu cầu phát triển của hệ thống,
chúng ta lại cần xây dựng một view V2 rất giống với V1, chỉ khác ở filter node type, thay vì node 
type là NT1 thì là NT2. Rõ ràng, lúc này, chúng ta phải lặp lại nhiều thao tác đã thực hiện ở V1 
vào lại V2. Giả sử, chúng ta có N view như vậy, khi chỉnh sửa các view này theo nhu cầu thực tế, 
công sức của chúng ta sẽ xN.

Argument được đặt ra như là một mở rộng của filter. Thay vì là tĩnh ở mỗi view, argument cung cấp 
khả năng lọc nôi dung trong view bằng các giá trị có thể thay đổi động. Trở lại với thí dụ trên, 
thay vì định nghĩa một filter clause cho view, chúng ta sẽ định nghĩa một argument: "node type", 
và ở URL, chúng ta sẽ thay /content/foo  thành /content/foo/%. Lúc này, khi người dùng truy cập URL
/content/foo/NT1, view sẽ lọc nội dung và chỉ trả về những node có node type là NT1, ...

###10. Relationships###
Là một tính năng mới thêm vào Views 2, cung cấp cho view khả năng truy vấn kết quả khác từ các kết 
quả đã tìm được. Một thí dụ thực tế tương đối dễ hiểu: (1) Hệ thống chúng ta vừa tạo ra một node 
type là "track". (2) Chúng ta tạo thêm hai node type khác là "album" và "artist". (3) Tạo node 
reference từ "track" đến "album", từ "album" đến "artist" (Sử dụng module node reference của CCK) (4)
Tạo một vào node ứng với các node type vừa tạo ở trên (5.1) Tạo một view; (5.2) Thiết lập output 
style thành "table"; (5.3) Ở mục "relationships", thêm vào 2 node reference đã tạo ở bước 3; (5.4) 
Ở mục "fields", thêm 3 lần field "Node: Title" và "Node: Body", ở node thứ nhì, chọn relatioship 
đến 'albumn', và ở node thử ba, chọn relationship đến 'artist' (6) Xem thử kết quả.

###11. Các thuộc tính khác###

####11.1 Tags####
Có thể gán cho mỗi view những tag khác nhau để dễ dàng hơn cho việc quản lý.

####11.2 View name####
Là tên của view được xác định lúc view mới được khởi tạo. Không giống như các display name (tên của 
display), view name không thể chỉnh sửa.

####11.3 Use AJAX####
Nếu view/output tương ứng có thiết lập sử dụng pager và thuộc tính Use AJAX được thiết lập là Yes, 
khi người dùng click vào các liên kết ở mục phân trang, thay vì trình duyệt sẽ di chuyển sang trang, 
thì nội dung mới sẽ được nạp theo dạng AJAX.

####11.4 Use pager####
Thiết lập view có sử dụng bộ phân trang hay không.

####11.5 Items to display####
Số dòng kết quả trình bày ở mỗi lần trình bày của view/output sẽ không vượt quá giá trị thiết lập ở 
mục này. Nên thiết lập để view/output sử dụng bộ phân trang để người dùng có thể xem được nhiều kết
quả hơn.

####11.6 More link####
Thêm liên kết, vào phía dưới kết quả của view, dẫn đến page view. Trường hợp view của chúng ta cung 
cấp hơn một page display, mục này cần chỉ định rõ page display nào cần được trỏ đến.

####11.7 Distinct####
Buộc view chỉ trình bày những kết quả thật sự khác nhau. Thuộc tính này có thể làm chậm đi quá trình
phát sinh kết quả của view.

####11.8 Access####
Giới hạn các vai trò người dùng (role) được truy cập view/output.

####11.9 Header####
Bản văn được trình bày ở phía trên của view/output.

####11.10 Footer####
Bản văn được trình bày ở phía dưới của view/output.

####11.11 Empty text####
Bản văn được trình bày khi view/output không trả về kết quả nào.

####11.12 Theme information####
Trình bày các thông tin về giao diện giúp người xây dựng giao diện của hệ thống có thể dễ dàng xây 
dựng các khuôn mẫu giao diện quá tải.

Thế Hồng @JOC