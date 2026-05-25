---
layout: post
title: "Smart File Manager：桌面端智能安全文件管理系统"
date: 2026-05-25 19:10:00 +0800
categories: 项目
tags: [课程项目, 文件管理, 信息安全, Tauri, Rust, Next.js, FastAPI, pgvector, Ollama, PostgreSQL]
author: myh
description: "一个把桌面文件管理、AI摘要、语义检索、隐写处理、风险审计和实时监控结合起来的智能安全文件管理系统。"
---

Smart File Manager 是一个偏桌面端的智能安全文件管理系统。它不只解决“文件在哪里”的问题，还进一步尝试回答“文件是什么、有没有风险、能不能按语义找到、是否存在隐写或伪装、操作过程能否被审计”。

<!--more-->

<style>
.sfm-post {
  --sfm-bg: #07111f;
  --sfm-panel: rgba(10, 20, 36, .82);
  --sfm-line: rgba(103, 232, 249, .22);
  --sfm-cyan: #67e8f9;
  --sfm-blue: #38bdf8;
  --sfm-green: #34d399;
  --sfm-pink: #f472b6;
  --sfm-purple: #a78bfa;
  --sfm-text: #e8f7ff;
  --sfm-muted: #9fb8ca;
  color: var(--sfm-text);
  line-height: 1.82;
}
.sfm-post * { box-sizing: border-box; }
.sfm-hero,
.sfm-section {
  border: 1px solid var(--sfm-line);
  border-radius: 24px;
  background:
    radial-gradient(circle at 12% 8%, rgba(103, 232, 249, .22), transparent 34%),
    radial-gradient(circle at 88% 0%, rgba(244, 114, 182, .14), transparent 28%),
    linear-gradient(135deg, rgba(6, 17, 32, .96), rgba(15, 23, 42, .84));
  box-shadow: 0 24px 64px rgba(2, 8, 23, .22);
}
.sfm-hero { padding: 34px; }
.sfm-kicker {
  display: inline-flex;
  padding: 6px 12px;
  border: 1px solid rgba(103, 232, 249, .35);
  border-radius: 999px;
  color: var(--sfm-cyan);
  background: rgba(103, 232, 249, .08);
  font-size: 13px;
  letter-spacing: .08em;
}
.sfm-hero h2 {
  margin: 18px 0 12px;
  color: #f8fdff;
  font-size: 32px;
  line-height: 1.22;
}
.sfm-hero p,
.sfm-section p {
  color: #c9ddeb;
}
.sfm-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 22px;
}
.sfm-button {
  display: inline-flex;
  padding: 10px 14px;
  border: 1px solid rgba(103, 232, 249, .32);
  border-radius: 13px;
  color: #eaffff;
  text-decoration: none;
  background: rgba(103, 232, 249, .1);
  font-weight: 700;
}
.sfm-button.primary {
  border-color: rgba(52, 211, 153, .42);
  background: linear-gradient(135deg, rgba(52, 211, 153, .22), rgba(56, 189, 248, .14));
}
.sfm-section {
  margin-top: 24px;
  padding: 26px;
}
.sfm-section h2 {
  margin: 0 0 12px;
  color: #f8fdff;
  font-size: 24px;
}
.sfm-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 14px;
}
.sfm-card {
  padding: 18px;
  border: 1px solid rgba(103, 232, 249, .16);
  border-radius: 18px;
  background: rgba(2, 8, 23, .35);
}
.sfm-card h3 {
  margin: 0 0 8px;
  color: var(--sfm-cyan);
  font-size: 17px;
}
.sfm-card p {
  margin: 0;
  color: var(--sfm-muted);
}
.sfm-flow {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 10px;
}
.sfm-flow span {
  min-height: 112px;
  padding: 13px;
  border: 1px solid rgba(103, 232, 249, .16);
  border-radius: 16px;
  color: #e8fbff;
  background: rgba(15, 23, 42, .62);
  font-weight: 700;
}
.sfm-flow small {
  display: block;
  margin-top: 8px;
  color: var(--sfm-muted);
  font-weight: 400;
}
.sfm-table {
  overflow-x: auto;
  border: 1px solid rgba(103, 232, 249, .16);
  border-radius: 18px;
}
.sfm-table table {
  width: 100%;
  margin: 0;
  border-collapse: collapse;
  background: rgba(2, 8, 23, .28);
}
.sfm-table th,
.sfm-table td {
  padding: 12px 14px;
  border-bottom: 1px solid rgba(103, 232, 249, .12);
  color: #cfe3ef;
}
.sfm-table th {
  color: #f8fdff;
  background: rgba(56, 189, 248, .12);
}
@media (max-width: 900px) {
  .sfm-grid,
  .sfm-flow {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
@media (max-width: 560px) {
  .sfm-hero,
  .sfm-section {
    padding: 20px;
  }
  .sfm-grid,
  .sfm-flow {
    grid-template-columns: 1fr;
  }
}
</style>

<div class="sfm-post">
  <section class="sfm-hero">
    <div class="sfm-kicker">AI + Desktop Security File Manager</div>
    <h2>把普通文件管理器升级成“文件理解 + 安全审计”工具</h2>
    <p>传统文件管理器通常只负责展示目录、移动文件和打开文件。这个项目在桌面端文件管理基础上加入 AI 摘要、向量检索、真实格式识别、隐写处理、风险审计、实时文件监控和性能遥测，让文件系统具备一定的理解能力与安全分析能力。</p>
    <div class="sfm-actions">
      <a class="sfm-button primary" href="https://github.com/myh11/Smart-File-Manager" target="_blank" rel="noopener">查看 GitHub 仓库</a>
      <a class="sfm-button" href="#sfm-architecture">系统架构</a>
      <a class="sfm-button" href="#sfm-security">安全能力</a>
    </div>
  </section>

  <section class="sfm-section">
    <h2>项目定位</h2>
    <p>这个项目的核心想法是：文件管理不应该只停留在路径和文件名层面。很多文件真正有价值的信息藏在内容里，很多风险也不会直接体现在扩展名上。因此系统通过 Rust + Tauri 接入本地文件能力，通过 Python AI 服务生成摘要和向量，通过 PostgreSQL + pgvector 存储语义向量，再通过 Next.js 前端展示分析结果。</p>
  </section>

  <section id="sfm-architecture" class="sfm-section">
    <h2>系统架构</h2>
    <div class="sfm-grid">
      <div class="sfm-card">
        <h3>桌面端后端</h3>
        <p>Tauri 2 + Rust 负责文件扫描、真实格式识别、加密解密、事件推送、数据库读写和命令桥接。</p>
      </div>
      <div class="sfm-card">
        <h3>前端界面</h3>
        <p>Next.js、React、Tailwind CSS、ECharts、Framer Motion 构建控制台、风险面板、搜索页和监控页。</p>
      </div>
      <div class="sfm-card">
        <h3>AI 与数据层</h3>
        <p>FastAPI + Ollama 提供摘要与 embedding，PostgreSQL + pgvector 存储文件向量并支持相似度检索。</p>
      </div>
    </div>
  </section>

  <section class="sfm-section">
    <h2>核心能力链路</h2>
    <div class="sfm-flow">
      <span>目录扫描<small>递归读取本地目录，收集文件路径、格式和基础元数据。</small></span>
      <span>AI 分析<small>提取可读内容，调用 AI 服务生成摘要与向量。</small></span>
      <span>语义检索<small>查询文本转向量，通过 pgvector 计算相似度。</small></span>
      <span>风险审计<small>识别扩展名伪装、隐写样本、可疑格式和操作风险。</small></span>
      <span>实时监控<small>监听文件变化，推送风险事件和系统运行指标。</small></span>
    </div>
  </section>

  <section id="sfm-security" class="sfm-section">
    <h2>安全相关设计</h2>
    <div class="sfm-table">
      <table>
        <thead>
          <tr>
            <th>能力</th>
            <th>实现思路</th>
            <th>价值</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>真实格式识别</td>
            <td>Rust 读取文件头，通过 Magic Number 判断真实 MIME 和扩展名</td>
            <td>发现扩展名伪装，避免只相信文件名</td>
          </tr>
          <tr>
            <td>LSB 隐写处理</td>
            <td>将文本按 bit 写入图片 RGB 通道最低有效位，并支持提取校验</td>
            <td>展示图像隐写的基本原理，并将隐写样本纳入风险审计</td>
          </tr>
          <tr>
            <td>文件加密与重锁定</td>
            <td>使用 Rust 后端完成加密、临时解密会话和重新锁定</td>
            <td>让敏感文件在桌面端也具备访问控制和操作留痕</td>
          </tr>
          <tr>
            <td>风险面板</td>
            <td>汇总风险等级、风险明细、隐写日志和文件定位动作</td>
            <td>形成“发现风险 -> 定位文件 -> 继续处理”的闭环</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

  <section class="sfm-section">
    <h2>语义检索为什么是亮点</h2>
    <p>普通文件搜索依赖文件名或关键词，但真实文件名经常并不规范，比如 `final-v2.txt`、`scan3.png`、`report-old.docx`。语义检索则先把文件内容和查询语句转换成向量，再比较向量距离。这样用户可以用“找和财务报告相关的文件”“找包含路线规划内容的资料”这种自然语言方式定位文件。</p>
    <p>项目中使用固定维度的 embedding，并在 PostgreSQL 中通过 `pgvector` 进行余弦距离检索。前端把相似度展示成百分比和距离条，让检索结果不仅能返回，还能解释“为什么它排在前面”。</p>
  </section>

  <section class="sfm-section">
    <h2>运行与演示重点</h2>
    <div class="sfm-grid">
      <div class="sfm-card">
        <h3>演示一：语义搜索</h3>
        <p>输入自然语言查询，返回语义上最接近的文件，并展示相似度百分比。</p>
      </div>
      <div class="sfm-card">
        <h3>演示二：隐写样本</h3>
        <p>展示图片隐写写入、提取校验和隐写风险标签，说明安全检测场景。</p>
      </div>
      <div class="sfm-card">
        <h3>演示三：实时监控</h3>
        <p>监听目录文件变化，前端通知中心实时接收风险事件和系统状态变化。</p>
      </div>
    </div>
  </section>

  <section class="sfm-section">
    <h2>项目总结</h2>
    <p>Smart File Manager 的有趣之处在于，它把文件管理、AI 理解和安全审计放在同一条链路里：文件被扫描后，不仅能被保存和展示，还能被摘要、向量化、检索、标记风险、监控变化，并留下可回溯的操作记录。</p>
    <p>如果用一句话概括：这是一个把“桌面文件管理器”向“智能安全分析工具”推进的课程项目。</p>
  </section>
</div>
