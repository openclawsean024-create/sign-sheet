# CHANGELOG · sign-sheet

> 規格書版本演進：v1.0 → v3.0 (sweet-spot rewrite) → v3.0.2 (fleet hardening)
> 完整規格書見 [`PRD/SPEC.md`](./SPEC.md)

---

## v3.0.2 · 2026-09-07 · fleet hardening (Batch 8B)

**Patch 性質**：純部署面 / CI 面 hardening，不變更產品 spec。

### Added
- `PRD/CHANGELOG.md` — 本檔案（v1.0 / v3.0 / v3.0.2 變更日誌）
- `.github/workflows/ci.yml` — 4-job CI（lint / test / build / deploy to GitHub Pages）

### Changed
- `PRD/SPEC.md` — 頂端新增 v3.0.2 patch header（**既有 v3.0 sweet-spot rewrite v2 的產品 spec 全部保留**，§1–§18 不變）
- 部署契約：補上 GitHub Pages deploy job（`actions/deploy-pages@v4` + `upload-pages-artifact@v3`）
- 觸發條件：`push to main` + `pull_request` + `workflow_dispatch`

### Validation
- `dashboard.html` 14 KB 純靜態 — mint 主題 + Tailwind CDN + localStorage 持久化
- 內部連結 / 外部連結：0 失效
- Pages 部署目標：靜態檔案直接 publish，無需 build step
- 觸發分支：`main`

### Risk
- 預設分支若改為 `master`，需更新 `ci.yml` 觸發條件為 `[main, master]`
- 部署後若 Vercel 仍存活，Pages 與 Vercel 雙軌並行（不衝突，URL 各自獨立）

---

## v3.0 · 2026-07-19 · sweet-spot rewrite v2 (Group D)

**重大改寫**：從「台灣中小企業 200 萬家企業電子簽名」改為「**微型店家 30 萬家 + LINE 整合電子簽單**」。

### 變更動機
- DocuSign 在台灣已是企業默認選項，轉換成本高
- Hitrust 鎖定政府 / 金融，SMB 市場反而是 DocuSign 滲透較低的 niche
- 台灣市場天花板低：2300 萬人口，企業 < 200 萬家
- 電子簽章需通過台灣認證（TAICS 等），合規成本高
- PDF 編輯 + 簽名 field 處理是 commodity 技術，差異化難做

### 甜蜜點
- **目標客層**：5-20 人微型店家（出貨單/維修單/服務單）
- **價格甜蜜點**：NT$299/月（vs DocuSign NT$800-3,000/月）
- **LINE 整合**：30 萬微型店家已有 LINE 官方帳號，0 學習成本

### 規格書內容
- §1 產品概述（問題陳述 / 目標使用者 / 核心價值主張 / Non-Goals）
- §2 使用者場景與流程
- §3 功能需求
- §4 Non-Functional Requirements
- §5 技術架構
- §6 Definition of Done
- §7 部署契約
- §8 Out of Scope
- §9-§18 細節（行銷 / 變現 / 風險 / 踩坑記錄 / 路線圖）

---

## v1.0 · 2026-05-15 · initial spec

初版規格書（企業電子簽名定位）：
- 目標：台灣中小企業 200 萬家
- 痛點：紙本簽單流轉耗時 / 倉儲管理困難 / 追蹤不易
- 解決方案：雲端電子簽名 + LINE 通知 + 後台管理
- 變現：NT$499-2,999/月

### 結果
- Sweet Spot 體檢 3/10：紅海中的紅海（DocuSign 已是台灣企業默認）
- v3.0 改寫為「微型店家 + LINE 整合」甜蜜點
