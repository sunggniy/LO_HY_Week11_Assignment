# Red Velvet 封面 — PixPlot 視覺分群 vs 文化概念分類

> 這份報告比較**三套分類**：外部給定的 Red/Velvet 概念、PixPlot 的自動視覺分群、以及人工檢視封面後的分組。
> 人工分組是 WorkBuddy 實際看過 24 張封面後寫的，**不是模型輸出**。自動分群原樣保留在 `output/data/hotspots/`，未修改。

## 基本資料

| 項目 | 內容 |
|---|---|
| 圖檔 | `~/Desktop/Red_Velvet_Album_Covers/`，24 張 1200×1200 JPG |
| Part 2 輸出 | `~/Desktop/RedVelvet_PixPlot_Trial_01/output/`（8.7 MB） |
| Reviewed 副本 | `~/Desktop/RedVelvet_PixPlot_Trial_01_Reviewed/output/`（點大小放大 3 倍） |
| 自動方法 | InceptionV3 2048 維特徵 → KMeans `k=7`（HDBSCAN 未安裝，自動回退） |
| 外部標籤來源 | NamuWiki「Past Album Concepts」表、PopDaily Chill Kill 專文、Apple Music |
| 外部標籤分布 | Red 9 / Velvet 6 / Mixed 9 |
| 原圖完整性 | 跑前跑後 SHA256 全數一致 |

## 核心發現：加權純度 66.7%

把每個自動 cluster 裡「最多的外部標籤」當作該群預測，16/24 張命中（66.7%）。
但**自動分群有 7 群，外部只有 3 類**——這個落差本身就是重點。

| 自動群 | 張數 | 外部標籤分布 | 多數標籤 | 純度 |
|---|---:|---|---|---:|
| C1 | 11 | Red 6 / Mixed 3 / Velvet 2 | Red | 55% |
| C2 | 3 | Velvet 2 / Mixed 1 | Velvet | 67% |
| C3 | 3 | Mixed 2 / Red 1 | Mixed | 67% |
| C4 | 2 | Mixed 2 | Mixed | 100% |
| C5 | 2 | Velvet 1 / Mixed 1 | Velvet | 50% |
| C6 | 2 | Red 2 | Red | 100% |
| C7 | 1 | Velvet 1 | Velvet | 100% |

**分布不對稱**：Red 集中在 C1(6) 與 C6(2)，共 8/9；Velvet 卻散在 C1(2)、C2(2)、C5(1)、C7(1) 四個不同群。
也就是說模型對 Red 的視覺把握較一致，對 Velvet 則沒有形成穩定群組。

## 四個關鍵衝突案例

| # | 專輯 | 外部標籤 | 人眼看到的 | 模型怎麼放 |
|---:|---|---|---|---|
| 13 | The Perfect Red Velvet | **Velvet** | 整片正紅、強烈對比 | 放進 C5，跟 Birthday(Mixed) 一起，**沒跟其他 Velvet 聚** |
| 24 | Velvet Summer | **Velvet** | 明亮沙灘、夏日感 | 放進 C2，跟 Perfect Velvet(暗色房子)、Queendom(粉彩氣球) 一起 |
| 22 | Chill Kill | Mixed | 黑底古典框、明確偏 Velvet | 放進最大的 C1（以 Red 為主） |
| 5 | Russian Roulette | Mixed | 淡藍底、只有字體 | 與 Cosmic 單獨成 C4（2 張、100% Mixed） |

**#13 是最有力的一張**：專輯名與官方概念都屬 Velvet，但封面是高飽和紅色。
模型讀到的是「紅」，人眼與產業標籤讀到的是「Velvet」。這直接證明視覺相似度≠文化概念。

## 模型做對的地方（要公平呈現）

- **C6**：把 ReVe Festival Day 1 與 Day 2 聚在一起（2 張、100% Red）。同一系列的美術設計相近，模型抓到了。
- **C4**：把 Russian Roulette 與 Cosmic 聚在一起（2 張、100% Mixed）。兩者都是字體主導的淺底封面。

所以模型不是完全亂分——它擅長抓**設計家族的視覺一致性**，但抓不到「這個紅色actually代表 Velvet 概念」。

## 人工視覺分組（5 組，24 張各一次）

| 組別 | 張數 | 索引 | 視覺證據 |
|---|---:|---|---|
| 高飽和紅與鮮豔暖色 | 5 | #2 #4 #9 #13 #19 | 大面積紅／桃紅、對比強烈；#13 封面整片正紅 |
| 暗色低明度與成熟戲劇感 | 5 | #1 #7 #11 #20 #22 | 黑／深褐／暗金、低飽和、構圖嚴肅；#1 為黑白 |
| 粉彩插畫與童趣夢幻 | 7 | #3 #8 #15 #16 #17 #21 #23 | 手繪／樂園／花草／夢幻元素，人物非寫實主體 |
| 柔和人像與留白空氣感 | 6 | #6 #10 #12 #14 #18 #24 | 人物為主體、光線柔和、留白多；#24 為明亮沙灘 |
| 文字主導極簡 | 1 | #5 | 幾乎只有字體與淺底色，無人物 |

## 工具限制（寫 reflection 要交代）

1. **`k=7` 是研究者給的**，不是資料自己決定的。外部只有 3 類，7 群必然會把概念拆碎或混在一起。
2. **UMAP 只決定畫面座標，不參與分群**。兩點靠近≠同一群；分群看的是 2048 維向量。
3. **小樣本會造出單張群**：C7 只有 RBB 一張，可能只是離群值，不是有意義的類別。
4. **`custom_hotspots` 會取代 `default_hotspots`**，PixPlot 不能並列顯示模型分群與人文分類；要並列得改 JS，Part 3 明確禁止，所以人工分組另存這份報告。
5. **外部標籤本身也有分歧**：Chill Kill 在 NamuWiki 是 Mixed、PopDaily 是 Velvet；Ice Cream Cake 雙主打分屬兩類。這不是模型的錯，是分類邊界本來就模糊。

## 可以直接寫進 reflection 的結論

PixPlot 把相似度變成可見空間，確實省去 24 張逐張比對，也找出 ReVe 系列與字體封面的視覺家族——這是它的**幫助**。
但它讀的是 InceptionV3 的色彩與紋理統計，不是概念：#13 的紅色封面被判為 Red 視覺，官方卻是 Velvet；Velvet 類散在四個群裡，**加權純度只有 66.7%**——這是它的**限制**。
因此 PixPlot 適合當**假設生成工具**，而不是分類的裁判；人文分類仍需外部脈絡與人工判讀，兩者並置才會顯出落差本身的意義。
