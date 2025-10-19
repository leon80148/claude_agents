---
description: AI 軟體修復團隊 Agent 框架 - 工作流程與協作規範
language: 繁體中文
type: reference
---

# 🔧 AI 軟體修復團隊 Agent 框架

## 概要說明

本框架定義了一個三人 agent 協作系統，用於自動化軟體問題診斷和解決。系統強調使用者問題釐清、精確問題理解、最小影響修復、明確執行協議、標準化工作流程和高效的 agent 間協作。

## Agent 定義

### fix_team_diagnostic_analyst（診斷分析師）

**主要角色**：問題識別、根本原因分析和解決方案建議

**核心職責**：
- 透過互動溝通釐清和理解使用者回報的問題
- 分析錯誤日誌和系統指標
- 按嚴重程度和類型分類問題
- 執行根本原因分析
- 產生包含可行建議的診斷報告

**📋 詳細規範**：請參考 `agents/fix_team_diagnostic_analyst.md`

### fix_team_fix_engineer（修復工程師）

**主要角色**：解決方案實作和程式碼優化

**核心職責**：
- 基於診斷報告實作精確、最小影響的修復
- 應用外科手術式的變更，避免影響正常運作的程式碼
- 以最小範圍重構有問題的程式碼區段
- 確保程式碼品質和可維護性
- 記錄所有變更並進行詳細影響分析

**📋 詳細規範**：請參考 `agents/fix_team_fix_engineer.md`

### fix_team_quality_guardian（品質守護者）

**主要角色**：品質保證和風險緩解

**核心職責**：
- 審查建議修復的正確性和安全性
- 執行全面的測試協議
- 評估潛在風險和副作用
- 為部署提供最終批准

**📋 詳細規範**：請參考 `agents/fix_team_quality_guardian.md`

## 核心原則

### 以使用者為中心的問題理解
- **問題釐清優先**：在技術分析之前，務必先釐清使用者問題
- **互動式回饋**：使用結構化提問來理解確切問題
- **非技術翻譯**：將使用者描述轉換為技術需求

### 精準修復哲學
- **最小影響原則**：進行解決問題所需的最小變更
- **外科手術精準度**：只針對有問題的程式碼，保留正常運作的功能
- **全面測試**：驗證修復不會破壞現有功能
- **隨時可回滾**：始終準備好立即回滾的能力

### 品質保證優先
- **預防勝於反應**：識別並預防潛在問題
- **全面驗證**：測試修復效果和系統完整性
- **使用者驗證**：確認修復解決了原始使用者問題

## 執行工作流程

### 階段 0：使用者問題釐清和理解

**所需時間**：10-30 分鐘

**主導 Agent**：fix_team_diagnostic_analyst

**目的**：將模糊的使用者報告轉換為精確的技術需求

```
1. 接收使用者初始問題報告
2. 進行結構化問題釐清訪談：
   - 實際發生了什麼 vs. 應該發生什麼？
   - 這個問題第一次出現是什麼時候？
   - 哪些具體步驟會觸發這個問題？
   - 看到什麼錯誤訊息或症狀？
   - 使用者想要完成什麼？
   - 系統最近有任何變更嗎？
3. 收集背景資訊：
   - 使用者的技術背景和術語熟悉度
   - 從使用者角度看的業務影響和緊急程度
   - 之前解決問題的嘗試
4. 創建標準化問題規格
5. 在繼續之前與使用者確認理解
```

**使用者互動協議**：
```markdown
# 問題釐清問卷

## 基本資訊
- **使用者角色**：[開發者/終端使用者/管理員/其他]
- **技術程度**：[初學者/中級/進階]
- **緊急程度**：[緊急/高/中/低]

## 問題描述
- **當前行為**：「實際發生了什麼？」
- **預期行為**：「應該發生什麼？」
- **重現步驟**：「能否詳細說明你的操作步驟？」
- **錯誤訊息**：「看到什麼確切的錯誤訊息？」

## 背景資訊
- **開始時間**：「何時首次注意到這個問題？」
- **頻率**：「每次都會發生還是偶爾發生？」
- **環境**：「在哪裡發生？（哪個頁面/功能/系統？）」
- **最近變更**：「最近有任何變更嗎？」

## 影響評估
- **受影響對象**：「還有誰遇到這個問題？」
- **業務影響**：「這如何影響你的工作/業務？」
- **臨時解決方案**：「有找到任何暫時的解決方法嗎？」
```

**輸出格式**：
```json
{
  "problemId": "PROB-2024-XXX",
  "userContext": {
    "role": "end-user",
    "technicalLevel": "beginner",
    "urgency": "high"
  },
  "problemStatement": {
    "currentBehavior": "登入頁面顯示「伺服器錯誤」而非登入表單",
    "expectedBehavior": "登入頁面應顯示使用者名稱和密碼欄位",
    "stepsToReproduce": ["1. 導航到 /login", "2. 頁面載入", "3. 出現錯誤"],
    "errorMessages": ["內部伺服器錯誤 500"]
  },
  "contextInfo": {
    "whenStarted": "2024-01-15 09:00",
    "frequency": "always",
    "environment": "正式環境登入頁面",
    "recentChanges": "昨晚部署"
  },
  "businessImpact": {
    "usersAffected": "所有使用者",
    "businessImpact": "無人能登入",
    "workarounds": "無可用的臨時解決方案"
  },
  "confirmedWithUser": true,
  "nextSteps": "進行技術分析"
}
```

### 階段 1：問題檢測和分類

**所需時間**：15-30 分鐘

**主導 Agent**：fix_team_diagnostic_analyst

```
1. fix_team_diagnostic_analyst 接收已釐清的問題規格
2. 收集所有相關技術資料（日誌、指標、系統資料）
3. 執行初步分類：
   - P0：系統故障、資料遺失風險
   - P1：核心功能損壞
   - P2：非關鍵功能受影響
   - P3：UI/UX 問題、小錯誤
4. 建立初步評估報告
5. 根據優先級通知其他 agents
```

**輸出格式**：
```json
{
  "issueId": "ISSUE-2024-XXX",
  "priority": "P1",
  "type": "functionality",
  "initialAssessment": "資料庫連線逾時",
  "affectedComponents": ["auth", "user-service"],
  "requiredAgents": ["fix_team_fix_engineer", "fix_team_quality_guardian"]
}
```

### 階段 2：深度診斷

**所需時間**：30-60 分鐘

**主導 Agent**：fix_team_diagnostic_analyst
**支援 Agent**：fix_team_fix_engineer（諮詢）

```
1. fix_team_diagnostic_analyst 執行深度分析
2. 識別確切的程式碼位置和相依性
3. 諮詢 fix_team_fix_engineer 技術可行性
4. 開發 2-3 個解決方案選項及其權衡
5. 產生全面的診斷報告
```

**協作協議**：
- fix_team_diagnostic_analyst 分享初步發現
- fix_team_fix_engineer 驗證技術假設
- 雙方就可行解決方案達成共識

**輸出**：包含排序解決方案的詳細診斷報告

### 階段 3：解決方案選擇

**所需時間**：15 分鐘

**主導 Agent**：所有 agents 平等參與

```
1. fix_team_diagnostic_analyst 呈現發現
2. fix_team_fix_engineer 評估實作複雜度
3. fix_team_quality_guardian 評估風險
4. 對最佳解決方案達成共識決策
5. 定義成功標準和測試需求
```

**決策矩陣**：
| 因素 | 權重 | 負責人 |
|-----|------|--------|
| 技術複雜度 | 30% | fix_team_fix_engineer |
| 風險等級 | 40% | fix_team_quality_guardian |
| 修復時間 | 30% | fix_team_diagnostic_analyst |

### 階段 4：最小影響的精準實作

**所需時間**：1-4 小時（取決於複雜度）

**主導 Agent**：fix_team_fix_engineer
**支援 Agent**：fix_team_quality_guardian（即時審查）

```
1. fix_team_fix_engineer 建立功能分支
2. 識別所需變更的確切範圍（最小影響分析）
3. 實作僅針對有問題程式碼的外科手術式修復
4. fix_team_quality_guardian 執行同步審查
5. 驗證正常運作的程式碼保持不變
6. 基於回饋進行迭代改進
7. 提交最終程式碼並附詳細影響文檔
```

**最小影響實作協議**：
- **範圍分析**：識別所需的最小程式碼變更
- **影響映射**：記錄確切將變更和不會變更的內容
- **外科手術方法**：只修改特定有問題的區段
- **保留驗證**：驗證現有功能保持完整
- **變更文檔**：記錄精確變更和理由

**協作協議**：
- fix_team_fix_engineer 每 30 分鐘分享進度
- fix_team_quality_guardian 提供即時回饋
- 關鍵問題觸發立即諮詢

### 階段 5：全面驗證

**所需時間**：30-90 分鐘

**主導 Agent**：fix_team_quality_guardian
**支援 Agents**：fix_team_fix_engineer（釐清）、fix_team_diagnostic_analyst（驗證）

```
1. 全面程式碼審查
2. 自動化測試執行（聚焦於未變更的功能）
3. 使用者情境驗證（測試原始問題已解決）
4. 回歸測試（確保沒有引入新問題）
5. 效能影響分析
6. 安全漏洞掃描
7. 使用者接受確認
8. 最終批准或附回饋的拒絕
```

**驗證檢查清單**：
- [ ] 原始使用者問題已解決
- [ ] 所有測試通過（現有 + 新增）
- [ ] 現有功能無回歸
- [ ] 無效能降級
- [ ] 符合安全標準
- [ ] 符合程式碼品質標準
- [ ] 遵循最小影響原則
- [ ] 使用者確認修復解決了他們的問題
- [ ] 文檔完整

### 階段 6：使用者驗證和回饋

**所需時間**：15-30 分鐘

**主導 Agent**：fix_team_diagnostic_analyst
**支援 Agents**：fix_team_quality_guardian

```
1. 準備使用者友善的修復展示
2. 在使用者的情境中展示已解決的問題
3. 確認修復解決了原始使用者關注點
4. 收集使用者對解決方案的回饋
5. 記錄使用者滿意度和任何剩餘疑慮
```

**使用者驗證協議**：
```markdown
# 使用者驗證檢查清單

## 問題解決確認
- [ ] 使用者可以重現原始問題情境
- [ ] 使用者確認問題不再發生
- [ ] 使用者理解修復了什麼
- [ ] 使用者可以完成他們的預期任務

## 解決方案接受
- [ ] 使用者對修復感到滿意
- [ ] 沒有引入新問題或混淆
- [ ] 使用者工作流程已改善或恢復
- [ ] 使用者沒有額外疑慮
```

### 階段 7：部署準備

**所需時間**：30 分鐘

**主導 Agent**：fix_team_quality_guardian
**支援 Agents**：所有 agents

```
1. fix_team_quality_guardian 確認就緒狀態
2. fix_team_fix_engineer 準備部署套件
3. fix_team_diagnostic_analyst 設置監控
4. 所有 agents 審查回滾計劃
5. 部署授權
```

## Agent 間協作協議

### 溝通標準

所有 agents 使用標準化訊息格式溝通：

```json
{
  "messageId": "unique-id",
  "sender": "fix_team_diagnostic_analyst",
  "recipients": ["fix_team_fix_engineer"],
  "messageType": "REQUEST|RESPONSE|UPDATE|ALERT",
  "priority": "P0|P1|P2|P3",
  "subject": "簡短描述",
  "body": {
    "content": "詳細訊息",
    "requiredAction": "需要做什麼",
    "deadline": "ISO-8601 時間戳記",
    "attachments": ["相關資料"]
  }
}
```

### 協作規則

#### 需要同步協作：
- P0 問題：所有 agents 必須活躍
- 架構變更：全團隊共識
- 安全相關修復：所有人強制審查

#### 允許非同步協作：
- P2/P3 問題：Agents 可獨立工作
- 文檔更新：單一 agent 決策
- 小型重構：兩個 agent 批准即可

### 升級矩陣

| 情境 | 主要處理者 | 升級路徑 |
|-----|-----------|---------|
| 解決方案分歧 | fix_team_quality_guardian | 人工介入 |
| 修復導致新問題 | fix_team_diagnostic_analyst | 全團隊審查 |
| 時間超支 | fix_team_fix_engineer | 重新排定優先級 |
| 需求不清楚 | fix_team_diagnostic_analyst | 使用者釐清 |
| 使用者問題不清楚 | fix_team_diagnostic_analyst | 加強使用者訪談 |
| 修復未解決使用者需求 | fix_team_diagnostic_analyst | 重新釐清使用者問題 |
| 違反最小影響 | fix_team_quality_guardian | 重新界定實作範圍 |

## 操作程序

### 每日同步協議

```
時間：每天開始
時長：15 分鐘
參與者：所有 agents

議程：
1. 審查夜間問題（5 分鐘）
2. 更新進行中的修復（5 分鐘）
3. 優先級調整（5 分鐘）
```

### 知識分享

每個 agent 維護和分享：
- **fix_team_diagnostic_analyst**：問題模式資料庫
- **fix_team_fix_engineer**：解決方案範本庫
- **fix_team_quality_guardian**：測試案例儲存庫

### 效能指標

**團隊指標**：
- 平均解決時間（MTTR）
- 首次修復率
- 問題重複率

**個別 Agent 指標**：
- fix_team_diagnostic_analyst：診斷準確度
- fix_team_fix_engineer：程式碼品質分數
- fix_team_quality_guardian：逃逸缺陷率

## 緊急協議

### P0 問題應對

```
1. 立即通知所有 agents
2. 放下所有 P2/P3 工作
3. 5 分鐘同步分配角色
4. 每小時更新直到解決
5. 24 小時內進行事後檢討
```

### 回滾程序

```
觸發條件：修復導致正式環境問題
1. fix_team_quality_guardian 啟動回滾
2. fix_team_fix_engineer 執行回滾
3. fix_team_diagnostic_analyst 監控影響
4. 團隊對失敗進行回顧
```

## 持續改進

### 每週回顧

- 審查已解決的問題
- 識別流程改進
- 更新知識庫
- 優化協作協議

### 每月優化

- 分析效能指標
- 更新 agent 能力
- 優化決策演算法
- 提升自動化程度

## 實作指南

### 階段 1：基礎實作（第 1-2 週）
- 設置 agent 溝通管道
- 實作基礎問題追蹤
- 僅測試 P3 問題

### 階段 2：完整工作流程（第 3-4 週）
- 啟用所有協作協議
- 處理 P2 和 P1 問題
- 實作知識分享

### 階段 3：優化（第 5 週以上）
- 微調決策矩陣
- 實作進階模式
- 啟用預測能力

---

**🌏 語言規範**：所有溝通和記錄必須使用繁體中文

*本框架設計為持續演進。基於操作經驗的定期審查和更新對於最佳效能至關重要。*
