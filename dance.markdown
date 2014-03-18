---
layout: default
title: Dance Posts
---
#### Dance

{% for post in site.posts %}
  {% if post.categories contains 'dance' %}
* {{post.date | date_to_string}} - [{{post.title}}]({{post.url}})
  {% endif %}
{% endfor %}
