---
title: Teaching
permalink: /teaching/
lede: Courses I have taught, most recent first.
collapse_all: true   # TEST: floating "collapse all cards" button (_includes/collapse-all.html)
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
        <div class="course-body">
          <div class="course-desc">{{ course.description | markdownify }}</div>
          {%- if course.notes or course.sheets %}
          {%- comment %} Each file links only once it is in the site; until then it shows as coming soon. {% endcomment %}
          <div class="course-materials">
            {%- if course.notes %}
            {%- assign found = site.static_files | where: "path", course.notes %}
            {%- if found.size > 0 %}
            <a class="course-notes" href="{{ course.notes | relative_url }}" download>{% include download-icon.html %}Lecture notes</a>
            {%- else %}
            <span class="course-notes is-pending">{% include download-icon.html %}Lecture notes <span class="pending-note">coming soon</span></span>
            {%- endif %}
            {%- endif %}
            {%- if course.sheets %}
            {%- assign with_solutions = course.sheets | where_exp: "sheet", "sheet.solutions" %}
            <div class="course-sheets-head">
              <h4 class="course-materials-title">Problem sheets</h4>
              {%- if with_solutions.size > 0 %}
              {%- comment %} Swaps each sheet for its version with solutions (the script at the end of the page) {% endcomment %}
              <button class="solutions-toggle" type="button" role="switch" aria-checked="false"><span class="switch-track" aria-hidden="true"></span>Solutions</button>
              {%- endif %}
            </div>
            <ul class="course-sheets">
              {%- for sheet in course.sheets %}
              <li{% if sheet.solutions %} class="has-solutions"{% endif %}>
                {%- assign found = site.static_files | where: "path", sheet.file %}
                {%- if found.size > 0 %}
                <a class="sheet-plain" href="{{ sheet.file | relative_url }}" download>{% include download-icon.html %}{{ sheet.title }}</a>
                {%- else %}
                <span class="sheet-plain is-pending">{% include download-icon.html %}{{ sheet.title }} <span class="pending-note">coming soon</span></span>
                {%- endif %}
                {%- if sheet.solutions %}
                {%- assign found = site.static_files | where: "path", sheet.solutions %}
                {%- if found.size > 0 %}
                <a class="sheet-solutions" href="{{ sheet.solutions | relative_url }}" download>{% include download-icon.html %}{{ sheet.title }} <span class="solutions-note">with solutions</span></a>
                {%- else %}
                <span class="sheet-solutions is-pending">{% include download-icon.html %}{{ sheet.title }} <span class="pending-note">solutions coming soon</span></span>
                {%- endif %}
                {%- endif %}
              </li>
              {%- endfor %}
            </ul>
            {%- endif %}
          </div>
          {%- endif %}
        </div>
        {%- if course.syllabus %}
        <div class="course-aside course-syllabus">
          <h4 class="course-materials-title">Syllabus</h4>
          {%- if course.syllabus.first %}
          <ol>
            {%- for item in course.syllabus %}
            <li><strong>{{ item.topic }}.</strong> {{ item.contents }}</li>
            {%- endfor %}
          </ol>
          {%- else %}
          <div class="course-placeholder syllabus-placeholder">Syllabus coming soon</div>
          {%- endif %}
        </div>
        {%- elsif course.image %}
        {%- assign found = site.static_files | where: "path", course.image %}
        <figure class="course-aside course-figure{% if course.diagram %} is-diagram{% endif %}">
          {%- if found.size > 0 %}
          <img src="{{ course.image | relative_url }}" alt="{{ course.image_alt }}" loading="lazy">
          {%- else %}
          <div class="course-placeholder" aria-hidden="true">
            <svg viewBox="0 0 24 24" width="28" height="28" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"><rect x="3" y="5" width="18" height="14" rx="2"/><circle cx="9" cy="10" r="1.8"/><path d="m4 18 5.5-5 4 3.5 3-2.5L21 18"/></svg>
            Photo coming soon
          </div>
          {%- endif %}
        </figure>
        {%- endif %}
      </details>
      {%- else %}
      {{ course_summary }}
      {%- endif %}
    </li>
    {%- endfor %}
  </ul>
</section>
{% endfor %}

<script>
  // The Solutions switch shows each problem sheet's version with solutions in place of the plain one
  document.querySelectorAll('.solutions-toggle').forEach(function (button) {
    var materials = button.closest('.course-materials');
    button.addEventListener('click', function () {
      var on = button.getAttribute('aria-checked') !== 'true';
      button.setAttribute('aria-checked', on);
      materials.classList.toggle('show-solutions', on);
    });
  });
</script>
