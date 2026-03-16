---
title: "讓 AI 幫你測試程式碼：Agentic Manual Testing 實踐指南"
pubDatetime: 2026-03-16T11:00:00+08:00
tags: [AI, Coding-Agent, Testing, TDD]
description: "當 AI 寫程式碼，如何確認真的能運作？Simon Willison 的 Agentic Manual Testing 模式：讓 AI Agent 不只寫測試，還會像人類一樣「試用」程式碼。從 CLI 快速驗證到瀏覽器自動化測試，補足 Unit Test 的盲點。"
---

# 讓 AI 幫你測試程式碼：Agentic Manual Testing 實踐指南

當你讓 AI 寫程式碼，你會如何確認它真的能運作？

這是 Coding Agent 時代最核心的問題。Simon Willison 在他的 [Agentic Engineering Patterns](https://simonwillison.net/guides/agentic-engineering-patterns/) 系列中，詳細探討了一個關鍵模式：**Agentic Manual Testing**——讓 AI Agent 不只會寫測試,還會「手動」測試程式碼。

## 為什麼需要 Manual Testing？

先說結論：**永遠不要假設 LLM 生成的程式碼能正常運作，除非已經執行過。**

這也是為什麼 Coding Agent（能執行自己寫的程式碼的 AI）比單純輸出程式碼的 LLM 有用得多——它們能驗證、迭代、修正。

但即使有 Unit Test，也不代表程式真的能用：

- 測試都通過了，但伺服器一啟動就崩潰
- UI 元素根本沒渲染出來
- 測試覆蓋不到的邊界情況出問題

任何寫過測試的工程師都知道：**自動化測試無法取代手動測試**。在發布功能前，你會想親眼看到它正常運作。

Agentic Manual Testing 就是讓 AI Agent 也做同樣的事——用「眼睛」（vision model）和「手」（CLI/Browser automation）實際操作、檢查程式碼是否如預期運作。

## 機制一：用 CLI 快速驗證

### Python: `python -c`

對 Python library 來說，最快的手動測試方法是 `python -c`：

```bash
python -c "import mymodule; print(mymodule.do_something())"
```

Agent 通常已經知道這個技巧，但你可以明確提示：

> "After implementing, test it with python -c to verify it works"

### Web API: `curl`

對於 JSON API，用 `curl` 實際打 endpoint 是最直接的驗證：

> "Use curl to explore the new API endpoints you created"

「explore」這個詞很好用——Agent 會主動嘗試不同的 API 參數、邊界情況，快速覆蓋大範圍的行為。

**發現問題後怎麼辦？** Simon 的建議是：**用 Red/Green TDD 修正**。這樣不只修掉 bug，還能確保這個 case 被永久加進自動化測試中。

## 機制二：Browser Automation 測試 Web UI

如果是 Web UI，手動測試變得更重要——也更難。

過去 10 年，瀏覽器自動化工具已經大幅改善。現在的 Coding Agent 都很會用這些工具：

### Playwright：全功能瀏覽器自動化

[Playwright](https://playwright.dev/) 是目前最強大的選擇，由 Microsoft 開發，支援多語言、多瀏覽器引擎。

簡單一句話就能讓 Agent 開始用：

> "Test that with Playwright"

Agent 會自己選擇合適的語言 binding，或直接用 `playwright-cli`。

### agent-browser / Rodney：專為 Agent 設計的 CLI

- [**agent-browser**](https://github.com/vercel-labs/agent-browser)：Vercel 出品，基於 Playwright 的 Agent 專用 CLI
- [**Rodney**](https://github.com/simonw/rodney)：Simon Willison 的專案，直接用 Chrome DevTools Protocol 控制 Chrome

Simon 常用的 prompt：

> "Use uvx rodney --help to learn how to use Rodney. Test the new feature by starting a server, then opening it in Rodney. Look at screenshots."

這個 prompt 有三個巧妙之處：

1. **`uvx rodney --help`**：用 [uvx](https://docs.astral.sh/uv/guides/tools/) 自動安裝並執行，第一次呼叫就自動裝好
2. **`rodney --help` 本身就是 Agent 教學文件**：包含所有使用說明（[完整 help text](https://github.com/simonw/rodney/blob/main/help.txt)）
3. **「Look at screenshots」**：提示 Agent 用 vision model 檢查畫面

一句簡單的 prompt，就包含了完整的手動測試流程！

### 避免 Flaky Tests 的痛苦

傳統上，瀏覽器自動化測試很容易「脆弱」——HTML 微調就可能導致大量測試壞掉。

但當 **Coding Agent 負責維護這些測試** 時，更新測試的成本大幅降低，這讓瀏覽器測試變得更實用。

## 機制三：Showboat — 讓 Agent 記錄測試過程

測試不只是找 bug，也是**展示功能如何運作**的方式。

Simon 開發了 [Showboat](https://github.com/simonw/showboat) 來讓 Agent 記錄「手動測試」的完整流程：

> "Use uvx showboat --help to learn about Showboat. Document your testing with notes, commands, and screenshots."

Showboat 有三個核心指令：

1. **`note`**：寫 Markdown 筆記
2. **`exec`**：記錄指令 + 執行 + 記錄輸出
3. **`image`**：加入圖片（如 Rodney 抓的截圖）

其中 **`exec` 最重要**，因為它強迫 Agent 不能「作弊」——它會記錄真實的執行結果，而不是 Agent「希望」發生的事。

這樣的文件不只證明「測試過了」，還成為功能的**實際 demo 文件**。

## 實戰建議

1. **不要只依賴 Unit Test**：讓 Agent 跑一遍實際流程（CLI、curl、browser）
2. **用 `--help` 教學**：設計 CLI 工具時，把 Agent 需要的所有資訊放進 `--help`
3. **發現問題後用 TDD 修正**：確保 bug 被測試覆蓋
4. **記錄測試過程**：用 Showboat 或類似工具留下可驗證的 artifacts

## 總結

Agentic Manual Testing 的核心思想：

> **AI Agent 不只會寫測試，還會像人類一樣「試用」程式碼。**

這不是取代自動化測試，而是補足它的盲點。

當你把「手動測試」這件事也交給 Agent 時，你不只得到更可靠的程式碼，還得到可追溯的測試紀錄和 demo 文件。

這就是 Agentic Engineering 的威力：**不是用 AI 取代人類，而是讓 AI 做得跟人類一樣謹慎、全面。**

---

**延伸閱讀：**
- [Simon Willison: Agentic Engineering Patterns](https://simonwillison.net/guides/agentic-engineering-patterns/)
- [Rodney - Chrome DevTools CLI for Agents](https://github.com/simonw/rodney)
- [Showboat - Document Agent Testing](https://github.com/simonw/showboat)
