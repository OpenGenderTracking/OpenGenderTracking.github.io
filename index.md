---
layout: page
---
{% include JB/setup %}

{% assign first_post = site.posts.first %}

# <a href="{{first_post.url}}">{{ first_post.title }}</a>
<div class="posted-by">
  Published: <span>{{ first_post.date |   date_to_long_string }}</span>
  {% unless first_post.author == empty %}
    by {{ first_post.author }}
  {% endunless %}
</div>
<br>
{{ first_post.content }}
<div class="secondary-footer">
  <div style="float:left">
    <a href="{{ first_post.url }}">Comments</a>
  </div>

  <div style="float:right">
    <a href="/archive.html">Read previous posts here</a>
  </div>
</div>