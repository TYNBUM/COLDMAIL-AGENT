##COLDMAIL AGENT
面向导师联系邮件生成和信息抓取的 Node 工具集。

## 功能概览
- PDF 简历解析：`pdfReader.mjs`
- 套磁信生成：`runContactPdfUrl.mjs` / `runContactInteractive.mjs`，调用 `profContactAgent.mjs`
- 邮箱托管 CLI：`metaAgent.mjs`（Gmail IMAP/SMTP，列表/回复/AI 草稿）
- 信息抓取：`spiderAgent.mjs`（导师简介页抓取、Crossref 摘要、可选 Bing、学院站内浅爬、LLM 结构化）

#npm install
# 如需抓取/结构化：
# node-fetch, https-proxy-agent 已在项目中使用
环境变量

# OpenAI
OPENAI_API_KEY=...

# 邮箱托管（metaAgent）
GMAIL_USER=you@gmail.com
GMAIL_APP_PASSWORD=xxxx xxxx xxxx xxxx
POLL_INTERVAL_MS=60000
AUTO_SEND=false

# 抓取/搜索
HTTP_PROXY=http://127.0.0.1:7890    # 可选
BING_SEARCH_KEY=...                 # 可选，用于 Bing Web Search
BING_ENDPOINT=https://api.bing.microsoft.com/v7.0/search  # 可选
使用示例
套磁信（PDF + URL）
sh

node src/runContactPdfUrl.mjs
# 交互输入 PDF 路径、导师页面 URL，可自动猜导师/学院，生成套磁信
邮箱托管 CLI（Gmail）
sh

node src/metaAgent.mjs
# 列表未读邮件，分页查看，AI/手动回复并确认发送，发送后可选标记已读
导师信息抓取与结构化
sh

node -e "import('./src/spiderAgent.mjs').then(async m => {
  const info = await m.crawlProfessorInfoWithSearch({
    url: 'https://example.com/prof',     // 导师简介页
    enableCrossrefSearch: true,
    enableBingSearch: true,
    enableSchoolCrawl: true,
    schoolSiteStartUrl: 'https://school.edu/faculty', // 学院入口
    profName: '张三',
  });
  const structured = await m.normalizeWithLLM(info);
  console.log(JSON.stringify(structured, null, 2));
}).catch(err => { console.error(err); process.exit(1); });"
文件说明
src/runContactPdfUrl.mjs：CLI，读 PDF、抓导师页、AI 生成邮件。
src/runContactInteractive.mjs：交互版，粘贴简历/导师简介或抓取 URL。
src/profContactAgent.mjs：套磁信生成核心（prompt + OpenAI 调用）。
src/pdfReader.mjs：PDF 解析。
src/metaAgent.mjs：Gmail IMAP/SMTP 邮件托管 CLI。
src/spiderAgent.mjs：抓取、Crossref/Bing/站内爬、LLM 结构化。
限制与注意
强反爬站点（验证码/登录/高度动态渲染）需人工或官方 API。
Crossref 摘要字段不保证存在；Bing 搜索需 BING_SEARCH_KEY。
请遵守目标网站的 robots/条款与版权要求。
