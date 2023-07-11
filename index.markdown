---
layout: page
---

<div style="display: flex; flex-flow: row; align-items: flex-start;">

  <img style="width: 192px; height: 192px; margin-right: 20px;"
    src="/assets/images/android-chrome-192x192.png"
    alt="Logo: the sound hole and rosette of a hand-made classical guitar">

  <div style="display: flex; flex-direction: column; align-items: flex-start;">

    <div>
      <h2> Hello, World! </h2>
      <p>Michael Sleigh, Head of Integrated Forecast Systems at the European Centre for Medium-Range Weather Forecasts.</p>
    </div>

    <div>
      <h2> Quick links </h2>
      <p>You can find me on:
        <ul>
        {% for link in site.social.links %}
        <li><a rel="me" href="{{ link }}">{{ link }}</a></li>
        {% endfor %}
        </ul>
        </p>
        </div>

  </div>
</div>
