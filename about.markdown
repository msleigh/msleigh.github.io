---
layout: page
title: About
permalink: /about
---

I'm Michael, and I'm the Head of Integrated Forecast Systems at the [European Centre for Medium-Range Weather Forecasts](https://www.ecmwf.int).

I'm a physicist by background (I was previously the Group Leader for Computational Physics, and the Head of Profession for Physics and Maths, at [AWE](https://www.awe.co.uk)).

Now I'm interested in programming, software engineering / software development, high-performance computing, numerical modelling, and computing and technology in general. My personal interests include playing classical guitar, music, hiking, gardening, and coding.

You can find me on:
  {% for link in site.social.links %}
  - <a rel="me" href="{{ link }}">{{ link | replace: "_", "\_" }}</a>
  {% endfor %}
