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

  h1 { color: var(--color-text); font-weight: 700; font-size: 1.7em; margin: 0 0 0.4em 0; border-bottom: none; }
  h2 { color: var(--color-text); font-weight: 700; font-size: 1.25em; margin: 0.5em 0 0.3em 0; border-bottom: 3px solid var(--color-line); padding-bottom: 6px; }
  h3 { color: var(--color-accent); font-weight: 500; font-size: 1.05em; margin: 0.5em 0 0.2em 0; }

  code { font-family: 'IBM Plex Mono', 'Menlo', monospace; background: var(--color-bg-code); padding: 2px 6px; border-radius: 3px; font-size: 0.85em; }
  pre { background: var(--color-bg-code); border-left: 4px solid var(--color-accent); border-radius: 4px; padding: 16px; }
  pre code { background: none; padding: 0; }

  table { font-size: 0.82em; width: 100%; }
  th { background: var(--color-text); color: white; font-weight: 500; }
  tr:nth-child(even) { background: #F0F4FF; }

  blockquote { border-left: 4px solid var(--color-accent); background: var(--color-bg-light); padding: 12px 20px; margin: 12px 0; font-size: 0.95em; }

  section.title { text-align: center; display: flex; flex-direction: column; justify-content: center; border-bottom: 3px solid var(--color-line); }
  section.title h1 { font-size: 2.7em; margin-bottom: 0; }
  section.title h2 { font-size: 1.16em; font-weight: 400; color: var(--color-text); border: none; padding: 0; }
  section.title p { color: #999; font-size: 0.85em; }

  section.section { display: flex; flex-direction: column; justify-content: center; background: linear-gradient(135deg, #FAFAFA 0%, #F0F0F0 100%); }
  section.section h1 { font-size: 2.2em; color: var(--color-accent); text-align: center; }
  section.section p { text-align: center; color: #777; font-size: 1.1em; }

  section.ai-exercise h2 { color: var(--color-purple); border-bottom-color: #D1C4E9; }
  .ai-badge { display: inline-block; background: var(--color-purple); color: white; padding: 2px 12px; border-radius: 4px; font-size: 0.8em; font-weight: 500; margin-right: 8px; }
  .prompt-box { background: var(--color-bg-code); border: 1px solid #DDD; border-left: 4px solid var(--color-purple); border-radius: 4px; padding: 14px 18px; font-family: 'IBM Plex Mono', monospace; font-size: 0.78em; line-height: 1.55; margin: 10px 0; }

  .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 28px; align-items: start; }
  .flow { font-family: 'IBM Plex Mono', 'Menlo', monospace; background: var(--color-bg-code); border-left: 4px solid var(--color-accent); border-radius: 4px; padding: 14px 18px; line-height: 1.55; }
  .note-box { background: var(--color-bg-light); border-left: 4px solid var(--color-accent); border-radius: 4px; padding: 12px 16px; }
  .warn-box { background: #FFF4F4; border-left: 4px solid var(--color-red); border-radius: 4px; padding: 12px 16px; }
  .site-wireframe { width: 92%; margin: 12px auto 10px auto; border: 3px solid #B8DDE2; border-radius: 8px; overflow: hidden; background: #FFFFFF; box-shadow: 0 8px 20px rgba(0, 151, 167, 0.10); font-size: 0.72em; }
  .wf-header { display: flex; justify-content: space-between; align-items: center; padding: 10px 16px; background: #EAF7F8; border-bottom: 2px solid #B8DDE2; }
  .wf-brand { font-weight: 700; color: var(--color-text); }
  .wf-nav { display: flex; gap: 8px; }
  .wf-pill { background: #FFFFFF; border: 1px solid #A9D5DA; border-radius: 999px; padding: 3px 10px; color: var(--color-accent); font-size: 0.82em; }
  .wf-hero { display: grid; grid-template-columns: 1.25fr 0.75fr; gap: 18px; padding: 16px 18px; background: linear-gradient(135deg, #FFFFFF 0%, #F5FBFC 100%); border-bottom: 2px solid #D7EBEE; }
  .wf-hero-title { font-weight: 700; font-size: 1.15em; color: var(--color-text); margin-bottom: 8px; }
  .wf-line { height: 9px; border-radius: 99px; background: #DCECEF; margin: 7px 0; }
  .wf-line.short { width: 70%; }
  .wf-tags { display: flex; gap: 8px; margin-top: 12px; }
  .wf-tag { background: #E9F4FF; color: var(--color-accent2); border: 1px solid #C9E0FF; border-radius: 4px; padding: 4px 8px; font-size: 0.78em; }
  .wf-photo { border: 2px dashed #B8DDE2; border-radius: 6px; display: flex; align-items: center; justify-content: center; color: #789; background: #FFFFFF; min-height: 78px; }
  .wf-main { display: grid; grid-template-columns: 0.9fr 1.1fr; border-bottom: 2px solid #D7EBEE; }
  .wf-panel { padding: 14px 18px; min-height: 124px; }
  .wf-panel + .wf-panel { border-left: 2px solid #D7EBEE; }
  .wf-heading { font-weight: 700; color: var(--color-accent); margin-bottom: 10px; }
  .wf-profile-row { display: flex; align-items: center; gap: 10px; margin-bottom: 9px; }
  .wf-dot { width: 24px; height: 24px; border-radius: 50%; background: #D7EBEE; border: 2px solid #9FCFD6; }
  .wf-row { display: grid; grid-template-columns: 92px 1fr; gap: 8px; margin: 7px 0; align-items: center; }
  .wf-label { color: #667; font-size: 0.78em; }
  .wf-bottom { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; padding: 12px 14px; background: #FAFCFC; }
  .wf-card { border: 1px solid #C9E3E6; border-radius: 6px; padding: 10px 12px; background: #FFFFFF; min-height: 58px; }
  .wf-card-title { font-weight: 700; color: var(--color-text); margin-bottom: 6px; }

  section.summary h2 { border-bottom-color: var(--color-green); }
  .highlight { background: linear-gradient(transparent 60%, #FFF9C4 60%); font-weight: 500; }
  .red { color: var(--color-red); }
  .blue { color: var(--color-accent2); }
  .teal { color: var(--color-accent); }
  .purple { color: var(--color-purple); }
  .green { color: var(--color-green); }
  .orange { color: var(--color-orange); }
  .small { font-size: 0.82em; }
  .smaller { font-size: 0.74em; }

footer: "情報論 2026 ｜ matsulab"
---

<!-- _class: title -->

# GitHub演習とWebサイト作成
## 情報論 2026 第7回 ― AI活用(5)

日本大学大学院理工学研究科 ｜ 松野 裕
matsuno.yutaka@nihon-u.ac.jp
2026年6月3日（オンデマンド授業）

---

## 本日のアジェンダ

| 時間 | 内容 |
|------|------|
| 10分 | Git/GitHubとGitHub Pagesの概要 |
| 10分 | 環境準備（GitHub・GitHub Desktop・VS Code） |
| 20分 | 修士課程学生のWebサイト設計 |
| 25分 | AIでWebサイトの初期案を生成し、内容を編集 |
| 20分 | GitHub Pagesで公開 |
| 5分 | 提出方法・自己チェック |

<span class="small">台風のため、本回はオンデマンドで実施します。次回の対面授業では第6回の内容を扱います。</span>

---

## 授業の目標

この授業を終えると、以下のことができるようになります:

1. <span class="teal">**GitHub Pages**</span>で自分のWebサイトを公開できる
2. AIを使って、Webサイトの初期案を効率よく作成できる
3. 修士課程学生として<span class="highlight">公開してよい情報・避けるべき情報</span>を判断できる
4. WebサイトをGitHubで管理し、更新内容をコミット・プッシュできる

> 本回のゴール: `https://ユーザー名.github.io/` で自分のページを表示する

---

## なぜ大学院生がWebサイトを持つのか

### 研究活動を「見える化」する

- 研究テーマ、関心分野、使用技術を整理できる
- 学会・共同研究・就職活動で自己紹介資料になる
- GitHub上のコード、論文、発表資料への入口になる
- 研究の進展に合わせて継続的に更新できる

<div class="note-box">
Webサイトは「派手な自己紹介」ではなく、研究者としての活動を簡潔に伝えるポートフォリオです。
</div>

---

## Gitとは

### 分散型バージョン管理システム

- <span class="teal">**変更履歴の記録**</span>: いつ、何を変更したかを残す
- <span class="teal">**過去の状態への復元**</span>: 間違えても戻せる
- <span class="teal">**共同作業**</span>: 研究室やチームで同じファイルを扱える

### 基本イメージ

```text
編集 → add → commit → push
```

> 今日の演習では、コマンドラインではなく <span class="highlight">GitHub Desktop</span> を使います

---

## GitHubとは

### Gitリポジトリのホスティングサービス

| 機能 | 今日の使い方 |
|------|--------------|
| リポジトリ | WebサイトのHTML/CSSを保存 |
| コミット履歴 | どの内容をいつ更新したか記録 |
| GitHub Pages | Webサイトとして公開 |
| プロフィール | 研究・開発活動への入口 |

<span class="small">研究コード、論文用LaTeX、実験スクリプトの管理にも利用できます。</span>

---

<!-- _class: section -->

# 環境準備

今日使う3つの道具

---

## 準備するもの

| ツール | 用途 | URL |
|--------|------|-----|
| GitHub | リポジトリ作成・Pages設定 | `https://github.com` |
| GitHub Desktop | コミット・プッシュのGUI操作 | `https://desktop.github.com` |
| VS Code | AIが生成したコードの編集 | `https://code.visualstudio.com` |

### VS Codeの推奨拡張機能

- **Live Server**: Webページをブラウザで即時プレビュー
- **Prettier**: コードの自動整形
- **Japanese Language Pack**: VS Codeの日本語化

---

## GitHubアカウント作成

### 手順

1. [github.com](https://github.com) にアクセス
2. 「Sign up」をクリック
3. メールアドレス、パスワード、ユーザー名を入力
4. メール認証を完了

### ユーザー名のポイント

- ポートフォリオとして使うため、本名または研究用に使いやすい名前を推奨
- 短く、読みやすく、長く使えるもの
- 例: `yutaka-matsuno`, `matsuno-y`

---

## GitHub Desktopの基本操作

| 操作 | 意味 | 今日の操作 |
|------|------|------------|
| Clone | GitHub上のリポジトリをPCへコピー | File → Clone Repository |
| Commit | 変更を履歴として記録 | Summary入力 → Commit |
| Push | PCの変更をGitHubへ送信 | Push origin |
| Pull | GitHubの変更をPCへ取得 | Fetch origin / Pull origin |

<div class="flow">
VS Codeで編集<br>
→ GitHub Desktopで変更確認<br>
→ Commit<br>
→ Push<br>
→ GitHub Pagesで公開
</div>

---

<!-- _class: section -->

# Webサイト設計

修士課程学生として適切な内容を考える

---

## Webサイトの目的を決める

### 良いWebサイトは「誰に何を伝えるか」が明確

| 読み手 | 伝える内容 |
|--------|------------|
| 研究者・教員 | 研究テーマ、方法、成果、連絡先 |
| 企業・採用担当者 | 技術スキル、プロジェクト経験、GitHub |
| 研究室の後輩 | 研究分野、使用ツール、学習の入口 |
| 自分自身 | 活動履歴、成果物、更新ログ |

> 今日作るページは <span class="highlight">研究ポートフォリオ</span> として設計します

---

## 推奨するページ構成

| セクション | 掲載する内容 |
|------------|--------------|
| Profile | 名前、所属、学年、研究室 |
| Research | 研究テーマ、背景、目的、手法の概要 |
| Projects | 開発物、実験システム、公開可能なコード |
| Skills | 使用言語、ツール、分析手法 |
| Publications | 論文、学会発表、ポスター、受賞 |
| Contact | 大学メール、GitHub、Google Scholar等 |

<span class="small">最初は1ページ構成で十分です。成果が増えたらページを分けます。</span>

---

## 研究テーマの書き方

### 専門家以外にも伝わる1段落を用意する

| 項目 | 例 |
|------|----|
| 研究分野 | ソフトウェア工学、AI安全性、画像処理など |
| 課題 | 何が困っているのか |
| アプローチ | どの方法で解決しようとしているか |
| 期待される貢献 | 何が良くなるのか |

### 悪い例

<span class="red">「〇〇について研究しています」だけで終わる</span>

### 良い例

<span class="teal">背景、目的、方法、成果の見込みが短く書かれている</span>

---

## 掲載してよい内容・避ける内容

| 掲載してよい | 避ける |
|--------------|--------|
| 公開済み・発表済みの成果 | 未発表データ、共同研究先の秘密情報 |
| 大学メール、GitHubリンク | 学生番号、私用電話番号、住所 |
| 自分で作成した図・画像 | 著作権の不明な画像、無断転載 |
| 公開リポジトリ | APIキー、パスワード、個人情報 |

<div class="warn-box">
公開前に「研究室のルール」「共同研究契約」「論文投稿前の公開可否」に反していないか確認してください。
</div>

---

## 修士課程学生サイトのワイヤーフレーム

<div class="site-wireframe">
  <div class="wf-header">
    <div class="wf-brand">氏名 / 所属</div>
    <div class="wf-nav">
      <span class="wf-pill">Research</span>
      <span class="wf-pill">Projects</span>
      <span class="wf-pill">Contact</span>
    </div>
  </div>
  <div class="wf-hero">
    <div>
      <div class="wf-hero-title">研究テーマを1文で説明</div>
      <div class="wf-line"></div>
      <div class="wf-line short"></div>
      <div class="wf-tags">
        <span class="wf-tag">キーワード</span>
        <span class="wf-tag">使用技術</span>
      </div>
    </div>
    <div class="wf-photo">写真・研究図・概要図</div>
  </div>
  <div class="wf-main">
    <div class="wf-panel">
      <div class="wf-heading">Profile</div>
      <div class="wf-profile-row"><span class="wf-dot"></span><span>所属・学年・研究室</span></div>
      <div class="wf-profile-row"><span class="wf-dot"></span><span>関心分野・リンク</span></div>
    </div>
    <div class="wf-panel">
      <div class="wf-heading">Research Summary</div>
      <div class="wf-row"><span class="wf-label">背景</span><span class="wf-line"></span></div>
      <div class="wf-row"><span class="wf-label">目的</span><span class="wf-line"></span></div>
      <div class="wf-row"><span class="wf-label">手法</span><span class="wf-line short"></span></div>
    </div>
  </div>
  <div class="wf-bottom">
    <div class="wf-card"><div class="wf-card-title">Projects</div><div class="wf-line"></div></div>
    <div class="wf-card"><div class="wf-card-title">Publications</div><div class="wf-line"></div></div>
    <div class="wf-card"><div class="wf-card-title">Contact</div><div class="wf-line"></div></div>
  </div>
</div>

<span class="small">派手さより、読みやすさ・更新しやすさ・公開情報の適切さを重視します。</span>

---

<!-- _class: section -->

# AIでWebサイトを作成

初期案を生成し、自分の内容に修正する

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">AI演習</span> Webサイトの初期案を生成する

### プロンプト例

<div class="prompt-box">
修士課程1年の学生が公開する研究ポートフォリオサイトを作成してください。<br>
HTML/CSS/JavaScriptを1つの `index.html` にまとめてください。<br>
含めるセクションは Profile, Research, Projects, Skills, Publications, Contact です。<br>
研究テーマは「[自分の研究テーマ]」、所属は「日本大学大学院 理工学研究科 [専攻名]」、研究室は「[研究室名]」です。<br>
落ち着いた配色、レスポンシブデザイン、アクセシビリティに配慮した構成にしてください。
</div>

---

## AIに渡す情報を整理する

### 先にメモを作る

| 項目 | 記入例 |
|------|--------|
| 氏名 | 山田 太郎 |
| 所属 | 日本大学大学院 理工学研究科 情報科学専攻 |
| 研究室 | 松野研究室 |
| 研究テーマ | 自動運転システムの安全性保証 |
| 技術 | Python, JavaScript, Git, LaTeX |
| 公開リンク | GitHub, Google Scholar, ORCID |

<span class="small">AIには、公開してよい情報だけを渡してください。</span>

---

## 生成後に必ず直すところ

### AI生成ページは「たたき台」

- 名前、所属、研究テーマを自分の情報に置き換える
- 研究内容が<span class="highlight">誇張表現</span>になっていないか確認する
- 存在しない論文・受賞・スキルが入っていないか確認する
- 画像、アイコン、外部リンクの出典を確認する
- スマートフォン表示で読めるか確認する

<div class="warn-box">
AIが自動生成した「架空の業績」は必ず削除してください。
</div>

---

## VS Codeで編集する

### 手順

1. 新しいフォルダを作成
2. VS Codeで開く
3. `index.html` を作成
4. AIが生成したコードを貼り付ける
5. Live Serverでプレビュー
6. 内容を自分の情報へ修正

### 編集のコツ

- まずは動く状態を作る
- 1回に1箇所だけ直して確認する
- 変更が増えたらコミットする

---

## HTMLが分からなくてもWebサイトは作れる

### AIを使う場面

- Webサイトの初期案を作る
- 配色やレイアウトを調整する
- 文章を自然に整える
- エラーや表示崩れの原因を相談する

### 自分で必ず確認すること

- 研究内容・所属・連絡先が正しいか
- 公開してよい情報だけになっているか
- スマートフォンでも読めるか
- 架空の業績や無断転載画像が入っていないか

---

## 公開前チェックリスト

| 観点 | チェック内容 |
|------|--------------|
| 内容 | 研究テーマ、所属、連絡先が正確 |
| 公開範囲 | 秘密情報・個人情報・無断転載がない |
| 表示 | PCとスマートフォンで読める |
| リンク | GitHub、論文、メールリンクが動く |
| 品質 | 誤字、過度な装飾、架空情報がない |

<span class="small">迷った場合は、公開しない、表現をぼかす、教員に確認する、という順で判断します。</span>

---

<!-- _class: section -->

# GitHub Pagesで公開

リポジトリを作り、Webサイトとして公開する

---

## リポジトリ作成

### GitHub上で新規リポジトリを作成

1. GitHubにログイン
2. 右上の「+」→「New repository」
3. 設定:
   - **Repository name**: `自分のユーザー名.github.io`
   - **Public** を選択
   - **Add a README file** にチェック
4. 「Create repository」をクリック

### 公開URL

```text
https://ユーザー名.github.io/
```

---

## GitHub Desktopでコミット・プッシュ

### 手順

1. **Clone**: File → Clone Repository
2. クローンしたフォルダに `index.html` を置く
3. GitHub Desktopで変更内容を確認
4. Summaryに `Add research portfolio page` と入力
5. **Commit to main**
6. **Push origin**

<div class="note-box">
コミットメッセージは「何をしたか」が分かる短い文にします。
</div>

---

## GitHub Pages設定

### 設定手順

1. GitHubのリポジトリページを開く
2. **Settings** タブをクリック
3. 左メニューの **Pages** をクリック
4. Sourceを **Deploy from a branch** に設定
5. Branchを **main**、フォルダを **/ (root)** に設定
6. Saveをクリック

### 反映確認

- 数分待ってから `https://ユーザー名.github.io/` を開く（最大10分程度）
- 表示されない場合はブラウザを再読み込みする

---

## 更新の基本フロー

```text
VS Codeで編集
  ↓
保存してブラウザで確認
  ↓
GitHub Desktopで差分確認
  ↓
Commit
  ↓
Push
  ↓
GitHub Pagesで公開確認
```

### コミットメッセージ例

- `Update research summary`
- `Add publication list`
- `Fix mobile layout`

---

## よくあるトラブル

| 症状 | 原因 | 対処 |
|------|------|------|
| ページが404になる | Pages設定が未完了 | Settings → Pagesを確認 |
| 表示が古い | 反映待ち・キャッシュ | 数分待つ、再読み込み |
| CSSが効かない | ファイル名・パス違い | `index.html`内の参照を確認 |
| 画像が出ない | 画像パス・大文字小文字 | ファイル名を確認 |
| Pushできない | サインイン未完了 | GitHub Desktopで再ログイン |

<span class="small">困ったときは、エラー画面・公開URL・試した手順をメモして、次回の授業で質問してください。</span>

---

<!-- _class: section -->

# 演習

AIで作成し、GitHub Pagesで公開する

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">AI演習</span> 研究ポートフォリオを公開する（40分）

| 時間 | 作業内容 |
|------|----------|
| 5分 | GitHub / GitHub Desktop / VS Codeの確認 |
| 10分 | AIで `index.html` の初期案を生成 |
| 10分 | 内容を自分の研究情報に修正 |
| 5分 | リポジトリ作成・クローン |
| 5分 | コミット・プッシュ・Pages設定 |
| 5分 | 公開URL確認・微修正 |

<span class="small">自分の研究テーマが未確定の場合は、現在の関心分野・取り組みたい課題で構いません。</span>

---

<!-- _class: summary -->

## 課題

### 提出物

GitHub Pagesで公開した研究ポートフォリオWebサイトのURL

### 要件

- `https://ユーザー名.github.io/` でアクセスできる
- Profile, Research, Contactを最低限含む
- 修士課程学生として公開してよい内容になっている
- AI生成の架空情報、秘密情報、無断転載画像がない

### 締切

2週間後（2026年6月17日（水））

---

## 評価観点

| 観点 | 内容 |
|------|------|
| 公開 | GitHub Pagesで正常に表示される |
| 内容 | 研究テーマ・所属・連絡先が明確 |
| 適切性 | 公開情報の範囲が妥当 |
| 技術 | HTML/CSSが破綻せず、レスポンシブ対応 |
| 更新性 | GitHubで管理され、今後更新できる |

<span class="small">完成度よりも、公開・更新できる研究ポートフォリオの基礎を作ることを重視します。</span>
