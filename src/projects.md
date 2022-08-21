---
title: Personal Projects
layout: "base.njk"
---

A little showcase of my latest personal projects:

<br>

{% for post in collections.posts reversed %}

[{{ post.data.title }}]({{ post.url }}) ∘ {{ post.data.date | postDate}}



{{ post.data.description }}


<br>


{% endfor %}

