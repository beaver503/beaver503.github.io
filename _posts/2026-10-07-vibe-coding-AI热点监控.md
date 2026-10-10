---
title: AI热点监控
date: 2026-10-07
categories: vibe-coding
tags:
  - vibe-coding
  - 博客
render_with_liquid: false
---
# 一、需求分析
## 1.1 需求分析

第一时间获取一些热点
不依赖人工搜索
自动发现指定热点变化
并及时给我发送通知

几个具体化功能
1.用户手动输入几个要监控的关键词，当关键词内容为真时（注意利用ai识别假冒的内容）第一时间发送通知
2.每隔一段时间，自动收集用户输入的指定范围内的热点，并仍用户看到

产品的形式
1.响应兼容的Web页面
2.封装成Agent Skills，能够交给ai来监控和发现热点

谁会用这个工具？
解决什么问题？
用什么方式呈现？
能否实现？
先做什么？先做Web核心功能，再封装Skills

敏捷开发
需求明确且轻量
快输迭代
用户即开发者

先做出能用的版本，再不断迭代完善

## 1.2 环境准备

### 1.2.1 最新 vs code

### 1.2.2 GitHub Copilot 插件

打开聊天 ctrl + alt + i
Copilot的工作模式：
内联补全 | 在编辑器中实时提供代码建议
chat对话 | 与ai对话，方案设计，问题排查
agent模式 | ai自主规划并执行多步骤任务，开发，代码重构

>使用agent模式从方案设计到代码开发，只需在关键节点进行人工确认

### 1.2.3 claude 大模型

Opus 4.5 ：负责写代码、生成方案
OpenRouter ：负责运行时的内容分析，集成在我们开发的工具中

## 1.3 扩展工具

### 1.3.1 MCP

模型上下文协议，定义了一套标准接口，让ai模型和外部工具和数据源进行交互

如：Firecrawl MCP（网页抓取能力）
Context7 MCP 获取最新的技术文档，避免使用过时的 API 和代码
### 1.3.2 Skills

封装给ai的技能包
纯文件，无需额外进程
提示词 + 脚本 + 参考资料

如：UI UX Pro Max(前端美化技能)

我们使用
Firecrawl 网页内容抓取

Context7 获取最新文档，防止ai使用了过时的代码

UI UX Pro Max 前端美化
Skill Creator 制作技能，推荐使用Vercel的Skills工具

Skills 工具的作用是可以同一行命令帮你快速安装AI技能

使用 Skills 需要安装 npx

npx --version 检验 npx 是否安装

### 1.3.3 npx

npx 是 Node.js 自带的包执行工具
他可以直接执行远程的 npm 包，不需要全局安装

如：npx skills add ... 直接运行这个Skills工具

