# 第7章：Titanicデータ分析

## 必要なファイル

- `titanic-walkthrough.ipynb`：本文のコード6本を順に試すノートブックです。最後に結果を照合するセルを加えています。
- `verify_titanic.py`：本文中の数値を再計算します。
- `gen_figures.py`：本文掲載用の図をPDFで生成します。
- `requirements.txt`：必要なPythonライブラリの一覧です。
- `train.csv`：Titanicの学習用データです。[Kaggleの配布ページ](https://www.kaggle.com/c/titanic)で利用条件を確認して取得してください。

使う教材と `train.csv` を同じフォルダーに置きます。
`train.csv` は本サイトでは再配布していません。

## ノートブックで順に試す

Google Colabまたは手元のJupyterで `titanic-walkthrough.ipynb` を開きます。
Colabでは `train.csv` をファイル一覧からアップロードしてください。
必要なライブラリがない場合は、`requirements.txt` も用意して、コードセルで `!python -m pip install -r requirements.txt` を実行します。
説明を読みながら、先頭のセルから順に実行してください。

保存済みの出力は、2026年9月5日に全セルを順に実行した結果です。
実行環境は次のとおりです。

- Python 3.12.14
- pandas 3.0.5
- matplotlib 3.11.1
- scikit-learn 1.9.0

891行・12列のデータで、訓練712件・評価179件、正解率0.804、混同行列 `[[98, 12], [23, 46]]` を確認しています。
先頭行の個票を含むセルの出力は、再配布を避けるため保存していません。
データやライブラリの版が違うと、結果が変わることがあります。
最初のコードセルではライブラリの版を表示し、データが同じか照合するための値（SHA-256）も記録します。

## スクリプトで数値と図を確認する

1. `python -m pip install -r requirements.txt` を実行します。
2. 数値の確認は `python verify_titanic.py` を実行します。
3. 図の生成は `python gen_figures.py` を実行します。
4. 生成された図は `figs` フォルダーに保存されます。

実行結果が書籍の値と異なる場合は、まず `train.csv` の出所・行数・列名とライブラリの版を確認してください。
