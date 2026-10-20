# Paul Skenes 投手分析（2025年）

2025年にサイ・ヤング賞を満票で受賞したポール・スキーンズの投球を、データで読み解いた分析です。

📝 解説記事（note）: https://note.com/tome_baseball/n/nd346073346bc

## 分析の問い

- なぜ、スキーンズは満票でサイ・ヤング賞を獲得したのか？
- 2024年（新人王）と比べて、投球内容はどう変わったのか？

## 使用データ

| データ | 出典 | 内容 |
|---|---|---|
| reference_2024 / 2025 | Baseball Reference | 年間の投手成績（IP、ERA、SO、WHIP、WARなど） |
| savant_2024 / 2025 | Baseball Savant（Statcast） | 年間の投球指標（K%、BB%、Whiff%、Hard-Hit%、xwOBA） |
| savant_pitch_type_2024 / 2025 | Baseball Savant（Statcast） | 球種別の使用率・Whiff%・Hard-Hit%・xwOBA |

- 対象期間：2024年・2025年レギュラーシーズン
- 取得日：【2026年9月27日～9月29日】
- 各サイトからCSVをダウンロードして使用しています。

## 使用技術

- Python（pandas、sqlite3）
- SQLite
- Google Colab

## 分析の流れ

1. 6本のCSVを pandas で読み込む
2. sqlite3 でデータベース（`skenes.db`）に登録する
3. SQLで必要な指標を抽出する（`SELECT`、別名（`AS`）、`UNION ALL` で2024年と2025年を縦に結合）
4. pandas で整形し、比較表を作成する

## ファイル構成

| ファイル | 内容 |
|---|---|
| paul_skenes_analysis.ipynb | 上記の分析一式（読み込み → DB登録 → SQL抽出 → 表の作成） |
| 2024_paul skines_data_reference.csv | 2024年の年間成績（Baseball Reference） |
| 2025_paul skines_data_reference.csv | 2025年の年間成績（Baseball Reference） |
| savant_2024_paul skenes.csv | 2024年の年間投球指標（Baseball Savant） |
| savant_2025_paul skenes.csv | 2025年の年間投球指標（Baseball Savant） |
| savant_2024_paul skenes(pitch type).csv | 2024年の球種別データ（Baseball Savant） |
| savant_2025_paul skenes(pitch type).csv | 2025年の球種別データ（Baseball Savant） |

## 実行方法

1. CSV6本を、ノートブックと同じ場所（Colabの作業フォルダ）に置く
2. paul_skenes_analysis.ipynb を Google Colab で開く
3. 上から順にセルを実行する

## 注意点・限界

- SQLの処理は基礎的な集計（抽出・結合）が中心です。統計的な検定や高度な分析は行っていません。
- 数値や解釈に誤りが含まれる可能性があります。

## 今後の改善予定

- 他の主要候補との比較を追加する
- 球種別のHard-Hit%とxwOBAの関係を深掘りする
- リーグ内での順位（パーセンタイル）を、データから計算して示す
