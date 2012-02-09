---
layout    : post
permalink : /drupal/hook_menu_alter-lam-duoc-lam-tro
title     : hook_menu_alter làm được lắm trò
comments  : true
author    : thehong
file      : ./_posts/page/2009-05-11-hook-menu-alter-lam-duoc-lam-tro.md
tags      : ['Drupal', 'Drupal 6', 'hook']
category  : Drupal
---
{% include JB/setup %}
Hệ thống menu ở Drupal 6 đã được cải tiến rất nhiều, đẹp hơn, gọn hơn và uyển chuyển hơn. Đáng kể nhất ở đây là hook_menu_alter đã được thêm vào, giúp người thảo chương thực hiện một số thao tác tưởng chừng khó mà nay rất dễ.

Các bước để Drupal xây dựng cấu trúc menu là:
1. Gọi các hook_menu của các module để lấy về các menu items.
2. Gọi hook_menu_alter của các module, cho phép chúng thay đổi tuỳ ý cấu trúc menu vừa được thu lượm.
3. Lưu cấu trúc menu items đã được alter vào CSDL.

Một trang trong Drupal được định nghĩa đầy đủ bởi một menu item, bao gồm, path, quyền truy cập, tiêu đề trang, callback, ... như vậy, thay đổi cấu trúc một menu item, có dẫn đến việc thay đổi hoàn toàn một trang đang có.
Hệ thống menu ở Drupal 6 đã được cải tiến rất nhiều, đẹp hơn, gọn hơn và uyển chuyển hơn. Đáng kể nhất ở đây là hook_menu_alter đã được thêm vào, giúp người thảo chương thực hiện một số thao tác tưởng chừng khó mà nay rất dễ.

Các bước để Drupal xây dựng cấu trúc menu là:
1. Gọi các hook_menu của các module để lấy về các menu items.
2*. Gọi hook_menu_alter của các module, cho phép chúng thay đổi tuỳ ý cấu trúc menu vừa được thu lượm.
3. Lưu cấu trúc menu items đã được alter vào CSDL.

Một trang trong Drupal được định nghĩa đầy đủ bởi một menu item, bao gồm, path, quyền truy cập, tiêu đề trang, callback, ... như vậy, thay đổi cấu trúc một menu item, có dẫn đến việc thay đổi hoàn toàn một trang đang có.

Thí dụ, workflow tab của một node được định nghĩa bởi một menu item có dạng sau:

{% highlight php linenos startinline %}
  $items['node/%node/workflow'] = array(
    'title' => 'Workflow',
    'type' => MENU_LOCAL_TASK,
    'access callback' => 'workflow_node_tab_access',
    'access arguments' => array(1),
    'page callback' => 'workflow_tab_page',
    'page arguments' => array(1),
    'file' => 'workflow.pages.inc',
    'weight' => 2,
  );
{% endhighlight %}

Nếu như chúng ta thay đổi, thuộc tính cho `access callback` thành `my_workflow_node_tab_access` quyền truy cập của user vào node này, không còn phụ thuộc vào hàm workflow_node_tab_access() nữa, mà phụ thuộc vào hàm 'my_workflow_node_tab_access'.
  
Khi làm việc với các project, rất có thể chúng ta gặp phải các trường hợp như sau, và hook_menu_alter có thể giúp chúng ta giải quyết dễ dàng:

1. Module print_pdf xử lý quá nặng nề để tạo ra file PDF > 1 MB. Coder cần tích hợp module captcha, buộc người dùng nhập mã chống bot trước khi tải về.
2. Coder xây dựng module tuỳ chỉnh để thêm quyền truy cập vào workflow tab.
3. Text field nhập tên người dùng, trong hộp soạn thảo node, có tính năng auto-complete rất hay, tuy nhiên, kết quả trả về không có highlight. Coder có nhiệm vụ highlight từ khóa trong kết quả này.
4 ...

hook_menu_alter làm được lắm trò, nhỉ.