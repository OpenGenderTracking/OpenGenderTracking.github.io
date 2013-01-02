---
layout: page
show_logo: true
title: OpenGenderTracking Project
tagline: Tracking Gender Balance in News Content
---
{% include JB/setup %}

The OpenGenderTracking project aims to build software that assists with analyzing the gender balance of news content.
<br>To learn more about the project, see our <a href="/about.html">about</a> page.

<hr>

{% assign first_post = site.posts.first %}

# Latest Post: <a href="{{first_post.url}}">{{ first_post.title }}</a>
<h4 style="color:#999; font-size: 0.9em; font-weight: normal">
  Published: <span>{{ first_post.date |   date_to_long_string }}</span>
  {% unless first_post.author == empty %}
    by {{ first_post.author }}
  {% endunless %}
</h4>
<br>
{{ first_post.content }}

<div style="float:left">
  <a href="{{ first_post.url }}">Comments</a>
</div>

<div style="float:right">
  <a href="/archive.html">Read previous posts here...</a>
</div>