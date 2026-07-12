---
layout: default
title: FR05TBYTE
---

# 🦿 ↗️  🗻

I am Frost and this is my corner of the internet. I write about AI + Cyber Security.

## ✍️ articles

{% assign sorted_posts = site.posts | sort: "date" | reverse %}
{% for post in sorted_posts %}
* [{{ post.title }}]({{ post.url }})<br>Written: {{ post.date | date: "%B %d, %Y" }}{% if post.last_modified_at %}<br><span style="color: #666; font-size: 0.9em;">Updated: {{ post.last_modified_at | date: "%B %d, %Y" }}</span>{% endif %}
{% endfor %}

---

## 👤 contact me

You can reach me on [LinkedIn](https://www.linkedin.com/in/frostsec) or via [contact@frost.fyi](mailto:contact@frost.fyi)
Find me on Twitter/X [@FR05TBYTEX](https://x.com/FR05TBYTEX)

---
