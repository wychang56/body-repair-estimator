# 外板鈑金修正指數計算器

依「Oddic 外板板金修正指數表」的邏輯做的網頁版計算器。純前端，不需要伺服器、不需要安裝任何東西，可以直接部署到 GitHub Pages。

車體部位圖直接取自你提供的原圖（車身外板件名稱與位置說明），裁成側／正／後／俯視圖四張，點擊區域疊在圖片上。

## 檔案結構

```
index.html          主頁面
assets/side.png      側視圖（車身左右側部位）
assets/front.png     正視圖（水箱護罩、大燈、保險桿等）
assets/rear.png      後視圖（行李箱蓋、尾燈、保險桿）
assets/top.png       俯視圖（前擋板、車頂、行李箱蓋）
```

**這四個檔案要一起部署，缺一張圖車身圖就會破圖（顯示不出來）。**

## 這個工具做了什麼

- 點車身圖上的部位（前保險桿、A/B/C 柱、前後葉子板、前後車門、側裙、引擎蓋、水箱護罩、大燈、行李箱蓋、尾燈⋯），自動新增一張部位卡片並帶入名稱
- 有左右之分的部位（葉子板、車門、側裙）用上方「左側／右側」切換鈕決定
- 每個部位可以加入多個損傷點，依形狀（矩形／圓形／三角形／多邊形／線狀）輸入尺寸，自動算出面積（dm²）
- 每個損傷點回答三題難易度判定（是／否），自動判斷 A／B／C 等級
- 同一部位多處損傷：面積取合計、難易度取最高等級
- 依「面積 × 難易度」查表得出修正指數，再乘上你設定的費率算出金額
- 可以列印估價單

## 這個工具沒做的

- 骨體作業（原手冊有提到，但沒有給出零件與工時對照數據，無法還原）
- 車輛基本資料建檔、估價記錄查詢（原系統的資料庫功能，此版本不含資料庫）

## 部署到 GitHub Pages（約 5 分鐘）

**如果你還沒有這個專案的 GitHub Repo：**

1. 到 https://github.com/new 建立一個新 repo（例如叫 `body-repair-estimator`），Public 或 Private 都可以（但 Pages 免費方案要 Public 才能開啟網站功能，除非你是 GitHub Pro/Team）
2. 在你電腦上，打開終端機，進到放 `index.html` 和 `assets/` 資料夾的目錄，執行：

```bash
git init
git add index.html assets README.md
git commit -m "外板鈑金修正指數計算器"
git branch -M main
git remote add origin https://github.com/你的帳號/body-repair-estimator.git
git push -u origin main
```

3. 到 repo 頁面 → **Settings** → 左側選單 **Pages**
4. 「Build and deployment」的 Source 選 **Deploy from a branch**，Branch 選 **main** / **/(root)**，按 **Save**
5. 等 1～2 分鐘，網址會出現在同一頁最上方，通常是：
   `https://你的帳號.github.io/body-repair-estimator/`

**如果你已經有 repo：** 把 `index.html` 和整個 `assets/` 資料夾複製進去，`git add / commit / push` 即可，Pages 設定只要做一次。

## 之後想自己修改

樣式在 `<style>`、邏輯在 `<script>`，用任何文字編輯器（VS Code）打開改完存檔、`git add . && git commit -m "更新" && git push` 就會自動更新網站。

常見會想調整的地方：
- 費率預設值：搜尋 `id="rateInput"` 那行的 `value="800"`
- 對照表數值：搜尋 `var TABLE = [`
- 難易度三個問題文字：搜尋 `var QUESTIONS = [`
- 車身圖點擊區域位置：搜尋 `class="hotspot"`，每個熱區用 `left/top/width/height` 百分比定位，對照對應圖片調整即可

