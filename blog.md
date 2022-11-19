---
layout: default
permalink: /blog
---

<div class="post-container">
	{% for post in site.posts %}
        {% if post.external_url %}
        {% elsif post.tags contains "skip" %}
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

</div>

<h2>External Posts</h2>
<div class="post-container">
    <div class="post-list">
        <a class="post-title" href="https://medium.com/pinterest-engineering/addressing-python-dependency-confusion-at-pinterest-e0a0609c8e9">Addressing Python Dependency Confusion at Pinterest
        </a>
        <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">March 10, 2022</time>
    </div>
    <div class="post-list">
        <a class="post-title" href="https://medium.com/google-cloud/a-tensorflow-glossary-cheat-sheet-382583b22932"> A TensorFlow Glossary/Cheat Sheet</a>
        <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">August 29, 2017</time>
    </div>
     <div class="post-list">
        <a class="post-title" href="https://medium.com/google-cloud/scalable-video-transcoding-with-app-engine-flexible-621f6e7fdf56">  Scalable Video Transcoding with App Engine Flexible </a>
        <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">August 29, 2017</time>
    </div>
     <div class="post-list">
        <a class="post-title" href="https://medium.com/google-cloud/local-django-on-kubernetes-with-minikube-89f5ad100378">  Local Django on Kubernetes with Minikube </a>
        <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">December 13, 2016</time>
    </div>
</div>
