# 第7章：Titanicデータ分析

## 必要なファイル

- `verify_titanic.py`：本文中の数値を再計算します。
- `gen_figures.py`：本文掲載用の図をPDFで生成します。
- `requirements.txt`：必要なPythonライブラリです。
- `train.csv`：Titanicの学習用データです。配布元の利用条件を確認して取得してください。

4ファイルを同じフォルダーに置きます。`train.csv` は本サイトでは再配布していません。

## 実行手順

1. `python -m pip install -r requirements.txt` を実行します。
2. 数値の確認は `python verify_titanic.py` を実行します。
3. 図の生成は `python gen_figures.py` を実行します。
4. 生成された図は `figs` フォルダーに保存されます。

実行結果が書籍の値と異なる場合は、まず `train.csv` の出所・行数・列名とライブラリの版を確認してください。
