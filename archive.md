---
layout: page
permalink: /archive/
title: Archive
---

<p>Articles from my old blog website that was hosted at <a href="http://blog.therat.gr">blog.therat.gr</a>.</p>

<ul class="post-list">
  {% for doc in site.archive %}
  <li>
    <span class="post-meta">{{ doc.date | date: "%B %-d, %Y" }}</span>

    <h2>
      <a class="post-link" href="{{ doc.permalink | prepend: site.baseurl }}">{{ doc.title }}</a>
    </h2>
  </li>
  {% endfor %}
</ul>