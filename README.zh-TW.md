# gstack（繁體中文導讀）

> 這是社群維護的繁體中文文件，幫助中文開發者快速理解 gstack。
> 內容為**新增檔案**，不修改任何上游原始檔，因此能安全地與 [garrytan/gstack](https://github.com/garrytan/gstack) 的更新合併。
> 權威來源仍是英文版 [`README.md`](README.md)；若有出入，以英文版為準。

---

## gstack 是什麼

gstack 把 **Claude Code 變成一支虛擬工程團隊**。它不是一個程式，而是一組 **slash command（斜線指令）技能**，每個技能扮演一種專家角色：

- 重新思考產品的 **CEO**（`/office-hours`、`/plan-ceo-review`）
- 鎖定架構的 **工程主管**（`/plan-eng-review`）
- 抓 AI 設計毛病的 **設計師**（`/design-review`、`/design-consultation`）
- 找出上線後才爆的 bug 的 **程式碼審查者**（`/review`）
- 真的開一個瀏覽器來測的 **QA**（`/qa`、`/browse`）
- 跑 OWASP + STRIDE 稽核的 **資安長**（`/cso`）
- 幫你開 PR、出版本的 **發布工程師**（`/ship`、`/land-and-deploy`）

全部是 Markdown、全部免費、MIT 授權。作者是 Y Combinator 的總裁暨執行長 Garry Tan，這是他每天在用的開源「軟體工廠」。

## 適合誰

- **創辦人 / CEO** — 尤其是還想自己出貨的技術型創辦人
- **第一次用 Claude Code 的人** — 用結構化角色取代一張白紙的提示
- **技術主管 / staff 工程師** — 每個 PR 都有嚴謹的審查、QA、發布自動化

---

## 快速開始

1. 安裝 gstack（約 30 秒，見下方）
2. 跑 `/office-hours` — 描述你想做的東西
3. 對任何功能想法跑 `/plan-ceo-review`
4. 對任何有改動的分支跑 `/review`
5. 對你的 staging URL 跑 `/qa`
6. 到這裡就好。你會知道這套適不適合你。

## 安裝

**需求：** [Claude Code](https://docs.anthropic.com/en/docs/claude-code)、[Git](https://git-scm.com/)、[Bun](https://bun.sh/) v1.0+、[Node.js](https://nodejs.org/)（僅 Windows 需要）

### 步驟 1：安裝到你的機器

打開 Claude Code，貼上這段，其餘交給 Claude：

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack \
  && cd ~/.claude/skills/gstack && ./setup
```

`./setup` 會：編譯瀏覽器 binary、把所有技能 symlink 進 `~/.claude/skills/`、依你選的 host（Claude Code / Codex…）註冊技能。

### 步驟 2：團隊模式（共用 repo 推薦）

在你的 repo 裡執行，讓隊友自動取得 gstack、無需手動升級：

```bash
(cd ~/.claude/skills/gstack && ./setup --team) \
  && ~/.claude/skills/gstack/bin/gstack-team-init required \
  && git add .claude/ CLAUDE.md && git commit -m "require gstack for AI-assisted work"
```

把 `required` 換成 `optional` 就從「強制」變成「提示」。

> ⚠️ **不要再把 gstack vendor（複製）進專案 repo**。請用「全域安裝 + `./setup --team`」。詳見英文 README 的 team mode 說明。

---

## 想更深入了解專案？

| 文件 | 內容 |
|------|------|
| [`docs/zh/專案架構.md`](docs/zh/專案架構.md) | gstack 由哪三層組成、生成管線怎麼運作、各目錄的職責 |
| [`docs/zh/開發指南.md`](docs/zh/開發指南.md) | 常用指令、`.tmpl → SKILL.md` 工作流、測試分層、貢獻注意事項 |

英文深入文件：
- [`ARCHITECTURE.md`](ARCHITECTURE.md) — 系統架構（瀏覽器 server、安全分層）
- [`BROWSER.md`](BROWSER.md) — `browse` binary 完整說明
- [`ETHOS.md`](ETHOS.md) — 「Boil the Lake」建造哲學
- [`CONTRIBUTING.md`](CONTRIBUTING.md) — 貢獻流程

---

## 授權

MIT。Fork 它、改進它、讓它變成你的。
