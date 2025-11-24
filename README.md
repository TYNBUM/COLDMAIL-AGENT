# COLDMAIL-AGENT

面向导师联系邮件生成和信息抓取的 Node 工具集。

## 功能概览
- PDF 简历解析：`pdfReader.mjs`
- 套磁信生成：`runContactPdfUrl.mjs` / `runContactInteractive.mjs`，调用 `profContactAgent.mjs`
- 邮箱托管 CLI：`metaAgent.mjs`（Gmail IMAP/SMTP，列表/回复/AI 草稿）
- 信息抓取：`spiderAgent.mjs`（导师简介页抓取、Crossref 摘要、可选 Bing、学院站内浅爬、LLM 结构化）

## 依赖安装
```sh
npm install
# 如需抓取/结构化：
# node-fetch, https-proxy-agent 已在项目中使用
