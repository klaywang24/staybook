# Staybook 🏨

> A guest-first web app for collecting hotel keycards and tracking your stays, loyalty progress, and world footprint across Marriott, Hilton & Hyatt.
> 一个「游客优先」的酒店房卡收藏 Web App，追踪你在万豪 / 希尔顿 / 凯悦的住宿足迹、合格夜与忠诚度进度。

**Live / 线上：** https://staybook-myself.netlify.app

## Features · 功能

- 🗂️ **Keycard wallet / 房卡卡包** — collect cards by chain; upload real keycard photos or auto-generate brand-styled faces. 按集团收藏房卡，可上传真实房卡照片，或自动生成品牌风格卡面。
- 🏆 **Loyalty tracking / 忠诚度追踪** — qualifying nights & tier progress per program, computed automatically. 各计划合格夜与等级进度，自动累计。
- 🌍 **Unlock the Earth / 解锁地球** — visualize the countries & cities you've stayed in, with an exportable share card. 可视化住过的国家与城市，并可导出分享图。
- 👤 **Guest-first / 游客优先** — browse instantly with no login; sign in (email or Google) to sync across devices. 免登录即可浏览；邮箱或 Google 登录后多设备云端同步。
- ☁️ **Cloud sync / 云端同步** — cards, photos & memberships stored per-user with row-level security. 房卡、照片、会员资料按用户隔离存储（RLS）。

## Stack · 技术栈

- **Frontend / 前端** — a single `index.html` (vanilla HTML/CSS/JS, no build step). 单文件，无构建步骤。
- **Backend / 后端** — [Supabase](https://supabase.com) (Auth + Postgres + Storage).
- **Hosting / 托管** — [Netlify](https://netlify.com).

## Deploy / Update · 部署与更新

Edit `index.html`, then pick one. / 编辑 `index.html` 后，二选一：

```bash
# A — GitHub reachable / 网络通时（自动部署 + 备份）
git add . && git commit -m "…" && git push

# B — direct deploy / 直连部署（绕过 GitHub）
netlify deploy --prod --dir .
```

## Backend notes · 后端要点

- **Auth / 登录** — email/password (instant signup) + Google OAuth. 邮箱（注册即时）+ Google。
- **Tables / 数据表** — `profiles`, `cards`, `memberships`, all with RLS so each user sees only their own rows. 均启用 RLS，按用户隔离。
- **Storage / 存储** — `keycards` bucket for uploaded card photos. 存房卡照片。
- **Keep-alive / 防休眠** — a daily `pg_cron` job writes to a `keepalive` table so the free-tier project never pauses. 每日 pg_cron 写一次，避免免费项目闲置被暂停。

## Security · 安全

The repo ships only the Supabase **public anon key** and the **Google client ID** — both safe to expose. The Google client secret stays server-side in Supabase, never in the code. RLS protects all user data.
仓库只含 Supabase 公开 anon key 与 Google client ID（均可公开）；Google client secret 存于 Supabase 服务端，不在代码里；RLS 保护所有用户数据。

## License · 许可

MIT — see [LICENSE](LICENSE). / 采用 MIT 许可，详见 LICENSE。

## Author · 作者

Built and maintained by [@klaywang24](https://github.com/klaywang24).
由 [@klaywang24](https://github.com/klaywang24) 构建与维护。

This is open infrastructure: a guest-first app shell, a Supabase auth / data / storage schema, and a hotel-brand & loyalty data model. If it's useful to your project / startup / team, fork it and make it yours.
这是一套开放基建：一个「游客优先」的应用骨架、一套 Supabase 认证 / 数据 / 存储 schema，以及一份酒店品牌与忠诚度数据模型。如果对你的项目 / 创业 / 团队有用，尽管 fork 拿去改成你自己的。

If you add a hotel brand, a loyalty program, or a new card design, submit a PR.
如果你新增了酒店品牌、忠诚度计划或卡面设计，欢迎提 PR。
