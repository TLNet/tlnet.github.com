---
layout    : post
permalink : /them-views-filter-cho-date-fields
title     : Thêm views filter cho các date field
comments  : true
author    : thehong
file      : ./_posts/page/2010-03-06-them-views-filter-cho-cac-date-field.md
tags      : ['Drupal', 'Drupal 6']
category  : Drupal
---
{% include JB/setup %}
Date là một module rất tốt để bổ sung các field date/date time cho các kiểu dữ liệu. Tuy nhiên, các field này lại không hỗ trợ views-filter, cho nên chúng ta không thể sử dụng views để lọc bớt nội dung dựa trên các field này. Để thực hiện điều này, chúng ta cần phải viết module bổ sung.

Chúng ta đi xây dựng date_custom, để thêm filter cho các date field. Đầu tiên, hãy định nghĩa file info:

name = Date custom
version = 6.x-1.x-alpha-1
description = Add views-filter to date-fields
denpendencies[] = views
denpendencies[] = date
core = 6.x

Giờ là date_custom.module, chúng ta cần cho views biết module của chúng ta có tích hợp views, bằng cách implements hook_views_api():

{% highlight php linenos startinline %}
/**
 * Implements hook_views_api().
 */
function date_custom_views_api() {
  return array(
    'api' => 2,
  );
}
{% endhighlight %}

Định nghĩa xong hàm trên, views sẽ nhận biết được module của chúng ta có tích hợp views, views sẽ tự động load file date_custom.views.inc để gọi các hook mà views hỗ trợ. Ở file date_custom.views.inc, chúng ta cần định nghĩa hook_views_data_alter(&$data) để alter lên các views-data của các date-field

{% highlight php linenos startinline %}
/**
 * Implements hook_views_data_alter().
 */
function date_custom_views_data_alter(&$data) {
  // Loop to all content-fields
  foreach (content_fields() as $field) {
    // We only want to alter to date-fields
    if ($field['module'] === 'date') {
      $column_name = "{$field['field_name']}_value";
      $field_data = &$data["node_data_{$field['field_name']}"][$column_name];

      // Add basic date filter for date-field.
      $field_data['filter']['handler'] = 'date_custom_handler_filter_date';
    }
  }
}
{% endhighlight %}

Ở trên, chúng ta đã xác định handler cho filter này là class date_custom_handler_filter_date. Chúng ta cần implement date_custom_views_handlers() để cung cấp các thông tin liên quan đến clas này.

{% highlight php linenos startinline %}
/**
 * Implements hook_views_handlers().
 */
function date_custom_views_handlers() {
  return array(
    'handlers' => array(
      'date_custom_handler_filter_date' => array(
        'parent' => 'views_handler_filter_date',
        'file'   => 'date_custom_views_field_handlers.inc',
      ),
    )
  );
}
{% endhighlight %}

Chúng ta phải định nghĩa class ở một file khác, vì class thừa kế class views_handler_filter_date và class views_handler_filter_date không được định nghĩa theo mặc định.

Nội dung của file date_custom_views_field_handlers.inc có nội dung:

{% highlight php linenos startinline %}
// $Id$

class date_custom_handler_filter_date extends views_handler_filter_date {
  function op_simple($field) {
    $stamp = strtotime($this->value['value']);
    $value = date('Y-m-d', $stamp);
    
    $this->query->add_where(
      $this->options['group'], 
      "$field $this->operator '%s'",
      $value
    );
  }
}
{% endhighlight %}

Nếu không có gì trở ngại, chúng ta sẽ có filter như sau:

<img style="border: 1px #555 solid;" src="https://docs.google.com/a/toila.net/File?id=dhsf5s3g_35dcjq3mc7_b" />

Thế Hồng