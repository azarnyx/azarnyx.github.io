---
layout: page
title: Engineer the world <br /> to be a better place!
tagline: Supporting tagline
---
{% include JB/setup %}

Some information to be appeared here soon!

## Recent Posts

Some posts will be here:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



