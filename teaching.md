---
title: Teaching
permalink: /teaching/
lede: Courses I have taught, most recent first.
---

{%- comment -%}
  The intro below is free Markdown. The course lists come from _data/teaching.yml.
{%- endcomment -%}

I have taught mathematics at Uppsala University and Durham University since 2019, lecturing and
leading tutorial groups for students of mathematics, physics, engineering, computing and biology.

{% for group in site.data.teaching %}
<section>
  <h2 class="section-title">{{ group.section }}</h2>
  <ul class="courses">
    {%- for course in group.courses %}
    {%- capture course_summary %}
      <div class="course-head">
        <h3 class="course-title">
          {%- if course.url %}<a href="{{ course.url | relative_url }}">{{ course.title }}</a>{% else %}{{ course.title }}{% endif -%}
        </h3>
        {%- if course.code %}<span class="course-code">{{ course.code }}</span>{% endif %}
      </div>
      <p class="course-meta">
        {{ course.role }}{% if course.role and course.institution %} · {% endif %}{{ course.institution }}
      </p>
      {%- if course.terms %}
      <ul class="tags">
        {%- for term in course.terms %}<li>{{ term }}</li>{% endfor %}
      </ul>
      {%- endif %}
    {%- endcapture %}
    <li class="course">
      {%- comment %} Cards with a description collapse; the description shows only when opened. {% endcomment %}
      {%- if course.description %}
      <details class="course-details">
        <summary class="course-summary">{{ course_summary }}</summary>
        <div class="course-desc">{{ course.description | markdownify }}</div>
      </details>
      {%- else %}
      {{ course_summary }}
      {%- endif %}
    </li>
    {%- endfor %}
  </ul>
</section>
{% endfor %}
