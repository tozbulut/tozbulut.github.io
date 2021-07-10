---
layout: single2
permalink: /
excerpt: "Derin Mavi"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<div style="display: flex; flex-wrap: wrap; margin-right: -15px; margin-left: -15px;">
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
	<div style="display: flex;">
    <div style="width: 50%;">Category</div>
    <div style="width: 50%;"><time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date_to_long_string }}</time></div>
	</div>
	  
    <div style="display: flex;"><a style="padding-top: 1rem; font-weight: bold; font-size: 24px; line-height: 30px; color: #212529; text-decoration: none;" href="{{ post.url }}">{{ post.title }}</a></div>
	  <div style="display: flex;"><div style=" padding-top: 1rem;">{{ post.description }}</div></div>
    <div style="display: flex;">
	    <div style="width: 50%;"></div>
	    <div style="width: 50%;">Yazıyı Oku</div>
	    </div>
  </div>
  
</div>
{% endfor %}
</div>
<div style="flex: 0 0 33.333333%; max-width: 33.333333%;">
	Test3
</div>

</div>
