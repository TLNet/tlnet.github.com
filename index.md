---
layout  : page
title   : Welcome to toila.net
tagline : Andy T's personal homepage
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

> - _I am converting old Drupal site to Jekyll -- semi static CMS, some posts maybe missing._
> - **Any question about Drupal, please ask at http://groups.drupal.org/vietnam**
