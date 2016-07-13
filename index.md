---
layout: page
title: Engineer the world to be a better place!
tagline: Supporting tagline
---
{% include JB/setup %}

Some information to be appeared here soon!

<div id="articles">
{% for post in site.posts limit:3%}
  <article>
    <div class="item">
      <div class="item_details">
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <h4><a href="{{ post.url }}" title="{{ post.title }}">{{ post.date | date_to_long_string }}</a> by <a href="http://twitter.com/_azarnyx">Dmitrii Azarnykh</a></h4>
      </div>
      <div class="item_content">
        {{ post.content }}
      </div>
      <div class="item_meta">
        <span class="item_tags">
          Tags: 
          {% for tag in post.tags %}
          <a href="/tags/{{ tag }}.html" title="View posts tagged with &quot;{{ tag }}&quot;">{{ tag }}</a>{% if forloop.last != true %}, {% endif %}
          {% endfor %}
        </span>
      </div>
    </div>
  </article>
{% endfor %}
</div>

## Recent Posts

Some posts will be here:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



