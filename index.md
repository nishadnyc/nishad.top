---
layout: default
title: Blog | NishadNYC@github
---

{% include nav.html paths="index.md,about.md" %}

<div class="home">
  <h2 class="post-list-heading">Posts</h2>
  
  <ul class="post-list">
    {% for post in site.posts %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %d, %Y" }}</span>
        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>
        {% if post.excerpt %}
          <div class="post-excerpt">
            {{ post.excerpt | strip_html | truncatewords: 30 }}
          </div>
        {% endif %}
      </li>
    {% endfor %}
  </ul>

</div>
