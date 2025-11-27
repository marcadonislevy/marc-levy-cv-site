---
layout: home
title: "Marc Levy | Commercial & Data Infrastructure Leadership"
author_profile: true
---

{% assign about_page = site.pages | where: "permalink", "/about/" | first %}
{% if about_page %}
{{ about_page.content | markdownify }}
{% else %}
<!-- About page content not found. -->
{% endif %}
