---
layout    : post
permalink : /node/3672
title     : Thời điểm Drupal AppStore bắt đầu?
comments  : false
author    : vnsiberia
file      : ./_posts/page/2011-03-18-thoi-diem-drupal-appstore-bat-dau.md
category  : Drupal
tags      : ['Drupal', 'Market']
---
{% include JB/setup %}
Trong kỳ hội nghị DrupalCon Chicago 2011 vừa qua, một kế hoạch đã được đề cập đến trong ba ngày phát biểu và thuyết trình, nói về mục đích trước mắt mà Drupal đang hướng tới, vừa là một cộng đồng, vừa là một project. Sau đây là tổng hợp toàn bộ nội dung của ý tưởng này.

###"Quần xã phần mềm" chứ không phải "tính năng"###
Trong bài phát biểu khai mạc, Dries Buytaert - nhà sáng lập Drupal đã nói rằng trong tương lai không biết chừng những gì Drupal cung cấp sẽ hơn cả tính năng. Nếu mọi người phải chọn giữa hai nền tảng tốt, ông cho rằng họ sẽ chọn nền tảng nào có "quần xã phần mềm" tốt hơn.

Nói về một hệ thống quản lí nội dung trang web, quần xã phần mềm của nó bao gồm cơ cấu tổ chức hỗ trợ cho người dùng và nhà phát triển. Vậy nên, chất lượng và số lượng công cụ dành cho các nhà phát triển, cũng như sự hiện diện của một thứ như App Store đều đóng những vai trò quan trọng tiếp thêm sức mạnh cho quần xã phần mềm.

###Công cụ và quy trình phát triển###
Lưu ý rằng ông ấy đã nói là "công cụ cho các nhà phát triển". Một cộng đồng vững mạnh là một yếu tố hết sức quan trọng, thậm chí là không thể thiếu cho bất kì dự án mã nguồn mở nào. Chính sự lớn mạnh và nhiệt tình của cộng đồng ủng hộ dự án là nguồn động lực cho hàng ngàn module và ứng dụng mở rộng ra đời. 

Buytaert đã cho rằng sự tích hợp GitHub (Git) của project là cần thiết cho nhu cầu cải thiện quần xã nhà phát triển của họm cùng với một hệ thống phân cấp project mới để đề phòng trường hợp ai đó trở nên bế tắc. Cách ông hình dung Drupal 8 được phát triển có lẽ sẽ có tác dụng như thế này: 

1. Những đoạn code của nhà phát triển nằm trong một hộp cát (sandbox) Git, kéo mã nguồn Drupal vào một môi trường riêng tư để làm nên thay đổi mà không ảnh hưởng đến code chính thức.

2. Khi họ đã quyết định thay đổi, code của họ sẽ được đi qua giai đoạn kiểm tra lỗi kỹ thuật tự động, để xem họ đang làm việc trên lõi Drupal hay trên một module

3. Nếu không có lỗi nào đáng kể, code của họ sẽ đi đến một giai đoạn kiểm tra khả năng truy cập tự động nữa để bảo đảm có thể tiếp tục công đoạn chuẩn bị hướng dẫn sử dụng cho giao diện người dùng có thể truy cập được.

4. Nếu code qua được giai đoạn kiểm tra này, nó sẽ được gửi cho những người sở hữu ban đầu, những người sẽ xem xét những thay đổi về mặt hiệu suất, khả năng sử dụng, tài liệu hay bất cứ mặt nào mà người sở hữu riêng biệt chịu trách nhiệm.

5. Những người sở hữu ban đầu sẽ lại gửi những bình luận và đề xuất của mình, cung cấp cho các nhà phát triển những ý kiến đóng góp mà họ nhận được trong thời gian qua.

6. Nhà phát triển lại thực hiện lại từ bước ban đầu của quá trình này cho tới khi nào những thay đổi của họ được chính thức chấp nhận.

Loại cấu trúc này đã rất hiệu quả với các nhà phát triển nhân Linux trong nhiều năm, cung cấp sự cân bằng tốt giữa hệ thống phân cấp và sự phát triển người theo chủ nghĩa bình đẳng. Có thể nó cũng sẽ hiệu quả cho một project phức tạp như Drupal.

###Có lẽ nên có một App Store###

Bây giờ đề cập đến một Drupal App Store, chúng ta sẽ nhận được một trong hai phản ứng: vui mừng hoặc bối rối. Nhiều người bối rối không hiểu vấn đề và có thể sẽ hỏi "Bạn không thể có mọi module từ trang Drupal.org sao?". Còn những người vui mừng thì sẽ có xu hướng gắn bó với một khía cạnh mới, chẳng hạn như install dễ dàng hoặc những mô hình kinh doanh mới.

Tất nhiên là bạn có thể có mọi module từ trang Drupal.org, nhưng bạn không thể có chúng một cách dễ dàng và tiện lợi như App Store của Apple được. Nhìn lại hồi tháng 8 năm 2010, Ravish của JustSkins.com đã tranh luận rằng một số thách mới đối với Drupal, như một đường vòng nghiên cứu phóng đại và quá nhiều module cần được sử đổi để hoạt động. Một mặt, App Store sẽ thúc đẩy sự tiến lên phía trước, kinh nghiệm đơn giản hóa với module được thiết kế để kết nối vào một trang web dễ dàng. Để làm như vậy đòi hỏi phải có một cách khác tiếp cận sự phát triển Module, nhưng đó không phải là điều gì xấu.

Những công ty như Phase 2 Technology đã và đang thử nghiệm mô hình này, xây dựng chức năng trình duyệt ứng dụng vào OpenPublic. Họ đã mời bất cứ ai có mong muốn tham gia vào cuộc thử nghiệm này để xem module ứng dụng OpenPublic. Làm như thế sẽ giúp mọi người hiểu rằng cái gì thực sự được bao gồm trong việc tiếp cận các module.

###Những mô hình kinh doanh và tính phổ biến###
Ai cũng cần ăn. Đi qua tầng trưng bày, bạn có thể thấy rõ nhiều công ty sống sót nhờ buôn bán các dịch vụ Drupal như hosting, xây dựng trang web và phát triển khách hàng. Nhưng còn những thứ như theme và module có trả phí thì sao? Bán những thứ đó cho các project có nền tảng là giấy phép công chúng có thể sẽ đầy thử thách, vì bạn không thể giới hạn những gì người ta sẽ làm với code. Tuy nhiên, những cộng đồng như WordPress và Joomla đều đã quản lí được vấn đề này.

Hôm đó Ravish đã chỉ ra rằng "Bữa này, tình trạng của Drupal cũng giống như của WordPress vào năm 2007", nghĩa là khi đó các sản phẩm WordPress không miễn phí bắt đầu xuất hiện. Chính thị trường buôn bán những sản phẩm không miễn phí đó đã đóng góp cho sự lớn mạnh của WordPress như ngày hôm nay, một phần vì số lượng - chất lượng của theme và module miễn phí tăng theo số lượng - chất lượng của những thứ không miễn phí. Nhưng liệu WordPress có một app store nào sẵn sàng để cạnh tranh không? Rất dễ để install theme và plugin miễn phí nhờ giao diện quản trị WordPress, nhưng bạn không thể cũng dùng nó cho mục đích thương mại.

Vậy Drupal có thể làm tốt hơn không? Drupal có nên tiếp tục đi hướng đó chăng? Và cuối cùng, Drupal là một nền tảng hơn là một sản phẩm chìa khóa trao tay. Chắc bạn sẽ cho rằng các app store và add-on không miễn phí thì sẽ phù hợp hơn.

Theo www.cmswire.com

Chú thích:

- **Quần xã phần mềm (Ecosystem):** Một phần mềm, tự nó xây dựng một quần xã, cho phép những phần mềm khác xây dựng (kiếm sống) quanh nó, và nuôi lại nó.