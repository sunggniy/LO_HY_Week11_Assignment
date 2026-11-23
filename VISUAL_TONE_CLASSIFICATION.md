# Red Velvet 封面：纯视觉分类（风格 × 色温）

> 这份分类只用人眼看到的色彩、构图与氛围来分组，**不使用 PixPlot 的 cluster，也不以官方 Red / Velvet / Mixed 作为分组依据**。官方标签只在最后一栏用来对照。

## 两个关键反例

| 封面 | 视觉风格 | 色温 | 为什么重要 |
|---|---|---|---|
| #22 Chill Kill | Velvet | 冷（黑 / 银 / 古典框） | 暗色、哥特、成熟构图，明显是 Velvet 语汇；但色温偏冷。PixPlot 没有把它放进 Velvet 为主的群，而是丢进最大、最混杂的 C1。 |
| #13 The Perfect Red Velvet（Psycho 时期） | Velvet（概念）/ Red（表面色彩） | 暖（正红 / 黑） | 官方与歌曲叙事都是 Velvet，但封面是高饱和暖红。PixPlot 把它和 Birthday 放进 C5，明显跟着“红色”走，而不是跟着“Velvet 概念”走。 |

> 注：资料夹里没有单独的 `Psycho.jpg`；#13 就是 `The Perfect Red Velvet`，主打曲为〈Psycho〉。若另有单独的 Psycho 单曲封面，可补进资料夹后重跑 PixPlot。

## 视觉风格 × 色温矩阵

| | 冷调 | 暖调 |
|---|---|---|
| **Red 感** | 5 张：Rookie、Cookie Jar、Summer Magic、Russian Roulette、ReVe Festival Day 2 | 6 张：Happiness、The Red、The Red Summer、SAPPY、ReVe Festival Day 1、Birthday |
| **Velvet 感** | 4 张：Perfect Velvet、Feel My Rhythm、**Chill Kill**、Cosmic（另：Be Natural 为黑白中性） | 4 张：The Velvet、RBB、Bloom、**Psycho / The Perfect Red Velvet** |
| **Mixed / 两者之间** | 3 张：Ice Cream Cake、ReVe Festival Finale、Queendom | 1 张：Velvet Summer |

关键点：**同样是 Velvet 感，可以冷（Chill Kill），也可以暖（Psycho / The Perfect Red Velvet）**。色温和概念是两条独立的轴；PixPlot 只抓到前者。

## 24 张逐张对照表

图例：R = Red 视觉；V = Velvet 视觉；M = 混合 / 难判。V* 表示“概念 Velvet，但表面色彩是 Red”。

| # | 专辑 | 视觉风格 | 色温 | 官方标签 | PixPlot 群 |
|---:|---|---|---|---|---|
| 1 | Be Natural | V | 中性（黑白） | Velvet | C1 |
| 2 | Happiness | R | 暖 | Red | C1 |
| 3 | Ice Cream Cake | M | 冷（粉彩） | Mixed | C1 |
| 4 | The Red | R | 暖 | Red | C1 |
| 5 | Russian Roulette | R（字体主导） | 冷（浅蓝） | Mixed | C4 |
| 6 | The Velvet | V | 暖（粉） | Velvet | C1 |
| 7 | Perfect Velvet | V | 冷（暗绿黑） | Velvet | C2 |
| 8 | Rookie | R | 冷（蓝天） | Red | C1 |
| 9 | The Red Summer | R | 暖（红橙） | Red | C3 |
| 10 | Cookie Jar | R | 冷（粉蓝） | Red | C1 |
| 11 | RBB | V | 暖（金褐） | Velvet | C7 |
| 12 | Summer Magic | R | 冷（蓝天） | Red | C1 |
| 13 | The Perfect Red Velvet（Psycho） | V* | 暖（正红） | Velvet | C5 |
| 14 | SAPPY | R | 暖（粉红绿） | Red | C1 |
| 15 | ReVe Festival Day 1 | R | 暖（橙黄） | Red | C6 |
| 16 | ReVe Festival Day 2 | R | 冷（粉蓝） | Red | C6 |
| 17 | ReVe Festival Finale | M | 冷（绿蓝） | Mixed | C3 |
| 18 | Queendom | M | 冷（蓝天） | Mixed | C2 |
| 19 | Birthday | R | 暖（桃红） | Mixed | C5 |
| 20 | Bloom | V | 暖（暗金） | Mixed | C1 |
| 21 | Feel My Rhythm | V | 冷（绿金） | Mixed | C3 |
| 22 | Chill Kill | V | 冷（黑银） | Mixed | C1 |
| 23 | Cosmic | V | 冷（粉蓝） | Mixed | C4 |
| 24 | Velvet Summer | M（夏日明亮） | 暖（阳光沙滩） | Velvet | C2 |

## 这组视觉分类改变了什么

- 纯视觉看，Velvet 感不只官方的 6 张，而是 **9 张**：多了 Bloom、Feel My Rhythm、Chill Kill、Cosmic；同时 Velvet Summer 看起来反而更像夏日 Red / Mixed。
- Velvet 内部明显分成冷暖两路：**冷路** = Perfect Velvet / Feel My Rhythm / Chill Kill / Cosmic；**暖路** = The Velvet / RBB / Bloom / Psycho。
- PixPlot 的表现正好印证限制：它把暖 Velvet（Psycho）和暖 Red（Birthday）放进 C5，却把冷 Velvet（Chill Kill）丢进混杂的 C1。它跟着色彩与纹理走，看不到“它们都属于 Velvet 视觉语汇”。

## 可直接写进 reflection 的一句话

即使把范围缩到纯视觉，PixPlot 仍会把概念相同但色温相反的两张封面分开：Chill Kill 是冷调 Velvet，Psycho 是暖调 Velvet，模型却没有把它们聚在一起。这说明它的限制不只是样本量或 `k=7` 的设定，而是方法本身只读取视觉统计，不读取概念。
