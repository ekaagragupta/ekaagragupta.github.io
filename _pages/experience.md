---
layout: page
title: experience
permalink: /experience/
nav: true
nav_order: 2
---

<div class="experience">

{% assign experiences = site.experience | sort: "importance" | reverse %}

{% for experience in experiences %}

<details class="mb-4">

<summary>

<h3 style="display:inline;">
{{ experience.title }}
</h3>

<p style="margin:0;color:gray;">
{{ experience.company }} • {{ experience.duration }}
</p>

</summary>

<div class="mt-3">

{{ experience.content }}

</div>

</details>

{% endfor %}

</div>