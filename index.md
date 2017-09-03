---
layout: default
---

{% assign fileToInclude = '_posts/' | append: site.posts.first.fileName %}

{% include_relative {{fileToInclude}} %}