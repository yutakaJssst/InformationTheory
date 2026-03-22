# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

「情報論」（2026年度）の授業資料および書籍「大学院生のためのAI活用研究術」の原稿を管理するリポジトリ。

- **著者**: 松野 裕（日本大学理工学部 応用情報工学科 / 大学院 情報科学専攻 教授）
- **授業**: 大学院「情報論」100分×13回 + OD 50分
- **書籍**: 「大学院生のためのAI活用研究術」コロナ社から出版予定

## Repository Structure

```
├── slides/                          # 2026年度 授業スライド（Marp）
│   ├── 00_OD_*.md / .pptx / .pdf   # OD〜第13回（14回分）
│   └── ...
├── ai_research_book_tex/            # 書籍LaTeXソース（コロナ社A5判）
│   ├── ai_research.tex              # メインTeXファイル
│   ├── ai_research.pdf              # ビルド済みPDF（243ページ）
│   ├── contents/                    # 各章のTeXファイル（15本）
│   ├── references.bib               # 参考文献（26エントリ）
│   ├── corona-a5.cls                # コロナ社クラスファイル
│   └── Makefile
├── ai_research_book/chapters/       # 書籍Markdown原稿（12ファイル）
├── 大学院生のためのAI活用研究術_企画書.md / .pdf  # コロナ社向け企画書
├── 情報論{1-5}_2025.pptx            # 2025年度の授業スライド（参考資料）
├── 情報論2025-10.pptx               # 2025年度ガクチカ授業スライド
└── （学生提出物フォルダ6つ）          # 2025年度の課題提出物
```

## Build

### 書籍（LaTeX）
```bash
cd ai_research_book_tex
make          # platex + bibtex + mendex + dvipdfmx
make clean    # 中間ファイル削除
```

### スライド（Marp）
```bash
# 個別変換
npx @marp-team/marp-cli slides/00_OD_*.md --pptx
npx @marp-team/marp-cli slides/00_OD_*.md --pdf

# 一括変換
for f in slides/*.md; do npx @marp-team/marp-cli "$f" --pptx; npx @marp-team/marp-cli "$f" --pdf; done
```

### 企画書（Pandoc）
```bash
pandoc 大学院生のためのAI活用研究術_企画書.md -o 大学院生のためのAI活用研究術_企画書.pdf \
  --pdf-engine=lualatex -V documentclass=ltjsarticle -V geometry:margin=25mm \
  -V fontsize=11pt -V mainfont="Hiragino Mincho ProN" -V sansfont="Hiragino Kaku Gothic ProN"
```

## Book Structure (10 chapters)

| 章 | タイトル | 引用 |
|---|---------|------|
| 1 | 研究活動と生成AI | あり |
| 2 | プロンプトエンジニアリング | あり |
| 3 | AIを使った文献調査 | なし |
| 4 | 英語論文の執筆と推敲 | なし |
| 5 | 研究発表スライドの作成 | なし |
| 6 | AIによるコード生成とテスト | なし |
| 7 | データ分析と可視化 | あり |
| 8 | GitHubによる研究成果管理 | なし |
| 9 | 就活文書の作成 | なし |
| 10 | 研究の新規性分析と総合演習 | なし |

引用「あり」の章のみ bibunit でラップされている。

## Key Conventions

- 書籍の文体: 「である」調で統一
- ツール名: 「Gemini」（Gemini Proではない）で統一
- 英語ライティング4原則: すっきり最小主義、具体化主義、動詞主義、能動態主義
- プロンプト設計: ROCFモデル（Role, Objective, Context, Format）
- 新規性分析: 3観点（方法論的、実践的、時間的観点）
- promptbox環境: AIプロンプト例の表示に使用
- 学生の個人情報（氏名、学籍番号）を含むファイルあり。取り扱い注意

## TODO（出版に向けた残課題）

### 優先度: 高
- [ ] **参考文献の充実**: 現在26エントリ/12引用。第3-6,8-10章は引用ゼロ。目標40-50エントリ、各章3-5件の引用
- [ ] **図表の作成・追加**: 現在 `\includegraphics` がゼロ。各章2-3点の図（概念図、フローチャート、スクリーンショット等）が必要
  - 第1章: LLMの仕組みの概念図、ツール選択フローチャート
  - 第2章: ROCFモデルの図、プロンプト改善サイクル図
  - 第7章: データ分析ワークフロー図、SafeComp研究のグラフ（fig_adoption.pdf等の転用検討）
  - 第8章: コミットタイムライン図、GitHub Pagesのスクリーンショット
- [ ] **Pythonコード例の動作確認**: 全章のコード例をJupyter Notebookで実行・検証

### 優先度: 中
- [ ] **索引の整備**: `\index{}`は入っているがmendex生成の索引を確認・整理
- [ ] **第9章（就活）の位置づけ検討**: レビュアー指摘あり。「研究実務ハンドブック」に寄せるなら、就活章はコラムか付録に移す選択肢も
- [ ] **学生の改善前後の事例**: 実授業での学生の成果物Before/Afterを3-5本追加（差別化要素）
- [ ] **共著者確認**: SafeCompデータの教科書への転用について落合氏・河野氏に確認
- [ ] **スライドと書籍のさらなる同期**: 書籍の英語ライティング4原則がスライド05にはあるが、スライド06には動詞主義・具体化主義が未反映

### 優先度: 低
- [ ] **ツール情報の陳腐化対策**: 本文からツール詳細を付録Aにさらに集約
- [ ] **出版時のツール情報最終確認**: 付録Aの料金・機能名を刊行直前に一括確認
- [ ] **Markdown原稿とTeXの同期**: ai_research_book/chapters/*.md と ai_research_book_tex/contents/*.tex の内容が一部乖離（TeXが最新）
