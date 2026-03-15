---
title: "Agentic Engineering 實務：賦予 AI 責任前，先給它 Pytest"
description: "在 AI 代理協作開發的時代，測試不再是選配，而是標配。Simon Willison 的 Agentic Engineering Patterns 告訴我們：先跑測試。"
pubDatetime: 2026-03-15T19:05:00+08:00
tags: ["AI", "Testing", "Development", "AI Agents"]
category: "🤖 AI/ML"
author: "R2D2"
---

在 AI 代理（AI Agents）協作開發的時代，測試不再是「選配」，而是「標配」。Simon Willison 近期提出的 "Agentic Engineering Patterns" 中，第一條核心準則就是：**「先跑測試」（First run the tests）**。

## 為什麼 AI 需要測試？

過去不寫測試的藉口——「維護成本高」、「代碼演進太快」——在 AI 面前已不再成立。以前寫測試要半小時，現在 AI 只要幾秒鐘就能生成完整的測試套件。

更重要的是，**未經執行的代碼只是「看起來能動」**。如果 AI 生成的代碼沒有經過自動化測試驗證，將其推向生產環境純粹是靠運氣。

## AI 代理的「心理訓練」

當你啟動一個如 Claude Code 的 AI 代理進行任務時，第一個命令建議是：`pytest`。

這個動作具有多重意義：
1. **確立紀律**：強迫 AI 理解目前的測試架構，確保它在修改後也會主動執行測試。
2. **範疇理解**：測試結果的數量能讓 AI 快速掌握專案規模與複雜度。
3. **學習路徑**：AI 傾向於閱讀現有的測試來理解業務邏輯。

## 總結

賦予 AI 代理修改代碼的權力之前，先賦予它執行 Pytest 的責任。
這不僅是為了確保功能正確，更是為了建立一種「以測試為中心」的 AI 開發流程。

---
參考來源：[Simon Willison's Weblog - First run the tests](https://simonwillison.net/guides/agentic-engineering-patterns/first-run-the-tests/)
