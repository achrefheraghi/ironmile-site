---
layout: default
wide: true
title: Support
description: How to get help with Ironmile apps, plus every app's privacy policy and terms.
---
<p class="prose">Email <a href="mailto:support@ironmile.dev">support@ironmile.dev</a>. We reply by email. Each app's support page says what to include.</p>
<div class="index-grid" id="legal">
{% for p in site.data.products %}{% unless p.external %}
<section class="index-card">
  <header><img src="{{ p.icon }}" alt="" width="40" height="40"><h2>{{ p.name | escape }} <span class="muted">{{ p.suffix }}</span></h2></header>
  <ul>
    <li><a href="/{{ p.slug }}/support">Support</a></li>
    <li><a href="/{{ p.slug }}/privacy">Privacy policy</a></li>
    {% if p.security_page %}<li><a href="/{{ p.slug }}/security">Security policy</a></li>{% endif %}
    <li><a href="/{{ p.slug }}/terms">Terms of service</a></li>
  </ul>
</section>
{% endunless %}{% endfor %}
</div>
<p class="prose">Ironmile is the trading name of Achref Heraghi, Tunisia.</p>
