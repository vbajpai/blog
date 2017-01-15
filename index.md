---
layout: page
tagline: Supporting tagline
---
{% include JB/setup %}

Vaibhav Bajpai is a Postdoctoral Fellow at [TU
München](https://www.tum.de). His website offers some additional
background.

[www.vaibhavbajpai.com &rarr;](http://www.vaibhavbajpai.com)  
  
<hr/>

<br/>
  
## Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
