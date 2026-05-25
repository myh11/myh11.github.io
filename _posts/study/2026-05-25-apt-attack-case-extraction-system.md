---
layout: post
title: "APT攻击案例信息抽取系统"
date: 2026-05-25 08:00:00 +0800
categories: 学习
tags: [APT, 知识图谱, 信息抽取, Neo4j, React]
author: myh
---

<!--more-->

<style>
.apt-showcase {
  --apt-bg: #07111f;
  --apt-panel: rgba(10, 25, 43, .86);
  --apt-panel-2: rgba(16, 38, 63, .78);
  --apt-line: rgba(103, 232, 249, .28);
  --apt-cyan: #67e8f9;
  --apt-blue: #38bdf8;
  --apt-lime: #a3e635;
  --apt-amber: #fbbf24;
  --apt-orange: #fb923c;
  --apt-text: #e8f7ff;
  --apt-muted: #9fb8ca;
  color: var(--apt-text);
  font-family: "Microsoft YaHei", "PingFang SC", "Noto Sans CJK SC", sans-serif;
  line-height: 1.75;
}
.markdown-body .apt-showcase * {
  box-sizing: border-box;
}
.apt-showcase a {
  color: inherit;
  text-decoration: none;
}
.apt-hero {
  position: relative;
  overflow: hidden;
  padding: 44px;
  border: 1px solid rgba(103, 232, 249, .28);
  border-radius: 30px;
  background:
    radial-gradient(circle at 18% 18%, rgba(103, 232, 249, .28), transparent 32%),
    radial-gradient(circle at 86% 10%, rgba(163, 230, 53, .18), transparent 28%),
    linear-gradient(135deg, #08111f 0%, #0d2638 48%, #07111f 100%);
  box-shadow: 0 28px 80px rgba(2, 8, 23, .35), inset 0 0 80px rgba(56, 189, 248, .08);
}
.apt-hero::before {
  content: "";
  position: absolute;
  inset: -120px;
  background-image:
    linear-gradient(rgba(103, 232, 249, .1) 1px, transparent 1px),
    linear-gradient(90deg, rgba(103, 232, 249, .1) 1px, transparent 1px);
  background-size: 34px 34px;
  transform: rotate(-8deg);
  opacity: .45;
}
.apt-hero::after {
  content: "";
  position: absolute;
  width: 280px;
  height: 280px;
  right: -70px;
  top: -70px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(103, 232, 249, .35), rgba(103, 232, 249, 0) 65%);
  animation: apt-breathe 4.8s ease-in-out infinite;
}
.apt-hero-inner {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1.1fr .9fr;
  gap: 34px;
  align-items: center;
}
.apt-kicker {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 7px 13px;
  border: 1px solid rgba(163, 230, 53, .32);
  border-radius: 999px;
  color: var(--apt-lime);
  background: rgba(163, 230, 53, .08);
  font-size: 13px;
  letter-spacing: .08em;
}
.apt-kicker::before {
  content: "";
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--apt-lime);
  box-shadow: 0 0 18px var(--apt-lime);
}
.apt-hero h2 {
  margin: 22px 0 16px;
  color: #f8fdff;
  font-size: 40px;
  line-height: 1.18;
  letter-spacing: -.04em;
}
.apt-hero p {
  margin: 0;
  color: #cbe3f1;
  font-size: 16px;
}
.apt-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 26px;
}
.apt-button {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 11px 16px;
  border-radius: 14px;
  font-weight: 700;
  border: 1px solid rgba(103, 232, 249, .34);
  background: rgba(103, 232, 249, .1);
  color: #eaffff;
  transition: transform .2s ease, box-shadow .2s ease, background .2s ease;
}
.apt-button.primary {
  border-color: rgba(163, 230, 53, .48);
  background: linear-gradient(135deg, rgba(163, 230, 53, .32), rgba(56, 189, 248, .2));
  box-shadow: 0 10px 30px rgba(56, 189, 248, .2);
}
.apt-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 16px 34px rgba(56, 189, 248, .25);
}
.apt-terminal {
  position: relative;
  overflow: hidden;
  border: 1px solid rgba(103, 232, 249, .25);
  border-radius: 22px;
  background: rgba(2, 8, 23, .62);
  box-shadow: inset 0 0 40px rgba(103, 232, 249, .06);
}
.apt-terminal-bar {
  display: flex;
  gap: 7px;
  padding: 14px 16px;
  border-bottom: 1px solid rgba(103, 232, 249, .14);
  background: rgba(148, 163, 184, .08);
}
.apt-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
.apt-dot:nth-child(1) { background: #fb7185; }
.apt-dot:nth-child(2) { background: #fbbf24; }
.apt-dot:nth-child(3) { background: #34d399; }
.apt-terminal pre {
  margin: 0;
  padding: 20px;
  color: #d9fbff;
  background: transparent;
  font-size: 13px;
  white-space: pre-wrap;
}
.apt-terminal code {
  color: inherit;
  background: transparent;
}
.apt-metrics {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 14px;
  margin: 22px 0;
}
.apt-metric {
  padding: 20px;
  border: 1px solid rgba(103, 232, 249, .18);
  border-radius: 20px;
  background: linear-gradient(180deg, rgba(12, 30, 51, .88), rgba(6, 17, 32, .9));
  box-shadow: 0 18px 46px rgba(2, 8, 23, .18);
}
.apt-metric strong {
  display: block;
  color: var(--apt-cyan);
  font-size: 30px;
  line-height: 1.1;
}
.apt-metric span {
  display: block;
  margin-top: 8px;
  color: var(--apt-muted);
  font-size: 13px;
}
.apt-section {
  margin-top: 30px;
  padding: 28px;
  border: 1px solid rgba(103, 232, 249, .18);
  border-radius: 26px;
  background:
    linear-gradient(180deg, rgba(8, 20, 36, .94), rgba(4, 12, 24, .92)),
    radial-gradient(circle at 0 0, rgba(56, 189, 248, .16), transparent 34%);
}
.apt-section h2 {
  margin: 0 0 12px;
  color: #f8fdff;
  font-size: 26px;
  letter-spacing: -.03em;
}
.apt-section h3 {
  margin: 0 0 8px;
  color: #eaffff;
  font-size: 17px;
}
.apt-section p {
  color: #c9ddea;
}
.apt-section-intro {
  margin: 0 0 22px;
  color: var(--apt-muted);
}
.apt-grid-2 {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 18px;
}
.apt-grid-3 {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
}
.apt-card {
  position: relative;
  overflow: hidden;
  padding: 20px;
  border: 1px solid rgba(103, 232, 249, .16);
  border-radius: 20px;
  background: rgba(15, 35, 57, .7);
}
.apt-card::before {
  content: "";
  position: absolute;
  width: 120px;
  height: 120px;
  right: -54px;
  top: -60px;
  border-radius: 50%;
  background: rgba(103, 232, 249, .12);
}
.apt-card p {
  margin: 0;
  color: #b9cedd;
}
.apt-tag-row {
  display: flex;
  flex-wrap: wrap;
  gap: 9px;
  margin-top: 16px;
}
.apt-tag {
  padding: 6px 10px;
  border: 1px solid rgba(103, 232, 249, .22);
  border-radius: 999px;
  color: #cffafe;
  background: rgba(103, 232, 249, .08);
  font-size: 12px;
}
.apt-flow {
  display: grid;
  grid-template-columns: repeat(6, minmax(0, 1fr));
  gap: 12px;
}
.apt-flow-step {
  min-height: 178px;
  padding: 16px;
  border: 1px solid rgba(103, 232, 249, .18);
  border-radius: 18px;
  background: linear-gradient(180deg, rgba(13, 32, 52, .92), rgba(5, 15, 28, .94));
}
.apt-flow-step b {
  display: inline-flex;
  width: 32px;
  height: 32px;
  align-items: center;
  justify-content: center;
  margin-bottom: 14px;
  border-radius: 11px;
  color: #07111f;
  background: linear-gradient(135deg, var(--apt-cyan), var(--apt-lime));
}
.apt-flow-step p {
  margin: 0;
  color: #a9bfce;
  font-size: 13px;
}
.apt-graph-wrap {
  position: relative;
  overflow: hidden;
  border: 1px solid rgba(103, 232, 249, .18);
  border-radius: 24px;
  background:
    radial-gradient(circle at 50% 50%, rgba(56, 189, 248, .18), transparent 44%),
    linear-gradient(180deg, rgba(2, 8, 23, .88), rgba(8, 20, 36, .96));
}
.apt-graph {
  width: 100%;
  display: block;
}
.apt-graph .link {
  stroke: rgba(103, 232, 249, .38);
  stroke-width: 2;
  stroke-dasharray: 8 10;
  animation: apt-flow-line 6s linear infinite;
}
.apt-graph .link-hot {
  stroke: rgba(163, 230, 53, .65);
}
.apt-graph text {
  fill: #e8f7ff;
  font-size: 13px;
  font-family: "Microsoft YaHei", sans-serif;
}
.apt-graph .node circle {
  stroke: rgba(255, 255, 255, .35);
  stroke-width: 2;
  filter: drop-shadow(0 0 10px rgba(103, 232, 249, .35));
}
.apt-graph .case circle { fill: #38bdf8; }
.apt-graph .org circle { fill: #f97316; }
.apt-graph .tech circle { fill: #a3e635; }
.apt-graph .ioc circle { fill: #fbbf24; }
.apt-graph .tool circle { fill: #22c55e; }
.apt-matrix {
  overflow-x: auto;
  border: 1px solid rgba(103, 232, 249, .16);
  border-radius: 20px;
}
.apt-matrix table {
  width: 100%;
  border-collapse: collapse;
  margin: 0;
  background: rgba(4, 12, 24, .55);
}
.apt-matrix th,
.apt-matrix td {
  padding: 13px 14px;
  border-bottom: 1px solid rgba(103, 232, 249, .12);
  color: #cde4ef;
  font-size: 14px;
}
.apt-matrix th {
  color: #f8fdff;
  background: rgba(103, 232, 249, .1);
}
.apt-chip {
  display: inline-flex;
  padding: 4px 8px;
  border-radius: 999px;
  color: #07111f;
  background: var(--apt-lime);
  font-size: 12px;
  font-weight: 700;
}
.apt-chip.blue {
  background: var(--apt-cyan);
}
.apt-chip.orange {
  background: var(--apt-orange);
}
.apt-stack {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 12px;
}
.apt-stack-item {
  padding: 16px;
  border-radius: 18px;
  border: 1px solid rgba(103, 232, 249, .16);
  background: rgba(2, 8, 23, .45);
}
.apt-stack-item strong {
  display: block;
  color: var(--apt-cyan);
  margin-bottom: 6px;
}
.apt-stack-item span {
  color: #abc1d0;
  font-size: 13px;
}
.apt-callout {
  margin-top: 22px;
  padding: 20px;
  border-left: 4px solid var(--apt-lime);
  border-radius: 18px;
  background: rgba(163, 230, 53, .08);
  color: #dcfce7;
}
@keyframes apt-breathe {
  0%, 100% { transform: scale(.96); opacity: .7; }
  50% { transform: scale(1.08); opacity: 1; }
}
@keyframes apt-flow-line {
  to { stroke-dashoffset: -120; }
}
@media (max-width: 980px) {
  .apt-hero-inner,
  .apt-grid-2,
  .apt-grid-3 {
    grid-template-columns: 1fr;
  }
  .apt-metrics,
  .apt-stack {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
  .apt-flow {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
@media (max-width: 640px) {
  .apt-hero,
  .apt-section {
    padding: 22px;
    border-radius: 22px;
  }
  .apt-hero h2 {
    font-size: 28px;
  }
  .apt-metrics,
  .apt-stack,
  .apt-flow {
    grid-template-columns: 1fr;
  }
}
</style>

<div class="apt-showcase">
  <section class="apt-hero">
    <div class="apt-hero-inner">
      <div>
        <div class="apt-kicker">Threat Intelligence Graph System</div>
        <h2>把APT报告变成可查询、可对比、可解释的攻击知识图谱</h2>
        <p>这个项目不是简单做一个案例列表，而是围绕“报告输入、信息抽取、实体归一、攻击链构建、Neo4j入库、前端分析”形成一条完整链路。系统最终能把分散在威胁情报报告里的组织、技术、IOC、漏洞、工具和攻击步骤组织成图谱，并进一步做质量诊断、攻击链完整度分析和相似案例推荐。</p>
        <div class="apt-actions">
          <a class="apt-button primary" href="https://github.com/myh11/apt-attack-case-extraction-system">查看GitHub仓库</a>
          <a class="apt-button" href="#apt-extraction">看信息抽取实现</a>
          <a class="apt-button" href="#apt-analysis">看分析亮点</a>
        </div>
      </div>
      <div class="apt-terminal">
        <div class="apt-terminal-bar">
          <span class="apt-dot"></span>
          <span class="apt-dot"></span>
          <span class="apt-dot"></span>
        </div>
        <pre><code>$ start-system.bat
[1] Neo4j container ready
[2] Python API server ready
[3] Vite frontend ready
[4] seed demo cases into graph

frontend  http://localhost:18080
api       http://localhost:8765/api
neo4j     http://localhost:7474</code></pre>
      </div>
    </div>
  </section>

  <section class="apt-metrics">
    <div class="apt-metric">
      <strong>59</strong>
      <span>已整理APT案例</span>
    </div>
    <div class="apt-metric">
      <strong>1173</strong>
      <span>图谱节点</span>
    </div>
    <div class="apt-metric">
      <strong>5821</strong>
      <span>图谱关系</span>
    </div>
    <div class="apt-metric">
      <strong>3</strong>
      <span>分析增强能力</span>
    </div>
  </section>

  <section class="apt-section">
    <h2>为什么这个项目不只是“把页面做出来”</h2>
    <p class="apt-section-intro">APT报告的难点在于内容不是结构化数据：同一个组织可能有多个别名，攻击技术可能散落在长段落里，IOC、恶意软件、工具和漏洞之间又存在跨案例关联。如果只是把报告标题列出来，系统价值很有限；真正有价值的是把这些非结构化文本转成可分析的数据资产。</p>
    <div class="apt-grid-3">
      <div class="apt-card">
        <h3>从文本到实体</h3>
        <p>抽取APT组织、攻击技术、IOC、恶意软件、工具、漏洞和攻击步骤，让报告里的关键信息从自然语言中“浮出来”。</p>
      </div>
      <div class="apt-card">
        <h3>从实体到关系</h3>
        <p>把“案例使用技术”“组织关联案例”“案例包含IOC”“技术属于阶段”等关系写入Neo4j，形成可查询的知识图谱。</p>
      </div>
      <div class="apt-card">
        <h3>从展示到分析</h3>
        <p>在案例库、全局图谱、攻击链对比和问题分布分析之外，进一步做弱案例原因、链路完整度和相似案例推荐。</p>
      </div>
    </div>
  </section>

  <section id="apt-extraction" class="apt-section">
    <h2>信息抽取是怎么实现的</h2>
    <p class="apt-section-intro">系统采用“解析、抽取、归一、建链、入库、分析”的流水线。每一步都不是孤立处理，而是服务于后续的可视化和研判：抽取结果要能进入图谱，图谱关系要能支撑页面查询，分析指标要能解释案例为什么强或弱。</p>
    <div class="apt-flow">
      <div class="apt-flow-step">
        <b>01</b>
        <h3>报告输入</h3>
        <p>支持txt、md、html和文本型pdf，统一转换为可处理文本，保留案例名称和来源信息。</p>
      </div>
      <div class="apt-flow-step">
        <b>02</b>
        <h3>文本清洗</h3>
        <p>去除噪声、切分段落、合并上下文，降低报告格式差异对抽取结果的影响。</p>
      </div>
      <div class="apt-flow-step">
        <b>03</b>
        <h3>实体抽取</h3>
        <p>识别组织、IOC、恶意软件、漏洞、工具、攻击阶段和攻击技术等核心对象。</p>
      </div>
      <div class="apt-flow-step">
        <b>04</b>
        <h3>技术映射</h3>
        <p>结合AttacKG、关键词映射和补偿规则，将报告描述映射到ATT&CK技术与阶段。</p>
      </div>
      <div class="apt-flow-step">
        <b>05</b>
        <h3>实体归一</h3>
        <p>处理组织别名、技术编号、IOC格式和重复实体，避免图谱里出现大量孤岛节点。</p>
      </div>
      <div class="apt-flow-step">
        <b>06</b>
        <h3>图谱入库</h3>
        <p>将案例、组织、技术、IOC、工具和攻击步骤写入Neo4j，供前端查询和联动展示。</p>
      </div>
    </div>
  </section>

  <section class="apt-section">
    <h2>核心数据图谱</h2>
    <p class="apt-section-intro">知识图谱的意义不是“画很多点”，而是让不同案例之间的共性能够被看见：多个案例共享同一技术、同一组织使用不同工具、同一类IOC指向相似基础设施，这些关系都能支撑后续的横向分析。</p>
    <div class="apt-graph-wrap">
      <svg class="apt-graph" viewBox="0 0 820 420" role="img" aria-label="APT攻击案例知识图谱示意图">
        <defs>
          <radialGradient id="aptNodeGlow" cx="50%" cy="50%" r="50%">
            <stop offset="0%" stop-color="#ffffff" stop-opacity=".55"></stop>
            <stop offset="100%" stop-color="#ffffff" stop-opacity="0"></stop>
          </radialGradient>
        </defs>
        <path class="link link-hot" d="M410 210 C330 120 245 94 160 92"></path>
        <path class="link" d="M410 210 C522 92 610 76 710 96"></path>
        <path class="link" d="M410 210 C322 254 250 306 152 330"></path>
        <path class="link link-hot" d="M410 210 C510 274 604 308 706 328"></path>
        <path class="link" d="M410 210 C412 120 420 78 422 42"></path>
        <path class="link" d="M410 210 C398 308 396 352 390 382"></path>
        <path class="link" d="M160 92 C280 70 470 64 710 96"></path>
        <path class="link" d="M152 330 C308 356 516 352 706 328"></path>
        <g class="node case">
          <circle cx="410" cy="210" r="42"></circle>
          <circle cx="410" cy="210" r="70" fill="url(#aptNodeGlow)"></circle>
          <text x="410" y="207" text-anchor="middle">APT Case</text>
          <text x="410" y="226" text-anchor="middle">攻击案例</text>
        </g>
        <g class="node org">
          <circle cx="160" cy="92" r="32"></circle>
          <text x="160" y="97" text-anchor="middle">组织</text>
        </g>
        <g class="node tech">
          <circle cx="710" cy="96" r="34"></circle>
          <text x="710" y="101" text-anchor="middle">技术</text>
        </g>
        <g class="node ioc">
          <circle cx="152" cy="330" r="31"></circle>
          <text x="152" y="335" text-anchor="middle">IOC</text>
        </g>
        <g class="node tool">
          <circle cx="706" cy="328" r="32"></circle>
          <text x="706" y="333" text-anchor="middle">工具</text>
        </g>
        <g class="node tech">
          <circle cx="422" cy="42" r="27"></circle>
          <text x="422" y="47" text-anchor="middle">阶段</text>
        </g>
        <g class="node org">
          <circle cx="390" cy="382" r="28"></circle>
          <text x="390" y="387" text-anchor="middle">漏洞</text>
        </g>
        <text x="278" y="115">attributed_to</text>
        <text x="536" y="137">uses_technique</text>
        <text x="244" y="296">contains_ioc</text>
        <text x="540" y="288">uses_tool</text>
        <text x="438" y="112">belongs_to_phase</text>
      </svg>
    </div>
  </section>

  <section id="apt-analysis" class="apt-section">
    <h2>与众不同的分析增强</h2>
    <p class="apt-section-intro">普通项目容易停在“能上传、能列表、能详情”。这个系统进一步把抽取结果转成分析指标，回答三个更像安全分析的问题：这份案例质量够不够、攻击链完整不完整、它和哪些案例相似。</p>
    <div class="apt-grid-3">
      <div class="apt-card">
        <h3>数据质量诊断</h3>
        <p>从组织识别、IOC丰富度、技术命中、阶段覆盖和关系密度等维度评分，能解释为什么某个案例看起来“空”或“不完整”。</p>
        <div class="apt-tag-row">
          <span class="apt-tag">弱案例原因</span>
          <span class="apt-tag">缺失项定位</span>
          <span class="apt-tag">质量评分</span>
        </div>
      </div>
      <div class="apt-card">
        <h3>攻击链完整度分析</h3>
        <p>将抽取到的技术和步骤映射到ATT&CK阶段，判断一个案例是否覆盖初始访问、执行、持久化、横向移动、命令控制等关键过程。</p>
        <div class="apt-tag-row">
          <span class="apt-tag">ATT&CK阶段</span>
          <span class="apt-tag">链路缺口</span>
          <span class="apt-tag">步骤覆盖</span>
        </div>
      </div>
      <div class="apt-card">
        <h3>相似案例推荐</h3>
        <p>根据共享技术、共享IOC、共享工具、共同组织和图谱邻居关系进行推荐，帮助从单个案例扩展到一组可比较的攻击活动。</p>
        <div class="apt-tag-row">
          <span class="apt-tag">共享技术</span>
          <span class="apt-tag">横向对比</span>
          <span class="apt-tag">相似度解释</span>
        </div>
      </div>
    </div>
  </section>

  <section class="apt-section">
    <h2>页面功能不是堆菜单，而是围绕分析闭环组织</h2>
    <div class="apt-matrix">
      <table>
        <thead>
          <tr>
            <th>页面</th>
            <th>解决的问题</th>
            <th>展示重点</th>
            <th>价值</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>案例导入</td>
            <td>新报告如何进入系统</td>
            <td><span class="apt-chip blue">上传与抽取</span></td>
            <td>把非结构化报告变成结构化案例结果</td>
          </tr>
          <tr>
            <td>案例库</td>
            <td>已有案例如何检索和复盘</td>
            <td><span class="apt-chip">攻击链详情</span></td>
            <td>快速进入单案例研判视角</td>
          </tr>
          <tr>
            <td>图谱态势</td>
            <td>案例之间有什么关系</td>
            <td><span class="apt-chip blue">节点与关系</span></td>
            <td>从全局上观察组织、技术和IOC连接</td>
          </tr>
          <tr>
            <td>攻击链对比</td>
            <td>多个案例哪里相同、哪里不同</td>
            <td><span class="apt-chip orange">共性技术</span></td>
            <td>支撑同源性分析和战术差异分析</td>
          </tr>
          <tr>
            <td>APT组织画像</td>
            <td>一个组织的行为特征是什么</td>
            <td><span class="apt-chip">技术画像</span></td>
            <td>按组织聚合案例、技术、步骤和实体</td>
          </tr>
          <tr>
            <td>问题分布分析</td>
            <td>哪些数据质量不够好</td>
            <td><span class="apt-chip orange">诊断与解释</span></td>
            <td>定位弱案例和抽取薄弱环节</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

  <section class="apt-section">
    <h2>技术架构</h2>
    <p class="apt-section-intro">系统采用前后端分离加图数据库的方式组织。前端负责交互和可视化，后端负责报告处理、抽取流水线、图谱写入和分析接口，Neo4j负责保存节点关系并支撑图谱查询。</p>
    <div class="apt-stack">
      <div class="apt-stack-item">
        <strong>Frontend</strong>
        <span>React、TypeScript、Vite、Tailwind CSS、Recharts、React Flow</span>
      </div>
      <div class="apt-stack-item">
        <strong>Backend</strong>
        <span>Python API、报告解析、实体抽取、攻击链构建、批量处理</span>
      </div>
      <div class="apt-stack-item">
        <strong>Graph DB</strong>
        <span>Neo4j存储案例、组织、技术、IOC、工具和关系</span>
      </div>
      <div class="apt-stack-item">
        <strong>Runtime</strong>
        <span>Docker Compose启动数据库，脚本启动后端和前端</span>
      </div>
    </div>
    <div class="apt-callout">
      项目公开仓库只保留运行和展示必需内容：前端源码、后端抽取与分析服务、Neo4j启动配置、演示用结构化案例数据和一键启动脚本；没有提交本机环境变量、虚拟环境、node_modules、构建产物、运行日志、课程文档和原始大体积报告。
    </div>
  </section>

  <section class="apt-section">
    <h2>本地运行方式</h2>
    <p class="apt-section-intro">项目已经整理成可本地联调的公开版本。准备好Docker Desktop、Python 3、Node.js 18+和npm后，在仓库根目录运行启动脚本即可。</p>
    <div class="apt-grid-2">
      <div class="apt-terminal">
        <div class="apt-terminal-bar">
          <span class="apt-dot"></span>
          <span class="apt-dot"></span>
          <span class="apt-dot"></span>
        </div>
        <pre><code>git clone https://github.com/myh11/apt-attack-case-extraction-system.git
cd apt-attack-case-extraction-system
start-system.bat</code></pre>
      </div>
      <div class="apt-card">
        <h3>默认访问地址</h3>
        <p>前端：http://localhost:18080</p>
        <p>后端API：http://localhost:8765/api</p>
        <p>Neo4j Browser：http://localhost:7474</p>
        <div class="apt-tag-row">
          <span class="apt-tag">一键启动</span>
          <span class="apt-tag">自动灌入演示数据</span>
          <span class="apt-tag">本地可复现</span>
        </div>
      </div>
    </div>
  </section>

  <section class="apt-section">
    <h2>项目总结</h2>
    <p>这个系统的核心价值，是把APT威胁报告从“只能阅读的文本”变成“可以计算、可以查询、可以对比的图谱数据”。它的亮点不在于页面数量，而在于抽取链路和分析闭环：报告进入系统后，先被解析成结构化实体，再被组织成Neo4j知识图谱，最后通过前端形成案例复盘、攻击链对比、组织画像和数据质量诊断。</p>
    <p>如果用一句话概括：它不是一个静态展示系统，而是一个把威胁情报报告加工成可视化安全分析资产的原型平台。</p>
  </section>
</div>
