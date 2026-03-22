# 第7章 データ分析と可視化

---

## 学習目標

本章を学ぶことで、以下の能力を身につけることができる。

1. **AIを活用したデータ分析ワークフロー（前処理→分析→可視化）を実践できる** — 研究データの読み込みから結果のグラフ作成までを一貫して行えるようになる
2. **論文品質のグラフを効率的に作成できる** — 学会発表や論文投稿に耐えうる高品質な可視化を、AIの力を借りて短時間で作成する
3. **統計的検定の基礎と適切な手法選択を理解する** — データに応じた正しい統計手法を選び、結果を正しく解釈できる力を養う

---

## 7.1 研究におけるデータ分析

### 7.1.1 なぜデータ分析が重要か

大学院での研究において、データ分析は以下の場面で不可欠な役割を果たす。

1. **実験結果の解釈**: 収集したデータから意味のあるパターンを見出す
2. **仮説の検証**: 統計的手法により、仮説が支持されるかを客観的に判断する
3. **論文の説得力**: 適切な分析と可視化は、論文の査読者を説得する強力な武器である
4. **新たな発見**: 探索的データ分析（EDA）により、予想外の知見が得られることがある

データ分析のスキルは、理系・文系を問わず、現代の大学院生に求められる基本能力である。心理学の実験データ、社会調査の回答データ、生物学の測定データ、工学のシミュレーション結果――あらゆる研究分野でデータ分析が行われている。

### 7.1.2 AIがデータ分析をどう変えるか

従来、データ分析を行うには、プログラミング言語（Python, R等）の習得に多くの時間を要した。AIの登場により、この障壁は大幅に低下している。

**AIが特に役立つ場面:**

- **分析コードの生成**: 「このデータでt検定を行いたい」と伝えるだけで、コードが得られる
- **手法の選択支援**: データの特性を伝えると、適切な統計手法を提案してくれる
- **グラフの作成**: 「論文に載せる棒グラフを作って」という指示で、出版品質のグラフコードが得られる
- **結果の解釈**: 統計結果の意味を平易な言葉で説明してもらえる

ただし、**AIはあくまで道具であり、分析の設計と結果の解釈は研究者の責任である**。本章では、AIの力を正しく活用しつつ、データ分析の基礎力を養うことを目指す。

---

## 7.2 データ分析ワークフロー

### 7.2.1 Step 1: データの理解と前処理

データ分析の第一歩は、手元のデータを正しく理解することである。

**プロンプト例: CSVデータの概要分析コード生成**

```
以下のCSVファイルを読み込み、データの概要を把握するPythonスクリプトを作成してください。

ファイル: experiment_results.csv
使用ライブラリ: pandas

以下の情報を出力してください:
1. データの形状（行数×列数）
2. 各列のデータ型
3. 最初の5行の表示
4. 基本統計量（数値列: 平均・標準偏差・最小・最大、カテゴリ列: ユニーク数・最頻値）
5. 欠損値の数と割合（列ごと）
6. 各数値列のヒストグラム
```

**AIが生成するコードの例:**

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np


def explore_data(file_path: str) -> pd.DataFrame:
    """CSVファイルを読み込み、データの概要を表示する"""

    # データ読み込み
    df = pd.read_csv(file_path)

    # 1. データの形状
    print("=" * 50)
    print(f"データの形状: {df.shape[0]}行 × {df.shape[1]}列")
    print("=" * 50)

    # 2. 各列のデータ型
    print("\n【データ型】")
    print(df.dtypes.to_string())

    # 3. 最初の5行
    print("\n【最初の5行】")
    print(df.head().to_string())

    # 4. 基本統計量
    print("\n【基本統計量（数値列）】")
    print(df.describe().to_string())

    print("\n【カテゴリ列の情報】")
    cat_cols = df.select_dtypes(include=["object", "category"]).columns
    for col in cat_cols:
        print(f"\n  {col}:")
        print(f"    ユニーク数: {df[col].nunique()}")
        print(f"    最頻値: {df[col].mode().iloc[0]}")
        print(f"    値の分布:\n{df[col].value_counts().to_string()}")

    # 5. 欠損値
    print("\n【欠損値】")
    missing = df.isnull().sum()
    missing_pct = (missing / len(df) * 100).round(2)
    missing_df = pd.DataFrame({
        "欠損数": missing,
        "欠損率(%)": missing_pct
    })
    print(missing_df[missing_df["欠損数"] > 0].to_string())
    if missing.sum() == 0:
        print("  欠損値なし")

    # 6. ヒストグラム
    num_cols = df.select_dtypes(include=[np.number]).columns
    if len(num_cols) > 0:
        fig, axes = plt.subplots(1, len(num_cols),
                                  figsize=(5 * len(num_cols), 4))
        if len(num_cols) == 1:
            axes = [axes]
        for ax, col in zip(axes, num_cols):
            df[col].hist(ax=ax, bins=20, edgecolor="black")
            ax.set_title(col)
            ax.set_xlabel("値")
            ax.set_ylabel("頻度")
        plt.tight_layout()
        plt.savefig("data_overview_histograms.png", dpi=150)
        plt.show()

    return df
```

**欠損値処理の主な方法:**

| 方法 | 適用場面 | Pythonコード |
|------|---------|------------|
| 行の削除 | 欠損が少ない場合 | `df.dropna()` |
| 平均値補完 | 正規分布に近いデータ | `df.fillna(df.mean())` |
| 中央値補完 | 外れ値がある場合 | `df.fillna(df.median())` |
| 前方補完 | 時系列データ | `df.fillna(method='ffill')` |
| 多重代入法 | 欠損が多い場合 | `from sklearn.impute import IterativeImputer` |

**外れ値検出のプロンプト例:**

```
以下のDataFrameの数値列について、外れ値を検出するコードを作成してください。
外れ値の定義: IQR法（Q1 - 1.5*IQR 未満、または Q3 + 1.5*IQR 超過）
外れ値がある行を表示し、箱ひげ図で可視化してください。
```

### 7.2.2 Step 2: 探索的データ分析（EDA）

探索的データ分析（Exploratory Data Analysis, EDA）は、データの構造やパターンを視覚的に把握するプロセスである。

**相関分析のプロンプト例:**

```
以下のDataFrameについて、探索的データ分析（EDA）を行うPythonコードを作成してください。

分析内容:
1. 数値列間の相関行列の計算とヒートマップの作成
2. 各数値列の分布（ヒストグラム + 正規分布フィット）
3. カテゴリ列ごとのグループ別統計量
4. 主要な変数間の散布図マトリクス

使用ライブラリ: pandas, matplotlib, seaborn
グラフは日本語フォントに対応させてください。
```

**AIが生成するEDAコードの例:**

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats

# 日本語フォント設定
plt.rcParams["font.family"] = "Hiragino Sans"  # macOS
# plt.rcParams["font.family"] = "MS Gothic"    # Windows


def perform_eda(df: pd.DataFrame, output_dir: str = "./eda_results"):
    """探索的データ分析を実行する"""
    import os
    os.makedirs(output_dir, exist_ok=True)

    num_cols = df.select_dtypes(include=[np.number]).columns.tolist()
    cat_cols = df.select_dtypes(include=["object", "category"]).columns.tolist()

    # 1. 相関行列ヒートマップ
    if len(num_cols) >= 2:
        fig, ax = plt.subplots(figsize=(10, 8))
        corr_matrix = df[num_cols].corr()
        sns.heatmap(corr_matrix, annot=True, fmt=".2f",
                    cmap="RdBu_r", center=0, vmin=-1, vmax=1,
                    square=True, ax=ax)
        ax.set_title("相関行列", fontsize=14)
        plt.tight_layout()
        plt.savefig(f"{output_dir}/correlation_heatmap.png", dpi=300)
        plt.close()
        print("相関行列を保存しました")

        # 強い相関の報告
        print("\n【強い相関（|r| > 0.5）】")
        for i in range(len(corr_matrix)):
            for j in range(i + 1, len(corr_matrix)):
                r = corr_matrix.iloc[i, j]
                if abs(r) > 0.5:
                    print(f"  {corr_matrix.index[i]} × "
                          f"{corr_matrix.columns[j]}: r = {r:.3f}")

    # 2. 分布の確認
    n_num = len(num_cols)
    if n_num > 0:
        fig, axes = plt.subplots(1, n_num, figsize=(5 * n_num, 4))
        if n_num == 1:
            axes = [axes]
        for ax, col in zip(axes, num_cols):
            data = df[col].dropna()
            ax.hist(data, bins=25, density=True, alpha=0.7,
                    edgecolor="black", label="データ")
            # 正規分布フィット
            mu, sigma = data.mean(), data.std()
            x = np.linspace(data.min(), data.max(), 100)
            ax.plot(x, stats.norm.pdf(x, mu, sigma),
                    "r-", linewidth=2, label="正規分布フィット")
            ax.set_title(f"{col} の分布")
            ax.legend()
            # Shapiro-Wilk 検定
            if len(data) <= 5000:
                stat, p = stats.shapiro(data)
                normality = "正規" if p > 0.05 else "非正規"
                ax.text(0.05, 0.95, f"Shapiro-Wilk p={p:.4f}\n({normality})",
                        transform=ax.transAxes, va="top", fontsize=9)
        plt.tight_layout()
        plt.savefig(f"{output_dir}/distributions.png", dpi=300)
        plt.close()

    # 3. カテゴリ別統計量
    if cat_cols and num_cols:
        print("\n【カテゴリ別統計量】")
        for cat in cat_cols:
            print(f"\n  グループ変数: {cat}")
            summary = df.groupby(cat)[num_cols].agg(["mean", "std", "count"])
            print(summary.to_string())

    # 4. 散布図マトリクス
    if len(num_cols) >= 2:
        plot_cols = num_cols[:5]  # 多すぎる場合は5列まで
        if cat_cols:
            g = sns.pairplot(df, vars=plot_cols, hue=cat_cols[0],
                            diag_kind="kde", height=2.5)
        else:
            g = sns.pairplot(df, vars=plot_cols,
                            diag_kind="kde", height=2.5)
        g.savefig(f"{output_dir}/pairplot.png", dpi=300)
        plt.close()
        print("散布図マトリクスを保存しました")
```

### 7.2.3 Step 3: 統計的検定

研究の仮説を検証するためには、適切な統計的検定を行う必要がある。以下に、よく使われる検定手法とその選び方を示す。

**統計的検定の選び方フローチャート:**

```
データは正規分布に従うか？
├── はい → 2群比較か？
│   ├── はい → 対応のあるデータか？
│   │   ├── はい → 対応のあるt検定
│   │   └── いいえ → 独立2標本t検定
│   └── いいえ → 3群以上の比較
│       ├── 対応のあるデータ → 反復測定分散分析
│       └── 対応なし → 一元配置分散分析（ANOVA）
└── いいえ → 2群比較か？
    ├── はい → 対応のあるデータか？
    │   ├── はい → Wilcoxon符号順位検定
    │   └── いいえ → Mann-Whitney U検定
    └── いいえ → 3群以上の比較
        └── Kruskal-Wallis検定

カテゴリデータ同士の関連 → カイ二乗検定
```

**正規性の確認を含めた統計検定のプロンプト例:**

```
以下のデータについて、2群間の平均値の差を検定するPythonコードを作成してください。

データ構造:
- DataFrame に "group" 列（"control" と "treatment"）と "score" 列がある
- 各群の被験者数は異なる可能性がある

処理手順:
1. 各群のデータの正規性を Shapiro-Wilk 検定で確認
2. 等分散性を Levene 検定で確認
3. 結果に応じて適切な検定を自動選択:
   - 両群とも正規分布 & 等分散 → Studentのt検定
   - 両群とも正規分布 & 不等分散 → Welchのt検定
   - 非正規分布あり → Mann-Whitney U検定
4. 効果量（Cohen's d または r）を計算
5. 結果を分かりやすくレポート出力

使用ライブラリ: scipy.stats, pandas, numpy
```

**AIが生成する検定コードの例:**

```python
import pandas as pd
import numpy as np
from scipy import stats


def compare_two_groups(df: pd.DataFrame,
                       group_col: str,
                       value_col: str,
                       alpha: float = 0.05) -> dict:
    """
    2群間の平均値の差を適切な検定で検定する。

    Parameters
    ----------
    df : pd.DataFrame
        データフレーム
    group_col : str
        群を示す列名
    value_col : str
        比較する数値列名
    alpha : float
        有意水準（デフォルト: 0.05）

    Returns
    -------
    dict
        検定結果を含む辞書
    """
    groups = df[group_col].unique()
    if len(groups) != 2:
        raise ValueError(f"2群が必要ですが、{len(groups)}群あります")

    group1 = df[df[group_col] == groups[0]][value_col].dropna()
    group2 = df[df[group_col] == groups[1]][value_col].dropna()

    results = {
        "group1_name": groups[0],
        "group2_name": groups[1],
        "group1_n": len(group1),
        "group2_n": len(group2),
        "group1_mean": group1.mean(),
        "group2_mean": group2.mean(),
        "group1_std": group1.std(),
        "group2_std": group2.std(),
    }

    # 1. 正規性の検定（Shapiro-Wilk）
    if len(group1) >= 3:
        sw1_stat, sw1_p = stats.shapiro(group1)
    else:
        sw1_stat, sw1_p = np.nan, 0.0  # サンプル不足
    if len(group2) >= 3:
        sw2_stat, sw2_p = stats.shapiro(group2)
    else:
        sw2_stat, sw2_p = np.nan, 0.0

    results["shapiro_group1_p"] = sw1_p
    results["shapiro_group2_p"] = sw2_p
    normal1 = sw1_p > alpha
    normal2 = sw2_p > alpha
    both_normal = normal1 and normal2

    # 2. 等分散性の検定（Levene）
    lev_stat, lev_p = stats.levene(group1, group2)
    results["levene_p"] = lev_p
    equal_var = lev_p > alpha

    # 3. 適切な検定の選択と実行
    if both_normal:
        if equal_var:
            test_name = "Studentのt検定"
            t_stat, p_value = stats.ttest_ind(group1, group2,
                                               equal_var=True)
        else:
            test_name = "Welchのt検定"
            t_stat, p_value = stats.ttest_ind(group1, group2,
                                               equal_var=False)
        results["test_statistic"] = t_stat

        # Cohen's d
        pooled_std = np.sqrt(
            ((len(group1) - 1) * group1.std()**2 +
             (len(group2) - 1) * group2.std()**2) /
            (len(group1) + len(group2) - 2)
        )
        cohens_d = (group1.mean() - group2.mean()) / pooled_std
        results["effect_size"] = abs(cohens_d)
        results["effect_size_type"] = "Cohen's d"
    else:
        test_name = "Mann-Whitney U検定"
        u_stat, p_value = stats.mannwhitneyu(group1, group2,
                                              alternative="two-sided")
        results["test_statistic"] = u_stat

        # 効果量 r
        n = len(group1) + len(group2)
        z = stats.norm.ppf(p_value / 2)
        r = abs(z) / np.sqrt(n)
        results["effect_size"] = r
        results["effect_size_type"] = "r"

    results["test_name"] = test_name
    results["p_value"] = p_value
    results["significant"] = p_value < alpha

    # 効果量の解釈
    es = results["effect_size"]
    if results["effect_size_type"] == "Cohen's d":
        if es < 0.2:
            interpretation = "ごく小さい（negligible）"
        elif es < 0.5:
            interpretation = "小さい（small）"
        elif es < 0.8:
            interpretation = "中程度（medium）"
        else:
            interpretation = "大きい（large）"
    else:  # r
        if es < 0.1:
            interpretation = "ごく小さい（negligible）"
        elif es < 0.3:
            interpretation = "小さい（small）"
        elif es < 0.5:
            interpretation = "中程度（medium）"
        else:
            interpretation = "大きい（large）"
    results["effect_interpretation"] = interpretation

    # レポート出力
    print("=" * 60)
    print("2群間比較の検定結果")
    print("=" * 60)
    print(f"群1: {groups[0]} (n={len(group1)}, "
          f"M={group1.mean():.3f}, SD={group1.std():.3f})")
    print(f"群2: {groups[1]} (n={len(group2)}, "
          f"M={group2.mean():.3f}, SD={group2.std():.3f})")
    print("-" * 60)
    print(f"正規性（Shapiro-Wilk）: "
          f"{groups[0]} p={sw1_p:.4f} ({'正規' if normal1 else '非正規'}), "
          f"{groups[1]} p={sw2_p:.4f} ({'正規' if normal2 else '非正規'})")
    print(f"等分散性（Levene）: p={lev_p:.4f} "
          f"({'等分散' if equal_var else '不等分散'})")
    print(f"使用検定: {test_name}")
    print(f"検定統計量 = {results['test_statistic']:.4f}")
    print(f"p値 = {p_value:.4f}")
    print(f"効果量 ({results['effect_size_type']}) = {es:.4f} "
          f"({interpretation})")
    print("-" * 60)
    if results["significant"]:
        print(f"結論: 有意水準{alpha}で統計的に有意な差が認められた (p < {alpha})")
    else:
        print(f"結論: 有意水準{alpha}で統計的に有意な差は認められなかった (p >= {alpha})")
    print("=" * 60)

    return results
```

**p値の正しい解釈:**

p値は「帰無仮説が正しいと仮定した場合に、観察されたデータと同程度またはそれ以上に極端な結果が得られる確率」である。よくある誤解を以下にまとめる。

| 誤った解釈 | 正しい解釈 |
|-----------|-----------|
| p = 0.03は「差がある確率が97%」 | 帰無仮説の下でこの結果が得られる確率が3% |
| p < 0.05は「重要な差がある」 | 統計的に有意だが、実用的な重要性は効果量で判断 |
| p = 0.06は「差がない」 | 有意水準を超えただけで、差がないとは限らない |
| p値が小さいほど効果が大きい | p値はサンプルサイズの影響を受ける。効果量を見るべき |

---

## 7.3 論文品質のグラフ作成

### 7.3.1 matplotlib / seaborn の基本

Pythonでグラフを作成するための2大ライブラリが matplotlib と seaborn である。

- **matplotlib**: 低レベルの描画ライブラリ。細かいカスタマイズが可能
- **seaborn**: matplotlib の上位ライブラリ。統計的な可視化に特化し、美しいデフォルト設定を持つ

### 7.3.2 効果的なグラフの選び方

| データの性質 | 推奨グラフ | 用途 |
|------------|-----------|------|
| カテゴリ別の量的比較 | 棒グラフ（エラーバー付き） | 群間比較の結果表示 |
| 2変数の関係 | 散布図 | 相関関係の可視化 |
| 分布の比較 | 箱ひげ図 / バイオリンプロット | 群間の分布の違い |
| 変数間の関連 | ヒートマップ | 相関行列の可視化 |
| 時系列データ | 折れ線グラフ | 時間変化の表示 |
| 割合・構成比 | 積み上げ棒グラフ | カテゴリの内訳表示 |

### 7.3.3 論文に必要なグラフの要素

学術論文や学会発表のグラフには、以下の要素が不可欠である。

```
必須要素:
□ 明確な軸ラベル（単位を含む）
□ 適切なタイトル（Figure 1: ... の形式）
□ 凡例（複数系列の場合）
□ エラーバー（平均値を示す場合、標準誤差または95%信頼区間）
□ 適切なフォントサイズ（本文と同程度、最低8pt）
□ 高解像度（300dpi以上）

推奨要素:
□ グリッド線（読み取りやすさ向上）
□ 有意差マーク（* p < 0.05, ** p < 0.01, *** p < 0.001）
□ 個々のデータ点のプロット（小標本の場合）
□ 図の下部にキャプション
```

### 7.3.4 白黒印刷対応のグラフ設計

多くの学術論文は白黒で印刷されることがあるため、色だけに頼らないデザインが重要である。

**対応テクニック:**

1. **ハッチパターン**: 棒グラフにストライプや格子模様を加える
2. **マーカーの形状**: 散布図で○、△、□など異なるマーカーを使う
3. **線のスタイル**: 折れ線グラフで実線、破線、点線を使い分ける
4. **コントラスト**: 色を使う場合も、白黒にしたときに区別できるコントラストを確保する

### 7.3.5 AIでグラフ作成コードを生成するプロンプト例

**棒グラフ（群間比較）のプロンプト:**

```
以下の仕様で論文品質の棒グラフを作成するPythonコードを書いてください。

データ:
- 3群（Control, Treatment A, Treatment B）
- 各群の平均値と標準誤差がある

グラフの要件:
- matplotlib + seaborn を使用
- 白背景、枠線あり
- エラーバー（標準誤差）付き
- 各棒に異なるハッチパターン（白黒印刷対応）
- 有意差を示すブラケットと * マーク
- フォントサイズ: タイトル14pt、軸ラベル12pt、目盛り10pt
- 解像度 300dpi で PNG 保存
- 図のサイズ: 幅8cm × 高さ6cm（単カラム論文用）
- 日本語フォント対応
```

**AIが生成する論文品質グラフコードの例:**

```python
import matplotlib.pyplot as plt
import matplotlib.patches as mpatches
import numpy as np

# 日本語フォント設定
plt.rcParams["font.family"] = "Hiragino Sans"
plt.rcParams["axes.unicode_minus"] = False

# データ
groups = ["統制群", "処置A群", "処置B群"]
means = [72.3, 81.5, 85.2]
sems = [2.1, 2.8, 2.5]  # 標準誤差

# グラフ作成
fig, ax = plt.subplots(figsize=(8/2.54, 6/2.54), dpi=300)  # cm → inch変換

# 棒グラフ（ハッチパターン付き）
hatches = ["", "///", "xxx"]
colors = ["#CCCCCC", "#888888", "#444444"]
bars = ax.bar(groups, means, yerr=sems, capsize=4,
              color=colors, edgecolor="black", linewidth=0.8)
for bar, hatch in zip(bars, hatches):
    bar.set_hatch(hatch)

# 有意差ブラケット
def add_significance_bracket(ax, x1, x2, y, h, text):
    """有意差を示すブラケットを描画する"""
    ax.plot([x1, x1, x2, x2], [y, y+h, y+h, y],
            lw=1.0, color="black")
    ax.text((x1+x2)/2, y+h, text, ha="center", va="bottom", fontsize=8)

add_significance_bracket(ax, 0, 1, 88, 1.5, "*")
add_significance_bracket(ax, 0, 2, 93, 1.5, "**")

# 軸の設定
ax.set_ylabel("テストスコア（点）", fontsize=10)
ax.set_ylim(0, 105)
ax.tick_params(labelsize=8)
ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)

plt.tight_layout()
plt.savefig("group_comparison.png", dpi=300, bbox_inches="tight")
plt.savefig("group_comparison.pdf", bbox_inches="tight")  # PDF版も保存
plt.show()

print("グラフを保存しました: group_comparison.png, group_comparison.pdf")
```

**箱ひげ図 + データ点のプロンプト:**

```
2群のスコア分布を比較する箱ひげ図を作成してください。

要件:
- seaborn の boxplot + stripplot を重ね合わせる
- 個々のデータ点を半透明のドットで表示
- 中央値、四分位範囲が明確に分かるようにする
- 白黒印刷対応（グレースケール）
- 論文品質（300dpi、適切なフォントサイズ）
```

**散布図 + 回帰直線のプロンプト:**

```
2変数（学習時間 vs テストスコア）の散布図を作成してください。

要件:
- 回帰直線とその95%信頼区間を表示
- 相関係数 r と p 値をグラフ内に表示
- 群ごとに異なるマーカー（○と△）で色分け
- 凡例を右下に配置
- 論文品質（300dpi、フォントサイズ適切）
```

---

## 7.4 インタラクティブ可視化

### 7.4.1 Plotlyの紹介

Plotly は、インタラクティブなグラフを作成するライブラリである。マウスオーバーで値を表示したり、ズーム・パンができるため、データの探索段階で特に有用である。

**プロンプト例:**

```
Plotly を使って、以下のインタラクティブな可視化を作成してください。

1. 散布図: x軸 = 変数A, y軸 = 変数B, 色 = グループ
   - マウスオーバーで被験者IDと全変数値を表示
2. 3D散布図: 主成分分析の結果（PC1, PC2, PC3）をプロット
3. HTMLファイルとして保存（ブラウザで開ける形式）
```

```python
import plotly.express as px
import plotly.graph_objects as go

# インタラクティブ散布図
fig = px.scatter(
    df, x="variable_a", y="variable_b",
    color="group",
    hover_data=["subject_id", "age", "score"],
    title="変数Aと変数Bの関係",
    labels={"variable_a": "変数A", "variable_b": "変数B"}
)
fig.update_layout(
    font=dict(size=14),
    hoverlabel=dict(font_size=12)
)
fig.write_html("interactive_scatter.html")
fig.show()
```

### 7.4.2 Bokehの紹介

Bokeh も強力なインタラクティブ可視化ライブラリである。特に、大量のデータ点を扱う場合にパフォーマンスが良い。

```python
from bokeh.plotting import figure, show, output_file
from bokeh.models import HoverTool

output_file("bokeh_scatter.html")

p = figure(title="実験結果",
           x_axis_label="反応時間 (ms)",
           y_axis_label="正答率 (%)",
           width=800, height=500)

p.circle(x="reaction_time", y="accuracy",
         source=df, size=8, alpha=0.6)

hover = HoverTool(tooltips=[
    ("被験者", "@subject_id"),
    ("反応時間", "@reaction_time{0.0} ms"),
    ("正答率", "@accuracy{0.0}%")
])
p.add_tools(hover)

show(p)
```

### 7.4.3 データ探索での活用

インタラクティブ可視化は、以下の場面で特に有用である。

- **外れ値の特定**: マウスオーバーで外れ値の詳細情報を確認できる
- **パターンの発見**: ズーム機能で特定の領域を拡大して観察できる
- **プレゼンテーション**: ゼミ発表でリアルタイムにデータを探索できる
- **共同研究者との共有**: HTMLファイルを送るだけで、相手もインタラクティブに操作できる

ただし、**論文に掲載するグラフは静的な画像（matplotlib等）で作成する**こと。インタラクティブ可視化はあくまで探索・確認用である。

---

## 7.5 AIを使ったデータ分析の落とし穴

### 7.5.1 統計的な誤解

AIがデータ分析を手軽にする一方で、統計的な誤解に基づく分析が行われるリスクも増大している。

**p-hacking（p値ハッキング）:**

多数の検定を繰り返し、有意な結果が出たものだけを報告する行為。AIを使うと、様々な分析を手軽に試せるため、このリスクが高まる。

```
危険な例:
「AIに20種類の統計検定を試させたら、1つだけp < 0.05になった。
 その結果だけを論文に報告する。」

→ 有意水準5%で20回検定すれば、本当は差がなくても
  平均1回は「有意」になる（偽陽性）
```

**多重比較問題:**

複数の群を同時に比較する場合、検定の回数が増えるほど偽陽性の確率が高くなる。

```python
# 悪い例: 3群を全てのペアでt検定（多重比較補正なし）
from scipy import stats

# A vs B
stats.ttest_ind(group_a, group_b)  # p = 0.03
# A vs C
stats.ttest_ind(group_a, group_c)  # p = 0.12
# B vs C
stats.ttest_ind(group_b, group_c)  # p = 0.04

# → 3回検定しているので、Bonferroni補正が必要
# → 補正後の有意水準: 0.05 / 3 = 0.0167
```

```python
# 良い例: 適切な多重比較補正
from scipy import stats
from statsmodels.stats.multicomp import pairwise_tukeyhsd

# まずANOVAで全体の差を検定
f_stat, p_anova = stats.f_oneway(group_a, group_b, group_c)

if p_anova < 0.05:
    # Tukey HSD で多重比較
    result = pairwise_tukeyhsd(
        endog=all_scores,
        groups=all_groups,
        alpha=0.05
    )
    print(result)
```

### 7.5.2 過学習への注意

AIが提案する分析手法が必要以上に複雑になることがある。特に機械学習を使う場合、過学習（overfitting）のリスクに注意が必要である。

```
注意すべきサイン:
- 訓練データでは高い精度だが、新しいデータでは精度が下がる
- モデルの説明変数の数がサンプルサイズに対して多すぎる
- AIが「より高精度な手法」としてやたら複雑なモデルを提案してくる
```

**対策:**
- 交差検証（Cross-validation）を必ず行う
- 単純なモデルから始め、必要な場合にのみ複雑化する
- サンプルサイズに見合った分析手法を選ぶ

### 7.5.3 AIが出した統計結果を鵜呑みにしない

AIが生成した分析コードは、一見正しく見えても論理的な誤りを含むことがある。

**よくあるAIの間違い:**

1. **前提条件の未確認**: 正規性を確認せずにt検定を適用する
2. **片側検定と両側検定の混同**: 仮説に合わない検定を選択する
3. **対応のあるデータに独立t検定を適用**: 実験計画を正しく理解していない
4. **効果量の計算ミス**: 式の適用を間違える
5. **多重比較補正の欠如**: 複数の検定を行っているのに補正しない

**自分で確認すべきポイント:**

```
□ 検定の前提条件は満たされているか（正規性、等分散性）
□ 実験計画（対応あり/なし）に合った検定を使っているか
□ 有意水準は事前に設定されているか
□ 効果量も報告しているか
□ 多重比較を行う場合、補正は適切か
□ サンプルサイズは十分か
□ 結果の解釈は論理的か
```

---

## 演習問題

### 演習7-1: データの前処理と概要把握

以下のPythonコードでサンプルデータを生成し、AIを使ってデータの概要把握と前処理を行いなさい。

```python
import pandas as pd
import numpy as np

np.random.seed(42)
n = 100

data = pd.DataFrame({
    "subject_id": range(1, n + 1),
    "group": np.random.choice(["control", "treatment"], n),
    "age": np.random.normal(22, 3, n).round(0),
    "pre_score": np.random.normal(50, 10, n).round(1),
    "post_score": np.random.normal(55, 12, n).round(1),
})
# 欠損値を人工的に追加
data.loc[np.random.choice(n, 8, replace=False), "pre_score"] = np.nan
data.loc[np.random.choice(n, 5, replace=False), "post_score"] = np.nan
data.loc[np.random.choice(n, 3, replace=False), "age"] = np.nan
# 外れ値を追加
data.loc[95, "post_score"] = 120
data.loc[12, "age"] = 5

data.to_csv("sample_data.csv", index=False)
```

以下を実施し、レポートにまとめなさい。
1. データの概要を把握する（形状、型、分布、欠損値）
2. 外れ値を検出し、対処方針を決める
3. 欠損値を適切に処理する
4. 処理前後のデータを比較する

### 演習7-2: 探索的データ分析

演習7-1のデータについて、以下のEDAを実施しなさい。

1. group ごとの pre_score と post_score の記述統計量
2. pre_score と post_score の相関分析
3. 各変数の分布の可視化
4. 発見した特徴やパターンを3つ以上報告する

### 演習7-3: 適切な統計検定の実施

演習7-1のデータについて、以下の仮説を検定しなさい。

仮説: 「treatment群はcontrol群と比べて、pre_scoreからpost_scoreへの変化量が大きい」

1. 各群の変化量（post_score - pre_score）を計算する
2. 正規性の検定を行う
3. 適切な統計検定を選択し、実施する
4. 効果量を計算する
5. 結果を論文の「結果」セクションの書き方で報告する

### 演習7-4: 論文品質のグラフ作成

演習7-3の結果を以下のグラフで可視化しなさい。全てのグラフは論文品質（300dpi、適切なフォントサイズ、軸ラベル）で作成すること。

1. 群ごとのpre/postスコアの棒グラフ（エラーバー付き）
2. 群ごとの変化量の箱ひげ図（個別データ点付き）
3. pre_score と post_score の散布図（群ごとに色分け、回帰直線付き）

### 演習7-5: 総合分析レポート

自分の研究テーマ、または以下のサンプルテーマについて、データ分析の全工程を実施し、レポートにまとめなさい。

**サンプルテーマ**: 「睡眠時間と学業成績の関係」

1. サンプルデータの生成（被験者200名、睡眠時間・学習時間・GPA・学年等）
2. データの前処理とEDA
3. 適切な統計分析（相関分析、回帰分析等）
4. 論文品質のグラフ3枚以上
5. 結果のまとめ（発見した知見を3つ以上）

AIとの対話履歴の要約も合わせて提出すること。

---

> **本章のまとめ**: データ分析は「正しい手法を選び、正しく実行し、正しく解釈する」ことが重要である。AIはコード生成や手法の提案で大きな力を発揮するが、分析の設計と結果の解釈は研究者自身の責任である。特に、p-hackingや多重比較問題など、統計的な落とし穴には十分注意すること。論文品質のグラフ作成は、AIプロンプトの書き方一つで効率が劇的に変わるため、本章で学んだテクニックを活用してほしい。
