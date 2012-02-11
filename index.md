---
layout  : page
title   : Welcome to toila.net
tagline : Andy T's personal homepage
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    {% if post.hide != true %}
        <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>

> - _I am converting old Drupal site to Jekyll -- semi static CMS, some posts maybe missing._
> - **Any question about Drupal, please ask at http://groups.drupal.org/vietnam**

<div id="ninja">
    <style>
        .row .span14 {
            position: relative;
        }
        #ninja {
            background: url(/sites/toila.net/files/pictures/ninja.gif) -2px -11px no-repeat; 
            height: 122px;
            width: 286px;
            position: absolute;
            top: 0;
            left: 554px;
        }
    </style>
</div>
