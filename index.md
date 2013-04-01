---
layout: page
title: The Geek Debauchery!
tagline: Supporting tagline
---
{% include JB/setup %}

Vaibhav Bajpai is a PhD Student in the [Computer Networks and Distributed Systems](http://cnds.eecs.jacobs-university.de) research group at [Jacobs University Bremen](http://jacobs-university.de/). He is trying to understand the impact of network infrastructure changes using large-scale measurement platforms. His website offers some additional background.

[www.vaibhavbajpai.com &rarr;](http://www.vaibhavbajpai.com)  
  
<hr/>

<br/>
  
## Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
