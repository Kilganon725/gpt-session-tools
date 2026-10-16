# GPT Session Tools

基于 [gtxx3600/GPTSession2CPAandSub2API](https://github.com/gtxx3600/GPTSession2CPAandSub2API) 的个人维护分支，保留 MIT 许可证和原始作者版权。

[打开转换工具](https://kilganon725.github.io/gpt-session-tools/)

支持 CPA、sub2api、Cockpit、9router、Codex、AxonHub、Codex-Manager。粘贴或拖入 JSON，在浏览器内转换并下载；无需安装依赖。也可以下载仓库，直接打开 `docs/index.html` 离线使用。

## 能否用来做 API 中转站？

**它能简化凭据导入，但不是中转站，也不保证导入后可以调用。**

- 不包含 API 路由、用户密钥、计费、限流、支付或账号续期服务。
- 上游 README 已说明 Web session 转换不能绕过 Codex 手机绑定要求。
- Web session 通常缺少 refresh token，access token 到期后不能自动续期。
- 部分输出保留上游生成占位 id_token 的行为。占位 JWT 只是兼容解析结构，不是 OpenAI 签发的真实身份证明，也不会增加权限。
- ChatGPT 订阅登录与 Platform API key 是不同认证方式，转换不会把 Plus 变成官方 API 余额。通用 API 服务应独立配置和验证上游。
- 尚未用真实账号凭据进行目标中转工具导入、推理、续期、并发或计费验证，因此不声称商业中转方案已验证。

参考：[OpenAI 认证文档](https://learn.chatgpt.com/docs/auth)、[原项目说明](https://github.com/gtxx3600/GPTSession2CPAandSub2API)。核查日期：2026-10-16。

## 本分支调整

- 移除第三方推广入口，增加转换与真实认证的区别说明。
- 增加浏览器 CSP，禁止页面脚本联网（`connect-src 'none'`），不引入外部脚本。
- 保留原项目转换测试，并添加 GitHub Actions 自动检查。
- 页面只在内存中处理输入，不写 localStorage/sessionStorage。复制和下载由用户主动触发；下载文件仍包含敏感凭据，请妥善保存，不要提交到 Git。

## 本地运行与验证

直接打开 `docs/index.html`，或：

```sh
python3 -m http.server 8765 --bind 127.0.0.1 --directory docs
```

访问 http://127.0.0.1:8765 。运行格式转换测试：

```sh
node tests/convert-session.test.js
```

测试使用合成数据，不需要也不验证真实账号。GitHub Pages 仅托管静态文件，不承载 API 后端。
