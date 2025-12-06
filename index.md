---
layout: home
title: "쉿! 비밀이예요"
permalink: /
classes: wide
---

최신 할인정보 및 특가 상품들을 정리한 페이지입니다 😊  
쉿! 이 가격은 당신만 알고 있으셔야 해요!

{% assign groups = "가전/PC,패션,식품,생활용품,etc" | split: "," %}

{% for g in groups %}
## {{ g }}

<div class="cards">
  {% assign items = site.products | where_exp: "p", "p.categories contains g" | sort: "date" | reverse | slice: 0,3 %}
  {% if items.size == 0 %}
  아직 등록된 상품이 없습니다.
  {% else %}
    {% for p in items %}
    <article class="card">
      <a href="{{ p.url | relative_url }}">
        {% if p.thumbnail %}
          <img src="{{ p.thumbnail }}" alt="{{ p.title }}" loading="lazy">
        {% endif %}
        <h3>{{ p.title }}</h3>
      </a>
    </article>
    {% endfor %}
  {% endif %}
</div>

---

{% endfor %}


