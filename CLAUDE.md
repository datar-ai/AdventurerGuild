# CLAUDE.md

此檔案為 Claude Code (claude.ai/code) 在本儲存庫工作時的最新統一指引（已同步至目前實際檔案與資料內容）。

## 重要提醒
- 所有溝通、文件、描述一律使用繁體中文（技術術語或必要格式英文字除外）
- 保持角色/團隊/技能敘述的一致性與系統性
- 修改前先閱讀：`agent list.md`、`Adventurer Guild Role List.md`、`AGENT_FORMAT_GUIDE.md`

## 儲存庫現況（2025-09 更新）
目前實際存在的檔案結構（尚未建立 subagents 與 team-leaders 專屬目錄）：
```
AdventurerGuild/
├── .gitignore
├── Adventurer Guild Role List.md      # 知識庫：設計職能與技能表（多領域技能矩陣）
├── agent list.md                      # 全部 17 個團隊與 108 個成員清單（權威來源）
├── AGENT_FORMAT_GUIDE.md              # Subagent（子代理）格式標準與模板
├── CLAUDE.md                          # 本操作指引
└── profile/
    └── 個人概況.md                    # 公會長嘉彤（所有代理本體）個人基本資料
```
尚未出現但在規劃中的目錄（建立後應遵循本文件與 `AGENT_FORMAT_GUIDE.md`）：
```
.claude/agents/         # 子代理 YAML frontmatter 驅動配置檔（未建立）
```

## 核心概念
- 全部 AI Agent / 團隊成員皆為「公會長嘉彤」的 AI 分身
- `agent list.md` 是「團隊 → 成員 → 職位/專長」的唯一權威清單
- `Adventurer Guild Role List.md` 是「職能/技能標準」的共用知識底層
- Subagent 檔案（尚未實作）將以「任務分流 + 精準角色行為約束」為目的

## 團隊總覽（來自 agent list.md）
- 總團隊數：17
- 總成員數：108
- 目前定義團隊（依檔案順序）：  
  1. 網頁設計（Web）  
  2. VR/AR 技術（VR）  
  3. 書籍設計（Book）  
  4. 攝影（Photo）  
  5. 平面設計（Iris）  
  6. 作品分析（Anna）  
  7. 包裝設計（Pack）  
  8. 展場設計（Ex）  
  9. 設計議題（Issue）  
  10. 競賽策略（Red）  
  11. 創意思考（Creative）  
  12. 粒子特效（Particle）  
  13. 印刷工藝（Print）  
  14. 字體設計（Type）  
  15. 文創設計（Create）  
  16. 品牌識別（Logo）  
  17. IP 設計（IP）  

注意：舊版描述中的「3D（崔迪）」目前未在 `agent list.md` 列出，若需恢復須：
1. 補入 `agent list.md`
2. 對應新增技能組（如 3D 建模 / 渲染 / 材質）
3. 建立其團隊結構與角色職位

## 主要檔案用途
| 檔案 | 角色 |
|------|------|
| agent list.md | 實際團隊與成員主列表（權威狀態源） |
| Adventurer Guild Role List.md | 跨領域技能標準與參考來源（矩陣式知識庫） |
| AGENT_FORMAT_GUIDE.md | Subagent（YAML + 正文）結構規格 |
| profile/個人概況.md | 所有代理人格基底（身份一致性） |
| CLAUDE.md | 操作作業流程與協作規則 |

## 建議作業流程（增修任務類型）

### 1. 新增或調整團隊/成員
1. 編修 `agent list.md`
2. 若同時影響技能矩陣，更新 `Adventurer Guild Role List.md`
3. 建立/更新對應 subagent（待 `.claude/agents/` 建立）
4. 執行格式檢查（見下方「品質檢查」）

### 2. 建立 Subagent 配置（未來）
依 `AGENT_FORMAT_GUIDE.md`：
- 檔名：`{team}-{role}.md`
- Frontmatter：`name / description (/ tools / model)`
- 正文：依 Team Leader 或 Team Member 模板
- 語氣：專業、精準、無多餘寒暄
- 口頭禪與人格需與 `agent list.md` 一致

### 3. 維護技能知識庫
- 僅在已有技能分類下增補 → 直接插入一列  
- 新增分類 → 確保 3+ 代表性職能＋ 2~3 參考來源  
- 引用來源優先：標準 / 經典專書 / 官方指南 / 年鑑 / 實務標準

### 4. 對齊人格與口頭禪
- 若成員口頭禪在 subagent 配置中調整，需回寫 `agent list.md`
- 禁止出現互相矛盾（例如一個角色兩種完全不同定位）

### 5. 缺失角色補建
- 侷限：不可直接「想像新增」超出現有世界觀的職能
- 需要新增時：先在 `Adventurer Guild Role List.md` 建立技能依據，再補入 `agent list.md`

## Subagent 樣式速覽（簡化版）
（完整詳見 `AGENT_FORMAT_GUIDE.md`）

Team Leader：
```yaml
---
name: web-team-leader
description: 當需要統籌網頁設計策略與跨職能協調時使用此代理。擅長使用者體驗統整、無障礙規劃與效能策略。範例：<example>情境：需要同時檢視 IA、SEO 與可用性。user: "請幫我規劃新版官網資訊架構" assistant: "我會啟用 web-team-leader 進行多維評估" <commentary>涉及跨領域整合。</commentary></example>
tools: *
model: sonnet
---
你是……
```

Team Member：
```yaml
---
name: web-accessibility-specialist
description: 當需要審查或優化網站無障礙（WCAG）時使用此代理。擅長對比檢測、替代文字策略與可導航結構。範例：<example>情境：頁面改版需提升 A11y。user: "這頁是否符合 WCAG AA" assistant: "我會啟用 web-accessibility-specialist 做條目檢測" <commentary>需逐條檢查。</commentary></example>
model: sonnet
---
你是……
```

## 命名與一致性規則
| 項目 | 規則 | 例 |
|------|------|----|
| 檔名 | 全小寫 + `-` 分隔 | `issue-critic-commentator.md` |
| name | 與檔名一致 | `issue-critic-commentator` |
| 中文職位 | 不加「師」與「專家」之外的裝飾詞（保持職能精準） | 「無障礙設計專家」OK |
| 口頭禪 | 必填，置於正文結尾（Team Member）或指定區塊（Leader） | 「設計需要深度思考」 |

## 品質檢查（提交前）
- 角色是否存在於 `agent list.md`
- 技能描述是否可在 `Adventurer Guild Role List.md` 找到對應（或已補上）
- Frontmatter 欄位順序符合 `AGENT_FORMAT_GUIDE.md`
- 無簡體字／英文標點混用（技術語例外）
- 表格對齊（若新增於技能表）
- 不重複定義同職能的不同敘述（避免語義漂移）

## 文字風格原則
| 類型 | 風格 |
|------|------|
| 能力/技能 | 動詞開頭（列出價值行為） |
| 描述 | 由「使用時機 → 核心專長 → 產出形式」三段構成 |
| 範例 | 使用 `<example>` 包裝，含 user / assistant / commentary |
| 決策語氣 | 客觀、結構化，不使用情緒化語句 |

## 常見任務操作指引
| 任務 | 步驟 |
|------|------|
| 新增成員 | 更新 `agent list.md` →（必要）更新技能表 → 建立 subagent |
| 修正口頭禪 | `agent list.md` → 對應 subagent |
| 擴增技能分類 | 先於技能表新增 → 於相關角色敘述引用 |
| 清理不一致 | 交叉比對：角色清單 / 技能表 / 指引文件 |

## 版本與提交建議
Commit 格式（與 `AGENT_FORMAT_GUIDE.md` 一致）：
- `[新增] team-role：說明`
- `[更新] team-role：說明`
- `[修正] team-role：格式/敘述修正`
- `[重構] team-role：結構調整`

## 待建立（下階段建議）
1. 建立 `.claude/agents/` 目錄並產出前 3 個示範檔（1 Leader + 2 Member）
2. 將 `agent list.md` 拆出 `leaders-overview.md` / `teams-overview.md`（若規模再擴張）
3. 自動檢查腳本（YAML + Markdown lint + 角色對齊）
4. 加入缺席的 3D 團隊（若確定仍需要）

## 安全與一致性守則
- 不擅自「創造」未定義角色
- 不改動既有角色核心定位（除非由變更需求明示）
- 任何跨檔案修改需維護同步（來源：`agent list.md`）

## 參考來源關聯
- 角色技能引用：以 `Adventurer Guild Role List.md` 為唯一來源
- 若技能表無對應 → 先補技能表，再引用於角色（禁止裸寫未定義能力）

## 快速判斷流程（Decision Flow）
```
我要新增/修改 → 影響角色? → 是 → 先改 agent list.md
                     ↓
                影響技能? → 是 → 先改技能表（保持分類一致）
                     ↓
         需有執行單位(subagent)? → 是 → 依格式建立 YAML + 正文
                     ↓
              提交前跑：命名 / Frontmatter / 口頭禪 / 對齊檢查
```

---

保持：精準、結構化、可擴充。  
所有輸出（含後續自動生成 subagent）務必以本文件 + `AGENT_FORMAT_GUIDE.md` 為權威依據。
