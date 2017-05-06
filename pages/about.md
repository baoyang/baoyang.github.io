---
layout: page
title: About
description: 简单即自由
keywords: 远方, baoyang
comments: true
menu: 关于
permalink: /about/
---

我是鲍阳，像一条臭水沟中沟爬行的狗。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
