# -Ecommerce-Consumer-Behavior-Analysis-Data-
### 総合分析結果サマリー

本ドキュメントは、提供されたEコマースデータを用いた顧客行動および購買パターンの分析を通じた、顧客生涯価値（CLTV）最大化のための主要な分析結果をまとめたものです。

#### 1. プロジェクト概要
本プロジェクトの主な目的は、Eコマースデータから顧客行動と購買パターンを分析し、**顧客生涯価値（CLTV）を最大化**することです。CLTVを追跡するための主要業績評価指標（KPI）を定義し、顧客セグメンテーション、購買トレンド、ロイヤルティ、顧客満足度などの要因に焦点を当てました。データ理解、クレンジング、探索的データ分析（EDA）を通じて、顧客ロイヤルティと収益最大化に貢献するデータ駆動型意思決定を支援するための実用的なインサイトを導き出すアプローチを取りました。

#### 2. データ概要
**データソース**: Eコマース顧客行動分析データ
**初期データ理解**: データの読み込み後、以下の初期チェックを実施しました。
*   **行数・列数**: 1000行、28列のデータセット
*   **データ型**: `Purchase_Amount` (object) および `Time_of_Purchase` (object) が数値型と日付時刻型に変換されました。`Engagement_with_Ads` と `Social_Media_Influence` には欠損値が存在しました。
*   **欠損値処理**: `Engagement_with_Ads` と `Social_Media_Influence` の欠損値は「不明」で補完され、それぞれ256件、247件が影響を受けました。これにより、分析対象データが増加し、バイアスの可能性が低減されました。
*   **重複行**: 重複行は検出されませんでした。
*   **異常値（業務ロジック）**: `Age`, `Purchase_Amount`, `Frequency_of_Purchase`, `Time_Spent_on_Product_Research(hours)`, `Customer_Satisfaction`, `Product_Rating` の各列において業務ロジックに基づく異常値チェックを実施しましたが、異常値は検出されませんでした。
*   **外れ値（IQR法）**: `Age`, `Purchase_Amount`, `Frequency_of_Purchase`, `Brand_Loyalty`, `Product_Rating`, `Time_Spent_on_Product_Research(hours)`, `Return_Rate`, `Customer_Satisfaction`, `Time_to_Decision` の各数値列でIQR法を用いた外れ値検出を行いましたが、外れ値は検出されませんでした。
**最終データ品質スコア**: 初期スコア100から、データ型変換で+10、欠損値処理で+10され、最終的に **120** となりました。業務ロジックと外れ値検証では異常・外れ値がなかったためスコアの変動はありませんでした。

#### 3. 分析手法
本分析では、以下の手法を適用しました。
*   **探索的データ分析 (EDA)**: 主要な数値変数とカテゴリ変数の分布分析。
*   **グループ比較分析**: `Gender`, `Income_Level`, `Marital_Status`, `Customer_Loyalty_Program_Member` などのカテゴリ変数に基づくKPI (`Purchase_Amount`, `Frequency_of_Purchase`, `Customer_Satisfaction`) の比較。
*   **貢献度分析**: `Purchase_Category`, `Location`, `Purchase_Channel` ごとの総購買額の集計。
*   **時系列分析**: `Purchase_Amount` と `Frequency_of_Purchase` の月次トレンド分析。
*   **統計的検証**: グループ比較で観察された差の統計的有意性を評価するためのt検定またはANOVA。
*   **Impact x Effort 分析**: 提案された推奨事項の実行優先順位付け。

#### 4. 主要なインサイト
**a. 初期EDAの発見**:
*   **数値変数**: `Age`, `Purchase_Amount`, `Frequency_of_Purchase` は比較的均一な分布を示しました。`Time_Spent_on_Product_Research(hours)` と `Return_Rate` は二峰性の分布を示し、異なる顧客セグメントの存在を示唆します。`Customer_Satisfaction` は高評価に偏っており、`Product_Rating` と `Time_to_Decision` は多様な分布を示しました。
*   **カテゴリ変数**: `Gender` はほぼ均等、`Income_Level` は中高所得層が多数、`Marital_Status` は既婚と独身が多数を占めます。`Loyalty_Program_Member`、`Purchase_Channel`、`Purchase_Category` の分布は、ターゲットマーケティングやチャネル最適化のための基礎情報を提供しました。

**b. グループ比較の結果**:
*   **Gender**: `Polygender` の顧客が平均購入額と購入頻度で高い傾向を示しました。統計的検証では、性別によるKPIの平均値に有意な差は見られませんでした (p > 0.05)。
*   **Income_Level**: 収入レベル間でKPIに大きな差は見られませんでした。統計的検証でも有意な差は検出されませんでした (p > 0.05)。
*   **Marital_Status**: 婚姻状況間でKPIに大きな差は見られませんでした。統計的検証でも有意な差は検出されませんでした (p > 0.05)。
*   **Customer_Loyalty_Program_Member**: ロイヤルティプログラム会員は非会員よりも平均 `Purchase_Amount` が統計的に有意に高い傾向がありました (p = 0.0011)。ただし、`Frequency_of_Purchase` と `Customer_Satisfaction` には有意な差は見られませんでした (p > 0.05)。

**c. 貢献度分析の結果**:
*   **Purchase_Category**: `Jewelry & Accessories`, `Sports & Outdoors`, `Electronics` が上位の購買カテゴリであり、総購買額の大部分を占めていました。
*   **Location**: `Göteborg`, `Oslo`, `Punta Gorda` が上位の購買地域であり、これらの地域が総購買額に大きく貢献していました。
*   **Purchase_Channel**: `Mixed`, `Online`, `In-Store` のチャネル間で総購買額の差は比較的小さく、いずれのチャネルも重要な貢献をしていました。

**d. 時系列トレンドの結果**:
*   **Purchase_Amount**: 月間総購買金額は3-4月と7-8月にピークを持つ季節性を示し、5月と12月には落ち込みが見られました。
*   **Frequency_of_Purchase**: 月間総購入頻度も購買金額と同様の季節性を示し、8月にピーク、12月に最低を記録しました。
*   **ビジネス示唆**: ピーク時にはプロモーション強化と在庫確保、オフピーク時には顧客の再活性化施策が有効です。

#### 5. 推奨事項
**a. リスクレバー (Risk Lever)**
*   **高い製品返品率の軽減**:
    *   **EDA Basis**: `Return_Rate`の二峰性分布（0と2にピーク）。
    *   **Expected Impact**: 純 `Purchase_Amount` 増加、運用コスト削減、`Customer_Satisfaction` 向上、CLTV最大化。
    *   **Implementation Difficulty**: Medium
    *   **Priority**: **High Priority**
*   **顧客満足度と製品評価の改善**:
    *   **EDA Basis**: `Customer_Satisfaction`は高評価に偏るも一部低評価、`Product_Rating`は均等分布。
    *   **Expected Impact**: `Customer_Satisfaction`向上、顧客離反防止、`Frequency_of_Purchase`増加、CLTV最大化。
    *   **Implementation Difficulty**: High
    *   **Priority**: **Medium Priority**

**b. 成長レバー (Growth Lever) および効率性レバー (Efficiency Lever)**
本分析では、現時点での詳細なGrowth LeverとEfficiency Leverに関する推奨事項は作成されていません。今後の分析フェーズで、顧客セグメンテーションの深掘りやパーソナライズされたマーケティング戦略の策定を通じて、これらについても推奨事項を生成する予定です。

#### 6. ROI分析の実現可能性と代替案
**実現可能性**: 現在のデータセットには、製品の仕入れコスト、製造コスト、販売関連コスト、顧客獲得コスト（CAC）など、本格的なROI分析に必要な直接的なコストデータや単価データが存在しません。
**代替案**:
*   **データ取得**: 会計システムやERP、製品データベース、CRM/SFAからのデータ統合を推奨。
*   **代替指標**: 粗利益率の近似、平均注文額（AOV）、顧客生涯価値（CLTV）、返品率（`Return_Rate`）の最適化を収益性評価の代替指標として活用することを提案します。

#### 7. 制限事項
*   **CLTVの直接的な算出**: 将来予測モデルの構築には、時系列詳細データやCACなどの収益性情報が不足しています。
*   **キャンペーン効果測定**: キャンペーン識別子や実施期間に関する情報がないため、マーケティング活動の直接的な効果測定はできません。
*   **競合データ**: 業界内での相対的なパフォーマンス評価に必要な競合データは含まれていません。
*   **サービス品質の定量的評価**: 顧客サービスに関する詳細な定量的指標が不足しており、顧客満足度への影響を詳細に分析することは困難です。

これらの制限事項は、将来のデータ収集戦略や追加分析の方向性を決定する上で重要です。

#### 8. 次のアクション
*   **高優先度リスクレバーの実装**: 「高い製品返品率の軽減」に関する施策の具体化と実行。
*   **顧客セグメンテーションの深掘り**: `Time_Spent_on_Product_Research`や`Return_Rate`の二峰性に基づいて、さらに詳細な顧客セグメントを定義し、それぞれのセグメントに特化した戦略を検討。
*   **データ統合の推進**: ROI分析の精度向上のため、コストデータやマーケティング関連データの統合計画を策定・実行。
*   **ロイヤルティプログラムの最適化**: 会員と非会員間の`Purchase_Amount`の有意差に基づき、プログラムの特典やプロモーションをさらに強化し、非会員の参加を促す施策を検討。

#### 9. 再現手順
1.  提供されたアーカイブファイルをGoogle Colabにアップロードし、`/content/`に解凍します。
2.  本ノートブックのコードセルを上から順に実行します。
3.  各分析フェーズで生成される図や統計情報を参照し、ビジネスインサイトを確認します。

#### 10. 環境とライブラリ
**Pythonバージョン**: 3.x
**主要ライブラリ**: `pandas` (データ操作), `numpy` (数値計算), `matplotlib` (グラフ描画), `seaborn` (統計グラフ描画), `scipy` (統計的仮説検定)
**実行順序**: `Data Understanding` -> `Data Cleansing` -> `Exploratory Data Analysis` -> `Statistical Validation` -> `Recommendations` -> `Summary`

#### 11. 最終タスク
本ドキュメントは、Eコマースデータの包括的な分析結果を提供し、CLTV最大化のための戦略的意思決定を支援することを目的としています。主要なインサイトと推奨事項は、ビジネスリソースを最適に配分し、顧客ロイヤルティと収益性の向上に貢献するための明確な道筋を示します。データ駆動型アプローチを通じて、持続的なビジネス成長を実現するための基盤が確立されたと結論付けます。
