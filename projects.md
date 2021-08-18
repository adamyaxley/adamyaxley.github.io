{% for project in site.projects %}
## {{ project.name }}
{{ project.date }}
{{ project.description }}
{% endfor %}