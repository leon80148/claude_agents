# 🚀 Vibe Coding Agents - SDD + To-Do List 開發框架

## 📖 這是什麼？

一個專為**非專業程序員**設計的 AI 開發框架，讓你透過 Claude Code 自主完成軟體開發。

**核心理念**：
- **規範驅動開發（SDD）**：用清楚的文件告訴 AI 要做什麼
- **To-Do List 自動追蹤**：AI 自動建立和更新任務清單
- **Agent 團隊協作**：7 個專業 AI agent 分工完成開發

---

## 🏗️ 架構總覽

### 系統級文件（全局共用，設定一次）
```
~/.claude/agents/                    # 所有專案共用的 Agents
├── dev_team_product_manager.md
├── dev_team_ui_designer.md
├── dev_team_full_stack_developer.md
├── dev_team_quality_tester.md
├── fix_team_diagnostic_analyst.md
├── fix_team_fix_engineer.md
└── fix_team_quality_guardian.md
```

### 專案級文件（每個專案需要）
```
my-project/
├── CLAUDE.md                        # 專案配置（從本文件複製範本）
├── Development_Team_Framework.md    # 開發流程參考
├── Fix_Team_Framework.md           # 修復流程參考
├── docs/
│   ├── PRD.md                      # 產品需求文檔
│   └── DESIGN_SPEC.md              # 設計規範（可選）
└── todo.md                         # 任務清單（AI 自動生成）
```

---

## ⚡ 快速開始（3 步驟）

### 步驟 1：一次性系統設定（首次使用，5 分鐘）

```bash
# 創建系統 agents 目錄
mkdir -p ~/.claude/agents

# 複製 agents 到系統目錄（修改成你的 vibe-coding-agents 路徑）
cp /path/to/vibe-coding-agents/agents/*.md ~/.claude/agents/

# 驗證安裝
ls ~/.claude/agents/
# 應該看到 7 個 .md 文件
```

✅ **完成！之後所有專案都能使用這些 agents**

---

### 步驟 2：開始新專案（每個專案，2 分鐘）

```bash
# 1. 創建專案目錄
mkdir my-new-project && cd my-new-project
mkdir docs

# 2. 複製框架文件（修改成你的路徑）
cp /path/to/vibe-coding-agents/Development_Team_Framework.md .
cp /path/to/vibe-coding-agents/Fix_Team_Framework.md .

# 3. 創建 CLAUDE.md（從下方「Part 3」複製範本）
# 4. 創建 PRD
touch docs/PRD.md
```

---

### 步驟 3：開始開發

1. **編輯 CLAUDE.md**：填寫專案名稱和目標
2. **編輯 docs/PRD.md**：用白話文描述你要做什麼
3. **啟動 Claude Code**：
   ```bash
   claude
   ```
4. **召喚第一個 agent**：
   ```
   請扮演 dev_team_product_manager 的角色，
   參考 ~/.claude/agents/dev_team_product_manager.md 的規範，
   分析 docs/PRD.md 並建立開發計劃和 todo.md
   ```

🎉 **開始開發！**

---

## 📋 Part 3：CLAUDE.md 生成範本

> **使用方式**：複製以下完整內容到你的專案 CLAUDE.md 文件

```markdown
# 專案：【填入你的專案名稱】

## 🎯 專案目標

【用白話文描述專案要做什麼，例如：

我想做一個線上記帳本，使用者可以：
- 記錄每天的收入和支出
- 選擇支出類別（飲食、交通、娛樂等）
- 查看每月的統計圖表
- 設定預算提醒
】

---

## 📍 文件位置規範

### 專案文件
- **產品需求文檔**：`./docs/PRD.md`
- **設計規範文檔**：`./docs/DESIGN_SPEC.md`（可選）
- **任務追蹤清單**：`./todo.md`（AI 自動生成）

### 參考文件
- **開發團隊框架**：`./Development_Team_Framework.md`
- **修復團隊框架**：`./Fix_Team_Framework.md`

### Agent 配置（系統級）
- **Agents 位置**：`~/.claude/agents/`
- 包含 7 個 agent：
  - dev_team_product_manager
  - dev_team_ui_designer
  - dev_team_full_stack_developer
  - dev_team_quality_tester
  - fix_team_diagnostic_analyst
  - fix_team_fix_engineer
  - fix_team_quality_guardian

---

## 🤖 Claude 工作規則

### 每次開始工作前必須執行：
1. ✅ 使用 `Read` 工具讀取 `./todo.md` 確認當前任務
2. ✅ 如需了解需求，使用 `Read` 工具讀取 `./docs/PRD.md`
3. ✅ 如需設計規範，使用 `Read` 工具讀取 `./docs/DESIGN_SPEC.md`
4. ✅ 使用 `TodoWrite` 工具更新任務狀態為「🔄 進行中」

### 工作時必須遵守：
- **一次只執行一個任務**（todo.md 的「進行中」區域只能有一個任務）
- **所有註解使用中文**（讓非技術人員也能看懂）
- **每完成一個步驟立即更新 todo.md**
- **遇到不確定的問題立即詢問使用者**（不要自己猜測）
- **使用 TodoWrite 工具管理所有任務**

### 完成工作後必須執行：
1. ✅ 使用 `TodoWrite` 工具標記任務為「✅ 已完成」
2. ✅ 用簡單的語言告知使用者完成了什麼
3. ✅ 如發現新的待辦任務，加入 todo.md

---

## 📋 開發規範（給 AI 的指引）

### 檔案命名規則
- 使用有意義的名稱：`user_login.py`（好）vs `ul.py`（不好）
- 使用小寫字母和底線：`my_function.js`
- 避免特殊字元和空格

### 程式碼撰寫規則
- **每個函數都要有中文註解**說明功能、參數、回傳值
- **變數名稱要有意義**：`user_name`（好）vs `un`（不好）
- **一個函數只做一件事**
- **錯誤處理要有清楚的中文錯誤訊息**

### 範例（好的程式碼）
```python
def 計算商品總價(單價, 數量, 折扣=0):
    """
    計算商品的總價

    參數：
    - 單價：商品單價（數字）
    - 數量：購買數量（整數）
    - 折扣：折扣百分比，例如 0.1 表示 9 折（可選）

    回傳：總價（數字）
    """
    原價 = 單價 * 數量
    總價 = 原價 * (1 - 折扣)
    return 總價
```

---

## 🚀 使用方式

### 開發新功能（Development Team）

#### 1️⃣ 召喚產品經理（分析需求）
```
請扮演 dev_team_product_manager 的角色，
參考 ~/.claude/agents/dev_team_product_manager.md 的規範，
分析 docs/PRD.md 的需求並建立開發計劃和 todo.md
```

#### 2️⃣ 召喚 UI 設計師（設計介面）
```
請扮演 dev_team_ui_designer 的角色，
參考 ~/.claude/agents/dev_team_ui_designer.md 的規範，
根據 PRD 設計【功能名稱】的使用者介面
```

#### 3️⃣ 召喚全端工程師（實作功能）
```
請扮演 dev_team_full_stack_developer 的角色，
參考 ~/.claude/agents/dev_team_full_stack_developer.md 的規範，
根據 PRD 和 DESIGN_SPEC 實作【功能名稱】
```

#### 4️⃣ 召喚測試工程師（測試功能）
```
請扮演 dev_team_quality_tester 的角色，
參考 ~/.claude/agents/dev_team_quality_tester.md 的規範，
測試【功能名稱】是否正常運作
```

---

### 修復問題（Fix Team）

#### 1️⃣ 召喚診斷分析師（分析問題）
```
請扮演 fix_team_diagnostic_analyst 的角色，
參考 ~/.claude/agents/fix_team_diagnostic_analyst.md 的規範，
分析以下問題：【描述問題】
```

#### 2️⃣ 召喚修復工程師（修復問題）
```
請扮演 fix_team_fix_engineer 的角色，
參考 ~/.claude/agents/fix_team_fix_engineer.md 的規範，
根據診斷報告修復問題
```

#### 3️⃣ 召喚品質守護者（驗證修復）
```
請扮演 fix_team_quality_guardian 的角色，
參考 ~/.claude/agents/fix_team_quality_guardian.md 的規範，
驗證問題是否已修復
```

---

## 📖 詳細流程

### 完整開發流程
參考：`./Development_Team_Framework.md`

### 完整修復流程
參考：`./Fix_Team_Framework.md`

---

## ⚠️ 重要提醒

### ✅ 必須做：
- 每次工作前讓 Claude 確認 todo.md
- 保持 todo.md 即時更新
- 用白話文描述需求

### ❌ 不要做：
- 不要一次給太多任務
- 不要跳過測試步驟
- 不要讓「進行中」有多個任務

---

**準備好了嗎？開始用 AI 打造你的專案！** 🚀
```

---

## 📝 Part 4：文件範本

### todo.md 格式

```markdown
# 專案任務清單

## 🔄 進行中（只能有一個）
- [ ]

## 📋 待辦任務

### P0 - 最高優先（必須完成）
- [ ]

### P1 - 高優先（盡快完成）
- [ ]

### P2 - 中優先（有空再做）
- [ ]

## ✅ 已完成
- [x]

## ⚠️ 問題追蹤
- [ ]

## 📝 更新記錄
- YYYY-MM-DD：

---

### 📖 任務格式說明

```
- [ ] [優先級] 任務描述 (@負責的agent)
  - 開始：YYYY-MM-DD
  - 預計：YYYY-MM-DD
```

範例：
```
- [ ] [P0] 實作使用者登入功能 (@dev_team_full_stack_developer)
  - 開始：2025-01-10
  - 預計：2025-01-12
```
```

---

### docs/PRD.md 範本（精簡版）

```markdown
# 產品需求文檔 (PRD)

## 1. 專案目標（用白話文）
我想做【什麼應用】，讓使用者可以【做什麼事】

## 2. 主要功能清單

| 功能名稱 | 優先級 | 簡單描述 |
|---------|--------|----------|
| 使用者登入 | P0 | 使用帳號密碼登入系統 |
| 記帳功能 | P0 | 記錄收入和支出 |
| 統計圖表 | P1 | 顯示每月收支統計 |

## 3. 使用者操作流程（重要！）

用文字或 Mermaid 圖表描述使用者如何使用你的應用。

範例：
```
1. 使用者開啟網站
2. 如果未登入，顯示登入頁面
3. 輸入帳號密碼後登入
4. 登入成功後顯示主頁面
5. 使用者可以新增記帳記錄
```

## 4. 每個功能的詳細說明

### 功能 1：使用者登入

**目標**：讓使用者可以安全地登入系統

**操作步驟**：
1. 在登入頁面輸入帳號
2. 輸入密碼
3. 點擊「登入」按鈕
4. 系統驗證帳號密碼
5. 登入成功後導向主頁面

**驗收標準**（如何知道完成了）：
- [ ] 正確的帳號密碼可以成功登入
- [ ] 錯誤的帳號密碼會顯示錯誤訊息
- [ ] 登入後會記住使用者（不用每次都登入）

## 5. 不做什麼（邊界說明）

明確說明這個專案**不包含**什麼功能，避免範圍膨脹。

範例：
- ❌ 不支援第三方登入（Google、Facebook）
- ❌ 不做多人協作功能
- ❌ 暫時不做行動 APP

---

💡 **提示**：PRD 越清楚，AI 做出來的東西越符合你的期望！
```

---

### docs/DESIGN_SPEC.md 範本（可選）

如果你的專案有使用者介面（網頁、APP），建議填寫這個文件。

```markdown
# 設計規範文檔

## 📋 基本資訊
- 專案名稱：【填入】
- 設計風格：【例如：簡約現代、專業商務、活潑可愛】

## 🎨 色彩規範

### 主要顏色
- **主色調**：#007AFF（藍色） - 用於按鈕、連結
- **背景色**：#FFFFFF（白色）
- **文字色**：#1C1C1E（深灰）

### 功能顏色
- **成功**：#34C759（綠色）
- **警告**：#FF9500（橙色）
- **錯誤**：#FF3B30（紅色）

## 📐 基本規範

### 字體
- 主要字體：【例如：微軟正黑體、思源黑體】
- 標題大小：24px
- 正文大小：16px

### 按鈕
- 高度：44px（手指容易點擊）
- 圓角：8px
- 內邊距：左右 24px

### 間距
- 小間距：8px
- 標準間距：16px
- 大間距：24px

## 📱 響應式設計

- **手機**：小於 768px
- **平板**：768px - 1024px
- **桌面**：大於 1024px

---

💡 **提示**：如果你不確定設計規範，可以讓 dev_team_ui_designer 幫你建議！
```

---

## 💡 Part 5：實際使用範例

### 完整流程範例：開發一個待辦事項網站

#### Day 1：需求分析
```
我：「請扮演 dev_team_product_manager，
參考 ~/.claude/agents/dev_team_product_manager.md 的規範，
分析需求：

我想做一個待辦事項網站，使用者可以：
- 新增待辦任務
- 標記任務為完成
- 刪除任務
- 任務可以設定優先級（高、中、低）
」

↓ Claude 會：
1. 閱讀 docs/PRD.md（如果有）或根據你的描述
2. 建立 todo.md 任務清單
3. 提供技術建議
```

#### Day 2：介面設計
```
我：「請扮演 dev_team_ui_designer，
參考 ~/.claude/agents/dev_team_ui_designer.md 的規範，
設計待辦事項列表的介面」

↓ Claude 會：
1. 根據 PRD 設計頁面佈局
2. 建立 docs/DESIGN_SPEC.md
3. 提供設計建議
```

#### Day 3-5：開發功能
```
我：「請扮演 dev_team_full_stack_developer，
參考 ~/.claude/agents/dev_team_full_stack_developer.md 的規範，
實作新增任務功能」

↓ Claude 會：
1. 讀取 PRD 和 DESIGN_SPEC
2. 開發程式碼
3. 更新 todo.md
4. 告訴你完成了什麼

（依次實作：編輯功能、刪除功能、優先級功能）
```

#### Day 6：測試
```
我：「請扮演 dev_team_quality_tester，
參考 ~/.claude/agents/dev_team_quality_tester.md 的規範，
測試所有功能」

↓ Claude 會：
1. 執行測試
2. 回報測試結果
3. 列出發現的問題
```

#### 如果發現問題：
```
我：「請扮演 fix_team_diagnostic_analyst，
參考 ~/.claude/agents/fix_team_diagnostic_analyst.md 的規範，
分析問題：刪除任務後頁面沒有更新」

↓ Claude 分析問題

我：「請扮演 fix_team_fix_engineer，
參考 ~/.claude/agents/fix_team_fix_engineer.md 的規範，
修復這個問題」

↓ Claude 修復

我：「請扮演 fix_team_quality_guardian，
參考 ~/.claude/agents/fix_team_quality_guardian.md 的規範，
驗證問題是否解決」

↓ Claude 驗證
```

---

## ❓ Part 6：常見問題（FAQ）

### Q1：我完全不懂程式，真的能用嗎？
**A**：可以！你只需要：
1. 用白話文說明想做什麼（寫在 PRD.md）
2. 召喚對應的 agent
3. 確認結果是否符合預期

Claude 會處理所有技術細節。

---

### Q2：agents 一定要放在 ~/.claude/agents/ 嗎？
**A**：強烈建議！因為：
- 所有專案都能共用
- 更新一次，全局生效
- 符合 Claude Code 的標準

如果你真的想放在專案內，把 `~/.claude/agents/` 改成 `./agents/` 即可。

---

### Q3：一定要建立所有文件嗎？
**A**：最少需要：
- **CLAUDE.md**（必須）：告訴 Claude 如何工作
- **docs/PRD.md**（必須）：描述要做什麼
- **todo.md**（AI 自動生成）：任務清單

其他文件視專案需要決定：
- DESIGN_SPEC.md：有 UI 的專案需要
- 2 個 Framework 文件：參考用，建議放

---

### Q4：如果 Claude 做錯了怎麼辦？
**A**：
1. 明確告訴它哪裡不對
2. 用白話文說明你期望的結果
3. 可召喚 fix_team 來修復

範例：
```
「剛才的登入功能有問題，我期望的是：
使用者輸入錯誤密碼時，應該顯示『密碼錯誤，請重試』，
而不是直接跳到首頁。請修復這個問題。」
```

---

### Q5：可以中途修改需求嗎？
**A**：當然可以！
1. 告訴 Claude 你要修改什麼
2. 更新 docs/PRD.md
3. Claude 會自動調整 todo.md 和實作

---

### Q6：todo.md 需要我自己建立嗎？
**A**：不用！當你召喚 `dev_team_product_manager` 時，
它會自動建立 todo.md。

你只需要：
1. 準備好 PRD.md（描述需求）
2. 召喚 product_manager
3. 它會自動建立和管理 todo.md

---

### Q7：agents 檔案更新了怎麼辦？
**A**：
```bash
# 重新複製到系統目錄即可
cp /path/to/vibe-coding-agents/agents/*.md ~/.claude/agents/

# 所有專案立即使用新版本
```

---

### Q8：我可以自訂 agent 的行為嗎？
**A**：可以！
1. 編輯 `~/.claude/agents/` 下對應的 .md 文件
2. 修改後所有專案都會使用新設定
3. 建議先熟悉原始設定再修改

---

### Q9：如何知道目前有哪些任務？
**A**：
```
我：「請讀取 todo.md 並告訴我目前的任務狀態」

Claude 會列出：
- 進行中的任務
- 待辦任務
- 已完成任務
```

---

### Q10：多人協作怎麼辦？
**A**：
- 把 CLAUDE.md、Framework 文件、docs/ 目錄都提交到 git
- 每個人都安裝 agents 到 ~/.claude/agents/
- 透過 git 同步 todo.md 和 PRD.md

---

## 🔗 相關資源

### 框架文件
- **Development_Team_Framework.md**：開發團隊完整流程
- **Fix_Team_Framework.md**：修復團隊完整流程

### 範本文件
- **templates/PRD_Template.md**：完整的 PRD 範本（包含圖表）
- **templates/Diagrams_Guide.md**：如何畫流程圖和架構圖
- **templates/Testing_Framework_Guide.md**：測試指南

### Agents 規範
查看 `~/.claude/agents/` 目錄下的 7 個 agent 規範文件，
了解每個 agent 的完整能力和使用方式。

---

## 📌 最後提醒

### ✅ 成功的關鍵
1. **PRD 要清楚**：寫得越詳細，AI 做得越準確
2. **一步一步來**：不要急著一次完成所有功能
3. **保持溝通**：不確定就問，不要讓 AI 猜

### 🎯 開始第一個專案
1. 按照「快速開始」設定系統 agents
2. 複製 CLAUDE.md 範本到新專案
3. 填寫 PRD.md
4. 召喚 product_manager
5. 開始開發！

---

**準備好用 AI 打造你的專案了嗎？開始吧！** 🚀🎉
