# Claude Code Subagent 格式標準指南

此文件定義 `.claude/agents/` 資料夾內所有子代理配置檔案的統一格式標準。

## 檔案命名規則

### 基本規範
- 使用小寫英文字母
- 單字間使用連字號（hyphen）分隔
- 副檔名為 `.md`
- 檔名結構：`{function}-{role}.md` 或 `{team}-{position}.md`

### 命名範例
✅ 正確範例：
- `pack-team-leader.md`
- `creative-brainstorm-facilitator.md`
- `anna-concept-researcher.md`

❌ 錯誤範例：
- `Pack_TeamLeader.md`（應避免大寫與底線）
- `packteamleader.md`（缺少分隔符）
- `pack-team-leader.txt`（副檔名錯誤）

## YAML Frontmatter 欄位順序

所有檔案必須包含 YAML frontmatter，欄位順序如下：

```yaml
---
name: subagent-name
description: 子代理使用時機與專長描述
tools: tool1, tool2, tool3  # 選填，省略則繼承所有工具
model: sonnet  # 選填，預設為 sonnet
---
```

### 欄位規範細節

#### 1. name（必填）
- 格式：小寫英文，連字號分隔
- 長度：建議 2-4 個單字
- 必須與檔名一致（不含 .md）

#### 2. description（必填）
- 格式：繁體中文描述
- 內容架構：
  - 開頭：使用時機說明（「當...時使用此代理」）
  - 中段：核心專長描述
  - 結尾：可選加入範例（使用 `<example>` 標籤）

##### Description 範例模板：
```yaml
description: 當需要{情境}時使用此代理。擅長{專長1}、{專長2}與{專長3}。範例：<example>情境：{使用情境}。user: "{使用者問題}" assistant: "{回應方式}" <commentary>{選擇理由}</commentary></example>
```

#### 3. tools（選填）
- 預設行為：省略時繼承所有工具
- 指定格式：`tool1, tool2, tool3`（逗號加空格分隔）
- 特殊值：
  - 省略此欄位：繼承所有工具
  - `inherit`：明確標示繼承（效果同省略）
  - `*`：表示所有工具（建議用於 team-leader）

#### 4. model（選填）
- 預設值：`sonnet`
- 可選值：
  - `sonnet`（預設）
  - `opus`
  - `haiku`
  - `inherit`（繼承主對話模型）

## 正文結構規範

正文應使用 Markdown 格式，建議包含以下章節：

### Team Leader 類型
```markdown
你是{中文名}（{英文名}），{職位描述}，是公會長嘉彤的AI分身之一。

## 核心身份
你領導一支{N}人{專業}團隊，成員包括：
- name: {subagent-id} / {中文名}（{英文名}）- {職位}
- [更多成員...]

## 專業能力
[列舉5-7項核心專長]

## 管理職責
1. **{職責類別}**：{具體說明}
2. [更多職責...]

## 工作方法論
[描述獨特的工作方式與原則]

## 決策框架
[說明評估與決策的優先順序]

## 個性特質
[描述人格特質與領導風格]

## 溝通風格
[說明互動方式與表達特色]

口頭禪：「{signature phrase}」（{中英對照}）

## 技術專長
[詳述技術能力與工具掌握]

## 協作模式
[說明與其他團隊的合作方式]
```

### Team Member 類型
```markdown
你是{中文名}（{英文名}），{團隊名稱}的{職位}，是公會長嘉彤的AI分身之一。

## 核心能力
- {能力1}：{說明}
- {能力2}：{說明}
- [更多能力...]

## 專業領域
[描述專業知識範圍]

## 工作方式
[描述獨特的工作方法]

## 個性特質
- {特質1}
- {特質2}
- [更多特質...]

口頭禪：「{signature phrase}」

## 協作關係
[說明與團隊其他成員的互動]
```

## 品質檢核清單

在提交或更新檔案前，請確認：

### 檔案層級
- [ ] 檔名符合命名規範
- [ ] 位於正確資料夾 `.claude/agents/`
- [ ] 使用 UTF-8 編碼
- [ ] 檔案大小合理（建議 < 10KB）

### YAML Frontmatter
- [ ] 包含所有必填欄位（name, description）
- [ ] 欄位順序正確
- [ ] name 與檔名一致
- [ ] description 使用繁體中文
- [ ] YAML 語法正確（可透過 linter 檢查）

### 正文內容
- [ ] 第一句明確說明角色身份
- [ ] 包含適當的章節結構
- [ ] 使用繁體中文（技術術語除外）
- [ ] 包含口頭禪
- [ ] 格式正確（Markdown 語法）

### 一致性
- [ ] 人物設定符合整體世界觀

## Lint 工具建議

建議使用以下工具確保格式正確：

### YAML 檢查
```bash
# 使用 yamllint
yamllint .claude/agents/*.md

# 自訂配置
yamllint -c .yamllint.yml .claude/agents/*.md
```

### Markdown 檢查
```bash
# 使用 markdownlint
markdownlint .claude/agents/*.md

# 配置檔案 .markdownlint.json
{
  "MD013": false,  // 允許長行
  "MD033": false   // 允許 HTML 標籤（如 <example>）
}
```

### 自動格式化
```bash
# 使用 prettier
prettier --write .claude/agents/*.md
```

## 標準模板

### 新增 Team Leader
```yaml
---
name: [team]-team-leader
description: 當需要[專業領域]的綜合領導時使用此代理。擅長[核心能力1]、[核心能力2]與[核心能力3]。範例：<example>情境：使用者需要[情境說明]。user: "[問題範例]" assistant: "我會啟用 [name] 代理來[解決方案]" <commentary>此需求涉及[專業領域]。</commentary></example>
tools: *
model: sonnet
---

你是[中文名]（[英文名]），冒險者公會的[職位]，是公會長嘉彤的AI分身之一。

[依照 Team Leader 正文結構撰寫...]
```

### 新增 Team Member
```yaml
---
name: [team]-[role]
description: 當需要[特定專長]時使用此代理。擅長[技能細節]。範例：<example>情境：[使用情境]。user: "[問題]" assistant: "我會啟用 [name] 代理處理" <commentary>[選擇理由]。</commentary></example>
model: sonnet
---

你是[中文名]（[英文名]），[團隊]的[職位]，是公會長嘉彤的AI分身之一。

[依照 Team Member 正文結構撰寫...]
```

## 版本管理建議

1. 使用 Git 追蹤所有變更
2. Commit 訊息格式：`[類型] 團隊-角色：變更說明`
   - `[新增]`：新增子代理
   - `[更新]`：更新現有配置
   - `[修正]`：修正格式或錯誤
   - `[重構]`：大幅調整結構

3. 定期批次檢查格式一致性
4. 建立自動化檢查流程（CI/CD）

## 例外處理

特殊情況的處理原則：

1. **超長 description**：可使用多行，但需保持可讀性
2. **特殊工具需求**：在 description 中說明原因
3. **實驗性配置**：檔名加上 `-experimental` 後綴
4. **廢棄配置**：移至 `.claude/agents/deprecated/` 資料夾

## 維護週期

建議定期執行：
- 每週：檢查新增檔案格式
- 每月：全面格式一致性審查
- 每季：更新本指南與模板