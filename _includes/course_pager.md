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

{% if previous_page %}
[← Précédent : {{ previous_page.title }}]({{ previous_page.url | relative_url }})
{% endif %}

[Retour à la liste des cours]({{ "/cours/" | relative_url }})

{% if next_page %}
[Suivant : {{ next_page.title }} →]({{ next_page.url | relative_url }})
{% endif %}

{% endif %}
