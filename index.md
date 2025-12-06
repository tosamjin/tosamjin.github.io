---
layout: home
title: "쉿! 비밀이예요"
permalink: /
classes: wide
---

최신 할인정보 및 특가 상품들을 정리한 페이지입니다 😊  
쉿! 이 가격은 당신만 알고 있으셔야 해요!

{%- assign groups = "가전/PC,패션,식품,가구,etc" | split: "," -%}

{%- for g in groups %}
### {{ g }}

<div class="category-list">
  {%- assign items = site.products 
       | where_exp: "p", "p.categories contains g" 
       | sort: "date" 
       | reverse 
       | slice: 0,3 -%}   {# ← 3개만, 5개로 늘리고 싶으면 0,5 로 바꿔 #}

  {%- if items.size == 0 %}
  <p class="no-items">아직 등록된 상품이 없습니다.</p>
  {%- else %}
    {%- for p in items %}
    <a class="product-row" href="{{ p.url | relative_url }}">
      {%- if p.thumbnail %}
      <span class="product-thumb">
        <img src="{{ p.thumbnail }}" alt="{{ p.title }}" loading="lazy">
      </span>
      {%- endif %}
      <span class="product-info">
        <span class="product-title">{{ p.title }}</span>
      </span>
    </a>
    {%- endfor %}
  {%- endif %}
</div>

---

{%- endfor %}

<style>
.category-list {
  margin-bottom: 2.5rem;
}

.product-row {
  display: grid;
  grid-template-columns: 110px 1fr; /* 1열: 이미지, 2열: 텍스트 */
  gap: 0.75rem;
  align-items: center;
  padding: 0.5rem 0;
  border-bottom: 1px solid rgba(255,255,255,0.12);
  text-decoration: none;
}

.product-row:last-child {
  border-bottom: none;
}

.product-thumb img {
  width: 100%;
  max-height: 80px;
  object-fit: cover;
  border-radius: 6px;
}

.product-title {
  font-size: 0.95rem;
  line-height: 1.3;
}

.no-items {
  font-size: 0.85rem;
  color: rgba(255,255,255,0.6);
}
</style>

