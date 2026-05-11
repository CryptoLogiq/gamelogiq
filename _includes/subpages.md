{% assign selected_section = include.section | default: page.section %}
{% assign section_pages = site.pages | where: "section", selected_section | sort: "order" %}
{% for item in section_pages %}
{% if item.path != page.path and item.order > 0 %}
{{ item.order }}. [{{ item.title }}]({{ item.url | relative_url }})
{% endif %}
{% endfor %}
