---
layout: home
title: Home
---

<div class="hero">
  <h1>IsakWong</h1>
  <p class="hero-role">引擎工程师 / Game & Engine Developer</p>
  <p>目前在杭州网易互娱，持续做小游戏、游戏框架与引擎能力建设。</p>
</div>

<section class="featured-projects">
  <h2>精选作品</h2>
  <div class="project-grid">
    {% for project in site.projects %}
    {% if project.featured %}
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
    {% endif %}
    {% endfor %}
  </div>
  <p class="view-all"><a href="{{ '/projects/' | relative_url }}">查看全部作品 →</a></p>
</section>
