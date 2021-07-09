---
layout: single2
permalink: /
excerpt: "Derin Mavi"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<div style="flex: 0 0 66.666667%; max-width: 66.666667%;">
  {% for post in site.posts %}
  <div style="display: flex;padding-bottom: 1rem;">
  
  <div style="width:35.16%">
	<div>
	<a href="https://derinmavi.io/images/yedinci-kita.jpg">
	<img class="tmbimg" src="https://derinmavi.io/images/yedinci-kita.jpg" alt="{{ post.title }}" height="100%" width="100%"></a>
	</div>
  </div>
  
  <div style="width:64.84%; padding-left: 1rem;">
    <div>Category</div>
    <div><time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date_to_long_string }}</time></div>
    <div><a href="{{ post.url }}">{{ post.title }}</a></div>
    <div>{{ post.description }}</div>
    <div>Yazıyı Oku</div>
  </div>
  
</div>
{% endfor %}
</div>
<div style="flex: 0 0 33.333333%; max-width: 33.333333%;">
	Test3
</div>
