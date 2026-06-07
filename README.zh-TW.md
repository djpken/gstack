# gstack

> [English](README.md) · **繁體中文**
>
> 這是社群維護的繁體中文翻譯，內容對照英文 [`README.md`](README.md)。指令、程式碼、檔名維持原文。若翻譯與英文版有出入，**以英文版為準**。

> 「我大概從十二月開始就沒打過一行 code 了，基本上啦，這是個極大的改變。」 — [Andrej Karpathy](https://fortune.com/2026/03/21/andrej-karpathy-openai-cofounder-ai-agents-coding-state-of-psychosis-openclaw/)，No Priors podcast，2026 年 3 月

當我聽到 Karpathy 這麼說，我想搞清楚他是怎麼辦到的。一個人怎麼能像二十人的團隊一樣出貨？Peter Steinberger 幾乎是單槍匹馬靠 AI agent 做出了 [OpenClaw](https://github.com/openclaw/openclaw) — 247K GitHub stars。革命已經到了。一個有對的工具的建造者，可以比傳統團隊跑得更快。

我是 [Garry Tan](https://x.com/garrytan)，[Y Combinator](https://www.ycombinator.com/) 的總裁暨執行長。我跟數千家新創共事過 — Coinbase、Instacart、Rippling — 在他們還是車庫裡一兩個人的時候。在 YC 之前，我是 Palantir 最早期的工程/PM/設計師之一，共同創辦了 Posterous（賣給 Twitter），也打造了 YC 的內部社群網路 Bookface。

**gstack 就是我的答案。** 我做產品做了二十年，而現在我出貨的產品比以往任何時候都多。過去 60 天：3 個 production 服務、40+ 個出貨功能，兼職做的，同時還全職在跑 YC。以邏輯程式碼改動量計算 — 不是被 AI 灌水的原始 LOC — 我 2026 的速率是 **2013 的約 810 倍**（每天 11,417 對 14 行邏輯程式碼）。年初至今（到 4 月 18 日），2026 已經產出了 **整個 2013 年的 240 倍**。這是橫跨 40 個公開 + 私有 `garrytan/*` repo（含 Bookface）、排除一個 demo repo 後測得的。大部分是 AI 寫的。重點不是誰打的字，是出了什麼貨。

> LOC 的批評者說「原始行數會隨 AI 灌水」沒錯。但他們說「校正灌水後我生產力更低」就錯了。我生產力高很多。完整方法論、注意事項與重現腳本：**[On the LOC Controversy](docs/ON_THE_LOC_CONTROVERSY.md)**。

**2026 — 1,237 次貢獻且持續增加：**

![GitHub contributions 2026 — 1,237 contributions, massive acceleration in Jan-Mar](docs/images/github-2026.png)

**2013 — 我在 YC 做 Bookface 時（772 次貢獻）：**

![GitHub contributions 2013 — 772 contributions building Bookface at YC](docs/images/github-2013.png)

同一個人。不同時代。差別在工具。

**gstack 就是我做到這件事的方法。** 它把 Claude Code 變成一支虛擬工程團隊 — 一個重新思考產品的 CEO、一個鎖定架構的工程主管、一個抓 AI slop 的設計師、一個找出 production bug 的審查者、一個會開真瀏覽器的 QA 主管、一個跑 OWASP + STRIDE 稽核的資安長、一個把 PR 出掉的發布工程師。二十三個專家、八個強力工具，全是斜線指令、全是 Markdown、全部免費、MIT 授權。

這是我的開源軟體工廠。我每天都在用。我把它分享出來，是因為這些工具應該人人都能用。

Fork 它。改進它。讓它變成你的。如果你想酸免費開源軟體 — 歡迎，但我寧願你先試過再說。

**這是給誰用的：**
- **創辦人與 CEO** — 尤其是那些還想自己出貨的技術型
- **第一次用 Claude Code 的人** — 用結構化角色取代一張白紙的提示
- **技術主管與 staff 工程師** — 每個 PR 都有嚴謹的審查、QA 與發布自動化

## 快速開始

1. 安裝 gstack（30 秒 — 見下方）
2. 跑 `/office-hours` — 描述你想做的東西
3. 對任何功能想法跑 `/plan-ceo-review`
4. 對任何有改動的分支跑 `/review`
5. 對你的 staging URL 跑 `/qa`
6. 到這裡就好。你會知道這套適不適合你。

## 安裝 — 30 秒

**需求：** [Claude Code](https://docs.anthropic.com/en/docs/claude-code)、[Git](https://git-scm.com/)、[Bun](https://bun.sh/) v1.0+、[Node.js](https://nodejs.org/)（僅 Windows）

### 步驟 1：安裝到你的機器

打開 Claude Code 貼上這段，其餘交給 Claude。

> Install gstack: run **`git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup`** then add a "gstack" section to CLAUDE.md that says to use the /browse skill from gstack for all web browsing, never use mcp\_\_claude-in-chrome\_\_\* tools, and lists the available skills: /office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review, /design-consultation, /design-shotgun, /design-html, /review, /ship, /land-and-deploy, /canary, /benchmark, /browse, /connect-chrome, /qa, /qa-only, /design-review, /setup-browser-cookies, /setup-deploy, /setup-gbrain, /retro, /investigate, /document-release, /document-generate, /codex, /cso, /autoplan, /plan-devex-review, /devex-review, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade, /learn. Then ask the user if they also want to add gstack to the current project so teammates get it.

### 步驟 2：團隊模式 — 共用 repo 的自動更新（推薦）

在你的 repo 裡貼上這段。它會切換到團隊模式、把 repo 設定好讓隊友自動取得 gstack、並 commit 這個改動：

```bash
(cd ~/.claude/skills/gstack && ./setup --team) && ~/.claude/skills/gstack/bin/gstack-team-init required && git add .claude/ CLAUDE.md && git commit -m "require gstack for AI-assisted work"
```

你的 repo 裡沒有 vendor 檔案、沒有版本漂移、不用手動升級。每個 Claude Code session 開始時都會跑一次快速自動更新檢查（限流為每小時一次、網路失敗安全、完全靜默）。

把 `required` 換成 `optional`，就從「擋住隊友」變成「提醒隊友」。

### OpenClaw

OpenClaw 透過 ACP spawn Claude Code session，所以只要 Claude Code 裝了 gstack，每個 gstack 技能都能直接用。把這段貼給你的 OpenClaw agent：

> Install gstack: run `git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup` to install gstack for Claude Code. Then add a "Coding Tasks" section to AGENTS.md that says: when spawning Claude Code sessions for coding work, tell the session to use gstack skills. Include these examples — security audit: "Load gstack. Run /cso", code review: "Load gstack. Run /review", QA test a URL: "Load gstack. Run /qa https://...", build a feature end-to-end: "Load gstack. Run /autoplan, implement the plan, then run /ship", plan before building: "Load gstack. Run /office-hours then /autoplan. Save the plan, don't implement."

**設定好之後，就自然地跟你的 OpenClaw agent 說話：**

| 你說 | 會發生什麼 |
|---------|-------------|
| 「修掉 README 的錯字」 | 簡單 — 直接 Claude Code session，不需要 gstack |
| 「對這個 repo 跑安全稽核」 | spawn Claude Code 並 `Run /cso` |
| 「幫我做一個通知功能」 | spawn Claude Code，/autoplan → 實作 → /ship |
| 「幫我規劃 v2 API 重新設計」 | spawn Claude Code，/office-hours → /autoplan，存下計畫 |

進階的 dispatch routing 與 gstack-lite/gstack-full 提示模板，見 [docs/OPENCLAW.md](docs/OPENCLAW.md)。

### 原生 OpenClaw 技能（透過 ClawHub）

四個方法論技能，直接在你的 OpenClaw agent 裡運作，不需要 Claude Code session。從 ClawHub 安裝：

```
clawhub install gstack-openclaw-office-hours gstack-openclaw-ceo-review gstack-openclaw-investigate gstack-openclaw-retro
```

| 技能 | 用途 |
|-------|-------------|
| `gstack-openclaw-office-hours` | 用 6 個逼問題目拷問產品 |
| `gstack-openclaw-ceo-review` | 4 種範圍模式的戰略挑戰 |
| `gstack-openclaw-investigate` | 根因除錯方法論 |
| `gstack-openclaw-retro` | 每週工程回顧 |

這些是對話型技能。你的 OpenClaw agent 直接透過聊天執行它們。

### 其他 AI Agent

gstack 支援 10 種 AI coding agent，不只 Claude。setup 會自動偵測你裝了哪些：

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup
```

或用 `./setup --host <name>` 指定特定 agent：

| Agent | Flag | 技能安裝到 |
|-------|------|-------------------|
| OpenAI Codex CLI | `--host codex` | `~/.codex/skills/gstack-*/` |
| OpenCode | `--host opencode` | `~/.config/opencode/skills/gstack-*/` |
| Cursor | `--host cursor` | `~/.cursor/skills/gstack-*/` |
| Factory Droid | `--host factory` | `~/.factory/skills/gstack-*/` |
| Slate | `--host slate` | `~/.slate/skills/gstack-*/` |
| Kiro | `--host kiro` | `~/.kiro/skills/gstack-*/` |
| Hermes | `--host hermes` | `~/.hermes/skills/gstack-*/` |
| GBrain (mod) | `--host gbrain` | `~/.gbrain/skills/gstack-*/` |

**想加上對另一個 agent 的支援？** 見 [docs/ADDING_A_HOST.md](docs/ADDING_A_HOST.md)。一個 TypeScript 設定檔，零程式碼改動。

## 看它運作

```
你：    我想做一個給我行事曆用的每日簡報 app。
你：    /office-hours
Claude：[追問痛點 — 要具體例子，不要假設]

你：    多個 Google 行事曆、活動資訊過期、地點錯誤。
        準備超花時間而且結果還不夠好...

Claude：我要挑戰你的框定。你說「每日簡報 app」。
        但你實際描述的是一個個人幕僚長 AI。
        [抽出 5 個你沒意識到自己在描述的能力]
        [挑戰 4 個前提 — 你同意、不同意、或調整]
        [產出 3 種實作方法與工時估計]
        建議：明天先出最窄的切入點，從真實使用中學習。
        完整願景是 3 個月的專案 — 先從一個真的能用的
        每日簡報開始。
        [寫設計文件 → 自動餵給下游技能]

你：    /plan-ceo-review
        [讀設計文件、挑戰範圍、跑 10 段審查]

你：    /plan-eng-review
        [資料流的 ASCII 圖、狀態機、錯誤路徑]
        [測試矩陣、失敗模式、安全考量]

你：    批准計畫。離開 plan mode。
        [跨 11 個檔案寫了 2,400 行。約 8 分鐘。]

你：    /review
        [自動修正] 2 個問題。[詢問] race condition → 你批准修正。

你：    /qa https://staging.myapp.com
        [開真瀏覽器、點過各流程、找到並修掉一個 bug]

你：    /ship
        測試：42 → 51（+9 新）。PR：github.com/you/app/pull/42
```

你說的是「每日簡報 app」。agent 說「你在做的是幕僚長 AI」 — 因為它聽的是你的痛點，不是你的功能需求。八個指令，端到端。那不是 copilot。那是一支團隊。

## 這場 sprint

gstack 是一套流程，不是一堆工具。技能依照一場 sprint 的順序執行：

**想 → 規劃 → 建造 → 審查 → 測試 → 出貨 → 回顧**

每個技能都餵給下一個。`/office-hours` 寫出 `/plan-ceo-review` 會讀的設計文件。`/plan-eng-review` 寫出 `/qa` 會接手的測試計畫。`/review` 抓到的 bug，`/ship` 會驗證已修好。沒有東西會漏掉，因為每一步都知道前一步做了什麼。

| 技能 | 你的專家 | 他們做什麼 |
|-------|----------------|--------------|
| `/office-hours` | **YC Office Hours** | 從這裡開始。6 個逼問題目，在你寫 code 前重新框定產品。挑戰你的框定、質疑前提、產出實作替代方案。設計文件餵給每個下游技能。 |
| `/plan-ceo-review` | **CEO / 創辦人** | 重新思考問題。找出藏在需求裡的 10 星產品。四種模式：擴張、選擇性擴張、維持範圍、縮減。 |
| `/plan-eng-review` | **工程主管** | 鎖定架構、資料流、圖表、邊界情況與測試。把隱藏的假設逼到檯面上。 |
| `/plan-design-review` | **資深設計師** | 各設計維度評 0-10 分、說明 10 分長怎樣、然後改計畫去達成。AI Slop 偵測。互動式 — 每個設計選擇一個 AskUserQuestion。 |
| `/plan-devex-review` | **開發者體驗主管** | 互動式 DX 審查：探索開發者 persona、對標競品 TTHW、設計你的魔法時刻、逐步追蹤摩擦點。三種模式：DX 擴張、DX 打磨、DX 分流。20-45 個逼問。 |
| `/design-consultation` | **設計夥伴** | 從零打造完整設計系統。研究市場、提出有創意的風險、生成擬真產品 mockup。 |
| `/review` | **Staff 工程師** | 找出能過 CI、卻會在 production 爆掉的 bug。自動修明顯的。標出完整性缺口。 |
| `/investigate` | **除錯者** | 系統化根因除錯。鐵律：沒調查就不修。追蹤資料流、測試假設、3 次修正失敗就停。 |
| `/design-review` | **會寫 code 的設計師** | 跟 /plan-design-review 一樣的稽核，然後修掉發現的問題。原子 commit、前後對照截圖。 |
| `/devex-review` | **DX 測試者** | 即時開發者體驗稽核。真的去測你的上手流程：翻文件、試 getting started、計時 TTHW、把錯誤截圖。對照 `/plan-devex-review` 的評分 — 看計畫跟現實是否相符的迴力鏢。 |
| `/design-shotgun` | **設計探索者** | 「給我選項。」生成 4-6 個 AI mockup 變體、在瀏覽器開比較看板、收集你的回饋並迭代。品味記憶會學你喜歡什麼。重複到你愛上某個，再交給 `/design-html`。 |
| `/design-html` | **設計工程師** | 把 mockup 變成真的能用的 production HTML。Pretext 計算式排版：文字會 reflow、高度隨內容調整、版面是動態的。30KB、零相依。偵測 React/Svelte/Vue。依設計類型智慧 API routing（landing page vs dashboard vs form）。產出是可出貨的，不是 demo。 |
| `/qa` | **QA 主管** | 測你的 app、找 bug、用原子 commit 修掉、重新驗證。每個修正自動生成回歸測試。 |
| `/qa-only` | **QA 回報者** | 跟 /qa 一樣的方法論但只回報。純 bug report，不動 code。 |
| `/pair-agent` | **多 agent 協調者** | 把你的瀏覽器分享給任何 AI agent。一個指令、一次貼上、連上。支援 OpenClaw、Hermes、Codex、Cursor，或任何能 curl 的東西。每個 agent 有自己的分頁。自動 headed 模式讓你全程看著。自動為遠端 agent 啟 ngrok tunnel。scoped token、分頁隔離、限流、活動歸屬。 |
| `/cso` | **資安長** | OWASP Top 10 + STRIDE 威脅模型。零雜訊：17 條誤報排除、8/10+ 信心門檻、獨立 finding 驗證。每個 finding 都附具體的 exploit 情境。 |
| `/ship` | **發布工程師** | 同步 main、跑測試、稽核覆蓋率、push、開 PR。沒有測試框架的話幫你 bootstrap 一個。 |
| `/land-and-deploy` | **發布工程師** | 合併 PR、等 CI 與部署、驗證 production 健康。一個指令從「批准」到「production 已驗證」。 |
| `/canary` | **SRE** | 部署後監控迴圈。盯 console error、效能回歸、頁面失敗。 |
| `/benchmark` | **效能工程師** | 基準化頁面載入時間、Core Web Vitals、資源大小。每個 PR 比較前後。 |
| `/document-release` | **技術寫作者** | 更新所有專案文件以符合你剛出的貨。自動抓出過期的 README。建一張 Diataxis 覆蓋率地圖（reference / how-to / tutorial / explanation），讓缺口在 PR body 裡可見。 |
| `/document-generate` | **文件作者** | 用 Diataxis 框架從零生成缺的文件。先研究 codebase，再寫出真的符合程式碼的 reference / how-to / tutorial / explanation。可獨立呼叫，或在覆蓋率地圖發現缺口時由 `/document-release` 串接。了解更多：[tutorial](docs/tutorial-document-generate.md) • [how-to](docs/howto-document-a-shipped-feature.md) • [why Diataxis](docs/explanation-diataxis-in-gstack.md)。 |
| `/retro` | **工程主管** | 團隊感知的每週回顧。逐人拆解、出貨連勝、測試健康趨勢、成長機會。`/retro global` 橫跨你所有專案與 AI 工具（Claude Code、Codex、Gemini）。 |
| `/browse` | **QA 工程師** | 給 agent 一雙眼睛。真的 Chromium 瀏覽器、真的點擊、真的截圖。每個指令約 100ms。`/open-gstack-browser` 啟動帶 sidebar、反 bot stealth、自動模型 routing 的 GStack Browser。 |
| `/setup-browser-cookies` | **Session 管理者** | 從你真實的瀏覽器（Chrome、Arc、Brave、Edge）匯入 cookie 到 headless session。測試需登入的頁面。 |
| `/autoplan` | **審查 pipeline** | 一個指令，完整審查過的計畫。自動跑 CEO → 設計 → 工程審查，內建決策原則。只把需要品味判斷的決定丟給你批准。 |
| `/spec` | **Spec 作者** | 五階段把模糊意圖變成精確可執行的 spec（why、scope、含強制讀 code 的 technical、draft、file）。file 前有 Codex 品質門檻（低於 7/10 擋下）、fail-closed 機密 redaction、對既有 issue 去重、歸檔到 `$GSTACK_STATE_ROOT/projects/$SLUG/specs/` 供團隊語料回想。`--execute` 在全新 worktree spawn `claude -p`；`/ship` 在合併時自動關掉來源 issue。Plan-mode 感知。 |
| `/learn` | **記憶** | 管理 gstack 跨 session 學到的東西。檢視、搜尋、修剪、匯出專案專屬的模式、陷阱、偏好。learnings 跨 session 累積，所以 gstack 在你的 codebase 上會越來越聰明。 |

### 我該用哪個審查？

| 你在為...建造 | 計畫階段（寫 code 前） | 即時稽核（出貨後） |
|-----------------|--------------------------|----------------------------|
| **終端使用者**（UI、web app、mobile） | `/plan-design-review` | `/design-review` |
| **開發者**（API、CLI、SDK、docs） | `/plan-devex-review` | `/devex-review` |
| **架構**（資料流、效能、測試） | `/plan-eng-review` | `/review` |
| **以上全部** | `/autoplan`（跑 CEO → 設計 → 工程 → DX，自動偵測哪些適用） | — |

### 強力工具

| 技能 | 用途 |
|-------|-------------|
| `/codex` | **第二意見** — 來自 OpenAI Codex CLI 的獨立程式碼審查。三種模式：review（pass/fail 門檻）、對抗式挑戰、開放諮詢。當 `/review` 與 `/codex` 都跑過時做跨模型分析。 |
| `/careful` | **安全護欄** — 在破壞性指令前警告（rm -rf、DROP TABLE、force-push）。說「be careful」啟動。可覆蓋任何警告。 |
| `/freeze` | **編輯鎖** — 把檔案編輯限制在一個目錄。除錯時防止不小心改到範圍外。 |
| `/guard` | **完整安全** — `/careful` + `/freeze` 合一。production 工作的最高安全。 |
| `/unfreeze` | **解鎖** — 移除 `/freeze` 邊界。 |
| `/open-gstack-browser` | **GStack Browser** — 啟動帶 sidebar、反 bot stealth、自訂品牌、自動模型 routing（動作用 Sonnet、分析用 Opus）、一鍵 cookie 匯入、Claude Code 整合的 GStack Browser。清理頁面、智慧截圖、編輯 CSS、把資訊回傳給終端機。 |
| `/setup-deploy` | **部署設定器** — `/land-and-deploy` 的一次性設定。偵測你的平台、production URL、部署指令。 |
| `/setup-gbrain` | **GBrain 上手** — 5 分鐘內從零到 gbrain 運作。PGLite 本地、Supabase 既有 URL、或透過 Management API 自動 provision 新 Supabase 專案。為 Claude Code 註冊 MCP + 每 repo 信任三元（read-write/read-only/deny）。[完整指南](USING_GBRAIN_WITH_GSTACK.md)。 |
| `/sync-gbrain` | **讓 brain 跟上** — 透過 `gbrain sources add` + `gbrain sync --strategy code` 把此 repo 的程式碼重新索引進 gbrain、刷新 CLAUDE.md 的 `## GBrain Search Guidance` 段落、能力檢查失敗時自動移除指引。`--incremental`（預設）、`--full`、`--dry-run`。冪等；可安全重跑。 |
| `/gstack-upgrade` | **自我更新器** — 升級 gstack 到最新。偵測全域 vs vendor 安裝、兩者都同步、顯示改了什麼。 |
| `/ios-qa` | **iOS 真機 QA（v1.43.0.0+）** — 透過 app 內嵌的 `StateServer`，用 USB CoreDevice 驅動真 iPhone。讀 Swift 原始碼、codegen typed `@Observable` accessor、跑 agent 迴圈。可選 `--tailnet` flag 把裝置暴露給 Tailscale tailnet 上的 OpenClaw 或任何 HTTP agent，讓遠端 agent 不碰硬體也能跑 iOS QA。能力分級 allowlist（observe/interact/mutate/restore）、每裝置 session lock、audit log。 |
| `/ios-fix`、`/ios-design-review`、`/ios-clean`、`/ios-sync` | iOS bug 修復迴圈、設計師之眼 HIG 稽核、debug-bridge 清理、accessor 重新同步。見 `docs/skills.md`。端到端走查：[docs/howto-ios-testing-with-gstack.md](docs/howto-ios-testing-with-gstack.md)。 |

### 新 binary（v0.19）

除了斜線指令技能，gstack 還附了獨立 CLI，用於不屬於 session 內的工作流：

| 指令 | 用途 |
|---------|-------------|
| `gstack-model-benchmark` | **跨模型 benchmark** — 同一個 prompt 跑過 Claude、GPT（透過 Codex CLI）、Gemini；比較延遲、token、成本、（可選）LLM-judge 品質分數。各 provider 自動偵測 auth、不可用的乾淨跳過。輸出為 table、JSON 或 markdown。`--dry-run` 驗證 flag + auth 而不花 API 呼叫。 |
| `gstack-taste-update` | **設計品味學習** — 把 `/design-shotgun` 的批准與拒絕寫進持久的每專案品味檔。每週衰減 5%。回饋給未來的變體生成，讓系統學你實際會挑什麼。 |
| `gstack-ios-qa-daemon` | **iOS QA daemon** — Mac 端在 agent 與透過 USB CoreDevice 連接的 iPhone 之間的 broker。預設 loopback；`--tailnet` 開一個面向 Tailscale 的 listener，帶身分把關的能力分級。透過 `~/.gstack/ios-qa-daemon.pid` 的 flock 確保單一實例。見 [docs/howto-ios-testing-with-gstack.md](docs/howto-ios-testing-with-gstack.md)。 |
| `gstack-ios-qa-mint` | **iOS allowlist 管理器** — tailnet allowlist 的 owner-grant CLI。對 `~/.gstack/ios-qa-allowlist.json`（mode 0600）做 `grant`/`revoke`/`list`。遠端 agent 永不自動加 allowlist；這是明確意圖的路徑。 |

### 持續 checkpoint 模式（opt-in，預設本地）

設 `gstack-config set checkpoint_mode continuous`，技能就會邊做邊自動 commit 你的工作，帶 `WIP:` 前綴加結構化的 `[gstack-context]` body（決策、剩餘工作、失敗過的方法）。能撐過 crash 與情境切換。`/context-restore` 讀這些 commit 重建 session 狀態。`/ship` 在開 PR 前 filter-squash 掉 WIP commit（保留非 WIP commit），讓 bisect 保持乾淨。push 是 opt-in 的（`checkpoint_push=true`）— 預設只本地，這樣你不會每個 WIP commit 都觸發 CI。

### Domain 技能 + 原始 CDP 逃生口

兩個新的瀏覽器原語讓 gstack agent 隨時間複利：

- **`$B domain-skill save`** — agent 存一個每站筆記（例如「LinkedIn 的 Apply 按鈕在 iframe 裡」），下次造訪那個 hostname 時自動觸發。隔離中 → 3 次成功使用後轉 active → 可選透過 `$B domain-skill promote-to-global` 跨專案晉升。儲存與 `/learn` 的每專案 learnings 檔放在一起。完整參考：**[docs/domain-skills.md](docs/domain-skills.md)**。
- **`$B cdp <Domain.method>`** — 原始 Chrome DevTools Protocol 逃生口，給罕見的 curated 指令漏掉的情況。預設拒絕：method 必須明確加進 `browse/src/cdp-allowlist.ts` 並附一行理由。雙層 mutex 把瀏覽器層級的 CDP 呼叫對每分頁工作序列化。資料外洩類 method 的輸出包在 UNTRUSTED 信封裡。

> 想要完全沒護欄、沒 allowlist、沒 daemon 的原始 CDP — 只要 agent 到 Chrome 的薄傳輸？[browser-use/browser-harness-js](https://github.com/browser-use/browser-harness-js) 是不同哲學（agent 自寫 helper vs gstack 的 curated 指令），如果你不想要 gstack 的安全堆疊，它是好選擇。兩者可共存：gstack 的 `$B cdp` 與 harness 都能透過 Playwright 的 `newCDPSession` attach 到同一個 Chrome。

**[每個技能的深入剖析、範例與哲學 →](docs/skills.md)**

### Karpathy 的四種失敗模式？已經涵蓋。

Andrej Karpathy 的 [AI coding rules](https://github.com/forrestchang/andrej-karpathy-skills)（17K stars）點出四種失敗模式：錯誤假設、過度複雜、正交編輯、命令式而非宣告式。gstack 的工作流技能四個全管。`/office-hours` 在寫 code 前就把假設逼到檯面。Confusion Protocol 阻止 Claude 在架構決策上瞎猜。`/review` 抓不必要的複雜與順手亂改。`/ship` 把任務變成可驗證的目標、測試先行執行。如果你已經用 Karpathy 風格的 CLAUDE.md 規則，gstack 就是讓它們橫跨整場 sprint 都生效的工作流強制層，而不只是單個 prompt。

## 平行 sprint

gstack 一場 sprint 就很好用。同時跑十場才有趣。

**設計是核心。** `/design-consultation` 從零打造你的設計系統、研究市場上有什麼、提出有創意的風險、寫出 `DESIGN.md`。但真正的魔法是 shotgun-to-HTML 這條 pipeline。

**`/design-shotgun` 是你探索的方式。** 你描述你要的。它用 GPT Image 生成 4-6 個 AI mockup 變體。然後在你瀏覽器開一個比較看板，所有變體並排。你挑最愛、留回饋（「多點留白」、「標題大膽點」、「拿掉漸層」），它生成新一輪。重複到你愛上某個。幾輪後品味記憶啟動，開始偏向你實際喜歡的。不用再用文字描述願景然後祈禱 AI 懂。你看選項、挑好的、視覺化迭代。

**`/design-html` 讓它成真。** 拿那個批准的 mockup（來自 `/design-shotgun`、CEO 計畫、設計審查、或只是一段描述）變成 production 品質的 HTML/CSS。不是那種在一個 viewport 寬度看起來還好、其他全爆的 AI HTML。這用 Pretext 做計算式文字排版：文字真的會在 resize 時 reflow、高度隨內容調整、版面是動態的。30KB 額外開銷、零相依。它偵測你的框架（React、Svelte、Vue）輸出對的格式。智慧 API routing 依 landing page、dashboard、form 或 card 版面挑不同的 Pretext 模式。產出是你真的會出貨的，不是 demo。

**`/qa` 是巨大的解鎖。** 它讓我從 6 個平行 worker 上到 12 個。Claude Code 說 *「我看到問題了」* 然後真的修好它、生成回歸測試、驗證修正 — 那改變了我工作的方式。agent 現在有眼睛了。

**智慧審查 routing。** 就像在一家運作良好的新創：CEO 不必看 infra bug 修正、後端改動不需要設計審查。gstack 追蹤跑了哪些審查、判斷什麼適合、然後就做對的事。Review Readiness Dashboard 在你出貨前告訴你站在哪。

**測試一切。** 如果你的專案沒有測試框架，`/ship` 從零幫你 bootstrap。每次 `/ship` 都產出覆蓋率稽核。每個 `/qa` bug 修正都生成回歸測試。100% 測試覆蓋是目標 — 測試讓 vibe coding 變安全而非 yolo coding。

**`/document-release` 是你從未有過的工程師。** 它讀你專案裡每個文件檔、交叉比對 diff、更新所有漂移的東西。README、ARCHITECTURE、CONTRIBUTING、CLAUDE.md、TODOS — 全自動保持最新。而且現在 `/ship` 會自動呼叫它 — 文件不用額外指令就保持最新。

**真瀏覽器模式。** `/open-gstack-browser` 啟動 GStack Browser，一個 AI 控制、帶反 bot stealth、自訂品牌、內建 sidebar 擴充的 Chromium。Google、NYTimes 這類網站不會被 captcha 擋。選單列寫「GStack Browser」而非「Chrome for Testing」。你平常的 Chrome 完全不受影響。所有現有 browse 指令照常運作。`$B disconnect` 回到 headless。只要視窗開著瀏覽器就活著... 不會在你工作時被閒置逾時殺掉。

**Sidebar agent — 你的 AI 瀏覽器助手。** 在 Chrome side panel 打自然語言，一個子 Claude 實例執行它。「導航到設定頁並截圖。」「用測試資料填這個表單。」「走過這個清單每個項目並抽出價格。」sidebar 自動 route 到對的模型：快動作（點擊、導航、截圖）用 Sonnet，閱讀與分析用 Opus。每個任務最多 5 分鐘。sidebar agent 跑在隔離 session，不會干擾你的主 Claude Code 視窗。從 sidebar footer 一鍵 cookie 匯入。

**個人自動化。** sidebar agent 不只給 dev 工作流用。例如：「逛我小孩學校的家長 portal，把其他家長的名字、電話、照片都加到我的 Google Contacts。」兩種驗證方式：(1) 在 headed 瀏覽器登入一次，session 會持續，或 (2) 點 sidebar footer 的「cookies」按鈕從你真實的 Chrome 匯入 cookie。驗證後 Claude 導航目錄、抽資料、建立聯絡人。

**Prompt injection 防禦。** 惡意網頁試圖綁架你的 sidebar agent。gstack 附了分層防禦：一個與瀏覽器打包的 22MB ML 分類器在本地掃描每個頁面與工具輸出、一個 Claude Haiku transcript 檢查對整段對話形狀投票、system prompt 裡一個隨機 canary token 抓跨文字/工具參數/URL/檔案寫入的 session 外洩、一個 verdict combiner 要求兩個分類器同意才 block（防止在 Stack Overflow 式指令頁上的單模型誤報）。sidebar header 的盾牌圖示顯示狀態（綠/琥珀/紅）。透過 `GSTACK_SECURITY_ENSEMBLE=deberta` opt in 721MB DeBERTa-v3 ensemble 做 2-of-3 同意。緊急 kill switch：`GSTACK_SECURITY_OFF=1`。完整堆疊見 [ARCHITECTURE.md](ARCHITECTURE.md#prompt-injection-defense-sidebar-agent)。

**AI 卡住時的瀏覽器交接。** 撞到 CAPTCHA、auth wall 或 MFA？`$B handoff` 在完全相同的頁面開一個可見的 Chrome，你的 cookie 與分頁全部完好。解決問題、跟 Claude 說你好了、`$B resume` 從剛剛離開的地方接回去。連續 3 次失敗後 agent 甚至會自動建議這麼做。

**`/pair-agent` 是跨 agent 協調。** 你在 Claude Code。你同時也跑著 OpenClaw。或 Hermes。或 Codex。你想讓它們都看同一個網站。打 `/pair-agent`、選你的 agent、一個 GStack Browser 視窗打開讓你看。技能印出一段指令。把那段貼進另一個 agent 的 chat。它用一次性 setup key 換 session token、建自己的分頁、開始瀏覽。你看到兩個 agent 在同一個瀏覽器工作、各在自己分頁、誰也不能干擾誰。裝了 ngrok 的話 tunnel 自動啟動，所以另一個 agent 可以在完全不同的機器上。同機 agent 有零摩擦捷徑直接寫憑證。這是不同廠商的 AI agent 第一次能透過共享瀏覽器協調、且有真正的安全：scoped token、分頁隔離、限流、網域限制、活動歸屬。

**多 AI 第二意見。** `/codex` 從 OpenAI 的 Codex CLI 取得獨立審查 — 一個完全不同的 AI 看同一個 diff。三種模式：帶 pass/fail 門檻的程式碼審查、主動試圖弄壞你 code 的對抗式挑戰、帶 session 連續性的開放諮詢。當 `/review`（Claude）與 `/codex`（OpenAI）都審過同一分支，你會得到跨模型分析，顯示哪些 finding 重疊、哪些各自獨有。

**隨需安全護欄。** 說「be careful」，`/careful` 就在任何破壞性指令前警告 — rm -rf、DROP TABLE、force-push、git reset --hard。`/freeze` 在除錯時把編輯鎖到一個目錄，這樣 Claude 不會不小心「修」到無關的 code。`/guard` 兩個都啟動。`/investigate` 會自動 freeze 到正在調查的模組。

**主動技能建議。** gstack 會注意你在哪個階段 — 腦力激盪、審查、除錯、測試 — 並建議對的技能。不喜歡？說「stop suggesting」，它會跨 session 記住。

## 10-15 場平行 sprint

gstack 一場 sprint 就很強。同時跑十場是質變。

[Conductor](https://conductor.build) 平行跑多個 Claude Code session — 每個在自己隔離的 workspace。一個 session 對新想法跑 `/office-hours`、另一個對 PR 做 `/review`、第三個實作功能、第四個對 staging 跑 `/qa`，還有六個在其他分支。全部同時。我常態跑 10-15 場平行 sprint — 那是目前實務上的上限。

sprint 結構是平行能運作的關鍵。沒有流程，十個 agent 是十個混亂源。有流程 — 想、規劃、建造、審查、測試、出貨 — 每個 agent 都確切知道做什麼、何時停。你像 CEO 管團隊那樣管它們：盯重要的決定、其餘讓它跑。

### 語音輸入（AquaVoice、Whisper 等）

gstack 技能有語音友善的觸發詞。自然地說出你要的 — 「跑個安全檢查」、「測這個網站」、「做工程審查」 — 對的技能就啟動。你不用記斜線指令名或縮寫。

## 解除安裝

### 選項 1：跑解除安裝腳本

如果 gstack 裝在你的機器上：

```bash
~/.claude/skills/gstack/bin/gstack-uninstall
```

這會處理技能、symlink、全域狀態（`~/.gstack/`）、專案本地狀態、browse daemon、暫存檔。用 `--keep-state` 保留設定與 analytics。用 `--force` 跳過確認。

### 選項 2：手動移除（沒有本地 repo）

如果你沒有 clone repo（例如你透過 Claude Code 貼上安裝、之後刪了 clone）：

```bash
# 1. Stop browse daemons
pkill -f "gstack.*browse" 2>/dev/null || true

# 2. Remove per-skill directories whose SKILL.md points into gstack/
find ~/.claude/skills -mindepth 1 -maxdepth 1 -type d ! -name gstack 2>/dev/null |
while IFS= read -r dir; do
  link="$dir/SKILL.md"
  [ -L "$link" ] || continue
  target=$(readlink "$link" 2>/dev/null) || continue
  case "$target" in
    gstack/*|*/gstack/*)
      rm -f "$link"
      rmdir "$dir" 2>/dev/null || true
      ;;
  esac
done

# 3. Remove gstack
rm -rf ~/.claude/skills/gstack

# 4. Remove global state
rm -rf ~/.gstack

# 5. Remove integrations (skip any you never installed)
rm -rf ~/.codex/skills/gstack* 2>/dev/null
rm -rf ~/.factory/skills/gstack* 2>/dev/null
rm -rf ~/.kiro/skills/gstack* 2>/dev/null
rm -rf ~/.openclaw/skills/gstack* 2>/dev/null

# 6. Remove temp files
rm -f /tmp/gstack-* 2>/dev/null

# 7. Per-project cleanup (run from each project root)
rm -rf .gstack .gstack-worktrees .claude/skills/gstack 2>/dev/null
rm -rf .agents/skills/gstack* .factory/skills/gstack* 2>/dev/null
```

### 清理 CLAUDE.md

解除安裝腳本不會編輯 CLAUDE.md。在每個加過 gstack 的專案，移除 `## gstack` 與 `## Skill routing` 段落。

### Playwright

`~/Library/Caches/ms-playwright/`（macOS）會留著，因為其他工具可能共用它。如果沒別的需要就移除它。

---

免費、MIT 授權、開源。沒有付費方案、沒有候補名單。

我把我建造軟體的方式開源了。你可以 fork 它、讓它變成你自己的。

> **我們在徵才。** 想以 AI coding 的速度出真產品、並幫忙加固 gstack？
> 來 YC 工作 — [ycombinator.com/software](https://ycombinator.com/software)
> 極具競爭力的薪資與股權。舊金山 Dogpatch 區。

## GBrain — 給你 coding agent 的持久知識

[GBrain](https://github.com/garrytan/gbrain) 是 AI agent 的持久知識庫 — 把它想成你 agent 真的會在 session 之間保留的記憶。GStack 給你一條從零到「它在跑了，我的 agent 能呼叫它」的單指令路徑。

```bash
/setup-gbrain
```

四條路徑，挑一條：

- **Supabase，既有 URL** — 你的雲端 agent 已經 provision 了一個 brain；貼上 Session Pooler URL，現在這台筆電用同一份資料。
- **Supabase，自動 provision** — 貼上 Supabase Personal Access Token；技能建一個新專案、polling 到健康、抓 pooler URL、交給 `gbrain init`。端到端約 90 秒。
- **PGLite 本地** — 零帳號、零網路、約 30 秒。只在這台 Mac 上的隔離 brain。適合先試；之後用 `/setup-gbrain --switch` 遷移到 Supabase。
- **遠端 gbrain MCP** — 你的 brain 跑在另一台機器（Tailscale、ngrok、內網）或隊友的伺服器；貼上 MCP URL 與 bearer token。可選搭配本地 PGLite 在 split-engine 模式做 symbol 感知的程式碼搜尋。最適合不架本地 DB 的跨機器記憶。

init 後，技能會提議把 gbrain 註冊為 Claude Code 的 MCP server（`claude mcp add gbrain -- gbrain serve`），這樣 `gbrain search`、`gbrain put` 等就以一級 typed 工具出現 — 不是 bash shell-out。

**讓 brain 保持最新。** 從任何 repo 跑 `/sync-gbrain` 把它的程式碼重新索引進 gbrain（預設 incremental、`--full` 全重索引、`--dry-run` 預覽）。技能透過 `gbrain sources add` 把 cwd 註冊為 federated source、跑 `gbrain sync --strategy code`、並寫一個 `## GBrain Search Guidance` 段落到你專案的 CLAUDE.md，讓 agent 偏好 `gbrain search`/`code-def`/`code-refs` 而非 Grep。能力檢查失敗時段落自動移除 — 不會留指向沒裝工具的過期指引。

**每 remote 信任政策。** 你機器上每個 repo 拿到三層之一：

- `read-write` — agent 能搜 brain 且能從此 repo 寫新頁面回去
- `read-only` — agent 能搜但永不寫（最適合多客戶顧問：搜共享 brain、不在客戶 B 的 repo 裡用客戶 A 的工作污染它）
- `deny` — 完全不與 gbrain 互動

技能每 repo 問一次。決定在同一 remote 的各 worktree 與分支間黏著。

**GStack 記憶同步（不同功能，同一私有 repo 基礎設施）。** 可選把你的 gstack 狀態（learnings、CEO 計畫、設計文件、retro、開發者 profile）push 到私有 git repo，讓你的記憶跨機器跟著你，帶一次性隱私提示（全部 allowlist / 只 artifacts / off）與一個 defense-in-depth 機密掃描器，在 AWS key、token、PEM block、JWT 離開你機器前擋下。

```bash
gstack-brain-init
```

**在 Conductor 裡跑 gstack？** Conductor 明確從每個 workspace 的 process env 剝掉 `ANTHROPIC_API_KEY` 與 `OPENAI_API_KEY`，所以付費 eval 與 gbrain embedding 預設不會動。改在 Conductor 的 workspace env 設定裡設 `GSTACK_ANTHROPIC_API_KEY` 與 `GSTACK_OPENAI_API_KEY` — gstack 的 TS 進入點在 runtime 把它們提升為標準名稱。完整細節與為新進入點加 import 的貢獻者清單：[Conductor + GSTACK_* env vars](USING_GBRAIN_WITH_GSTACK.md#conductor--gstack_-env-vars)。

**完整版 — 每個情境、每個 flag、每個 bin helper、每個排錯步驟：** [USING_GBRAIN_WITH_GSTACK.md](USING_GBRAIN_WITH_GSTACK.md)

其他參考：[docs/gbrain-sync.md](docs/gbrain-sync.md)（sync 專屬指南） • [docs/gbrain-sync-errors.md](docs/gbrain-sync-errors.md)（錯誤索引）

## 文件

**繁體中文文件（社群維護，新增檔案，不影響上游合併）：**

| 文件 | 內容 |
|------|------|
| [專案架構](docs/zh-TW/專案架構.md) | gstack 的三層構成、`.tmpl → SKILL.md` 生成管線、各目錄職責 |
| [開發指南](docs/zh-TW/開發指南.md) | 常用指令、修改技能的工作流、測試分層、commit 規範 |
| [技能總覽](docs/zh-TW/技能總覽.md) | 上半「開發場景 → 該用哪個 skill」對照表，下半全技能依角色分類逐一中文解說 |

**英文文件：**

| Doc | 涵蓋內容 |
|-----|---------------|
| [Skill Deep Dives](docs/skills.md) | 每個技能的哲學、範例與工作流（含 Greptile 整合） |
| [Builder Ethos](ETHOS.md) | 建造哲學：Boil the Lake、Search Before Building、三層知識 |
| [Using GBrain with GStack](USING_GBRAIN_WITH_GSTACK.md) | `/setup-gbrain` 的每條路徑、flag、bin helper 與排錯 |
| [GBrain Sync](docs/gbrain-sync.md) | 跨機器記憶設定、隱私模式、排錯 |
| [Architecture](ARCHITECTURE.md) | 設計決策與系統內部 |
| [Browser Reference](BROWSER.md) | `/browse` 的完整指令參考 |
| [Contributing](CONTRIBUTING.md) | 開發設定、測試、contributor 模式、dev 模式 |
| [Changelog](CHANGELOG.md) | 每個版本的新內容 |

## 隱私與遙測

gstack 包含 **opt-in（預設關閉）** 的使用遙測來幫助改進專案。確切會發生什麼：

- **預設關閉。** 除非你明確說好，否則什麼都不會傳到任何地方。
- **第一次跑時**，gstack 問你要不要分享匿名使用資料。你可以說不。
- **會傳什麼（如果你 opt in）：** 技能名稱、時長、成功/失敗、gstack 版本、OS。就這些。
- **永遠不會傳什麼：** 程式碼、檔案路徑、repo 名稱、分支名稱、prompt、或任何使用者產生的內容。
- **隨時改：** `gstack-config set telemetry off` 立刻關掉一切。

資料存在 [Supabase](https://supabase.com)（開源的 Firebase 替代品）。schema 在 [`supabase/migrations/`](supabase/migrations/) — 你可以確切驗證收集了什麼。repo 裡的 Supabase publishable key 是公開 key（像 Firebase API key）— row-level security 政策拒絕所有直接存取。遙測經過驗證的 edge function 流動，強制 schema 檢查、event type allowlist、欄位長度限制。

**本地 analytics 永遠可用。** 跑 `gstack-analytics` 從本地 JSONL 檔看你個人的使用 dashboard — 不需要遠端資料。

## 排錯

**技能沒出現？** `cd ~/.claude/skills/gstack && ./setup`

**`/browse` 失敗？** `cd ~/.claude/skills/gstack && bun install && bun run build`

**安裝過期？** 跑 `/gstack-upgrade` — 或在 `~/.gstack/config.yaml` 設 `auto_upgrade: true`

**想要更短的指令？** `cd ~/.claude/skills/gstack && ./setup --no-prefix` — 從 `/gstack-qa` 切到 `/qa`。你的選擇會被記住供未來升級用。

**想要 namespace 的指令？** `cd ~/.claude/skills/gstack && ./setup --prefix` — 從 `/qa` 切到 `/gstack-qa`。如果你跟 gstack 一起跑其他 skill pack 會有用。

**Codex 說「Skipped loading skill(s) due to invalid SKILL.md」？** 你的 Codex 技能描述過期了。修法：`cd ~/.codex/skills/gstack && git pull && ./setup --host codex` — 或 repo 本地安裝：`cd "$(readlink -f .agents/skills/gstack)" && git pull && ./setup --host codex`

**Windows 使用者：** gstack 透過 Git Bash 或 WSL 在 Windows 11 上運作。除了 Bun 還需要 Node.js — Bun 在 Windows 上對 Playwright 的 pipe transport 有已知 bug（[bun#4253](https://github.com/oven-sh/bun/issues/4253)）。browse server 會自動 fallback 到 Node.js。確保 `bun` 與 `node` 都在你的 PATH 上。

在沒有 Developer Mode 的 Windows（MSYS2 / Git Bash），`setup` 會 fallback 成檔案複製而非 symlink，因為 `ln -snf` 會產生不會在 `git pull` 時刷新的凍結副本。**每次 `git pull` 後重跑 `cd ~/.claude/skills/gstack && ./setup`**，讓你的技能檔與 repo 一致。`setup` 會印一行提醒。Unix 與 WSL 保留 symlink，不需要重跑。

**Claude 說它看不到技能？** 確保你專案的 `CLAUDE.md` 有 gstack 段落。加上這個：

```
## gstack
Use /browse from gstack for all web browsing. Never use mcp__claude-in-chrome__* tools.
Available skills: /office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review,
/design-consultation, /design-shotgun, /design-html, /review, /ship, /land-and-deploy,
/canary, /benchmark, /browse, /open-gstack-browser, /qa, /qa-only, /design-review,
/setup-browser-cookies, /setup-deploy, /setup-gbrain, /sync-gbrain, /retro, /investigate,
/document-release, /document-generate, /codex, /cso, /autoplan, /pair-agent, /careful, /freeze,
/guard, /unfreeze, /gstack-upgrade, /learn.
```

## 授權

MIT。永久免費。去建點東西吧。
