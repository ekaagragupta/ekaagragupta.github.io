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

<div class="projects">

{% assign teachings = site.teachings | sort: "importance" %}

{% if page.display_categories %}

  {% for category in page.display_categories %}

    <a id="{{ category }}" href=".#{{ category }}">
      <h2 class="category">{{ category }}</h2>
    </a>

    {% assign categorized_teachings = teachings | where: "category", category %}

    {% if page.horizontal %}

      <div class="container">
        <div class="row row-cols-1 row-cols-md-2">

          {% for project in categorized_teachings %}
            {% include projects_horizontal.liquid %}
          {% endfor %}

        </div>
      </div>

    {% else %}

      <div class="row row-cols-1 row-cols-md-3">

        {% for project in categorized_teachings %}
          {% include projects.liquid %}
        {% endfor %}

      </div>

    {% endif %}

  {% endfor %}

{% else %}

  {% if page.horizontal %}

    <div class="container">
      <div class="row row-cols-1 row-cols-md-2">

        {% for project in teachings %}
          {% include projects_horizontal.liquid %}
        {% endfor %}

      </div>
    </div>

  {% else %}

    <div class="row row-cols-1 row-cols-md-3">

      {% for project in teachings %}
        {% include projects.liquid %}
      {% endfor %}

    </div>

  {% endif %}

{% endif %}

</div>