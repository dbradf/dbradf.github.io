---
layout: default
title: Technology Posts
---
#### Technology Posts

{% for post in site.posts %}
  {% if post.categories contains 'technology' %}
* {{post.date | date_to_string}} - [{{post.title}}]({{post.url}})
  {% endif %}
{% endfor %}
