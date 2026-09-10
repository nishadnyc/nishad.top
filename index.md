---
layout: default
image: "https://avatars.githubusercontent.com/u/186933450?v=4"
order: 1
---

### Interactive Shell

{% include terminal-shell.html %}

<div class="home">
  <h2 class="post-list-heading">Recent Projects</h2>
  
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
            {{ post.excerpt | strip_html | truncatewords: 100 }}
          </div>
        {% endif %}
      </li>
    {% endfor %}
  </ul>

</div>
