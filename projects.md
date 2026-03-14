---
layout: page
title: 作品集
permalink: /projects/
---

<div class="project-grid">
  {% for project in site.projects %}
  <a class="project-card" href="{{ project.url | relative_url }}">
    {% if project.cover %}
    <div class="project-cover" style="background-image: url('{{ project.cover | relative_url }}');"></div>
    {% endif %}
    <div class="project-card-body">
      <h3>{{ project.title }}</h3>
      <p>{{ project.description }}</p>
      <div class="project-tags">
        {% for tag in project.tags %}<span class="tag">{{ tag }}</span>{% endfor %}
      </div>
    </div>
  </a>
  {% endfor %}
</div>

{% if site.projects.size == 0 %}
<p>作品整理中，敬请期待。</p>
{% endif %}
