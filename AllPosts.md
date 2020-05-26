---
layout: page
navbar-links:
---

<html>
  <head>
    <meta charset="utf-8"/>
    <title>All posts</title>
  </head>
  <body>
    {% assign posts = paginator.posts | default: site.posts %}

    <div class="posts-list">
      <ul>
      {% for post in posts %}
        <li>
          <article class="post-preview">
            <a href="{{ post.url | relative_url }}">
              {{ post.title }}
            </a>
          </article>
        </li>
      {% endfor %}
      </ul>
    </div>
  </body>
</html>
