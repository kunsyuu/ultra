---
layout: page
title: Link
---
<style type="text/css">
.flink {
  margin-bottom: 20px;
}
.flink .flink-list {
  overflow: auto;
  padding: 10px 10px 0;
  text-align: center;
}
.flink .flink-list > .flink-list-item {
  position: relative;
  float: left;
  overflow: hidden;
  margin: 15px 7px;
  width: calc(100% / 3 - 15px);
  height: 90px;
  border-radius: 8px;
  line-height: 17px;
  -webkit-transform: translateZ(0);
}
@media screen and (max-width: 1024px) {
  .flink .flink-list > .flink-list-item {
    width: calc(50% - 15px) !important;
  }
}
@media screen and (max-width: 600px) {
  .flink .flink-list > .flink-list-item {
    width: calc(100% - 15px) !important;
  }
}
.flink .flink-list > .flink-list-item:hover .flink-item-icon {
  margin-left: -10px;
  width: 0;
}
.flink .flink-list > .flink-list-item:before {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  background: var(--theme-color);
  content: '';
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  -ms-transition: -ms-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
  -webkit-transform: scale(0);
  -moz-transform: scale(0);
  -o-transform: scale(0);
  -ms-transform: scale(0);
  transform: scale(0);
}
.flink .flink-list > .flink-list-item:hover:before,
.flink .flink-list > .flink-list-item:focus:before,
.flink .flink-list > .flink-list-item:active:before {
  -webkit-transform: scale(1);
  -moz-transform: scale(1);
  -o-transform: scale(1);
  -ms-transform: scale(1);
  transform: scale(1);
}
.flink .flink-list > .flink-list-item a {
  color: var(--text-color);
  text-decoration: none;
}
.flink .flink-list > .flink-list-item a .flink-item-icon {
  float: left;
  overflow: hidden;
  margin: 15px 10px;
  width: 60px;
  height: 60px;
  border-radius: 35px;
  -webkit-transition: width 0.3s ease-out;
  -moz-transition: width 0.3s ease-out;
  -o-transition: width 0.3s ease-out;
  -ms-transition: width 0.3s ease-out;
  transition: width 0.3s ease-out;
}
.flink .flink-list > .flink-list-item a .flink-item-icon img {
  width: 100%;
  height: 100%;
  -webkit-transition: filter 375ms ease-in 0.2s, -webkit-transform 0.3s;
  -moz-transition: filter 375ms ease-in 0.2s, -moz-transform 0.3s;
  -o-transition: filter 375ms ease-in 0.2s, -o-transform 0.3s;
  -ms-transition: filter 375ms ease-in 0.2s, -ms-transform 0.3s;
  transition: filter 375ms ease-in 0.2s, transform 0.3s;
  object-fit: cover;
}
.flink .flink-list > .flink-list-item a .img-alt {
  display: none;
}
.flink .flink-item-name {
  padding: 16px 10px 0 0;
  height: 40px;
  font-weight: bold;
  font-size: 1.43em;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.flink .flink-item-desc {
  padding: 16px 10px 16px 0;
  height: 50px;
  font-size: 0.93em;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.flink .flink-name {
  margin-bottom: 5px;
  font-weight: bold;
  font-size: 1.5em;
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
        <div class="flink-item-icon"><img class="no-lightbox entered loaded" src="{{ linkitem.avatar }}" data-lazy-src="{{ linkitem.avatar }}" onerror="this.onerror=null;this.src='https://ucarecdn.com/921541ad-1874-42cf-862d-effec4798464/404.webp'" alt="{{ linkitem.name }}" data-ll-status="loaded"></div>
        <div class="flink-item-name">{{ linkitem.name }}</div>
        <div class="flink-item-desc" title=" {{ linkitem.descr }} ">{{ linkitem.descr }}</div>
      </a>
    </div>
  {% endfor %}
  </div>

{% endfor %}
</div>

{% include twikoo.html %}