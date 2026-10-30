---
title: Education & Experience
permalink: /cv/
lede: Academic positions, education and selected awards.
---

{%- comment -%}
  The entries on this page come from _data/cv.yml — edit that file, not this one.
{%- endcomment -%}

{% if site.author.cv_pdf %}
<p><a class="button" href="{{ site.author.cv_pdf | relative_url }}">Download full CV (PDF)</a></p>
{% endif %}

{% include timeline.html title="Positions" items=site.data.cv.experience %}

{% include timeline.html title="Education" items=site.data.cv.education %}

{% include timeline.html title="Awards & grants" items=site.data.cv.awards %}
