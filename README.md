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

| | 外部給定 | PixPlot 自動 |
|---|---|---|
| 依據 | NamuWiki / PopDaily / Apple Music 的概念分類 | InceptionV3 2048 維特徵 + KMeans `k=7` |
| 類別數 | 3（Red 9 / Velvet 6 / Mixed 9） | 7 個 hotspots |
| 可解釋性 | 可，有文化脈絡 | 只有色彩／紋理相似度 |

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
