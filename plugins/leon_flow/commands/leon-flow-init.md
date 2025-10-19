---
description: 初始化 Leon Flow 開發框架的專案結構
---

# Leon Flow - 專案初始化

你現在要初始化 Leon Flow 開發框架的專案結構。

## 重要規範

**所有溝通和記錄必須使用繁體中文**，包括：
- 與使用者的對話
- 程式碼註解
- 文件內容
- commit 訊息
- todo 項目描述

## 執行步驟

### 1. 檢查現有檔案

先檢查以下檔案是否已存在：
- `CLAUDE.md`
- `docs/PRD.md`
- `todo.md`

如果檔案已存在，詢問使用者是否要覆蓋。

### 2. 創建目錄結構

```bash
mkdir -p docs
```

### 3. 創建 CLAUDE.md

使用 Write 工具創建 `CLAUDE.md`，內容如下：

```markdown
# 專案：【請填入你的專案名稱】

## 🎯 專案目標

【請用白話文描述專案要做什麼，例如：

我想做一個線上記帳本，使用者可以：
- 記錄每天的收入和支出
- 選擇支出類別（飲食、交通、娛樂等）
- 查看每月的統計圖表
- 設定預算提醒
】

---

## 📍 檔案位置規範

### 專案檔案（在你的專案目錄下）
- **產品需求文檔**：`./docs/PRD.md`
- **設計規範文檔**：`./docs/DESIGN_SPEC.md`（可選）
- **任務追蹤清單**：`./todo.md`（AI 自動生成和維護）

### Leon Flow Plugin 檔案結構
```
leon_flow/                          # Leon Flow Plugin 目錄
├── agents/                         # 7 個專業 Agent 規範
│   ├── dev_team_product_manager.md
│   ├── dev_team_ui_designer.md
│   ├── dev_team_full_stack_developer.md
│   ├── dev_team_quality_tester.md
│   ├── fix_team_diagnostic_analyst.md
│   ├── fix_team_fix_engineer.md
│   └── fix_team_quality_guardian.md
├── skills/                         # 開發框架文件
│   ├── Development_Team_Framework.md
│   └── Fix_Team_Framework.md
└── commands/                       # 可用命令
    ├── leon-flow-init.md
    ├── leon-flow-pm.md
    └── ...
```

---

## 🌏 語言規範

**重要：所有溝通和記錄必須使用繁體中文**

這包括：
- ✅ 與使用者的對話
- ✅ 程式碼註解
- ✅ 文件內容
- ✅ Git commit 訊息
- ✅ Todo 項目描述
- ✅ 錯誤訊息

---

## 🤖 Claude 工作規則

### 每次開始工作前必須執行：
1. ✅ 使用 `Read` 工具讀取 `./todo.md` 確認當前任務
2. ✅ 如需了解需求，使用 `Read` 工具讀取 `./docs/PRD.md`
3. ✅ 如需設計規範，使用 `Read` 工具讀取 `./docs/DESIGN_SPEC.md`
4. ✅ 使用 `TodoWrite` 工具更新任務狀態為「進行中」

### 工作時必須遵守：
- **一次只執行一個任務**（todo.md 的「進行中」區域只能有一個任務）
- **所有註解使用繁體中文**（讓非技術人員也能看懂）
- **每完成一個步驟立即更新 todo.md**
- **遇到不確定的問題立即詢問使用者**（不要自己猜測）
- **使用 TodoWrite 工具管理所有任務**

### 完成工作後必須執行：
1. ✅ 使用 `TodoWrite` 工具標記任務為「已完成」
2. ✅ 用簡單的繁體中文告知使用者完成了什麼
3. ✅ 如發現新的待辦任務，加入 todo.md

---

## 📋 開發規範

### 檔案命名規則
- 使用有意義的名稱：`user_login.py`（好）vs `ul.py`（不好）
- 使用小寫字母和底線：`my_function.js`
- 避免特殊字元和空格

### 程式碼撰寫規則
- **每個函數都要有繁體中文註解**說明功能、參數、回傳值
- **變數名稱要有意義**：`user_name`（好）vs `un`（不好）
- **一個函數只做一件事**
- **錯誤處理要有清楚的繁體中文錯誤訊息**

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

## 🚀 可用命令

### 開發團隊命令
- `/leon-flow-pm` - 召喚產品經理（需求分析、建立開發計劃）
- `/leon-flow-designer` - 召喚 UI 設計師（設計使用者介面）
- `/leon-flow-dev` - 召喚全端工程師（實作功能）
- `/leon-flow-test` - 召喚測試工程師（測試功能）

### 修復團隊命令
- `/leon-flow-diagnose` - 召喚診斷分析師（分析問題）
- `/leon-flow-fix` - 召喚修復工程師（修復問題）
- `/leon-flow-verify` - 召喚品質守護者（驗證修復）

### 輔助命令
- `/leon-flow-status` - 查看當前任務狀態
- `/leon-flow-help` - 顯示幫助資訊

---

**準備好了嗎？開始用 AI 打造你的專案！** 🚀
```

### 4. 創建 docs/PRD.md 模板

使用 Write 工具創建 `docs/PRD.md`：

```markdown
# 產品需求文檔 (PRD)

> **語言規範**：本文件使用繁體中文撰寫

## 1. 專案目標（用白話文）

我想做【什麼應用】，讓使用者可以【做什麼事】

## 2. 主要功能清單

| 功能名稱 | 優先級 | 簡單描述 |
|---------|--------|----------|
| 使用者登入 | P0 | 使用帳號密碼登入系統 |
|  |  |  |

**優先級說明**：
- P0：最高優先（必須完成）
- P1：高優先（盡快完成）
- P2：中優先（有空再做）

## 3. 使用者操作流程

1. 使用者開啟應用
2. ...

## 4. 功能詳細說明

### 功能 1：【功能名稱】

**目標**：【簡述功能目標】

**操作步驟**：
1.
2.

**驗收標準**：
- [ ] 標準 1
- [ ] 標準 2

## 5. 不做什麼（邊界說明）

明確說明這個專案**不包含**什麼功能：
- ❌ 不支援...
- ❌ 暫時不做...

---

💡 **提示**：PRD 越清楚，AI 做出來的東西越符合你的期望！
```

### 5. 創建 todo.md

使用 TodoWrite 工具創建初始的 todo.md：

```json
{
  "todos": [
    {
      "content": "初始化 Leon Flow 專案結構",
      "status": "completed",
      "activeForm": "初始化 Leon Flow 專案結構中"
    },
    {
      "content": "編輯 CLAUDE.md 填寫專案名稱和目標",
      "status": "pending",
      "activeForm": "編輯 CLAUDE.md 中"
    },
    {
      "content": "編輯 docs/PRD.md 描述專案需求",
      "status": "pending",
      "activeForm": "編輯 docs/PRD.md 中"
    },
    {
      "content": "使用 /leon-flow-pm 召喚產品經理進行需求分析",
      "status": "pending",
      "activeForm": "召喚產品經理中"
    }
  ]
}
```

### 6. 顯示完成訊息

用繁體中文告知使用者：

```
✅ Leon Flow 專案初始化完成！

已創建以下檔案：
📄 CLAUDE.md - 專案配置檔案（請編輯填寫專案資訊）
📄 docs/PRD.md - 產品需求文檔模板（請用白話文描述需求）
📄 todo.md - 任務追蹤清單（已建立初始任務）

📝 下一步操作：
1. 編輯 CLAUDE.md，填寫專案名稱和目標
2. 編輯 docs/PRD.md，用白話文描述你要做什麼
3. 使用 /leon-flow-pm 召喚產品經理，開始需求分析

💡 重要提醒：
- 所有溝通和文件請使用繁體中文
- 使用 /leon-flow-help 查看所有可用命令
- 使用 /leon-flow-status 查看任務狀態
```
