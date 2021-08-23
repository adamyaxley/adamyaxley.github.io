---
layout: custom
title: Adam Yaxley
description: Portfolio
---

# About

A creative programmer who is passionate to explore his imagination, discover new ideas and turn them into a reality using the wonders of computer science.

Please contact me through [LinkedIn](https://www.linkedin.com/in/adam-yaxley-53249442/)

# Timeline

 - 2003 Started making own games at age 12
 - 2012 Graduated at the University of Warwick - Computing Systems, 1st Class Honours Bsc
 - 2012 Internship at Havok (Dublin, Ireland)
 - 2013 Software Engineer at G-Research (London, England)
 - 2015 Developer Relations Engineer at Havok (Tokyo, Japan)
 - 2017 Developer Relations Engineer 2 at Havok (Microsoft) (Tokyo, Japan)
 - 2020 Senior Developer Relations Engineer at Havok (Microsoft) (Tokyo, Japan)

# Personal Projects

{% for project in site.projects %}
<h2>
  <a href="{{ project.url }}">{{ project.title }}</a>
  <span style="float: right;">{{ project.date | date: "%Y/%m" }}</span>
</h2>
<p>{{ project.description }}</p>
{% endfor %}
