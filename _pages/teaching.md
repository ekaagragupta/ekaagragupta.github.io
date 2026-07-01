---
layout: page
permalink: /teaching/
title: community
description: Workshops, mentoring, technical talks, and community contributions.
nav: true
nav_order: 6

display_categories:
  - mentoring
  - community

horizontal: false
---

{% assign teachings = site.teachings | sort: "importance" %}

{% if page.display_categories %}
  {% for category in page.display_categories %}

  <a id="{{ category }}"></a>
  <div class="publications">
    <h2 class="category">{{ category }}</h2>

    {% assign categorized = teachings | where: "category", category %}

    {% if page.horizontal %}
      <div class="container">
        <div class="row row-cols-1 row-cols-md-2">
          {% for item in categorized %}
            {% include projects_horizontal.liquid %}
          {% endfor %}
        </div>
      </div>
    {% else %}
      <div class="grid">
        {% for item in categorized %}
          {% include projects.liquid %}
        {% endfor %}
      </div>
    {% endif %}

  </div>

  {% endfor %}

{% else %}

<div class="grid">
{% for item in teachings %}
{% include projects.liquid %}
{% endfor %}
</div>

{% endif %}