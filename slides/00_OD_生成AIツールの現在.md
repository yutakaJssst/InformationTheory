---
marp: true
theme: default
paginate: true
size: 16:9
style: |
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300;400;500;700&family=IBM+Plex+Mono&display=swap');

  :root {
    --color-text: #333333;
    --color-accent: #0097A7;
    --color-accent2: #4285F4;
    --color-green: #02BD35;
    --color-red: #D32F2F;
    --color-purple: #5E35B1;
    --color-orange: #FF8F00;
    --color-bg-light: #F5F5F5;
    --color-bg-code: #F8F9FA;
    --color-line: #D9EAD3;
  }

  section {
    font-family: 'Noto Sans JP', 'Hiragino Sans', 'Hiragino Kaku Gothic ProN', sans-serif;
    color: var(--color-text);
    background: #FFFFFF;
    padding: 40px 60px 60px 60px;
  }

  section::after {
    content: '';
    font-size: 0;
  }

  footer {
    font-family: 'Noto Sans JP', sans-serif;
    color: var(--color-green) !important;
    font-weight: 700;
    font-size: 14px !important;
    left: 40px !important;
    bottom: 16px !important;
    letter-spacing: 1px;
  }

  h1 {
    color: var(--color-text);
    font-weight: 700;
    border-bottom: none;
  }

  h2 {
    color: var(--color-text);
    font-weight: 700;
    font-size: 1.4em;
    border-bottom: 3px solid var(--color-line);
    padding-bottom: 8px;
  }

  h3 {
    color: var(--color-accent);
    font-weight: 500;
    font-size: 1.1em;
  }

  code {
    font-family: 'IBM Plex Mono', 'Menlo', monospace;
    background: var(--color-bg-code);
    padding: 2px 6px;
    border-radius: 3px;
    font-size: 0.85em;
  }

  pre {
    background: var(--color-bg-code);
    border-left: 4px solid var(--color-accent);
    border-radius: 4px;
    padding: 16px;
  }

  pre code {
    background: none;
    padding: 0;
  }

  table {
    font-size: 0.85em;
    width: 100%;
  }

  th {
    background: var(--color-text);
    color: white;
    font-weight: 500;
  }

  tr:nth-child(even) {
    background: #F0F4FF;
  }

  blockquote {
    border-left: 4px solid var(--color-accent);
    background: var(--color-bg-light);
    padding: 12px 20px;
    margin: 12px 0;
    font-size: 0.95em;
  }

  section.title {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    border-bottom: 3px solid var(--color-line);
  }

  section.title h1 {
    font-size: 2.8em;
    margin-bottom: 0;
  }

  section.title h2 {
    font-size: 1.2em;
    font-weight: 400;
    color: var(--color-text);
    border: none;
    padding: 0;
  }

  section.title p {
    color: #999;
    font-size: 0.85em;
  }

  section.section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: linear-gradient(135deg, #FAFAFA 0%, #F0F0F0 100%);
  }

  section.section h1 {
    font-size: 2.2em;
    color: var(--color-accent);
    text-align: center;
  }

  section.section p {
    text-align: center;
    color: #777;
    font-size: 1.1em;
  }

  section.ai-exercise h2 {
    color: var(--color-purple);
    border-bottom-color: #D1C4E9;
  }

  .ai-badge {
    display: inline-block;
    background: var(--color-purple);
    color: white;
    padding: 2px 12px;
    border-radius: 4px;
    font-size: 0.8em;
    font-weight: 500;
    margin-right: 8px;
  }

  .prompt-box {
    background: var(--color-bg-code);
    border: 1px solid #DDD;
    border-left: 4px solid var(--color-purple);
    border-radius: 4px;
    padding: 14px 18px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.82em;
    line-height: 1.6;
    margin: 10px 0;
  }

  section.summary h2 {
    border-bottom-color: var(--color-green);
  }

  .highlight {
    background: linear-gradient(transparent 60%, #FFF9C4 60%);
    font-weight: 500;
  }

  .red { color: var(--color-red); }
  .blue { color: var(--color-accent2); }
  .teal { color: var(--color-accent); }
  .purple { color: var(--color-purple); }
  .green { color: var(--color-green); }
  .orange { color: var(--color-orange); }
  .small { font-size: 0.82em; }
  .smaller { font-size: 0.75em; }

footer: "情報論 2025 ｜ matsulab"
---

<!-- _class: title -->
<!-- _paginate: false -->

# 情報論 2025 OD
## 生成AIツールの現在 ～私の使い方～

2025年度 前期 ｜ 松野 裕
オンデマンド配信: 2025年4月13日〜4月27日（50分）

---

# この授業について

## 情報論 2025 の概要

- **授業形式**: 100分 × 13回 ＋ オンデマンド（本回・50分）
- **テーマ**: **研究と就活における生成AIの効果的な活用**
- **対象**: 大学院理工学研究科の学生

### この授業で目指すこと

> 生成AIを「なんとなく使う」から「<span class="highlight">戦略的に使いこなす</span>」へ

- AIツールの特性を理解し、目的に応じて使い分けられる
- 研究活動（文献調査・論文執筆・発表）でAIを活用できる
- 就職活動（ES・面接準備）でAIを活用できる
- AIの限界を理解し、適切に付き合える

---

# 自己紹介

## 松野 裕（まつの ゆたか）

### 専門分野

| 分野 | 内容 |
|------|------|
| ソフトウェア安全性 | 安全なソフトウェアシステムの設計・検証 |
| D-Case / アシュアランスケース | システムの安全性を構造的に議論・記述する手法 |
| 自動運転の安全保証 | 自動運転システムの安全性を保証する枠組み |

### AI との関わり

- 研究・教育・日常のあらゆる場面で生成AIを活用中
- 2023年以降、授業にもAI活用を積極的に取り入れている

---

# 私のAI活用法（1）研究での活用

## 論文執筆支援

- 日本語の草稿 → AIで英語論文に翻訳・推敲
- 論文のロジック構成についてAIと壁打ち
- アブストラクトやイントロダクションの複数バージョン生成

## 文献調査

- 新しい研究テーマの関連研究を素早くサーベイ
- 論文の要約・比較表の作成
- 「この論文と似た研究は？」とAIに尋ねる

## 英語校正

- 文法チェックだけでなく、学術論文らしい表現への改善
- ネイティブチェック前の下準備として活用

---

# 私のAI活用法（2）教育での活用

## 授業スライド作成

- スライドの構成案をAIに相談、説明文の推敲
- 練習問題・クイズの自動生成

## 課題設計

- 学生の理解度に合わせた課題の難易度調整
- 採点ルーブリック・模範解答の作成支援

## 学生対応

- よくある質問への回答テンプレート作成
- フィードバックコメントの効率化

---

# 私のAI活用法（3）日常での活用

## メール作成

- 英語メールのドラフト作成（国際会議・共同研究先）
- 丁寧な日本語メールの推敲

## アイデア整理

- ブレインストーミングの相手としてAIを活用
- 思考の構造化・プロジェクト計画のたたき台作成

## その他

- 会議の議事録作成支援、プログラミング時のデバッグ
- 書類作成（申請書・報告書）の下書き

---

<!-- _class: section -->

# 生成AIの急速な進化

2022年〜2025年の主要なマイルストーン

---

# 生成AIの急速な進化

## 2022年〜2025年のタイムライン

| 時期 | できごと |
|------|----------|
| 2022年11月 | **ChatGPT** (GPT-3.5) 登場 → 世界に衝撃 |
| 2023年3月 | **GPT-4** リリース → 飛躍的な性能向上 |
| 2023年7月 | **Claude 2** (Anthropic) リリース |
| 2023年12月 | **Gemini** (Google) リリース |
| 2024年5月 | **GPT-4o** → マルチモーダル対応強化 |
| 2024年6月 | **Claude 3.5 Sonnet** → 長文理解で高評価 |
| 2024年12月 | **Gemini 2.0** → 推論能力が大幅向上 |
| 2025年〜 | 各社モデルがさらに進化、エージェント機能の台頭 |

> たった2〜3年で、AIは「おもちゃ」から「<span class="highlight">実用ツール</span>」へ変貌した

---

# 大学院生にとってのAI

## なぜ今、AIを学ぶべきか？

### 研究の効率化
- 文献調査にかかる時間を大幅に短縮
- 論文執筆のスピードアップ
- データ分析・可視化の支援

### スキルアップ
- プログラミング学習の加速、英語力の補強
- プレゼンテーション準備の効率化

### 就活準備
- ES（エントリーシート）の推敲、面接想定問答の練習
- 業界・企業研究の効率化

---

# この授業で身につくこと（前半）

## 全13回 ＋ OD のテーマ一覧

<span class="small">

| 回 | テーマ | 形式 |
|----|--------|------|
| OD | 生成AIツールの現在 ～私の使い方～ | オンデマンド |
| 1 | 授業ガイダンス＋AIツール総覧 | オンライン |
| 2 | プロンプトエンジニアリング実践 | 対面 |
| 3 | ガクチカ・ES作成 | 対面 |
| 4 | 面接・GD対策 | 対面 |
| 5 | AIを使った文献調査 | 対面 |

</span>

---

# この授業で身につくこと（後半）

## 全13回 ＋ OD のテーマ一覧（続き）

<span class="small">

| 回 | テーマ | 形式 |
|----|--------|------|
| 6 | 英語論文の読解・要約 | 対面 |
| 7 | AIを使った英語論文の作成 | 対面 |
| 8 | 効果的な研究発表スライドの作成 | 対面 |
| 9-13 | 発展テーマ（詳細は授業内で案内） | 対面 |

</span>

---

# この授業の進め方

## 毎回の流れ

1. **レクチャー**（30〜40分）: その回のテーマについて解説
2. **演習**（40〜50分）: 実際にAIツールを使ったハンズオン
3. **共有・ディスカッション**（10〜20分）: 結果の共有と議論

## 使用ツール

- <span class="teal">**Gemini Pro**</span>（Google）: 本授業の推奨ツール（**無料で利用可能**）
- その他のツールも適宜紹介・比較

## 連絡・提出

- 授業資料の配布: CSTポータル
- 課題の提出: CSTポータル

---

# 課題: 自分のAI利用経験レポート

## 提出期限: 4月27日（日）｜A4で1〜2枚程度

以下の項目について記述してください。

1. **普段使っているAIツール** — ツール名、使用頻度、有料/無料

2. **主な使用場面** — 研究・授業・就活・日常のどの場面で使っているか

3. **困っていること・疑問** — AIの信頼性や改善してほしい点

> ※ AIをまだ使ったことがない人は「AIに期待すること」を書いてください

---

# 次回予告

## 第1回: 授業ガイダンス＋AIツール総覧

**日時**: 2025年4月15日（火）オンライン授業

### 内容

- 授業の詳細ガイダンス（評価方法・スケジュール）
- AIツールの全体像を把握する
- <span class="teal">**Gemini Pro**</span> のセットアップと基本操作
- 無料で使える便利なAIツールの紹介

### 準備しておくこと

- Google アカウントの確認（Gemini Pro で使用）
- ノートPC を用意（演習で使用）

---

<!-- _class: section -->

# ご質問・ご相談は

CSTポータルまたはメールでお気軽にどうぞ

松野 裕 ｜ 情報科学専攻
