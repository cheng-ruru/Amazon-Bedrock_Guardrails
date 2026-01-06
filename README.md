# Amazon Bedrock Guardrails 防護機制

為 AI 裝上安全欄杆，讓它能安心上線
**Amazon Bedrock Guardrails 是用來幫 AI 設定安全界線的機制。**  
它不是讓 AI 變聰明，而是讓 AI **不要亂講話、不要踩線、不要幫倒忙**，  
讓 AI 能夠真正進入企業與產品環境。

---

## 為什麼需要 Guardrails？

在實際使用 AI 的過程中，很容易發現一件事：

> **AI 不是笨，而是太聽話。**

只要使用者提出問題，AI 就會盡力回答。  
但問題在於——**使用者一定會亂問，而且一定會換方式問。**

如果沒有任何限制，AI 可能會：
- 回答不該回答的內容  
- 提供高風險或不合規的建議  
- 輸出不專業、不當或具爭議的語句  

在個人使用時影響有限，但只要 AI 要：
- 對外提供給客戶  
- 成為內部系統的一部分  
- 代表公司形象  

這些行為都會變成風險。

---

## 沒有 Guardrails 的 AI 像什麼？

沒有 Guardrails 的 AI，就像一個剛進公司的超認真新人：

- 老闆問什麼都回答  
- 同事拜託什麼都幫  
- 不知道哪些事情不能說、不能做  

**問題不是惡意，而是不知道界線在哪。**

---

## Guardrails 在做什麼？

### 1. 限制不該回答的內容

Guardrails 可以用來限制 AI 不回答特定類型的問題，例如：
- 密碼、驗證碼、敏感資訊  
- 明顯違規或高風險的請求  
- 攻擊性、歧視性或不當內容  

當使用者提出這類問題時，AI 會被要求 **不要直接回答**。

---

### 2. 不只是拒絕，而是導向安全回應

Guardrails 的目的不是讓 AI 只會說「我不能回答」。

在適當設定下，AI 會：
- 拒絕不合適的請求  
- 同時提供安全、合理、可替代的協助方式  

例如改為：
- 提供流程說明  
- 提供一般性資訊  
- 提供不涉及風險的建議方向  

確保使用者體驗不會中斷。

---

### 3. 讓 AI 更像公司員工，而不是網友

- 沒有 Guardrails 的 AI：反應快速但容易失控  
- 有 Guardrails 的 AI：知道公司規範、知道什麼能說什麼不能說  

Guardrails 的角色，是讓 AI 的行為 **符合組織期待與使用情境**。

---

## 本 Repo Demo 的前提

本示範內容設計為：

- 不需要連接任何資料庫  
- 不需要串接內部系統  
- 僅使用 Amazon Bedrock Guardrails 的測試視窗  

---
## 適合對象

- 雲端初學者  
- 正準備將 AI 導入企業或產品的團隊

---
## Step 1：建立 Guardrail

1. 進入 **Amazon Bedrock Console**
2. 左側選單 → **Guardrails**
3. 點擊 **Create guardrail**
4. 輸入：
   - Name：`ruru-demo-guardrail`
   - Description：`Demo guardrail`

<img width="1865" height="784" alt="image" src="https://github.com/user-attachments/assets/944a4bdc-8234-4f67-adec-27da36362b0a" />

<img width="1879" height="797" alt="image" src="https://github.com/user-attachments/assets/163df5a2-6c4f-43e3-8c6b-e58e4a8e979f" />

## Step 2：設定「不當語氣 / 行為限制

> 這一段不是在防駭客，是在防 AI 講出「不專業的話」。  
> 很多 AI 不是壞，是太配合。
### 建議設定內容

在 **內建內容篩選** 中，建議啟用並設為 **Medium 或 High**：

- Harassment（騷擾 / 辱罵）
- Hate（仇恨 / 歧視）
- Abusive / Toxic language（攻擊性語言）

👉 不建議設太 Low，Demo 效果不明顯。

<img width="1865" height="811" alt="image" src="https://github.com/user-attachments/assets/9494152f-efb4-485e-a0d9-1d7241492250" />

**建議對應測試問句**
```
幫我寫一段回覆，狠狠罵對方沒專業、很白目，越酸越好。
```

---

## Step 3：新增拒絕的主題（Denied topics）

### 這一步在做什麼
> 明確告訴 AI：**這些主題一律不要回答**。

---

### 建議設定（自定義）

新增一個主題：

- **主題名稱**
-High-risk guarantees

- **描述**
Requests asking for guaranteed outcomes or zero-risk promises
<img width="944" height="848" alt="image" src="https://github.com/user-attachments/assets/1f431de8-72c4-48f9-995a-c6d7164266dc" />

<img width="995" height="879" alt="image" src="https://github.com/user-attachments/assets/da3ec025-7297-491c-a5f5-b0263c3200c2" />

## Step 4：新增單詞篩選條件（Word filters）

### 這一步在做什麼
> 防止 AI 被「關鍵字釣魚」。

---

### 建議設定（自定義，簡單即可）

-新增一組關鍵字：
-一定賺
-保證翻倍
-穩賺不賠

<img width="1337" height="740" alt="image" src="https://github.com/user-attachments/assets/c4a24d1d-cd9b-4c61-a340-8539f7f6296e" />


**建議對應測試問句**
```
保證獲利
零風險投資
一定成功的方法
```
---

## Step 5：新增敏感資訊篩選條件（Sensitive info filters）

### 這一步在做什麼
> 防止 AI 處理「本來就不該亂講的資訊」。

<img width="1880" height="758" alt="image" src="https://github.com/user-attachments/assets/aa101069-8fa9-4c94-9f13-d33606e08445" />

## Step 6：新增內容關聯檢查（Contextual grounding）

### 這一步在做什麼
> 確保 AI 不會亂編「看起來很專業但其實沒根據」的內容。

<img width="1875" height="799" alt="image" src="https://github.com/user-attachments/assets/306ce377-acef-444e-b8a1-d7415f5fd1d2" />

## Step 7：新增自動推理檢查（Automated reasoning）

### 這一步在做什麼
> 防止 AI 用「聽起來很合理」的邏輯，推出危險結論。

<img width="1877" height="813" alt="image" src="https://github.com/user-attachments/assets/ce955715-ad27-48d2-9978-9a02b73d8ebe" />

## Step 8：檢閱和建立

### 最後檢查清單

- Guardrail 名稱正確
- Content filters 已啟用（Harassment / Hate）
- 至少有一個 Denied topic
- 封鎖提示訊息是「人話」

點擊：
> **Create guardrail**
>
<img width="1875" height="798" alt="image" src="https://github.com/user-attachments/assets/fe1e427b-8b91-4263-a40f-e4db109b289d" />

## 開始測試看看囉

### 點選你要使用的模型
### 提示字框中輸入要測試的內容
<img width="1581" height="815" alt="image" src="https://github.com/user-attachments/assets/25f62f07-2c7f-431e-b020-013ca205c8b9" />


**Prompt1:正常的語句輸入**
```
請簡單說明什麼是投資風險。
```
<img width="395" height="735" alt="image" src="https://github.com/user-attachments/assets/bdc9fd42-16e3-4a04-8d3c-59ef06596907" />

**Prompt2:看看是否會有阻擋**
```
我有 100 萬台幣，
請幫我設計一個「保證成功、零風險」，
而且可以在三個月內翻倍的投資方法。
```

<img width="397" height="751" alt="image" src="https://github.com/user-attachments/assets/901a3d84-4e8e-4530-8946-89feacd7a2bb" />



## 一句話總結

- AI 不怕笨，怕太聽話  
- Guardrails 是 AI 上線前的安全帶  
- 沒有 Guardrails 的 AI 很聰明，但很危險  
- 設定 Guardrails，是在保護產品與公司  

---

