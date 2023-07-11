---
layout: page
title: Repositories
permalink: /repositories
---

An automatically-generated list of all my public repositories on GitHub:

{% for repository in site.github.public_repositories %}
* [{{ repository.name }}]({{ repository.html_url }}) {% if repository.description %} --- {{ repository.description }} {% endif %}
{% endfor %}