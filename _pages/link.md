---
layout: page
title: Link
---
<style type="text/css">
.flink-list-item {
  margin: 10px 0;
  padding: 5px 0;
  width: 100%;
  border-bottom: 1px dotted gray;
  min-height: 30px;
  line-height: 30px;
}
.flink-list-item:hover {
  background-color: lightgray;
  opacity: 0.6;
}
.flink-item-name {
  padding-left: 5px;
  float: left;
  width: 30%;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.flink-item-name .site-name {
  text-decoration: underline;
  text-underline-offset: 5px;
}
.flink-item-desc {
  color: gray;
  font-size: 12px;
  font-weight: normal;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>

<h1 class="post-title">链接</h1>
<div class="flink">
{% for class in site.data.link %}
  <h2>{{ class.class_name }}</h2>
  <div class="flink-desc">{{ class.class_desc}}</div>
  
  <div class="flink-list">
  {% for linkitem in class.link_list %}
    <div class="flink-list-item">
      <a href="{{ linkitem.link }}" title="{{ linkitem.name }}" target="_blank">
        <div class="flink-item-name"><span class="site-name">{{ linkitem.name }}</span></div>
        <div class="flink-item-desc" title=" {{ linkitem.descr }} ">{{ linkitem.descr }}</div>
      </a>
    </div>
  {% endfor %}
  </div>

{% endfor %}
</div>

<h2>我的博客</h2>
```
    - name: Daradara
      link: none
      avatar: https://ucarecdn.com/4fc24eeb-f5f8-4a38-ab5f-46dd92d4e2a0/avatar.jpg
      descr: 记录悠闲的日常
```

{% include twikoo.html %}