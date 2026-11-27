# 发布规范 · Publishing Guide

「零元情报。」上架流程的唯一标准。新卡唔跟呢份规范，一律唔准上架。

## 专区（六区，次序固定）

| zone id | 中文名 | English | 收什么 |
|---|---|---|---|
| `hot` | 🔥 错过哭死 | Must Not Miss | 全站精选、限时最劲嗰几则（跨区精选） |
| `games` | 🎮 游戏专区 | Games | 限免游戏、游戏内福利 |
| `deals` | 🧶 羊毛专区 | Freebies & Deals | 免费额度、零元资源、真优惠 |
| `earn` | 🏆 搞钱专区 | Earn | 比赛、悬赏、黑客松、agent 竞赛、有奖任务 |
| `tools` | 🧰 AI 工具箱 | AI Toolbox | Skills、MCP、生图 prompt、开源工具 |
| `ai` | 🤖 AI 资讯 | AI News | AI 新闻、模型发布、行业资讯（纯资讯） |

拆分判断：卡片本体是「攞嚟用既家伙」（skill / MCP / prompt 库 / 模板 / 开源工具）→ `tools`；
是「睇完就算跟上既消息」（发布、榜单观察、概念梳理、热话）→ `ai`。
卡片自带既类别标记可作参考：乙类·工具资源 → 多数入 `tools`；甲类·纯资讯 → 多数留 `ai`，但以内容为准。

## 双语铁律（No.021 起）

- **每张新卡必须全双语**：所有可见文字都要有 `<span class="lz">简体中文</span><span class="le">English</span>` 一对，
  包括：badge、cls 类别、h2 标题、hook、每个 fact 的 dt 与 dd（连 `<small>` 注脚）、CTA、origin 来源链接文字。
- 例外（语言中立，唔使包）：`.src` 来源行（来源名＋日期）、品牌/产品专名、数字、URL 本身。
- 中文用**简体普通话书面语**（唔好用粤语口语）；英文要完整句子，唔好逐字硬译。
- 旧卡 No.001–020 保持粤语原文，**永不改动**（定案）。
- 切换机制：`html[data-lang]` + CSS `[data-lang="zh"] .le{display:none}` / `[data-lang="en"] .lz{display:none}`，
  页首 🌐 按钮切换，选择存 `localStorage` 键 `zdf-lang`。新加任何框架文字（专区名、计数、按钮、状态句）
  必须同时有 lz/le 两份；JS 里动态生成既文字（如日期跳转状态句）要查 `window.__zdfLang` 出双语，
  专区英文名映射在 `jumpToDate` 的 `zonesTxt` 对象里，新专区必须同步加。

### 已知历史缺口（2026-11-28 审计）

- No.021–071 共 51 张：h2/hook/facts/cta/badge/cls 全部齐双语，无一缺结构。
- 其中 35 张（No.037–071 多数）的 origin 来源链接文字系中文单语（如「GitHub 仓库页」）——新卡唔准再犯；
  旧卡按「验证样本」方式逐张补：No.071 已于 2026-11-28 补齐并验证，其余留待逐批处理。

## 新卡模板

新卡加喺所属专区 `.deck` 的**第一张**位置，并写 `data-date="YYYY-MM-DD"`：

```html
<article class="dcard" data-cls="a" data-date="YYYY-MM-DD">
  <div class="card-scroll">
  <div class="card-top">
    <span class="badge ok"><span class="lz">✅ 已核实</span><span class="le">✅ Verified</span></span>
    <span class="cls"><span class="lz">📰 甲类 · 纯资讯</span><span class="le">📰 Intel only</span></span>
    <span class="src">来源名 · YYYY-MM-DD</span>
  </div>
  <div class="idx">N<b>o.</b>0XX</div>
  <h2><span class="lz">中文标题｜<span class="acc">重点词</span></span><span class="le">English Title｜<span class="acc">Key Term</span></span></h2>
  <p class="hook"><span class="lz">一句话钩子，讲清是什么、几劲、门槛。</span><span class="le">One-line hook: what it is, why it matters, what it takes.</span></p>
  <dl class="facts">
    <div class="fact"><dt><span class="lz">费用</span><span class="le">Price</span></dt><dd><span class="lz">完全免费<small>补充说明</small></span><span class="le">Free<small>Detail</small></span></dd></div>
    <div class="fact"><dt><span class="lz">门槛</span><span class="le">Requires</span></dt><dd><span class="lz">…</span><span class="le">…</span></dd></div>
    <div class="fact"><dt><span class="lz">截止</span><span class="le">Deadline</span></dt><dd><span class="lz">…</span><span class="le">…</span></dd></div>
  </dl>
  </div>
  <a class="cta" href="https://…" rel="noopener"><span class="lz">去领取 →</span><span class="le">Claim it →</span></a>
  <p class="origin"><span class="lz">一手来源：</span><span class="le">First-hand source: </span><a href="https://…" rel="noopener"><span class="lz">来源页中文名</span><span class="le">Source page name</span></a></p>
</article>
```

类别标记：甲类·纯资讯用 `data-cls="a"`、cls 文字「📰 甲类 · 纯资讯 / Intel only」；
乙类按内容二选一：「🔗 乙类 · 有得拎 / Claimable」（deals、earn、games）或
「🔗 乙类 · 工具资源 / Tools & Resources」（tools）。

## 卡片文案长度标准（2026-11-28 定，配合页面标准高）

页面已行「标准高」制度：宽屏行高统一（两栏 zh 700／en 750、三栏 zh 740／en 810 px）、
细屏 deck 定高（zh 约 675–720／en 约 743–780 px），卡内纵向 flex 将 CTA 钉底；
**超出标准高的卡靠卡内滚动条**（已做可见样式）。2026-11-28 结构定版：内容入 `.card-scroll` 层自碌，`.cta`／`.origin` 喺层外钉底——碌内容时掣常驻可见、永不遮字；模板唔再用 `.spacer`。新卡文案按以下上限写，
令绝大多数卡在标准高内全显、高度自然统一（上限按 2026-11-28 实测现行 78 张卡分布定，
约在 p75–p85 水平）：

| 部分 | 中文上限 | English 上限 | 现行实测（p50 / p90 / max） |
|---|---|---|---|
| h2 标题 | ≤ 40 字 | ≤ 80 字符 | zh 34 / 49 / 64；en 53 / 88 / 107 |
| hook | ≤ 100 字 | ≤ 260 字符 | zh 79 / 116 / 160；en 180 / 285 / 376 |
| facts 行数 | ≤ 4 行 | ≤ 4 行 | 全部 3–4 行 |
| 每行 dd 主文 | ≤ 35 字 | ≤ 60 字符 | zh 21 / 41 / 77；en 31 / 62 / 161 |
| 每行 dd 的 `<small>` 注脚 | ≤ 20 字 | ≤ 40 字符 | — |

超出处理（按次序）：
1. **先删减合并**：删重复信息、删 `<small>` 注脚、合并同类 fact 行（例如「费用＋门槛」并一行）。
2. **关键事实唔删得**：费用、截止、门槛、地区限制几贵都要留，宁愿超长。
3. 删无可删仍然超长 → **接受卡内滚动**，照上架；但同一专区唔好连续两张都超长（排版上要隔开）。
4. 内容多到滚动都唔合理（例如合集类）→ 拆做两张卡，或者只摘最值钱嗰部分，唔好塞爆一张。

## 上架检查清单

1. [ ] 编号接续全站最大编号 +1；同一则跨区精选（如入 hot）沿用原编号。
2. [ ] `data-date` 系上架日；新卡放专区 deck 第一张。
3. [ ] 事实核实：一手来源可达，价格/日期/奖金/规则与官方页一致；地区与门槛写明。
4. [ ] 双语逐项对：badge、cls、h2、hook、每个 dt/dd/small、CTA、origin 链接文字全部有 lz+le 对；无中文残留喺 span 外（`.src` 行除外）。
5. [ ] 专区 tile 的 `zcount` 数字 +1（lz「N 则」/ le「N items」同步改）；deckbar 的 `.total` 占位数字同步（JS 会自动重计，但占位要对）。
6. [ ] 文案长度跟「卡片文案长度标准」：h2／hook／facts 行数／dd 字数唔超上限；超长已按次序删减，关键事实（费用／截止／门槛）齐全。
7. [ ] 本地开站验证：`python3 -m http.server` 后逐区点入，计数正确；撳 🌐 切换中/英各一次，新卡两种语言都完整显示、无漏中文/漏英文；手机宽度（390px）无爆版、长卡可碌到底见 CTA。
8. [ ] Commit 讯息讲明：上架编号、所属专区、一手来源。Push 后 curl 线上页确认新版生效。
