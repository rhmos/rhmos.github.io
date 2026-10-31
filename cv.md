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

<script>
  // A second logo, once it pops out, stays out for at least 1.5 seconds, and for as long as the
  // pointer is on either logo after that (the CSS shows it while .is-open is set).
  (function () {
    var LINGER = 1500;
    document.querySelectorAll('.entry-logos.has-secondary').forEach(function (logos) {
      var openedAt = 0, timer = null;
      function open() {
        clearTimeout(timer);
        if (!logos.classList.contains('is-open')) {
          logos.classList.add('is-open');
          openedAt = Date.now();
        }
      }
      function close() {
        clearTimeout(timer);
        timer = setTimeout(function () { logos.classList.remove('is-open'); },
                           Math.max(0, openedAt + LINGER - Date.now()));
      }
      logos.addEventListener('mouseenter', open);
      logos.addEventListener('mouseleave', close);
      logos.addEventListener('focusin', open);
      logos.addEventListener('focusout', function (e) { if (!logos.contains(e.relatedTarget)) close(); });
    });
  })();
</script>
