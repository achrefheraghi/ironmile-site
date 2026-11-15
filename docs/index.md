---
layout: default
wide: true
title: Documentation
description: Documentation and guides for every Ironmile app.
---
<p class="muted">Setup, usage and limits for each app.</p>
<div class="index-grid">
{% for p in site.data.products %}{% unless p.external %}
<section class="index-card">
  <header><img src="{{ p.icon }}" alt="" width="40" height="40"><h2>{{ p.name | escape }} <span class="muted">{{ p.suffix }}</span></h2></header>
  <ul>
    <li><a href="{{ p.docs_url }}">{{ p.docs_label | default: 'Documentation' }}</a></li>
    {% for l in p.extra_links %}<li><a href="{{ l.url }}">{{ l.label }}</a></li>{% endfor %}
    <li><a href="/{{ p.slug }}/">Product page</a></li>
  </ul>
</section>
{% endunless %}{% endfor %}
</div>
