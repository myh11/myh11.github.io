---
layout: post
title: "基于元学习的加密流量分析系统"
date: 2026-05-25 18:20:00 +0800
categories: 项目
tags: [信息安全, 加密流量分析, 元学习, 入侵检测, Vue, ECharts, Node.js, MySQL, Docker]
author: myh
description: "一个把 pcap 检测、元学习模型推理、告警处置、MITRE 归类、溯源任务和态势大屏串起来的加密流量分析系统。"
---

<!--more-->

<style>
.meta-ids-post {
  --mi-bg: #07111f;
  --mi-panel: rgba(12, 24, 42, .86);
  --mi-line: rgba(56, 189, 248, .24);
  --mi-cyan: #67e8f9;
  --mi-blue: #38bdf8;
  --mi-green: #34d399;
  --mi-purple: #a78bfa;
  --mi-text: #e8f7ff;
  --mi-muted: #a9bed0;
  color: var(--mi-text);
  line-height: 1.78;
}
.meta-ids-post * { box-sizing: border-box; }
.mi-hero {
  position: relative;
  overflow: hidden;
  padding: 38px;
  border: 1px solid var(--mi-line);
  border-radius: 28px;
  background:
    radial-gradient(circle at 12% 18%, rgba(103, 232, 249, .26), transparent 30%),
    radial-gradient(circle at 88% 8%, rgba(167, 139, 250, .2), transparent 28%),
    linear-gradient(135deg, #08111f 0%, #10243b 52%, #07111f 100%);
  box-shadow: 0 24px 70px rgba(2, 8, 23, .34), inset 0 0 80px rgba(56, 189, 248, .08);
}
.mi-hero::before {
  content: "";
  position: absolute;
  inset: -120px;
  background-image:
    linear-gradient(rgba(103, 232, 249, .08) 1px, transparent 1px),
    linear-gradient(90deg, rgba(103, 232, 249, .08) 1px, transparent 1px);
  background-size: 32px 32px;
  transform: rotate(-7deg);
  opacity: .5;
}
.mi-hero-inner {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1.1fr .9fr;
  gap: 24px;
  align-items: center;
}
.mi-kicker {
  display: inline-flex;
  padding: 7px 12px;
  border: 1px solid rgba(52, 211, 153, .32);
  border-radius: 999px;
  color: var(--mi-green);
  background: rgba(52, 211, 153, .08);
  font-size: 13px;
  letter-spacing: .08em;
}
.mi-hero h2 {
  margin: 18px 0 12px;
  color: #f8fdff;
  font-size: 34px;
  line-height: 1.18;
}
.mi-hero p { margin: 0; color: #c9ddeb; }
.mi-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 22px;
}
.mi-button {
  display: inline-flex;
  align-items: center;
  padding: 10px 14px;
  border: 1px solid rgba(103, 232, 249, .34);
  border-radius: 14px;
  color: #effcff;
  background: rgba(56, 189, 248, .1);
  font-weight: 700;
  text-decoration: none;
}
.mi-terminal {
  border: 1px solid rgba(103, 232, 249, .26);
  border-radius: 20px;
  background: rgba(2, 8, 23, .62);
  overflow: hidden;
}
.mi-terminal-bar {
  display: flex;
  gap: 7px;
  padding: 13px 15px;
  border-bottom: 1px solid rgba(103, 232, 249, .14);
}
.mi-dot {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  background: var(--mi-cyan);
}
.mi-terminal pre {
  margin: 0;
  padding: 18px;
  color: #dffbff;
  background: transparent;
  white-space: pre-wrap;
  font-size: 13px;
}
.mi-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 14px;
  margin: 22px 0;
}
.mi-card {
  padding: 18px;
  border: 1px solid rgba(56, 189, 248, .18);
  border-radius: 18px;
  background: rgba(15, 23, 42, .06);
}
.mi-card strong {
  display: block;
  color: #075985;
  font-size: 17px;
  margin-bottom: 8px;
}
.mi-flow {
  display: grid;
  grid-template-columns: repeat(6, minmax(0, 1fr));
  gap: 10px;
  margin: 18px 0 26px;
}
.mi-step {
  min-height: 92px;
  padding: 14px;
  border: 1px solid rgba(14, 165, 233, .22);
  border-radius: 16px;
  background: linear-gradient(180deg, rgba(14, 165, 233, .08), rgba(15, 23, 42, .02));
}
.mi-step b {
  display: block;
  color: #0369a1;
  margin-bottom: 6px;
}
.mi-shot {
  margin: 24px 0;
  border: 1px solid #e5e7eb;
  border-radius: 22px;
  overflow: hidden;
  background: #fff;
  box-shadow: 0 16px 40px rgba(15, 23, 42, .08);
}
.mi-shot img {
  display: block;
  width: 100%;
  height: auto;
}
.mi-shot figcaption {
  padding: 12px 16px;
  color: #64748b;
  font-size: 14px;
}
@media (max-width: 900px) {
  .mi-hero-inner,
  .mi-grid,
  .mi-flow {
    grid-template-columns: 1fr;
  }
  .mi-hero { padding: 26px; }
}
</style>

<div class="meta-ids-post">
  <section class="mi-hero">
    <div class="mi-hero-inner">
      <div>
        <span class="mi-kicker">SECURITY PROJECT · META IDS</span>
        <h2>把“模型检测”做成一套可演示、可处置、可追踪的安全系统</h2>
        <p>这个项目的核心不是只跑一个分类模型，而是把 pcap 流量导入、DPLS 特征提取、元学习模型推理、MySQL 落库、告警处置、MITRE 归类、黑名单、溯源任务和态势大屏串成完整闭环。</p>
        <div class="mi-actions">
          <a class="mi-button" href="https://github.com/myh11/A-meta-learning-based-encrypted-traffic-analysis-system" target="_blank" rel="noopener">GitHub 仓库</a>
          <a class="mi-button" href="#flow">查看检测流程</a>
        </div>
      </div>
      <div class="mi-terminal">
        <div class="mi-terminal-bar"><span class="mi-dot"></span><span class="mi-dot"></span><span class="mi-dot"></span></div>
<pre><code>system: meta-learning encrypted traffic analysis
input : pcap / pcapng
model : PyTorch + DPLS sequence features
store : MySQL meta_ids
ui    : Vue main console + ECharts big screen
loop  : detect -> alert -> classify -> trace -> audit</code></pre>
      </div>
    </div>
  </section>

  <h2>项目定位</h2>
  <p>它面向的是“未知网络流量检测”这个场景：当传统规则或已知签名不够用时，系统通过模型对流量序列进行异常判断，再把检测结果转化为安全人员能继续处理的事件。相比只展示一个准确率指标，这个项目更强调工程闭环，也就是检测结果如何进入系统、如何被专家研判、如何形成审计记录。</p>

  <div class="mi-grid">
    <div class="mi-card"><strong>模型侧</strong>从 pcap 中提取双向包长序列 DPLS，使用 PyTorch 模型完成异常检测与攻击类型判断。</div>
    <div class="mi-card"><strong>业务侧</strong>提供告警列表、详情、状态流转、处置备注、专家领取、MITRE 归类、黑名单和溯源任务。</div>
    <div class="mi-card"><strong>展示侧</strong>主页面负责日常操作，大屏负责态势展示，两端共用同一套后端接口与数据库。</div>
  </div>

  <h2 id="flow">信息抽取与检测流程</h2>
  <p>系统最重要的一条链路是“从原始流量到可处置告警”。后端并不是直接把上传文件展示出来，而是调用 Detect 模块，把流量转换成模型能够理解的序列特征，再把推理结果同步为事件数据。</p>

  <div class="mi-flow">
    <div class="mi-step"><b>1. 导入流量</b>上传或放入 pcap / pcapng 文件。</div>
    <div class="mi-step"><b>2. 提取特征</b>按五元组聚合流，生成 DPLS 包长序列。</div>
    <div class="mi-step"><b>3. 模型推理</b>加载元学习/异常检测模型，输出检测结论。</div>
    <div class="mi-step"><b>4. 合并元数据</b>补充时间、协议、服务、IP、端口等字段。</div>
    <div class="mi-step"><b>5. 写入数据库</b>导入 detect_import 并同步到 events。</div>
    <div class="mi-step"><b>6. 处置展示</b>进入告警、专家工作台与态势大屏。</div>
  </div>

  <h2>系统亮点</h2>
  <p>我觉得这个项目最值得展示的地方，是它没有停留在“算法 Demo”，而是尽量把安全系统真实需要的流程补齐了。普通用户可以看总览、可视化和告警；专家可以领取未知攻击、做 MITRE ATT&CK 归类、加入黑名单和发起溯源；管理员可以做专家管理、用户管理和审计追踪。</p>

  <div class="mi-grid">
    <div class="mi-card"><strong>检测与业务打通</strong>pcap 检测结果不是孤立 CSV，而是能同步进数据库并在页面中继续流转。</div>
    <div class="mi-card"><strong>双端展示</strong>PC 主页面负责操作，大屏负责汇报展示，适合课程答辩和项目演示。</div>
    <div class="mi-card"><strong>处置闭环</strong>告警从“未处理”到“处理中、已归类、已关闭”，过程可记录、可审计。</div>
  </div>

  <figure class="mi-shot">
    <img src="/assets/images/projects/encrypted-traffic/overview.png" alt="系统实时总览页面">
    <figcaption>实时总览：把今日检测、告警、高危事件、未知攻击等关键指标放在首页，适合快速说明系统运行状态。</figcaption>
  </figure>

  <figure class="mi-shot">
    <img src="/assets/images/projects/encrypted-traffic/alerts.png" alt="异常告警页面">
    <figcaption>异常告警：检测结果进入事件列表后，可以继续筛选、查看详情、流转状态并交给专家处理。</figcaption>
  </figure>

  <figure class="mi-shot">
    <img src="/assets/images/projects/encrypted-traffic/topn.png" alt="TopN 可视化分析页面">
    <figcaption>TopN 分析：通过 ECharts 展示攻击、协议、服务、风险等级等分布，让检测结果更适合汇报表达。</figcaption>
  </figure>

  <figure class="mi-shot">
    <img src="/assets/images/projects/encrypted-traffic/traceback.png" alt="路径追踪页面">
    <figcaption>路径追踪：把安全事件进一步转化为溯源任务，补足“发现异常之后怎么办”的系统能力。</figcaption>
  </figure>

  <h2>技术结构</h2>
  <p>前端采用 Vue 3、Vue Router、Pinia、Vite 与 ECharts；后端使用 Node.js、Express、JWT、MySQL；检测模块使用 Python、Scapy、PyTorch、numpy 与 pymysql；部署方式使用 Docker Compose，把 MySQL、后端、主页面和动态感知大屏统一拉起。</p>

  <p>公开仓库中保留了系统源码、Docker 编排、数据库结构、文档、检测脚本和模型文件；没有上传本地依赖、构建产物、运行日志、环境文件和大体积 pcap 样本。这样仓库更适合展示和二次开发，也避免把本地运行痕迹一起公开。</p>

  <h2>下一步可以继续加强的地方</h2>
  <p>如果后续继续做，我会优先加强三个方向：第一是增加更标准的数据集接入和实验指标展示；第二是把模型检测结果的可解释性做出来，例如显示影响判断的关键流特征；第三是把大屏与告警处置之间的联动做得更强，让演示时能够从态势图直接跳到具体事件。</p>
</div>
