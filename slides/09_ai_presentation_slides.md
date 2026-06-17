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
    padding: 36px 60px 72px 60px;
    overflow: hidden;
    font-size: 26px;
  }

  section::after { content: ''; font-size: 0; }
  section p, section ul, section ol { margin: 0.5em 0; }
  section li { margin: 0.15em 0; }

  footer {
    font-family: 'Noto Sans JP', sans-serif;
    color: var(--color-green) !important;
    font-weight: 700;
    font-size: 14px !important;
    left: 40px !important;
    bottom: 20px !important;
    letter-spacing: 1px;
  }

  h1 { color: var(--color-text); font-weight: 700; font-size: 1.68em; margin: 0 0 0.4em 0; border-bottom: none; }
  h2 { color: var(--color-text); font-weight: 700; font-size: 1.22em; margin: 0.5em 0 0.3em 0; border-bottom: 3px solid var(--color-line); padding-bottom: 6px; }
  h3 { color: var(--color-accent); font-weight: 500; font-size: 1.05em; margin: 0.5em 0 0.2em 0; }

  code { font-family: 'IBM Plex Mono', 'Menlo', monospace; background: var(--color-bg-code); padding: 2px 6px; border-radius: 3px; font-size: 0.85em; }
  pre { background: var(--color-bg-code); border-left: 4px solid var(--color-accent); border-radius: 4px; padding: 14px; }
  pre code { background: none; padding: 0; }

  table { font-size: 0.82em; width: 100%; }
  th { background: var(--color-text); color: white; font-weight: 500; }
  tr:nth-child(even) { background: #F0F4FF; }

  blockquote { border-left: 4px solid var(--color-accent); background: var(--color-bg-light); padding: 12px 20px; margin: 12px 0; font-size: 0.95em; }

  section.title { text-align: center; display: flex; flex-direction: column; justify-content: center; border-bottom: 3px solid var(--color-line); }
  section.title h1 { font-size: 2.55em; margin-bottom: 0; }
  section.title h2 { font-size: 1.14em; font-weight: 400; color: var(--color-text); border: none; padding: 0; }
  section.title p { color: #999; font-size: 0.85em; }

  section.section { display: flex; flex-direction: column; justify-content: center; background: linear-gradient(135deg, #FAFAFA 0%, #F0F0F0 100%); }
  section.section h1 { font-size: 2.15em; color: var(--color-accent); text-align: center; }
  section.section p { text-align: center; color: #777; font-size: 1.1em; }

  section.ai-exercise h2 { color: var(--color-purple); border-bottom-color: #D1C4E9; }
  .ai-badge { display: inline-block; background: var(--color-purple); color: white; padding: 2px 12px; border-radius: 4px; font-size: 0.8em; font-weight: 500; margin-right: 8px; }
  .prompt-box { background: var(--color-bg-code); border: 1px solid #DDD; border-left: 4px solid var(--color-purple); border-radius: 4px; padding: 14px 18px; font-family: 'IBM Plex Mono', monospace; font-size: 0.74em; line-height: 1.5; margin: 10px 0; }

  .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 28px; align-items: start; }
  .three-col { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; align-items: stretch; }
  .flow { font-family: 'IBM Plex Mono', 'Menlo', monospace; background: var(--color-bg-code); border-left: 4px solid var(--color-accent); border-radius: 4px; padding: 14px 18px; line-height: 1.55; }
  .note-box { background: var(--color-bg-light); border-left: 4px solid var(--color-accent); border-radius: 4px; padding: 12px 16px; }
  .warn-box { background: #FFF4F4; border-left: 4px solid var(--color-red); border-radius: 4px; padding: 12px 16px; }
  .good-box { background: #F1FBF3; border-left: 4px solid var(--color-green); border-radius: 4px; padding: 12px 16px; }
  .card { border: 1px solid #DDE7EA; border-radius: 6px; padding: 14px 16px; background: #FFFFFF; box-shadow: 0 4px 12px rgba(0,0,0,0.04); }
  .card h3 { margin-top: 0; }
  .big-message { font-size: 1.45em; line-height: 1.45; font-weight: 700; color: var(--color-text); }
  .slide-mini { border: 2px solid #D8E8EA; border-radius: 6px; background: #FFFFFF; padding: 14px 16px; min-height: 245px; box-shadow: 0 8px 20px rgba(0, 151, 167, 0.08); }
  .slide-mini-title { font-size: 1.05em; font-weight: 700; color: var(--color-accent); border-bottom: 2px solid #D8E8EA; padding-bottom: 6px; margin-bottom: 10px; }
  .slide-mini ul { font-size: 0.82em; padding-left: 1.2em; }
  .tag { display: inline-block; background: #E9F4FF; color: var(--color-accent2); border: 1px solid #C9E0FF; border-radius: 4px; padding: 2px 8px; font-size: 0.76em; margin-right: 6px; }

  section.summary h2 { border-bottom-color: var(--color-green); }
  .highlight { background: linear-gradient(transparent 60%, #FFF9C4 60%); font-weight: 500; }
  .red { color: var(--color-red); }
  .blue { color: var(--color-accent2); }
  .teal { color: var(--color-accent); }
  .purple { color: var(--color-purple); }
  .green { color: var(--color-green); }
  .orange { color: var(--color-orange); }
  .small { font-size: 0.82em; }
  .smaller { font-size: 0.72em; }

footer: "情報論 2026 ｜ matsulab"
---

<!-- _class: title -->

# AIを使った研究発表スライド作成
## 情報論 2026 第9回 ― AI活用(7)

情報科学専攻 ｜ 松野 裕
matsuno.yutaka@nihon-u.ac.jp
2026年6月17日（対面授業・100分）

---

## 今日の中心メッセージ

<div class="big-message">
AIで「きれいなスライド」を作ることが目的ではない。<br>
<span class="highlight">自分が理解して、質問に答えられる発表資料</span>に直すことが目的。
</div>

<div class="note-box">
今回の材料は、前回までに作った英語Abstractと、その元になった論文本文。<br>
複数の作り方を試し、最後は自分で話しやすい方法を選ぶ。
</div>

---

## 本日のアジェンダ

| 時間 | 内容 |
|------|------|
| 10分 | AI時代の研究発表スライド |
| 15分 | 英語Abstractと論文本文をスライド構成に変換する |
| 25分 | NotebookLM / Marp / Gamma と Beamerの発展課題 |
| 40分 | 演習: 3つの方法を試し、完成版の方法を選ぶ |
| 10分 | 発表・相互レビュー・課題説明 |

---

## 今日の成果物

授業終了時に、次の4点を残す。

1. **英語Abstractと論文本文から作ったスライド構成案**
2. **NotebookLM / Marp / Gamma を試したメモ**
   - 正確性、編集しやすさ、発表しやすさを見る
3. **完成版で使う方法の候補**
   - 最終提出は選んだ1方式のスライドPDF
4. **修正すべき点のメモ**
   - 汎用表現、架空情報、説明できない用語を直す

<div class="note-box">
Beamerは希望者向けの発展課題として試してよい。
</div>

---

<!-- _class: section -->

# 1. AI時代の研究発表スライド

きれいに作る前に、伝える責任を持つ

---

## なぜこの授業でスライド作成を扱うのか

### 研究活動では、ほぼ必ず発表がある

- 研究室内の進捗報告
- 学会発表
- 修士論文発表
- 共同研究・企業との打ち合わせ
- 就職活動での研究紹介

> スライド作成は「デザイン作業」ではなく、<span class="highlight">研究を他者に説明できる形へ変換する作業</span>。

---

## AIを使うと何が変わるか

### AIが得意なこと
- 研究概要からスライド構成案を出す
- 専門用語を非専門家向けに言い換える
- 文章を短くする
- Marp / Beamer / HTML などの形式に変換する
- デザイン案や図解案を提案する

### AIだけに任せると危ないこと
- 結果・数値・文献を勝手に追加する
- 研究の新規性を過剰に盛る
- 発表者が説明できない図や言葉を入れる

---

## よくある「AIで作ったまま」のスライド

<div class="warn-box">

- タイトルが「背景」「目的」「手法」だけで、主張がない
- どの研究にも使える抽象語が多い
- 架空の成果、架空の評価値、架空の引用が入る
- それらしいアイコンや図があるが、発表者が説明できない
- 箇条書きを読むだけの発表になる

</div>

---

## 目指すべきスライド

<div class="good-box">

- 1枚ごとに「何を伝えるか」が明確
- 数値・図・引用・用語を自分で説明できる
- AIが作った一般論ではなく、自分の研究固有の内容になっている
- 聴衆に合わせて、専門性と分かりやすさのバランスを取っている

</div>

> きれいなスライドより、<span class="highlight">質問に答えられるスライド</span>。

---

## 判断基準: このスライドを話せるか

各スライドについて、次を自分に質問する。

1. このスライドの一番言いたいことは何か？
2. なぜこの情報をこの順番で出すのか？
3. 図や表の軸・単位・前提を説明できるか？
4. 数値や文献の出典を説明できるか？
5. 聴衆から質問されたら、自分の言葉で答えられるか？

---

<!-- _class: section -->

# 2. 良い研究発表スライドの構造

Abstractで骨格を作り、論文本文で具体化する

---

## 研究発表の基本構造

5〜8分程度の研究紹介なら、まずこの構成でよい。

| 枚数 | 役割 | 書くこと |
|---:|---|---|
| 1 | タイトル | 研究テーマ、名前、所属 |
| 2 | 背景 | なぜ重要か |
| 3 | 課題 | 何が未解決か |
| 4 | 目的 | 本研究で何を目指すか |
| 5 | 手法 | どう解くか |
| 6 | 結果/見込み | 何が分かったか、何を評価するか |
| 7 | 貢献 | 何が新しいか |
| 8 | まとめ | 持ち帰ってほしい結論 |

---

## 1枚1メッセージ

<div class="two-col">
<div class="slide-mini">
<div class="slide-mini-title red">弱い例</div>

### 研究背景

- 自動運転は重要
- 安全性が必要
- D-Caseがある
- 課題も多い

</div>
<div class="slide-mini">
<div class="slide-mini-title green">良い例</div>

### 自動運転では運用中の変化に安全説明が追従しにくい

- センサ構成や環境条件が変化する
- 従来の安全説明は設計時点に固定されやすい
- 運用中に説明を更新する仕組みが必要

</div>
</div>

---

## タイトルは「話題」ではなく「主張」

| 話題タイトル | 主張タイトル |
|---|---|
| 背景 | 高齢者見守りでは誤検知が現場負担になる |
| 目的 | 本研究は雑音環境での認識率低下を抑える |
| 手法 | 3種類の前処理を組み合わせて特徴量を安定化する |
| 結果 | 提案手法は誤検出を18%削減した |

> スライドタイトルを読むだけで、話の筋が追える状態にする。

---

## Abstractと論文本文からスライドへ変換する

### Abstractは圧縮された文章

- 背景、目的、手法、結果、意義が1段落に詰まっている
- そのまま貼ると、読むだけのスライドになる

### 論文本文は具体化の材料

- 手法、実験条件、図表、評価指標を確認する
- Abstractにない具体情報を補う
- ただし、本文にない結果や解釈は追加しない

<div class="note-box">
Abstractは全体の骨格、論文本文は根拠と具体例として使う。
</div>

---

## 変換例: Abstractの1文を分ける

<div class="prompt-box">
駅や空港では、放置手荷物を早期に検出することが安全管理上重要である。
</div>

### スライド化すると

- **背景スライド**: 公共空間では置き去り荷物の早期発見が必要
- **課題スライド**: 人手監視は見落とし・負担が大きい
- **目的スライド**: カメラ映像から放置手荷物を自動検出する

> 1文を1枚にするのではなく、<span class="highlight">聴衆が理解する順番</span>に分解する。

---

## 発表時間から逆算する

| 発表時間 | 目安枚数 | 1枚あたり |
|---:|---:|---:|
| 1分 | 1〜2枚 | 30〜60秒 |
| 3分 | 4〜5枚 | 35〜45秒 |
| 5分 | 6〜8枚 | 35〜50秒 |
| 10分 | 10〜14枚 | 40〜60秒 |

<div class="note-box">
今回の演習では、まず5〜8枚に絞る。<br>
詳細を増やすより、話せる構成を作る。
</div>

---

<!-- _class: section -->

# 3. AIでスライドを作るワークフロー

初稿生成 → 事実確認 → 自分の言葉へ修正

---

## 推奨ワークフロー

<div class="flow">
研究資料を集める<br>
→ AIに構成案を作らせる<br>
→ スライドごとの主張を決める<br>
→ ツールで初稿を生成する<br>
→ 架空情報・誇張・説明不能な表現を削る<br>
→ 短く発表して質問を受ける
</div>

---

## Step 1: AIに渡す材料を整理する

AIにいきなり「スライドを作って」と頼まない。

### 先に用意するもの
- 研究テーマ
- 背景と課題
- 目的
- 手法
- 結果、または今後評価する項目
- 既存研究との違い
- 発表時間と聴衆

<div class="warn-box">
未公開データ、個人情報、共同研究先の機密情報は入力しない。
</div>

---

## Step 2: まず構成案だけ作る

<div class="prompt-box">
あなたは大学院生の研究発表を支援する教員です。<br>
以下の英語Abstractと論文本文を、5分発表用の5〜8枚スライド構成にしてください。<br>
聴衆は情報系・電子系・機械系のM1学生です。<br><br>
条件:<br>
- 英語Abstractを全体構成のベースにする<br>
- 論文本文から手法、図表、実験条件、評価指標を補う<br>
- 1枚1メッセージにする<br>
- 各スライドに「主張タイトル」を付ける<br>
- 資料にない結果、解釈、文献は追加しない<br>
- 各スライドに、口頭で補足すべき内容を1行で書く<br><br>
[英語Abstractと論文本文を貼る]
</div>

---

## Step 3: スライド本文を短くする

<div class="prompt-box">
上の構成案の各スライドについて、本文を3箇条以内に短くしてください。<br>
各箇条は30字以内を目安にしてください。<br>
専門用語は必要最小限にし、削った内容はスピーカーノートに回してください。
</div>

### ポイント
- スライドは読む資料ではなく、話すための支え
- 詳細はノート、補足資料、口頭説明に回す

---

## Step 4: AI出力を批判的に見る

<div class="prompt-box">
以下のスライド案を、研究発表として批判的にレビューしてください。<br>
特に次を確認してください。<br>
1. 根拠のない誇張表現<br>
2. 資料にない数値・結果・文献<br>
3. 発表者が説明できない可能性がある専門用語<br>
4. 1枚1メッセージになっていないスライド<br><br>
出力は「問題点 / なぜ問題か / 修正案」の表にしてください。
</div>

---

## Step 5: 話してみて直す

### 見た目の修正より先に、声に出す

1. 1枚30〜45秒で説明してみる
2. 詰まった言葉に印を付ける
3. 説明できない図・数値・用語を削るか調べ直す
4. 友人に1分だけ聞いてもらう
5. 質問された箇所をスライドに反映する

> 発表練習は、スライドの品質チェックでもある。

---

<!-- _class: section -->

# 4. ツールの使い分け

NotebookLM / Marp / Gammaを基本に、Beamerは発展的に扱う

---

## 今回の課題で試す作り方

| 扱い | ツール | 何を見るか |
|---|---|---|
| 基本 | **NotebookLM** | 自分の資料に基づいて構成できるか |
| 基本 | **Marp** | Markdownで管理・再生成しやすいか |
| 基本 | **Gamma** | 見た目の初稿を短時間で作れるか |
| 発展 | **Beamer** | 論文調・数式中心の発表に向くか |

<div class="note-box">
完成版は1つの方法を選んでよい。比較して選ぶことと、最後に自分で直すことが重要。
</div>

---

## NotebookLM: 資料に基づく初稿作成

### 使い方
1. 前回作った英語Abstractを入れる
2. その元になった論文本文PDFを入れる
3. 必要なら文献調査メモや研究概要を追加する
4. 資料に基づいて質問する
5. Slide Deck機能で生成する
6. PDFとしてダウンロードする

<div class="note-box">
NotebookLMは、手元資料から話の流れを作る用途に向いている。<br>
ただし、出てきた内容は必ず元資料と照合する。
</div>

<span class="smaller">参考: Google NotebookLM Help, "Generate a Slide Deck in NotebookLM"</span>

---

## NotebookLMでのプロンプト例

<div class="prompt-box">
アップロードした資料だけに基づいて、5分発表用のスライド資料を作成してください。<br><br>
聴衆: 情報系・電子系・機械系のM1学生<br>
目的: 自分の研究の背景、課題、手法、貢献を理解してもらう<br><br>
条件:<br>
- 資料にない数値、文献、結果は追加しない<br>
- 各スライドは1メッセージにする<br>
- タイトルは「背景」ではなく主張文にする<br>
- 発表者が口頭で補足すべき内容をメモに入れる
</div>

---

## NotebookLMの注意点

<div class="warn-box">

- ソースに基づいていても、出力に不正確さが入ることがある
- 図やビジュアルが研究内容を正しく表しているとは限らない
- 生成後の修正では、ソースが反映されない場面もある
- 共有設定・公開範囲に注意する

</div>

> 「資料に基づく」ことは、<span class="highlight">正しいことの保証ではない</span>。

---

## Marp: Markdownからスライドを作る

### この授業のスライドもMarpで作っている

- 授業内容をAIに伝える
- Marp形式のMarkdownにする
- PDF / PPTXに変換する
- Gitで履歴管理する

<div class="good-box">
Marpは、文章構成と版管理を重視する研究発表に向いている。
</div>

<span class="smaller">参考: Marp Markdown Presentation Ecosystem</span>

---

## この授業スライドの作り方

### AI支援でMarp資料を作り、人が確認して直す

<div class="flow">
授業のねらい・扱うツール・課題方針を決める<br>
→ AIにスライド構成案とMarp Markdown初稿を作らせる<br>
→ 教員が内容、表現、課題条件、参考資料を確認する<br>
→ MarpでPDF / PPTXに変換する<br>
→ 表示崩れ、長いURL、提出条件の誤解を直す
</div>

<div class="two-col">
<div class="good-box">
<strong>AIに任せたこと</strong><br>
構成案、短い説明文、表、プロンプト例、Marp形式への整形
</div>
<div class="warn-box">
<strong>人が確認したこと</strong><br>
授業方針、事実関係、提出物、参考資料、AI未使用例との区別
</div>
</div>

---

## Marp用プロンプト例

<div class="prompt-box">
以下の研究発表構成を、Marp形式のMarkdownスライドにしてください。<br><br>
条件:<br>
- 16:9<br>
- 1スライド1メッセージ<br>
- 各スライドの本文は3箇条以内<br>
- 表が有効な箇所はMarkdown表を使う<br>
- 発表者が読み上げる原稿ではなく、話の支えになる短い文にする<br><br>
[構成案を貼る]
</div>

---

## Beamer: 発展課題として扱う

### 向いている場面
- 数式が多い
- 論文調の発表にしたい
- LaTeXで論文やレポートを書いている
- 図表や参考文献をLaTeXで管理したい

### 注意
- 今回の必須比較には含めない
- LaTeXに慣れていない人には負荷が高い
- Overleafは無料枠のコンパイル制限に注意

### Beamerで作った授業スライド例
<span class="smaller">松野の授業スライド（Overleaf）: https://www.overleaf.com/6334356467scvzgpzyqwnp</span>

<span class="smaller">参考: CTAN beamer package / Overleaf Plan limits / 松野の授業スライド例</span>

---

## Beamerを試すなら: OpenAI Prism

### Prismでできること

- ブラウザ上でLaTeXプロジェクトを編集・コンパイルする
- AIにBeamer形式の `.tex` を作ってもらう
- コンパイルエラーの原因を相談する
- 発表用PDFとして出力する

<div class="note-box">
BeamerはPrismやローカルLaTeX環境を使える人向けの発展課題にする。
</div>

<span class="smaller">参考: OpenAI Prism / Prism Help</span>

---

## 研究発表スライド例: SAFEComp 2025

### 松野の国際会議発表スライド

**Consensus Building in Level 4 Automated Driving Field Trials through Assurance Cases**

- Yutaka Matsuno, Michio Hayashi, Tomoyuki Tsuchiya
- SAFEComp 2025発表資料（23枚）
- Assurance Case / GSN、Safety Status Report、Questionnaire、Consensus Scoreを扱う

<div class="warn-box">
このスライドはAIを用いて作成したものではない。<br>
AI生成例ではなく、研究発表スライドの実例として見る。
</div>

<span class="smaller">https://safecomp2025.se/wp-content/uploads/2025/09/Consensus-Building-in-Level-4-Automated-Driving-Field-Trials-through-Assurance-cases.pdf</span>

---

## Gamma: 見た目の初稿をすばやく作る

### 強み
- 見た目の整った初稿がすぐ出る
- レイアウト案を考える負荷が小さい
- 短い発表や企画説明には便利

### 注意
- 内容が一般論になりやすい
- 研究固有の前提や制約が抜けやすい
- きれいだが説明できないスライドになりやすい
- 無料枠の範囲で試す

> Gammaは「デザインの初稿」、研究内容の最終判断は自分。

---

## どのツールを選ぶか

| 状況 | 推奨 |
|---|---|
| 元資料に沿って構成を作りたい | NotebookLM |
| 修正履歴や再生成を重視したい | Marp |
| まず見た目の方向性を試したい | Gamma |
| 数式やLaTeXに慣れている | Beamer（発展） |
| 最後にPowerPointで直したい | NotebookLM / GammaのPPTX出力 |

---

<!-- _class: section -->

# 5. AIで作ったままに見えないように直す

汎用表現を、研究固有の説明へ置き換える

---

## 「AIで作ったまま」に見える例

次のようなスライドは、見た目が整っていても発表資料として弱い。

- 「革新的」「大きな可能性」「重要な役割」だけで中身がない
- 研究対象、データ、評価条件が具体的でない
- 全スライドが同じ構成・同じ語尾
- 図がきれいだが、何を示すか説明できない
- タイトルを見ても結論が分からない

---

## 汎用表現を研究固有に直す

| 汎用的な表現 | 直し方 |
|---|---|
| 本研究は革新的な手法を提案する | 何が既存手法と違うかを書く |
| 実験により有効性を示した | データ数、評価指標、比較対象を書く |
| 精度が向上した | 何の精度が、どれだけ、どの条件で向上したかを書く |
| 社会に貢献できる | どの現場のどの負担を減らすかを書く |

---

## 図表は「説明できるもの」だけ使う

### 図を入れる前に確認する

- この図は何を示しているか
- 軸、単位、凡例を説明できるか
- どのデータから作ったか
- どこが自分の主張を支えているか
- 出典や作成方法を示せるか

<div class="warn-box">
AIが作った模式図は便利だが、研究手法や結果を誤って表すことがある。
</div>

---

## スピーカーノートを作る

スライドに全部書かない。話す内容を分ける。

| スライドに書く | ノートで話す |
|---|---|
| 主張タイトル | 背景の詳しい説明 |
| 重要な数値・図 | なぜその数値が重要か |
| キーワード | 用語の補足 |
| 結論 | 研究上の制約や今後の予定 |

> 発表者が理解していることは、ノートと口頭説明に現れる。

---

## 想定質問を作る

AIにスライドを作らせたあと、AIに質問者役をさせる。

<div class="prompt-box">
以下の研究発表スライド案を読んで、聴衆から出そうな質問を5つ作ってください。<br>
質問は、背景、手法、結果、新規性、限界の観点から出してください。<br>
それぞれについて、発表者が答えるべき要点も書いてください。
</div>

<div class="note-box">
答えられない質問が出たら、その部分はスライドの説明か自分の理解に不足がある。
</div>

---

<!-- _class: section -->

# 6. 演習

英語Abstractと論文本文を、5〜8枚の発表資料に変換する

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">演習手順</span> 全体の流れ

1. 材料を準備する
2. 構成案を作る
3. 3つの方法を短く試す
4. 完成版で使う方式を選ぶ
5. 自分で説明できる内容に直す
6. 発表して質問を受ける

<div class="good-box">
最終的に評価するのは、提出された完成スライドPDF。
</div>

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">演習手順</span> 材料を準備する

今日の基本材料は、第5〜6回で作った英語Abstractと、その元になった論文本文。

### 追加してよいもの

- 第4回の文献調査レポート
- 自分の研究概要メモ
- 卒論要旨、学会予稿、研究計画書
- 図表や評価結果のメモ

### メモにする項目
背景 / 課題 / 目的 / 手法 / 結果または見込み / 貢献

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">演習手順</span> 構成案を作る

まず1つの構成案を作る。ここではツールは自由。

<div class="prompt-box">
以下の英語Abstractと論文本文をもとに、5分発表用の5〜8枚スライド構成を作ってください。<br>
各スライドについて、主張タイトル、本文3箇条、口頭補足1行を出してください。<br>
英語Abstractを全体構成のベースにし、論文本文から具体情報を補ってください。<br>
資料にない結果・文献・数値は追加しないでください。<br><br>
[英語Abstractと論文本文を貼る]
</div>

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">演習手順</span> 3つの方法を試す

同じ英語Abstractと論文本文から、3つの方法を短く試す。

| 方法 | 試すこと | 今日見る点 |
|---|---|---|
| NotebookLM | 構成案または初稿 | 元資料に沿っているか |
| Marp | Markdown化の一部 | 自分で直しやすいか |
| Gamma | 見た目の初稿 | 見た目と内容のバランス |

<div class="note-box">
3つすべてを完成させる必要はない。違いを見て、完成版に使う方法を選ぶ。
</div>

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">演習手順</span> 比較して方式を選ぶ

3つの方法を比べて、完成版で使う方法を1つ選ぶ。

| 観点 | 確認すること |
|---|---|
| 正確性 | 資料にない内容を足していないか |
| 編集しやすさ | 自分で直しやすい形式か |
| 発表しやすさ | 自分の言葉で説明できるか |
| 見た目 | 研究内容を邪魔していないか |
| 再現性 | あとで修正・再生成しやすいか |

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">演習手順</span> 完成版に向けて直す

選んだ方式のスライドを、自分で説明できる内容に直す。

1. 汎用的な表現を、自分の研究固有の表現へ直す
2. 架空の成果・文献・図を削除する
3. 説明できない専門用語を削るか補足する
4. タイトルを主張文へ直す
5. スライド枚数・文字量を発表時間に合わせる

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">演習手順</span> 発表と相互レビュー

### ペアで実施

1. 作ったスライドの最初の2〜3枚を短く説明する
2. 聞き手は質問を2つ出す
3. 発表者は、答えられた質問・答えに詰まった質問を記録する
4. 詰まった箇所をスライド修正候補にする

### レビュー観点
内容は具体的か / AIで作ったままに見えないか / 発表者が説明できているか

---

## 課題の進め方

前回の英語Abstractを出発点にし、論文本文で内容を補う。

1. NotebookLM / Marp / Gammaの3つの方法を試す
2. 完成版に使う方式を1つ選ぶ
3. 選んだ方式でスライドを作る
4. 自分で説明できる内容に直す
5. 完成スライドPDFを提出する

<div class="note-box">
Beamerは発展課題。PrismやローカルLaTeX環境を使える人は追加で試してよい。
</div>

<div class="good-box">
最終提出は、選んだ1方式で作成した完成スライドPDFに統一する。
</div>

---

## 課題の提出物

### 提出物

1. **完成スライド**
   - 5〜8枚、PDF
   - NotebookLM / Marp / Gammaのいずれかで作成してよい
   - Beamerで作った場合もPDFなら提出してよい

### スライド内に含めること

- 研究の背景、課題、目的、手法、貢献
- 自分が説明できる図表・数値・用語
- 必要に応じて、出典や根拠

<div class="note-box">
提出するのは完成スライドPDFのみ。
</div>

<div class="good-box">
評価は、提出された完成スライドPDFを対象に行う。
</div>

---

## 発展課題と締切

### Beamerを試す場合

- NotebookLM / Marp / Gammaの代わりに、Beamerを完成版に選んでもよい
- 最終提出はPDFにそろえる

### 締切

次回授業開始時まで

---

## 評価観点

| 観点 | 内容 |
|---|---|
| 内容理解 | 発表者が自分の言葉で説明できる |
| 正確性 | 架空情報、誇張、根拠不明の図表がない |
| 構成 | 背景→課題→目的→手法→貢献がつながる |
| 研究固有性 | 汎用表現ではなく、自分の研究の内容になっている |
| 発表可能性 | 時間内に話せる量で、1枚1メッセージ |
| AI活用の工夫 | 選んだ方法の出力を、自分で説明できる形に直している |

<div class="note-box">
授業中の試作メモや途中ファイルではなく、最終提出されたPDFスライドで評価する。
</div>

---

<!-- _class: summary -->

## 今日のまとめ

- AIはスライド作成の初稿を速く作れる
- ただし、完成品としてそのまま使うと危ない
- NotebookLMは、自分の資料に基づく構成案作成に向いている
- Marpは、授業資料や研究発表をMarkdownで管理しやすい
- Gammaは、見た目の初稿作成に向いている
- Beamerは、Prismなどを使える人向けの発展課題
- 最終的に重要なのは、<span class="highlight">自分が理解して話せるスライド</span>に直すこと

---

## この授業内容の参考資料（1）

### スライド設計・研究発表の考え方

| 本授業で扱った考え方 | 参考にした資料 |
|---|---|
| 話題タイトルではなく主張タイトルにする | Assertion-Evidence approach |
| 1枚1メッセージで構成する | Assertion-Evidence approach |
| 箇条書きだけに頼らず、根拠・図表で支える | Assertion-Evidence approach |
| 発表者が画面を読むのではなく、証拠を説明する | Assertion-Evidence tutorial |

<span class="smaller">
参考: Michael Alley / Penn State, Rethinking Presentations in Engineering and Science<br>
https://www.assertion-evidence.com/<br>
https://www.assertion-evidence.org/tutorial.html
</span>

---

## この授業内容の参考資料（2）

### AI・スライド作成ツールの機能情報

| 本授業で扱った内容 | 参考にした資料 |
|---|---|
| NotebookLMでSlide Deckを生成し、PDF/PPTXで出力できる | Google NotebookLM Help |
| AI生成スライドには視覚的・事実的な不正確さが入り得る | Google NotebookLM Help |
| MarpでMarkdownからHTML/PDF/PPTXに変換できる | Marp official site |
| GammaはAIプレゼン作成・PDF/PPTX出力に対応する | Gamma official site |

<span class="smaller">
参考: https://support.google.com/notebooklm/answer/16757456<br>
https://marp.app/<br>
https://gamma.app/
</span>

---

## この授業内容の参考資料（3）

### Beamer・LaTeX環境の機能情報

| 本授業で扱った内容 | 参考にした資料 |
|---|---|
| BeamerはLaTeXのプレゼン・スライド作成用クラス | CTAN beamer |
| Overleaf無料プランにはコンパイル時間の制限がある | Overleaf Plan limits |
| Beamerで作った授業スライドの例 | 松野の授業スライド（Overleaf） |
| PrismでLaTeX作成・エラー診断・コンパイル支援ができる | OpenAI Prism / Prism Help |

<span class="smaller">
参考: https://ctan.org/pkg/beamer<br>
https://docs.overleaf.com/getting-started/free-and-premium-plans/plan-limits<br>
https://www.overleaf.com/6334356467scvzgpzyqwnp<br>
https://openai.com/index/introducing-prism/<br>
https://help.openai.com/en/articles/20001050-troubleshooting-and-getting-help-in-prism
</span>

---

## この授業内容の参考資料（4）

### 研究発表スライド例

| 本授業で扱った内容 | 参考にした資料 |
|---|---|
| 研究発表スライドの実例 | Matsuno, Hayashi, Tsuchiya, SAFEComp 2025 presentation slides |
| AIを用いずに作成した発表資料の例 | Consensus Building in Level 4 Automated Driving Field Trials through Assurance Cases |

<span class="smaller">
参考: https://safecomp2025.se/wp-content/uploads/2025/09/Consensus-Building-in-Level-4-Automated-Driving-Field-Trials-through-Assurance-cases.pdf
</span>

---

## 本資料での使い方

この授業資料は、上記の資料をそのまま要約したものではない。

### 授業向けに組み合わせた点

- Assertion-Evidenceの考え方を、M1の研究紹介スライドに適用
- NotebookLM、Marp、Gammaを基本に、Beamerを<span class="highlight">発展的な選択肢</span>として整理
- 本授業スライド自体を、AI支援で作成したMarp資料の例として扱う
- SAFEComp 2025発表資料を、AI未使用の研究発表スライド例として紹介
- 「AIで作る」よりも、<span class="highlight">AI出力を自分が説明できる形に直す</span>ことを重視
- 前回作った英語Abstractを、発表資料へ変換する演習に接続
