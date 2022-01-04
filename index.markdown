---
layout: default
permalink: /
---

<div class="post-container">
	{% for post in site.posts %}
        {% if post.external_url %}
        {% else %}
        <div class="post-list">
            <a class="post-title" href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
<!--            {% for tag in post.tags %}
                {{ tag }}
            {% endfor %} -->
            <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">{{ post.date |  date_to_long_string: "ordinal", "US" }}</time>
        </div>
    {% endif %}
    {% endfor %}
    <h2>External Posts</h2>
    {% for post in site.posts %}
        {% if post.external_url %}
        <div class="post-list">
            <a class="post-title" href="{{ post.external_url }}">{{ post.title }}</a>
            <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">{{ post.date | date_to_long_string: "ordinal", "US" }}</time>
        </div>
        {% endif %}
    {% endfor %}
</div>
