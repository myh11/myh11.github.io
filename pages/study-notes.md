---
layout: page
title: 学习笔记
description: 大二上期末复习笔记整理，按计算机网络、概率论、数据结构、信息安全数学基础四个方向归档。
keywords: 学习笔记, 期末复习, 计算机网络, 概率论, 数据结构, 信息安全数学基础
comments: false
menu: 学习笔记
permalink: /study-notes/
---

<style>
.study-notes-index {
  line-height: 1.85;
}
.study-notes-hero {
  padding: 28px;
  border: 1px solid rgba(56, 189, 248, .22);
  border-radius: 24px;
  background: linear-gradient(135deg, rgba(15, 23, 42, .92), rgba(8, 47, 73, .62));
  color: #e0f2fe;
}
.study-notes-hero h1 {
  margin: 0 0 12px;
  color: #f8fafc;
}
.study-notes-hero p {
  margin: 0;
  color: #b6c7d6;
}
.study-notes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 14px;
  margin: 20px 0 30px;
}
.study-notes-branch {
  display: block;
  padding: 18px;
  border: 1px solid rgba(56, 189, 248, .18);
  border-radius: 18px;
  background: rgba(15, 23, 42, .05);
  text-decoration: none;
}
.study-notes-branch strong {
  display: block;
  color: #0369a1;
  font-size: 18px;
}
.study-notes-section {
  margin-top: 30px;
}
.study-notes-section h2 {
  padding-bottom: 8px;
  border-bottom: 1px solid #e5e7eb;
}
.study-notes-list {
  margin: 0;
  padding: 0;
  list-style: none;
}
.study-notes-list li {
  margin: 12px 0;
  padding: 16px;
  border: 1px solid #e5e7eb;
  border-radius: 16px;
  background: #fff;
}
.study-notes-list a {
  color: #0f172a;
  font-weight: 700;
}
.study-notes-list p {
  margin: 8px 0 0;
  color: #64748b;
}
.study-notes-tags {
  margin-top: 10px;
  color: #64748b;
  font-size: 13px;
}
</style>

<section class="study-notes-index">
  <div class="study-notes-hero">
    <h1>学习笔记</h1>
    <p>这里整理大二上期末复习阶段形成的笔记。四个分支分别对应计算机网络、概率论、数据结构、信息安全数学基础；每篇文章都保留原始复习内容，并在开头补充导读和学习总结。</p>
  </div>

  <div class="study-notes-grid">
    <a class="study-notes-branch" href="#计算机网络"><strong>分支一：计算机网络</strong><span>概念、考点、学习复盘</span></a>
    <a class="study-notes-branch" href="#概率论"><strong>分支二：概率论</strong><span>题型、公式、统计推断</span></a>
    <a class="study-notes-branch" href="#数据结构"><strong>分支三：数据结构</strong><span>概念、考点、代码题</span></a>
    <a class="study-notes-branch" href="#信息安全数学基础"><strong>分支四：信息安全数学基础</strong><span>数论、同余、平方剩余</span></a>
  </div>

  {% assign subjects = "计算机网络|概率论|数据结构|信息安全数学基础" | split: "|" %}
  {% for subject in subjects %}
  <section class="study-notes-section" id="{{ subject }}">
    <h2>{{ subject }}</h2>
    <ol class="study-notes-list">
      {% for post in site.posts reversed %}
        {% if post.subject == subject %}
        <li>
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          <p>{{ post.description }}</p>
          <div class="study-notes-tags">
            {% for tag in post.tags limit: 6 %}#{{ tag }} {% endfor %}
          </div>
        </li>
        {% endif %}
      {% endfor %}
    </ol>
  </section>
  {% endfor %}
</section>
