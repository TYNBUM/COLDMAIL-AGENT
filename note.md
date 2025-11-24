NOTES
代理池：可用 PROXY_POOL=http://ip1:port,http://ip2:port 轮换代理，抓取时随机/轮询，失败换下一个。
UA/限速：为降低被封，建议随机 User-Agent，请求间隔 0.5–1.5s，失败指数退避重试。
证书问题：域名证书不匹配时优先改用正确域名或 http（谨慎）；不建议关闭 TLS 校验。
站内爬：crawlSchoolSiteForProfessor 只在同域浅爬，默认最多 12 页，匹配导师姓名。
强反爬：验证码/登录保护需人工或 headless 浏览器/官方 API，当前实现无法绕过。
输出结构化：normalizeWithLLM 生成 JSON，包含 profile 概述、papers、activities、web_results、school_hits，便于直接用于邮件生成。
