---
layout: home
title: Home
---

<div class="hero">
  <h1>IsakWong</h1>
  <p class="hero-role">Game & Engine Developer</p>
  <p>专注游戏开发与引擎技术，热衷于图形渲染、物理模拟与工具链开发。</p>
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
