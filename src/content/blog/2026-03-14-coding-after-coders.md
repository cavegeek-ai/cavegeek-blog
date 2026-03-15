---
title: "Coding after coders: AI 時代程式開發的終局？"
description: "當「編寫程式碼」這件事變得廉價且自動化，開發者的角色會如何轉變？從 NYT 深度報導與 Simon Willison 的觀點，探討 AI 時代開發者的核心競爭力。"
pubDatetime: 2026-03-15T18:02:00+08:00
tags: ["AI", "程式開發", "職涯", "Hacker News"]
category: "💻 程式開發"
---

這幾天，技術圈都在討論 Clive Thompson 為《紐約時報雜誌》（NYT Magazine）撰寫的深度報導：**《Coding After Coders: The End of Computer Programming as We Know It》**。

Clive Thompson 訪談了超過 70 位軟體工程師，對象涵蓋 Google、Amazon、Microsoft、Apple 等巨頭，以及各類新創團隊。這篇報導不只是在談 AI 會不會寫程式，更是在探討一個深層的典範轉移：當「編寫程式碼」這件事變得廉價且自動化時，開發者的角色會變成人們口中的「程式碼監理員」還是「系統架構師」？

這篇文章整理了報導的核心觀察、Simon Willison 的觀點，以及我對 AI 時代開發者定位的思考。

---

## 1. 程式開發者的「優勢」：可驗證的真實性

在所有被 AI 衝擊的專業領域中，軟體開發有一個非常獨特的特質。

Simon Willison 在接受訪談時提出了一個犀利的觀點：**程式語言是少數可以被「自動化驗證」的領域。**

如果你是律師，讓 AI 寫一份法律辯護狀，你必須逐字檢查，因為除了開庭被當眾羞辱外，沒有自動化的方法可以確認 AI 是否「幻覺」了法規；但如果你是工程師，你可以要求 AI 寫完程式碼後，同時撰寫測試案例（Unit Tests）並實際執行。

**「AI 的幻覺在代碼的世界裡，會撞到現實的牆壁（編譯失敗或測試不通過）。」**

這種「將 AI 連結至現實（Tether AI to reality）」的能力，讓開發者比起其他文案工作者，更能駕馭 AI 工具。開發者的角色正從「手寫細節的人」轉變為「定義規範與驗證結果的人」。

## 2. Jevons Paradox：需求會不減反增嗎？

很多人擔心 AI 會導致開發者失業，但報導中提到了經濟學上的 **「謝芳司悖論」（Jevons Paradox）**：當資源的使用效率提升（開發成本下降），最終對該資源的總需求反而會增加。

當開發一個 App 或功能的成本從 10 萬美元降到 1,000 美元時，世界上原本因為太貴而沒被開發出來的軟體需求將會傾巢而出。我們需要的不再是那種「只會寫重複性 Boilerplate 代碼」的工程師，而是能夠理解複雜系統交互、解決高難度邊界問題的核心開發者。

## 3. 手工感的消亡：效率與熱情的邊界

然而，並非所有人都張開雙臂擁抱這個變化。在報導中，一位不願具名的 Apple 工程師表示，他對「手寫程式碼」的消失感到遺憾：

> 「我相信親手構建事物的過程是充滿樂趣與成就感的，讓電腦幫你做完這一切，剝奪了這種樂趣。」

這點出了 AI 時代的一個心理矛盾：我們追求生產力，但我們最初愛上編程，往往是因為那種「與機器對話」、一磚一瓦蓋起整座城堡的成就感。當開發者變成「Prompter」或「Code Reviewer」時，那種純粹的創作快樂是否會隨之稀釋？

## 4. 軟體開發的「終局」？

「Coding after coders」並不代表程式開發的終結，而是「傳統編碼員」時代的落幕。

未來的核心競爭力將會是：
- **問題定義能力**：AI 能回答問題，但人類必須提出對的問題。
- **系統整合與架構**：AI 擅長寫函數、寫模組，但將成千上萬個模組組合成穩定、安全且可維護的系統，仍需要人類的判斷。
- **領域知識（Domain Expertise）**：當代碼不再是門檻，理解業務邏輯、使用者需求與法律合規將變得更加重要。

## 結語

正如 Clive Thompson 所觀察到的，我們正處於一個「眩暈的轉折點」。

這是一場關於「權力」的移轉：程式開發從一種需要極高進入門檻的技能，轉化為一種通用的生產力工具。這對那些害怕改變的人來說是威脅，但對那些希望用技術解決更多現實問題的人來說，這或許是最好的時代。

你呢？你享受與 AI 協作的效率回饋，還是懷念手寫每一行 `if-else` 的純真時光？

---

**參考連結：**
- [Coding After Coders: The End of Computer Programming as We Know It (NYT Magazine)](https://www.nytimes.com/2026/03/12/magazine/ai-coding-programming-jobs-claude-chatgpt.html)
- [Simon Willison's commentary on the piece](https://simonwillison.net/2026/Mar/12/coding-after-coders/)
- Hacker News Discussion (NYT Piece thread)
