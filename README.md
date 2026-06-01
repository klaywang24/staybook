# Staybook · 酒店房卡收藏

收藏酒店房卡、追踪三大集团（万豪 / 希尔顿 / 凯悦）住宿足迹与忠诚度进度的 Web App。

🔗 线上：https://staybook-myself.netlify.app

## 功能
- 游客免登录浏览；登录后云端同步、多设备通用
- 邮箱 / Google 登录；加卡需登录
- 房卡收藏（可上传真实房卡照片）、合格夜与等级进度
- 解锁地球（住过的国家 / 城市可视化 + 分享图）

## 技术栈
- 前端：单文件 `index.html`（原生 HTML/CSS/JS，无构建步骤）
- 后端：Supabase（Auth + Postgres + Storage），项目 ref `fnfoyntovduuiweknsgj`
- 托管：Netlify（`staybook-myself`）

## 更新与部署
编辑 `index.html` 后，二选一：

\`\`\`bash
# A：网络通时（推荐，含 GitHub 备份）
git add . && git commit -m "..." && git push   # Netlify 自动部署

# B：GitHub 连不上时
netlify deploy --prod --dir .                  # 直连 Netlify
\`\`\`

## 后端要点
- Auth：邮箱（已关邮箱验证，注册即时）+ Google OAuth
- 表：profiles / cards / memberships，均启用 RLS（每人仅能访问自己的数据）
- Storage：keycards bucket（房卡照片）
- 防休眠：staybook-keepalive（pg_cron）每日写一次 keepalive 表，避免免费项目闲置被暂停

## 安全
仓库仅含 Supabase 公开 anon key 与 Google client ID（均可公开）；
client secret 存于 Supabase 服务端，不在代码里。
