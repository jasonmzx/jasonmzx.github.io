---
layout: page
title: Projects
---

<style>
  .truncate {
    /* display: inline-block; */
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    /* max-width: 400px;  */
    max-width: 100%;
  }
</style>

{% for proj in site.projects %}
  <div class="link-item">
    <h2>
      <a href="#{{ proj.title | slugify }}">#</a>
      {{ proj.title }}

    </h2>

    <p>{{ proj.description }}</p>

    <ul>
                      {% for tag in proj.tags %}
                        <li>
                          <a href="{{ '/tag/' | append: tag | relative_url }}">{{ tag }}</a></li>
                      {% endfor %}
    </ul>


    <hr style="background-color: rgba(255, 255, 255, 0.5)">
  </div>
{% endfor %}
