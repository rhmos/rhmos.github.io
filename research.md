---
title: Research
permalink: /research/
lede: Research interests and publications.
collapse_all: true   # TEST: floating "collapse all cards" button (_includes/collapse-all.html)

# Each interest becomes a collapsible card: only the title shows until it is clicked.
# `description` is Markdown, so maths ($...$) and links work.
# Optional `image` (e.g. /assets/img/research/photo.png) and `image_alt` fill the square picture
# shown beside the description; without an image a placeholder square is shown.
# For a wide line drawing on a transparent background, add `diagram: true`: it is then shown
# full width under the description, and drawn light-on-dark in the dark theme.
# `papers` lists arXiv ids (in quotes) of entries in _data/publications.yml; each is shown as a
# link to that entry in the publication list below, which opens its abstract.
# Add, remove or reorder freely.
interests:
  - title: Coulomb branch geometry of 4d $\mathcal{N}=2$ SCFTs
    description: |
      The low-energy physics of a four-dimensional $\mathcal{N}=2$ superconformal field theory is
      encoded in the geometry of its Coulomb branch. I study which geometries can occur and what
      they imply: the allowed scaling dimensions of Coulomb branch operators, the characteristic
      dimension of these theories, and the structure of scale-invariant geometries, such as the
      result that completely (iso-)split ones are isotrivial.
    image: /assets/img/research/coulomb-branch.png
    image_alt: >-
      A Coulomb branch C with lines marking its singular locus; above a generic point alpha sits a
      smooth genus-two Riemann surface, and above a point alpha* on the singular locus a
      degenerate one
    diagram: true
    papers: ["2409.03820", "2405.19395", "2108.10884"]
  - title: Generalised symmetries, symmetry TFTs and anomalies
    description: |
      Higher-form and other generalised symmetries, and the symmetry TFTs that encode them, place
      new constraints on quantum field theories. I have studied the higher symmetries of
      five-dimensional orbifold SCFTs, the defect groups of $D_p^b(G)$ theories, and how symmetry
      TFTs and anomalies can be read off from geometric engineering. I am also a co-author of the
      Simons lectures on categorical symmetries.
    image: /assets/img/research/sym-tft.png
    image_alt: >-
      The SymTFT of a (d-1)-dimensional theory T on an interval between the boundary states
      D(B_n) and T, contracted to a single boundary giving the theory with that boundary condition
    diagram: true
    papers: ["2402.18646", "2201.08372", "2106.03878"]
  - title: Geometric engineering, orbifolds and quivers
    description: |
      Many quantum field theories arise from string theory on singular spaces. I use geometric
      engineering, in particular orbifold singularities and their McKay quivers, to construct
      theories and to understand their properties, including phenomena such as decomposition.
    image: /assets/img/research/geometric-engineering.png
    image_alt: >-
      Diagram of theories engineered from M-theory and Type IIB on the same space: a 5d N=1 theory
      reduces on a circle to a 4d N=2 theory and then to 3d N=4 quiver theories, related by 3d
      mirror symmetry
    diagram: true
    papers: ["2402.18646", "2208.07884", "2201.08372"]
---

{%- comment -%}
  The intro paragraph below is free Markdown. The interest cards come from `interests` in the
  front matter above, and the publication list from _data/publications.yml.
{%- endcomment -%}

## Research interests

I work in mathematical physics, on the structure of supersymmetric quantum field theories. Much of
my work uses geometry, both of Coulomb branches and of the singular spaces on which string theory
is compactified, to understand these theories and their symmetries.

<div class="interests">
  {%- for interest in page.interests %}
  <details class="interest">
    <summary class="interest-summary"><h3 class="interest-title">{{ interest.title }}</h3></summary>
    <div class="interest-content{% if interest.diagram %} has-diagram{% endif %}">
      <div class="interest-body">
        {{ interest.description | markdownify }}
        {%- if interest.papers %}
        <p class="interest-papers-title">Relevant papers</p>
        <ul class="interest-papers">
          {%- for id in interest.papers %}
          {%- for group in site.data.publications %}
          {%- for pub in group.items %}
          {%- if pub.arxiv == id %}
          <li><a href="#pub-{{ id | replace: '.', '-' }}">{{ pub.title }}</a> <span class="interest-paper-meta">{{ pub.venue }} {{ pub.year }}</span></li>
          {%- endif %}
          {%- endfor %}
          {%- endfor %}
          {%- endfor %}
        </ul>
        {%- endif %}
      </div>
      <figure class="interest-figure">
        {%- if interest.image %}
        <img src="{{ interest.image | relative_url }}" alt="{{ interest.image_alt | default: interest.title | strip_html | escape }}">
        {%- else %}
        <div class="interest-placeholder" aria-hidden="true">
          <svg viewBox="0 0 24 24" width="28" height="28"><rect x="3" y="4" width="18" height="16" rx="2" fill="none" stroke="currentColor" stroke-width="1.6"/><circle cx="9" cy="10" r="1.8" fill="currentColor"/><path d="M4 18l5-5 4 4 3-3 4 4" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linejoin="round"/></svg>
          <span>Picture</span>
        </div>
        {%- endif %}
      </figure>
    </div>
  </details>
  {%- endfor %}
</div>

## Publications

An up-to-date list, with citations, is on [INSPIRE](https://inspirehep.net/authors/1912084).

{%- comment -%}
  Your name is shown in bold in each author list. Entries with an `abstract` are collapsible:
  clicking the title, authors or venue shows the abstract; the links stay visible either way.
{%- endcomment -%}
{%- capture bold_name %}<strong>{{ site.author.name }}</strong>{% endcapture -%}

{% for group in site.data.publications %}
<section>
  <h2 class="section-title">{{ group.section }}</h2>
  <ol class="publications">
    {%- for pub in group.items %}
    {%- capture pub_head %}
        <span class="pub-title">{{ pub.title }}</span>
        <span class="pub-authors">{{ pub.authors | replace: site.author.name, bold_name }}</span>
        <span class="pub-venue">
          {%- if pub.venue %}<em>{{ pub.venue }}</em>{% endif -%}
          {%- if pub.volume %} <strong>{{ pub.volume }}</strong>{% endif -%}
          {%- if pub.year %} ({{ pub.year }}){% endif -%}
          {%- if pub.pages %} {{ pub.pages }}{% endif -%}
          {%- if pub.status %} <span class="pub-status">{{ pub.status }}</span>{% endif -%}
        </span>
    {%- endcapture %}
    <li class="publication"{% if pub.arxiv %} id="pub-{{ pub.arxiv | replace: '.', '-' }}"{% endif %}>
      {%- if pub.abstract %}
      <details class="pub-details">
        <summary class="pub-head pub-summary">{{ pub_head }}
        </summary>
        <div class="pub-abstract">{{ pub.abstract | markdownify }}</div>
        {%- if pub.preview %}
        <figure class="pub-preview">
          <a href="{% if pub.arxiv %}https://arxiv.org/pdf/{{ pub.arxiv }}{% elsif pub.pdf %}{{ pub.pdf | relative_url }}{% elsif pub.url %}{{ pub.url }}{% else %}{{ pub.preview | relative_url }}{% endif %}" aria-label="Read the paper">
            <img src="{{ pub.preview | relative_url }}" alt="First page of the paper" loading="lazy">
          </a>
        </figure>
        {%- endif %}
      </details>
      {%- else %}
      <div class="pub-head">{{ pub_head }}
      </div>
      {%- endif %}
      {%- if pub.arxiv or pub.doi or pub.pdf or pub.url %}
      <ul class="pub-links">
        {%- if pub.arxiv %}<li><a href="https://arxiv.org/abs/{{ pub.arxiv }}">arXiv:{{ pub.arxiv }}</a></li>{% endif %}
        {%- if pub.doi %}<li><a href="https://doi.org/{{ pub.doi }}">DOI</a></li>{% endif %}
        {%- if pub.pdf %}<li><a href="{{ pub.pdf | relative_url }}" download>PDF</a></li>{% endif %}
        {%- if pub.url %}<li><a href="{{ pub.url }}">{% if pub.url contains 'inspirehep.net' %}INSPIRE{% else %}Link{% endif %}</a></li>{% endif %}
      </ul>
      {%- endif %}
    </li>
    {%- endfor %}
  </ol>
</section>
{% endfor %}

<script>
  // Following a link to a publication (#pub-…), e.g. from a research card, opens its abstract.
  (function () {
    function openTarget() {
      var el = location.hash && document.getElementById(location.hash.slice(1));
      var details = el && el.querySelector('.pub-details');
      if (details) details.open = true;
    }
    window.addEventListener('hashchange', openTarget);
    document.addEventListener('click', function (e) {
      var link = e.target.closest('a[href^="#pub-"]');
      if (link && link.getAttribute('href') === location.hash) openTarget();
    });
    openTarget();
  })();
</script>
