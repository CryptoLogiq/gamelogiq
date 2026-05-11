{% assign previous_page = nil %}
{% assign next_page = nil %}
{% assign previous_item = nil %}
{% assign found_current = false %}

{% for section in site.data.course_sections %}
  {% assign section_pages = site.pages | where: "section", section.key | sort: "order" %}
  {% for item in section_pages %}
    {% if found_current and next_page == nil %}
      {% assign next_page = item %}
      {% assign found_current = false %}
    {% endif %}
    {% if item.path == page.path %}
      {% assign previous_page = previous_item %}
      {% assign found_current = true %}
    {% endif %}
    {% assign previous_item = item %}
  {% endfor %}
{% endfor %}

{% if previous_page or next_page %}

---

<nav class="course-pager" aria-label="Navigation entre les cours">
  <div class="course-pager__row">
{% if previous_page %}
    <a class="course-pager__button course-pager__button--prev" href="{{ previous_page.url | relative_url }}">← Précédent</a>
{% else %}
    <span class="course-pager__button course-pager__button--disabled" aria-disabled="true">← Précédent</span>
{% endif %}
{% if next_page %}
    <a class="course-pager__button course-pager__button--next" href="{{ next_page.url | relative_url }}">Suivant →</a>
{% else %}
    <span class="course-pager__button course-pager__button--disabled" aria-disabled="true">Suivant →</span>
{% endif %}
  </div>
  <a class="course-pager__home" href="{{ "/" | relative_url }}">Retour à l'accueil</a>
</nav>

{% endif %}
