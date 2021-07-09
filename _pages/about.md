---
layout: single2
permalink: /
excerpt: "Derin Mavi"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

  {% for post in site.posts %}
  <article>
    <h2>
      <a href="{{ post.url }}">
        {{ post.title }}
      </a>
    </h2>
    <time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date_to_long_string }}</time>
    {{ post.content }}
  </article>
{% endfor %}
