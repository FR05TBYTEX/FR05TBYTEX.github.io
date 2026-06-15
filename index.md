---
layout: default
title: FR05TBYTE
---

# 🦿 ↗️  🗻

I am Frost and this is my corner of the internet. I write about AI + Cyber Security.

## ✍️ articles
{% assign sorted_posts = site.posts | sort: "date" | reverse %}
{% for post in sorted_posts %}
* [{{ post.title }}]({{ post.url }}) - Written: {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
---

## 👤 contact me

You can reach me on [LinkedIn](https://www.linkedin.com/in/frostsec) or via [contact@frost.fyi](mailto:contact@frost.fyi)
Find me on Twitter/X [@FR05TBYTE_](https://x.com/FR05TBYTE_)

---
