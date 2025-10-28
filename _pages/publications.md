---
layout: page
permalink: /publications/
title: publications
description: An updated list of all published papers including refereed and non-refereed ones is available from <a href='https://scholar.google.com/citations?user=wgsX_zIAAAAJ&hl=en'>Google Scholar</a>
years: [2025, 2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015, 2014]
nav: true
nav_order: 3
---

Source codes are publicly available here: https://github.com/icclabo?tab=repositories

<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
