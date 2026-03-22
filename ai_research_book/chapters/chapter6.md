# 第6章 AIによるコード生成とテスト

---

## 学習目標

本章を学ぶことで、以下の能力を身につけることができる。

1. **AIを活用したコード生成の基本フローとプロンプト設計を習得する** — 自然言語からコードを生成するプロセスを理解し、効果的なプロンプトを書けるようになる
2. **テストコードの自動生成とAIコードレビューを実践できる** — テスト駆動開発の考え方を学び、AIを活用した品質向上手法を身につける
3. **AI生成コードの品質・セキュリティリスクを理解し対処できる** — 生成コードを盲信せず、適切に検証・修正する力を養う

---

## 6.1 AIとソフトウェア開発の現在

### 6.1.1 コード生成AIの普及状況

2024年以降、AIによるコード生成は研究者・開発者の日常的なツールとなった。主要なツールとその特徴を以下に整理する。

| ツール | 特徴 | 料金 |
|--------|------|------|
| GitHub Copilot | VS Code統合、コード補完に特化 | 学生無料（GitHub Education） |
| Cursor | AI統合型エディタ、対話的開発 | 無料枠あり、Pro月$20 |
| ChatGPT / GPT-4 | 汎用的、説明付きコード生成 | 無料枠あり、Plus月$20 |
| Gemini | Google連携、長文コンテキスト | 無料枠あり |
| Claude | 長文コンテキスト、正確な推論 | 無料枠あり、Pro月$20 |

### 6.1.2 開発者のAI利用統計

GitHub の2024年開発者調査によると、回答者の92%がAIコーディングツールを職場内外で利用しており、70%以上が「生産性が向上した」と回答している。特に以下の場面での活用が報告されている。

- **定型的なコードの作成**（ボイラープレートコード）: 87%
- **新しいプログラミング言語の学習**: 73%
- **バグの特定と修正**: 68%
- **テストコードの作成**: 62%

### 6.1.3 AIが変える開発ワークフロー

従来の開発ワークフローでは、プログラマが仕様を読み、設計し、コードを一行ずつ書いていた。AIの登場により、このプロセスは大きく変わりつつある。

**従来のワークフロー:**
```
仕様理解 → 設計 → コーディング → テスト → デバッグ → レビュー
```

**AI活用ワークフロー:**
```
仕様記述（プロンプト） → AI生成 → 人間がレビュー・修正 → AIでテスト生成 → 検証
```

重要なのは、AIは「コードを書く」部分を加速するが、「何を作るか」「なぜ作るか」を考えるのは依然として人間の仕事であるということだ。大学院生にとって、研究のロジックを明確にする力がますます重要になっている。

---

## 6.2 AIによるコード生成の基本

### 6.2.1 基本フロー

AIによるコード生成は、以下の3ステップで行う。

```
Step 1: 自然言語で仕様を記述する（プロンプト作成）
Step 2: AIがコードを生成する
Step 3: 人間がレビュー・テスト・修正する
```

このうち、最も重要なのは **Step 1（プロンプト作成）** である。曖昧な指示からは曖昧なコードしか生まれない。明確で具体的な仕様を書くことが、良いコードを得る鍵である。

### 6.2.2 効果的なプロンプトの4要素

AIに高品質なコードを生成させるためには、以下の4つの要素をプロンプトに含めることが重要である。

| 要素 | 内容 | 例 |
|------|------|-----|
| **1. 言語・フレームワーク指定** | 使用する言語やライブラリを明示 | 「Python 3.10、pandasを使用」 |
| **2. 入出力仕様** | 何を受け取り、何を返すか | 「CSVファイルパスを受け取り、DataFrameを返す」 |
| **3. 制約条件** | パフォーマンス、エラー処理等 | 「メモリ効率を重視、欠損値はNaNで保持」 |
| **4. 例示** | 具体的な入出力例 | 「入力: 'data.csv' → 出力: 100行×5列のDataFrame」 |

### 6.2.3 Bad prompt vs Good prompt の比較

**Bad prompt（悪い例）:**

```
CSVを読み込む関数を書いて
```

この指示では、言語もライブラリも不明であり、エラー処理の有無も分からない。AIは何らかのコードを返すが、研究の要件に合うかは運次第である。

**Good prompt（良い例）:**

```
以下の仕様でPython関数を作成してください。

## 関数名
load_experiment_data

## 目的
実験結果のCSVファイルを読み込み、前処理済みのDataFrameを返す

## 使用ライブラリ
- Python 3.10
- pandas 2.0以上

## 入力
- file_path: str — CSVファイルのパス

## 出力
- pd.DataFrame — 以下の前処理を適用済み
  1. 列名を英語の小文字に統一（スペースはアンダースコアに変換）
  2. 数値列の欠損値は列の中央値で補完
  3. 重複行を削除

## エラー処理
- ファイルが存在しない場合: FileNotFoundError を発生
- CSVの解析に失敗した場合: ValueError を発生（メッセージにファイル名を含む）

## 入出力例
入力ファイル (experiment_001.csv):
Subject ID, Response Time, Accuracy
1, 0.52, 0.95
2, , 0.87
3, 0.61, 0.95
2, 0.52, 0.95

出力DataFrame:
   subject_id  response_time  accuracy
0           1          0.520      0.95
1           2          0.565      0.87
2           3          0.610      0.95
（重複行が削除され、欠損値が中央値0.565で補完される）
```

このように具体的な仕様を書くことで、AIはより正確で実用的なコードを生成できる。

**AIが生成するコードの例:**

```python
import pandas as pd
import os


def load_experiment_data(file_path: str) -> pd.DataFrame:
    """
    実験結果のCSVファイルを読み込み、前処理済みのDataFrameを返す。

    Parameters
    ----------
    file_path : str
        CSVファイルのパス

    Returns
    -------
    pd.DataFrame
        前処理済みのDataFrame

    Raises
    ------
    FileNotFoundError
        ファイルが存在しない場合
    ValueError
        CSVの解析に失敗した場合
    """
    # ファイル存在確認
    if not os.path.exists(file_path):
        raise FileNotFoundError(f"ファイルが見つかりません: {file_path}")

    # CSV読み込み
    try:
        df = pd.read_csv(file_path)
    except Exception as e:
        raise ValueError(f"CSVの解析に失敗しました ({file_path}): {e}")

    # 1. 列名を英語の小文字に統一
    df.columns = (
        df.columns
        .str.strip()
        .str.lower()
        .str.replace(" ", "_")
    )

    # 2. 数値列の欠損値を中央値で補完
    numeric_cols = df.select_dtypes(include="number").columns
    for col in numeric_cols:
        median_val = df[col].median()
        df[col] = df[col].fillna(median_val)

    # 3. 重複行を削除
    df = df.drop_duplicates().reset_index(drop=True)

    return df
```

---

## 6.3 主要ツールの活用法

### 6.3.1 Gemini / ChatGPT / Claude でのコード生成

ブラウザベースのAIチャットツールは、最も手軽にコード生成を始められる方法である。

**活用のコツ:**

1. **新しいチャットで始める** — 過去の文脈が混ざらないよう、コード生成タスクは新しいセッションで行う
2. **コンテキストを最初に提供する** — 「私は大学院生で、心理学実験のデータを分析しています」のように背景を伝える
3. **段階的に依頼する** — 一度に全てを求めず、まず骨格を作り、次にエラー処理を追加するなど段階的に進める

**プロンプト例（Claude）:**

```
私は神経科学の大学院生です。脳波（EEG）データの解析スクリプトを作成しています。

以下の関数を Python で作成してください。
- MNE-Python ライブラリを使用
- .fif 形式のEEGデータを読み込む
- バンドパスフィルタ（1-40Hz）を適用
- アーティファクト除去（閾値: ±100μV）を行う
- エポック分割（-0.2〜0.8秒、イベントID指定可能）を行う

各処理ステップにログ出力を含めてください。
```

### 6.3.2 GitHub Copilot の活用

GitHub Copilotは、VS Code上でリアルタイムにコード補完を行うツールである。**大学院生はGitHub Educationを通じて無料で利用できる**。

**セットアップ手順:**

1. GitHub Education（https://education.github.com）で学生認証を行う
2. VS Code の拡張機能から「GitHub Copilot」をインストール
3. GitHub アカウントでサインイン
4. `.py` ファイルを開いてコメントを書くと、自動的にコード候補が表示される

**効果的な使い方:**

```python
# --- コメントで意図を書くと、Copilotが補完する ---

# CSVファイルを読み込み、欠損値の数を列ごとに表示する関数
def show_missing_values(file_path):
    # ← ここでTabキーを押すと、Copilotがコードを提案する
```

**Tips:**
- コメントは英語でも日本語でも良いが、具体的に書くほど精度が上がる
- `Alt + ]` で次の候補、`Alt + [` で前の候補を表示できる
- Copilot Chat（サイドパネル）を使えば、対話的にコードを改善できる

### 6.3.3 対話的コード開発のテクニック

AIとの対話を通じてコードを段階的に改善する方法を、「対話的コード開発」と呼ぶ。以下にその流れを示す。

**Step 1: 最初のプロンプト**
```
二群の平均値を比較する統計検定を行うPython関数を書いてください。
scipy.stats を使用してください。
```

**Step 2: 結果を見て追加指示**
```
ありがとうございます。以下の改善をお願いします：
1. 正規性の検定（Shapiro-Wilk検定）を先に行い、結果に応じてt検定またはMann-Whitney U検定を選択する
2. 効果量（Cohen's d）も計算する
3. 結果を辞書形式で返す
```

**Step 3: さらに改善**
```
結果の辞書に以下も追加してください：
- 検定名（使用した検定の名前）
- 自由度（該当する場合）
- 95%信頼区間
```

このように、段階的に要件を追加することで、自分の研究に最適なコードに近づけていく。

---

## 6.4 実践テクニック

### 6.4.1 段階的開発: 関数単位で生成・検証

AIにコード全体を一度に生成させるのではなく、**関数単位で生成し、一つずつ動作確認する**方法が最も効率的である。

```
手順:
1. まず、プログラム全体の構成を相談する
2. 各関数を一つずつ生成させる
3. 生成された関数を実行して動作確認する
4. 問題があれば修正を依頼する
5. 全関数が揃ったら統合テストを行う
```

**プロンプト例:**

```
以下の研究データ分析パイプラインを設計したいです。
まず、全体の構成（関数の一覧と役割）を提案してください。
コードはまだ書かなくて良いです。

処理の流れ:
1. 複数のCSVファイルを結合
2. データのクリーニング
3. 記述統計量の算出
4. 群間比較（統計検定）
5. 結果のグラフ作成
6. レポートの自動生成
```

### 6.4.2 テスト駆動: テストケースを先に書かせる

テスト駆動開発（TDD）の考え方をAIと組み合わせると、コードの品質が大幅に向上する。

**手順:**

```
1. 関数の仕様を決める
2. AIにテストケースを先に生成させる
3. AIに関数本体を生成させる
4. テストを実行して合格を確認する
```

**プロンプト例:**

```
以下の仕様の関数について、pytestのテストケースを先に書いてください。
関数本体はまだ書かないでください。

関数名: calculate_effect_size
入力: group1 (list[float]), group2 (list[float])
出力: dict（cohen_d, interpretation を含む）
仕様:
- Cohen's d を計算する
- 解釈: |d| < 0.2 → "negligible", < 0.5 → "small", < 0.8 → "medium", >= 0.8 → "large"
- 空リストが渡された場合は ValueError を発生
```

### 6.4.3 リファクタリング依頼

既存のコードをAIに改善させることも強力な活用法である。

**プロンプト例:**

```
以下のPythonコードをリファクタリングしてください。
改善ポイント:
1. 可読性の向上（変数名の改善、コメント追加）
2. 関数への分割（1関数1責任の原則）
3. エラー処理の追加
4. 型ヒントの追加

[既存のコードをここに貼り付ける]
```

### 6.4.4 デバッグ支援: エラーメッセージの活用

エラーに遭遇したとき、AIは強力なデバッグパートナーとなる。

**プロンプト例:**

```
以下のPythonコードを実行したところ、エラーが発生しました。
原因と修正方法を教えてください。

## コード
[コードを貼り付け]

## エラーメッセージ
Traceback (most recent call last):
  File "analysis.py", line 42, in <module>
    result = df.groupby("condition").apply(analyze_group)
  File "analysis.py", line 28, in analyze_group
    t_stat, p_value = stats.ttest_ind(group["pre"], group["post"])
ValueError: unequal length arrays

## 追加情報
- Python 3.10, pandas 2.0, scipy 1.11
- データは条件ごとに被験者数が異なります（条件A: 30名、条件B: 25名）
```

**Tips:** エラーメッセージだけでなく、コード全体と実行環境の情報を含めることで、AIの回答精度が大幅に向上する。

---

## 6.5 テストコードの自動生成

### 6.5.1 pytestによるテストケース生成

テストコードの作成は、研究コードの信頼性を担保する上で極めて重要である。AIを活用すれば、包括的なテストケースを短時間で生成できる。

**プロンプト例:**

```
以下のPython関数に対するpytestのテストケースを生成してください。
正常系、異常系、境界値テストを含めてください。

```python
def normalize_scores(scores: list[float], method: str = "min-max") -> list[float]:
    """スコアのリストを正規化する。"""
    if not scores:
        raise ValueError("スコアリストが空です")
    if method == "min-max":
        min_val, max_val = min(scores), max(scores)
        if min_val == max_val:
            return [0.0] * len(scores)
        return [(x - min_val) / (max_val - min_val) for x in scores]
    elif method == "z-score":
        mean_val = sum(scores) / len(scores)
        std_val = (sum((x - mean_val) ** 2 for x in scores) / len(scores)) ** 0.5
        if std_val == 0:
            return [0.0] * len(scores)
        return [(x - mean_val) / std_val for x in scores]
    else:
        raise ValueError(f"未対応の正規化方法: {method}")
```
```

**AIが生成するテストコードの例:**

```python
import pytest
from normalize import normalize_scores


class TestNormalizeScoresMinMax:
    """min-max正規化のテスト"""

    def test_basic_normalization(self):
        """基本的な正規化が正しく動作すること"""
        result = normalize_scores([0, 50, 100])
        assert result == [0.0, 0.5, 1.0]

    def test_negative_values(self):
        """負の値を含む場合"""
        result = normalize_scores([-10, 0, 10])
        assert result == [0.0, 0.5, 1.0]

    def test_single_element(self):
        """要素が1つの場合（min == max）"""
        result = normalize_scores([42.0])
        assert result == [0.0]

    def test_all_same_values(self):
        """全て同じ値の場合"""
        result = normalize_scores([5.0, 5.0, 5.0])
        assert result == [0.0, 0.0, 0.0]

    def test_already_normalized(self):
        """既に0-1範囲の値"""
        result = normalize_scores([0.0, 0.5, 1.0])
        assert result == [0.0, 0.5, 1.0]


class TestNormalizeScoresZScore:
    """z-score正規化のテスト"""

    def test_basic_z_normalization(self):
        """基本的なz-score正規化"""
        result = normalize_scores([2, 4, 6], method="z-score")
        assert pytest.approx(result[0], abs=1e-6) == -1.2247448713916
        assert pytest.approx(result[1], abs=1e-6) == 0.0
        assert pytest.approx(result[2], abs=1e-6) == 1.2247448713916

    def test_all_same_values_z(self):
        """全て同じ値の場合（標準偏差0）"""
        result = normalize_scores([3.0, 3.0, 3.0], method="z-score")
        assert result == [0.0, 0.0, 0.0]


class TestNormalizeScoresErrors:
    """異常系テスト"""

    def test_empty_list(self):
        """空リストでValueError"""
        with pytest.raises(ValueError, match="スコアリストが空です"):
            normalize_scores([])

    def test_invalid_method(self):
        """不正なメソッド名でValueError"""
        with pytest.raises(ValueError, match="未対応の正規化方法"):
            normalize_scores([1, 2, 3], method="invalid")


class TestNormalizeScoresBoundary:
    """境界値テスト"""

    def test_very_large_values(self):
        """非常に大きな値"""
        result = normalize_scores([0, 1e10])
        assert result == [0.0, 1.0]

    def test_very_small_differences(self):
        """非常に小さな差"""
        result = normalize_scores([1.0, 1.0 + 1e-10])
        assert len(result) == 2
        assert 0.0 <= result[0] <= 1.0
        assert 0.0 <= result[1] <= 1.0

    def test_two_elements(self):
        """要素が2つの最小ケース"""
        result = normalize_scores([10, 20])
        assert result == [0.0, 1.0]
```

### 6.5.2 テストカバレッジの考え方

テストカバレッジとは、テストがコードのどの程度をカバーしているかを示す指標である。

```bash
# カバレッジの測定
pip install pytest-cov
pytest --cov=my_module --cov-report=html tests/
```

研究コードでは、最低でも以下をカバーすることを目指す。

- **正常系**: 期待通りの入力に対する動作
- **異常系**: 不正な入力に対するエラー処理
- **境界値**: 最小値、最大値、空データ、要素1つなどの特殊なケース

### 6.5.3 AI生成テストの検証ポイント

AIが生成したテストコードは、以下の点を必ず確認する。

1. **テストが実際に実行できるか** — インポートパスやファイル名が正しいか
2. **期待値が正しいか** — AIが計算した期待値が本当に合っているか手計算で確認する
3. **テストの独立性** — 各テストが他のテストに依存していないか
4. **意味のあるテストか** — `assert True` のような無意味なテストが含まれていないか

---

## 6.6 AIコードレビューとリファクタリング

### 6.6.1 AIにコードレビューを依頼するプロンプト

AIは優れたコードレビュアーとして機能する。特に一人で研究を進める大学院生にとって、客観的なフィードバックを得る貴重な手段である。

**プロンプト例:**

```
以下のPythonコードをレビューしてください。
以下の観点でチェックし、改善提案をお願いします。

1. **可読性**: 変数名、関数名は適切か。コメントは十分か。
2. **効率性**: 不要なループや非効率な処理はないか。
3. **セキュリティ**: 入力検証は適切か。脆弱性はないか。
4. **エラー処理**: 例外処理は適切か。エッジケースへの対応は十分か。
5. **保守性**: コードの構造は適切か。将来の変更に対応しやすいか。

問題の深刻度を「重大」「中程度」「軽微」の3段階で分類してください。

[コードをここに貼り付け]
```

### 6.6.2 コードレビューチェックリスト

AIにレビューを依頼する際の観点をチェックリストとしてまとめる。

```
□ 可読性
  □ 変数名・関数名が意図を表しているか
  □ 適切なコメント・docstringがあるか
  □ コードの構造が論理的か

□ 効率性
  □ 不要なループや計算がないか
  □ 適切なデータ構造を使っているか
  □ メモリ使用量は適切か

□ セキュリティ
  □ ユーザー入力を適切に検証しているか
  □ ファイルパスの検証があるか
  □ SQLインジェクション等の脆弱性がないか

□ エラー処理
  □ 想定されるエラーを適切にキャッチしているか
  □ エラーメッセージが分かりやすいか
  □ リソースの解放が確実に行われるか

□ テスト可能性
  □ 関数が適切な粒度に分割されているか
  □ 外部依存を注入可能か
  □ 副作用が最小限か
```

### 6.6.3 リファクタリングの種類と適用場面

| リファクタリングの種類 | 適用場面 | プロンプト例 |
|----------------------|---------|------------|
| **関数の抽出** | 長い関数を分割 | 「この関数を責務ごとに小さな関数に分割して」 |
| **変数名の改善** | 意味不明な変数名 | 「変数名をより意味が通るように改善して」 |
| **重複の排除** | 類似コードの繰り返し | 「重複しているコードを共通関数にまとめて」 |
| **条件分岐の簡略化** | 複雑なif-else | 「この条件分岐を簡潔に書き直して」 |
| **データ構造の変更** | 不適切な構造 | 「リストの代わりに辞書を使うように変更して」 |

### 6.6.4 ドキュメント自動生成

AIを使って、コードのドキュメントを自動生成できる。

**docstring生成プロンプト:**

```
以下のPython関数にNumPyスタイルのdocstringを追加してください。
Parameters、Returns、Raises、Examples セクションを含めてください。

[関数のコードを貼り付け]
```

**README生成プロンプト:**

```
以下のPythonプロジェクトのREADME.mdを作成してください。

プロジェクト名: eeg-analysis-toolkit
概要: EEGデータの前処理・分析パイプライン
主要ファイル:
- preprocess.py: データ前処理
- analyze.py: 統計分析
- visualize.py: 結果の可視化
- requirements.txt: 依存パッケージ

以下のセクションを含めてください:
1. プロジェクト概要
2. インストール方法
3. 使い方（コード例付き）
4. ファイル構成
5. ライセンス
```

---

## 6.7 AI生成コードの品質と注意点

### 6.7.1 セキュリティリスク

AI生成コードには、以下のようなセキュリティリスクが含まれる場合がある。

**1. SQLインジェクション**

```python
# 危険: AI が生成しがちなコード
def get_user(name):
    query = f"SELECT * FROM users WHERE name = '{name}'"
    cursor.execute(query)

# 安全: パラメータ化クエリを使用
def get_user(name):
    query = "SELECT * FROM users WHERE name = ?"
    cursor.execute(query, (name,))
```

**2. 不適切な入力検証**

```python
# 危険: ファイルパスを検証していない
def read_file(path):
    with open(path) as f:
        return f.read()

# 安全: パスの検証を含む
def read_file(path, allowed_dir="/data/experiments"):
    real_path = os.path.realpath(path)
    if not real_path.startswith(os.path.realpath(allowed_dir)):
        raise ValueError("許可されていないパスです")
    with open(real_path) as f:
        return f.read()
```

**3. ハードコードされた秘密情報**

```python
# 危険: APIキーがコードに含まれている
api_key = "sk-1234567890abcdef"

# 安全: 環境変数から読み込む
import os
api_key = os.environ.get("API_KEY")
if not api_key:
    raise RuntimeError("API_KEY 環境変数が設定されていません")
```

### 6.7.2 ライセンス問題

AIが生成したコードには、学習データに含まれるオープンソースコードの断片が含まれる可能性がある。

- **研究コードの場合**: 論文の再現性のために公開する場合、ライセンスを明記する
- **推奨**: MITライセンスやApache 2.0ライセンスなど、許容的なライセンスを選択する
- **注意**: AI生成コードの著作権は法的にグレーゾーンであることを認識しておく

### 6.7.3 「信頼するが検証する」の原則

AI生成コードに対する基本姿勢は **「Trust, but verify（信頼するが検証する）」** である。

```
検証チェックリスト:
□ コードが意図通りに動作するか（手動テスト）
□ テストケースが全て通過するか（自動テスト）
□ エッジケースでも正しく動作するか
□ エラー処理が適切か
□ パフォーマンスが許容範囲内か
□ セキュリティ上の問題がないか
□ コードの論理が自分で理解できるか ← 最も重要
```

最後の項目が最も重要である。**自分で理解できないコードは使わない**。AIに説明を求め、納得してから使用すること。

### 6.7.4 研究コードの再現性確保

研究で使用するコードは、再現性が不可欠である。以下の対策を講じる。

1. **依存関係の固定**: `requirements.txt` や `pyproject.toml` でバージョンを固定する
2. **乱数シードの設定**: 結果の再現性のために、乱数シードを明示的に設定する
3. **環境情報の記録**: Python バージョン、OS、主要ライブラリのバージョンを記録する
4. **バージョン管理**: Git でコードの履歴を管理する（第8章で詳述）

```python
# 再現性確保のテンプレート
import random
import numpy as np

RANDOM_SEED = 42
random.seed(RANDOM_SEED)
np.random.seed(RANDOM_SEED)

# 実行環境の記録
import sys
import platform
print(f"Python: {sys.version}")
print(f"NumPy: {np.__version__}")
print(f"OS: {platform.platform()}")
```

---

## 演習問題

### 演習6-1: 基本的なコード生成

以下の仕様で、AIを使ってPython関数を生成しなさい。生成されたコードを実行し、正しく動作することを確認しなさい。

**仕様:**
- 関数名: `summarize_data`
- 入力: pandasのDataFrame
- 出力: 各数値列について、平均、中央値、標準偏差、最小値、最大値を含む辞書
- エラー処理: DataFrameが空の場合はValueErrorを発生

使用したプロンプトと、生成されたコードを提出すること。

### 演習6-2: テスト駆動開発

演習6-1で作成した `summarize_data` 関数に対して、AIを使ってpytestのテストケースを生成しなさい。以下のケースを最低限含めること。

- 正常なDataFrameに対するテスト
- 空のDataFrameに対するテスト
- 数値列のないDataFrameに対するテスト
- 欠損値を含むDataFrameに対するテスト

### 演習6-3: コードレビューとリファクタリング

以下のコードをAIにレビューさせ、改善版を作成しなさい。どのような問題が指摘され、どう改善されたかをレポートにまとめること。

```python
def proc(d):
    r = []
    for i in range(len(d)):
        if d[i] != None and d[i] > 0:
            x = d[i] * 2.5 + 10
            r.append(x)
    s = 0
    for j in r:
        s = s + j
    a = s / len(r)
    return a
```

### 演習6-4: デバッグ支援

以下のコードにはバグが含まれている。AIを使ってバグを特定し、修正しなさい。修正の過程で使用したプロンプトも提出すること。

```python
import pandas as pd

def calculate_growth_rate(df, value_col, time_col):
    """時系列データの成長率を計算する"""
    df = df.sort_values(time_col)
    growth_rates = []
    for i in range(len(df)):
        current = df.iloc[i][value_col]
        previous = df.iloc[i-1][value_col]
        rate = (current - previous) / previous * 100
        growth_rates.append(rate)
    df["growth_rate"] = growth_rates
    return df

# テストデータ
data = pd.DataFrame({
    "year": [2020, 2021, 2022, 2023],
    "revenue": [100, 120, 150, 180]
})

result = calculate_growth_rate(data, "revenue", "year")
print(result)
```

### 演習6-5: 研究データ分析スクリプトの作成

自分の研究テーマ（または以下のサンプルテーマ）に関連するデータ分析スクリプトをAIと対話的に作成しなさい。

**サンプルテーマ**: 「オンライン授業と対面授業の学習効果比較」

以下の機能を含むスクリプトを作成すること。
1. サンプルデータの生成（被験者50名、2群、テストスコアあり）
2. 記述統計量の算出
3. 適切な統計検定の実施
4. 結果のグラフ作成

AIとの対話履歴（プロンプトとレスポンスの要約）、最終的なコード、実行結果を提出すること。

---

> **本章のまとめ**: AIは強力なコーディングパートナーであるが、最終的な品質責任は使用者にある。「AIに書かせて、人間が検証する」という姿勢を常に持ち、特に研究コードでは再現性とセキュリティに十分注意すること。プロンプトの書き方一つでコードの品質が大きく変わるため、明確で具体的な仕様記述のスキルを磨くことが重要である。
