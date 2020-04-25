---
layout: null
---
{% assign testimonials = site.data.testimonials | sort | reverse %}
{% for testimonial in testimonials %}
  {% assign name = testimonial[1].name %}
  {% assign date = testimonial[1].date %}
  {% assign message = testimonial[1].message %}
  {{ name }}<br>
  {{ date | date: '%a %-d %b %Y @%H:%M' }}<br>
  {{ message }}<br>
{% endfor %}
