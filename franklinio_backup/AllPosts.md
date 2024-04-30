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
    <h1>All the posts</h1>
    <p>
    {% assign posts = paginator.posts | default: site.posts %}
    <div class="posts-list">
      <ul>
      {% for post in posts %}
        <li>
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </li>
      {% endfor %}
      </ul>
    </div>
    </p>
  </body>
</html>
