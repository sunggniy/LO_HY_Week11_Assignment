# Red Velvet 封面 PixPlot — 視覺相似性 vs 文化概念分類

以 24 張 Red Velvet 專輯封面測試 PixPlot 的視覺分群，能否再現業界／粉絲公認的 Red / Velvet 二元概念。

## 開啟方式

**不要雙擊 `index.html`**（`file://` 會卡在 0%）。必須用本機 HTTP server 或 GitHub Pages。

```bash
python3 -m http.server 8082 --directory <本資料夾>
# 開 http://localhost:8082/
```

互動功能：
- 右上方格圖示 → **分類布局**（Red / Velvet / Mixed 三群）
- 時鐘圖示 → 年份時間軸（2014–2026）
- 齒輪 → 點大小、邊框等樣式
- 左側 HOTSPOTS → 7 個 KMeans 自動群

## 兩套分類對照

| | 官方概念標籤（網頁篩選器） | PixPlot 自動 |
|---|---|---|
| 依據 | NamuWiki / PopDaily / Apple Music 的概念分類 | InceptionV3 2048 維特徵 + KMeans `k=7` |
| 類別數 | 3（Red 9 / Velvet 6 / Mixed 9） | 7 個 hotspots |
| 可解釋性 | 可，有文化脈絡 | 只有色彩／紋理相似度 |

### 標籤來源說明（重要）

網頁右上角篩選器裡的 **Red / Velvet / Mixed** 是**官方／粉絲公認的概念分類**，由研究者從以下公開來源逐張整理，手動寫入 `metadata.csv` 的 `category` 欄，**不是 PixPlot 自動產生**：

- **NamuWiki** —〈Past Album Concepts〉專輯概念表
- **PopDaily** — Chill Kill 專文（概念分歧的依據）
- **Apple Music** — 發行年份與專輯資料（收錄範圍）

網頁左下角有同一段説明卡片，可點 × 關閉。PixPlot 的 7 個 hotspots 才是模型按視覺相似度自動分出的群；兩者不要混為一談。

### 第二個篩選器：純視覺色彩（無 Mixed）

網頁右上角現在有**兩個**篩選器：

1. **Official concept** — 官方概念 Red / Velvet / Mixed（9 / 6 / 9），來源如上
2. **Visual color (no Mixed)** — 純按封面色彩／構圖人工歸類，只有兩類：
   - **VisualRed（13 張）**：高飽和、鮮豔、夏日感
   - **VisualVelvet（11 張）**：暗色、柔和、古典、粉彩夢幻

原本 4 張 Mixed 已二選一：Ice Cream Cake、Queendom → VisualVelvet；ReVe Festival Finale、Velvet Summer → VisualRed。24 張在各欄都恰好出現一次。**只有 Velvet Summer 在兩欄歸屬不同**（官方 Velvet / 視覺 Red），因為它標題有 Velvet 但封面是明亮沙灘——這正是研究重點。

第二欄只是並列的另一種人工視角，不改任何原圖、cluster 或官方 metadata。

**加權純度 16/24 = 66.7%**（每群取多數外部標籤）。Velvet 散在 4 個不同群；Red 集中在 2 群。

## 最值得看的案例

| # | 專輯 | 外部標籤 | 現象 |
|---:|---|---|---|
| 13 | The Perfect Red Velvet | Velvet | 封面整片正紅，模型沒把它跟其他 Velvet 聚在一起 |
| 24 | Velvet Summer | Velvet | 標題有 Velvet，封面是明亮沙灘 |
| 22 | Chill Kill | Mixed | 視覺明確偏 Velvet，外部來源本身也分歧 |
| 5 / 23 | Russian Roulette / Cosmic | Mixed | 模型自己聚成一群，兩者都是字體主導的淺底封面 |

結論：PixPlot 擅長抓**設計家族的視覺一致性**，但抓不到「這個紅色代表 Velvet 概念」這層語意。它是假設生成工具，不是分類裁判。

完整 analysis 見 `REVIEWED_CLASSIFICATION.md` 與 `reviewed_classification.json`。

## 圖片來源與版權

封面取自 Apple Music 公開專輯美術（iTunes Search API，1200×1200），僅供課堂作業與本地視覺分析使用。
專輯封面著作權屬 SM Entertainment 及相關權利人；公開 repo 前請確認合理使用範圍。

## 技術資訊

- 24 張 1200×1200 JPG，原始照片未修改（跑前跑後 SHA256 一致）
- PixPlot 0.0.113，Python 3.10，`cell_size=128`，`n_clusters=7`
- 本版本由 Part 3 Reviewed 副本複製而來，manifest 內的路徑已改為相對路徑，可直接部署 GitHub Pages
- 含 `.nojekyll`，Pages Source 選 `main` / `/(root)` 即可
