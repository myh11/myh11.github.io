---
layout: post
title: "留学申请与审核系统"
date: 2026-05-25 19:00:00 +0800
categories: 项目
tags: [课程项目, 留学申请, 审核流转, Spring Boot, Vue, MySQL, JWT, MyBatis-Plus]
author: myh
description: "一个围绕留学申请、国内审核、学校审核、候补调剂、名额占位和审计日志构建的业务管理系统。"
---

这个项目是一个面向留学申请业务的后台管理系统。它不是只做简单的表单提交，而是把“代理专员提交申请、国内审查员审核资质、学校专员审核专业适配、系统管理员维护基础配置”这条业务链路整理成可运行、可追踪、可约束的系统流程。

<!--more-->

<style>
.project-post {
  --pp-bg: #07111f;
  --pp-panel: rgba(15, 23, 42, .78);
  --pp-line: rgba(56, 189, 248, .22);
  --pp-blue: #38bdf8;
  --pp-cyan: #67e8f9;
  --pp-green: #34d399;
  --pp-purple: #a78bfa;
  --pp-text: #e5f4ff;
  --pp-muted: #9fb5c8;
  color: var(--pp-text);
  line-height: 1.82;
}
.project-post * { box-sizing: border-box; }
.project-hero,
.project-section {
  border: 1px solid var(--pp-line);
  border-radius: 24px;
  background:
    radial-gradient(circle at 12% 0%, rgba(103, 232, 249, .18), transparent 34%),
    linear-gradient(135deg, rgba(8, 16, 31, .94), rgba(15, 23, 42, .86));
  box-shadow: 0 24px 60px rgba(2, 8, 23, .2);
}
.project-hero {
  padding: 34px;
}
.project-kicker {
  display: inline-flex;
  padding: 6px 12px;
  border: 1px solid rgba(52, 211, 153, .35);
  border-radius: 999px;
  color: var(--pp-green);
  background: rgba(52, 211, 153, .08);
  font-size: 13px;
  letter-spacing: .08em;
}
.project-hero h2 {
  margin: 18px 0 12px;
  color: #f8fdff;
  font-size: 32px;
  line-height: 1.22;
}
.project-hero p,
.project-section p {
  color: #c6d7e4;
}
.project-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 22px;
}
.project-button {
  display: inline-flex;
  padding: 10px 14px;
  border: 1px solid rgba(103, 232, 249, .32);
  border-radius: 13px;
  color: #e8fbff;
  text-decoration: none;
  background: rgba(56, 189, 248, .1);
  font-weight: 700;
}
.project-button.primary {
  border-color: rgba(52, 211, 153, .42);
  background: linear-gradient(135deg, rgba(52, 211, 153, .22), rgba(56, 189, 248, .14));
}
.project-section {
  margin-top: 24px;
  padding: 26px;
}
.project-section h2 {
  margin: 0 0 12px;
  color: #f8fdff;
  font-size: 24px;
}
.project-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 14px;
}
.project-card {
  padding: 18px;
  border: 1px solid rgba(103, 232, 249, .16);
  border-radius: 18px;
  background: rgba(2, 8, 23, .35);
}
.project-card h3 {
  margin: 0 0 8px;
  color: var(--pp-cyan);
  font-size: 17px;
}
.project-card p {
  margin: 0;
  color: var(--pp-muted);
}
.project-table {
  overflow-x: auto;
  border: 1px solid rgba(103, 232, 249, .16);
  border-radius: 18px;
}
.project-table table {
  width: 100%;
  margin: 0;
  border-collapse: collapse;
  background: rgba(2, 8, 23, .28);
}
.project-table th,
.project-table td {
  padding: 12px 14px;
  border-bottom: 1px solid rgba(103, 232, 249, .12);
  color: #cfe3ef;
}
.project-table th {
  color: #f8fdff;
  background: rgba(56, 189, 248, .12);
}
.project-flow {
  display: grid;
  grid-template-columns: repeat(6, minmax(0, 1fr));
  gap: 10px;
}
.project-flow span {
  min-height: 96px;
  padding: 13px;
  border: 1px solid rgba(103, 232, 249, .16);
  border-radius: 16px;
  color: #dff7ff;
  background: rgba(15, 23, 42, .62);
  font-weight: 700;
}
.project-flow small {
  display: block;
  margin-top: 8px;
  color: var(--pp-muted);
  font-weight: 400;
}
@media (max-width: 900px) {
  .project-grid,
  .project-flow {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
@media (max-width: 560px) {
  .project-hero,
  .project-section {
    padding: 20px;
  }
  .project-grid,
  .project-flow {
    grid-template-columns: 1fr;
  }
}
</style>

<div class="project-post">
  <section class="project-hero">
    <div class="project-kicker">Study Abroad Workflow System</div>
    <h2>把复杂申请流程做成可控、可追踪的审核闭环</h2>
    <p>留学申请业务的难点不在于“能不能填表”，而在于多个角色、多个审核阶段、多个名额约束同时存在。系统围绕申请提交、国内审核、学校审核、专业占位、候补补位、调剂建议和审计日志构建业务闭环，让每一次状态变化都有规则、有权限、有记录。</p>
    <div class="project-actions">
      <a class="project-button primary" href="https://github.com/myh11/Study-Abroad-Management-System" target="_blank" rel="noopener">查看 GitHub 仓库</a>
      <a class="project-button" href="#study-abroad-flow">业务流程</a>
      <a class="project-button" href="#study-abroad-tech">技术实现</a>
    </div>
  </section>

  <section class="project-section">
    <h2>项目定位</h2>
    <p>这个系统模拟的是“去哪学”教育机构与海外高校合作的留学申请管理场景。代理专员负责创建和提交学生申请，国内审查员负责基础资质审核，学校专员负责本校专业审核和名额占位，系统管理员维护学校、专业、批次、配额和用户账号。</p>
    <p>相比普通 CRUD 后台，这个项目更强调业务规则：申请不能随意跳状态，名额不能被重复占用，候补补位要有顺序，调剂建议要保留来源，关键操作必须写入审计日志。</p>
  </section>

  <section id="study-abroad-flow" class="project-section">
    <h2>核心业务流程</h2>
    <div class="project-flow">
      <span>创建草稿<small>代理专员录入学生、学校、专业和材料信息。</small></span>
      <span>提交申请<small>系统校验批次、必填字段和申请约束。</small></span>
      <span>国内审核<small>审查材料完整性、成绩门槛和真实性风险。</small></span>
      <span>学校审核<small>学校专员判断专业适配度和录取可能性。</small></span>
      <span>占位 / 候补<small>结合学校总名额与专业名额进行双重控制。</small></span>
      <span>调剂 / 归档<small>给出调剂建议，记录最终处理结果和操作日志。</small></span>
    </div>
  </section>

  <section class="project-section">
    <h2>角色与权限设计</h2>
    <div class="project-table">
      <table>
        <thead>
          <tr>
            <th>角色</th>
            <th>主要职责</th>
            <th>权限边界</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>代理专员</td>
            <td>创建申请、上传材料、提交申请、查看状态、接收调剂建议</td>
            <td>只能操作自己负责的申请，撤销动作受状态限制</td>
          </tr>
          <tr>
            <td>国内审查员</td>
            <td>审核基础资质、材料完整性、成绩门槛和真实性风险</td>
            <td>不能直接修改学校录取结果和名额配置</td>
          </tr>
          <tr>
            <td>学校专员</td>
            <td>处理本校申请，完成学校审核、专业审核、占位和候补管理</td>
            <td>仅处理本校范围内数据，不查看无关敏感信息</td>
          </tr>
          <tr>
            <td>系统管理员</td>
            <td>维护学校、专业、批次、配额、用户账号和审计日志</td>
            <td>具备全局配置能力，但关键操作需要留痕</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

  <section id="study-abroad-tech" class="project-section">
    <h2>技术架构</h2>
    <div class="project-grid">
      <div class="project-card">
        <h3>后端</h3>
        <p>Java 17、Spring Boot 3.3.5、Spring Security、JWT、Spring Validation、MyBatis-Plus、Maven。</p>
      </div>
      <div class="project-card">
        <h3>前端</h3>
        <p>Vue 3、TypeScript、Vite、Vue Router、Pinia、Element Plus、Axios，用于构建后台管理台。</p>
      </div>
      <div class="project-card">
        <h3>数据库</h3>
        <p>MySQL 8.x，围绕用户、学校、专业、批次、配额、申请、审核、候补和审计日志建模。</p>
      </div>
    </div>
  </section>

  <section class="project-section">
    <h2>我认为这个项目的重点</h2>
    <div class="project-grid">
      <div class="project-card">
        <h3>状态机思维</h3>
        <p>申请状态不是页面上的文本，而是系统规则。提交、审核通过、驳回、补件、候补、调剂和归档都需要合法流转。</p>
      </div>
      <div class="project-card">
        <h3>配额并发控制</h3>
        <p>学校总名额和专业名额要同时控制，学校审核通过后还要考虑占位、释放、候补补位和调剂派生。</p>
      </div>
      <div class="project-card">
        <h3>审计可追踪</h3>
        <p>审核系统不能只保存最终结果，还要记录谁在什么时间做了什么操作，方便回溯责任和复盘流程。</p>
      </div>
    </div>
  </section>

  <section class="project-section">
    <h2>项目总结</h2>
    <p>这个项目让我更清楚地理解到，后台管理系统并不是“表格 + 按钮”的简单组合。真正重要的是把业务规则落到权限、状态、事务和数据结构里，让系统不仅能展示数据，还能约束流程、减少错误、保留过程。</p>
    <p>如果用一句话概括：这是一个以审核流转为核心、以角色权限和配额控制为约束、以审计日志为保障的留学申请业务管理系统。</p>
  </section>
</div>
