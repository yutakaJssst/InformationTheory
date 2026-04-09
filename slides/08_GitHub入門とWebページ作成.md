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

  table { font-size: 0.85em; width: 100%; }
  th { background: var(--color-text); color: white; font-weight: 500; }
  tr:nth-child(even) { background: #F0F4FF; }

  blockquote { border-left: 4px solid var(--color-accent); background: var(--color-bg-light); padding: 12px 20px; margin: 12px 0; font-size: 0.95em; }

  section.title { text-align: center; display: flex; flex-direction: column; justify-content: center; border-bottom: 3px solid var(--color-line); }
  section.title h1 { font-size: 2.8em; margin-bottom: 0; }
  section.title h2 { font-size: 1.2em; font-weight: 400; color: var(--color-text); border: none; padding: 0; }
  section.title p { color: #999; font-size: 0.85em; }

  section.section { display: flex; flex-direction: column; justify-content: center; background: linear-gradient(135deg, #FAFAFA 0%, #F0F0F0 100%); }
  section.section h1 { font-size: 2.2em; color: var(--color-accent); text-align: center; }
  section.section p { text-align: center; color: #777; font-size: 1.1em; }

  section.ai-exercise h2 { color: var(--color-purple); border-bottom-color: #D1C4E9; }
  .ai-badge { display: inline-block; background: var(--color-purple); color: white; padding: 2px 12px; border-radius: 4px; font-size: 0.8em; font-weight: 500; margin-right: 8px; }
  .prompt-box { background: var(--color-bg-code); border: 1px solid #DDD; border-left: 4px solid var(--color-purple); border-radius: 4px; padding: 14px 18px; font-family: 'IBM Plex Mono', monospace; font-size: 0.82em; line-height: 1.6; margin: 10px 0; }

  section.summary h2 { border-bottom-color: var(--color-green); }
  .highlight { background: linear-gradient(transparent 60%, #FFF9C4 60%); font-weight: 500; }
  .red { color: var(--color-red); }
  .blue { color: var(--color-accent2); }
  .teal { color: var(--color-accent); }
  .purple { color: var(--color-purple); }
  .green { color: var(--color-green); }
  .orange { color: var(--color-orange); }
  .small { font-size: 0.82em; }
  .smaller { font-size: 0.75em; }

footer: "情報論 2026 ｜ matsulab"
---

<!-- _class: title -->

# GitHub入門とWebページ作成
## 情報論 2026 第8回 ― AI活用(6)

情報科学専攻 ｜ 松野 裕
matsuno.yutaka@nihon-u.ac.jp
2026年6月10日（対面授業・100分）

---

## 本日のアジェンダ

| 時間 | 内容 |
|------|------|
| 15分 | Git/GitHubの紹介 |
| 15分 | 環境準備（アカウント作成・ツール設定） |
| 20分 | AIでWebページ作成 |
| 10分 | GitHub Pagesで公開 |
| 40分 | 演習 |

---

## Gitとは

### 分散型バージョン管理システム

- <span class="teal">**変更履歴の記録・追跡**</span>: いつ、誰が、何を変更したかを記録
- <span class="teal">**過去の状態への復元**</span>: 間違えても元に戻せる
- <span class="teal">**チーム開発の効率化**</span>: 複数人が同時に作業可能

### イメージ
```
v1.0 → v1.1 → v1.2 → v2.0（現在）
              ↘ v1.2-fix（修正版）
```

> Gitは <span class="highlight">ソフトウェア開発の必須ツール</span> であり、研究コード管理にも有用

---

## GitHubとは

### Gitリポジトリのホスティングサービス

### 主な機能
- <span class="teal">**リポジトリホスティング**</span>: コードをクラウドに保存
- <span class="teal">**チーム開発機能**</span>: Issue（課題管理）、Pull Request（レビュー）
- <span class="teal">**GitHub Pages**</span>: Webページの無料公開

### 特徴
- 世界最大の開発プラットフォーム（1億人以上のユーザー）
- 無料でパブリックリポジトリを作成可能
- <span class="highlight">学生は Pro プランが無料</span>（GitHub Education）

---

## なぜ大学院生がGitHubを使うべきか

### 1. 研究コードの管理
- 実験コードのバージョン管理
- 再現性の確保（どの時点のコードで結果を出したか）

### 2. 就活でのポートフォリオ
- 技術力の可視化
- <span class="highlight">企業の採用担当者がGitHubを確認するケースが増加</span>

---

## なぜ大学院生がGitHubを使うべきか（続き）

### 3. 共同研究の効率化
- 研究室メンバーとのコード共有
- 論文の共同執筆（LaTeXの管理）

---

<!-- _class: section -->

# 環境準備

---

## GitHubアカウント作成

### 手順

1. [github.com](https://github.com) にアクセス
2. 「Sign up」をクリック
3. メールアドレス、パスワード、ユーザー名を入力
4. メール認証を完了

### ユーザー名のポイント
- <span class="highlight">本名またはそれに近い名前</span> を推奨（ポートフォリオとして使うため）
- 短く覚えやすいもの
- 例: `yutaka-matsuno`, `matsuno-y`

---

## GitHub Desktop のインストールと設定

### インストール
1. [desktop.github.com](https://desktop.github.com) からダウンロード
2. インストール後、GitHubアカウントでサインイン

### GUIでの基本操作

| 操作 | 意味 | GitHub Desktop での操作 |
|------|------|------------------------|
| **クローン** | リポジトリをPCにコピー | File → Clone Repository |
| **コミット** | 変更を記録 | 変更をまとめて「Commit」ボタン |
| **プッシュ** | PCの変更をGitHubに反映 | 「Push origin」ボタン |

> コマンドラインが苦手でも <span class="highlight">GUIで直感的に操作可能</span>

---

## VS Code の準備

### Visual Studio Code
- Microsoft製の無料コードエディタ
- [code.visualstudio.com](https://code.visualstudio.com) からダウンロード

### GitHub連携
- VS Code内でGitの操作が可能
- 拡張機能「GitHub Pull Requests」をインストール

### 便利な拡張機能

| 拡張機能 | 用途 |
|----------|------|
| **Live Server** | HTMLのリアルタイムプレビュー |
| **Prettier** | コードの自動整形 |
| **Japanese Language Pack** | 日本語化 |

---

<!-- _class: section -->

# AIでホームページ作成

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">AI演習</span> AIチャットボットでHTML/CSSコード生成

### プロンプト例

<div class="prompt-box">
「大学院生の自己紹介Webページを作成してください。HTML/CSSで、名前・研究テーマ・所属・連絡先・研究業績のセクションを含めてください。モダンでシンプルなレスポンシブデザイン、1つのHTMLファイルにCSSも含めてください」
</div>

### 使用ツール
- ChatGPT / Claude / Gemini / Google AI Studio 等、お好みのAIツール

---

## VS Codeでの編集

### 手順

1. VS Codeで新規ファイルを作成: `index.html`
2. AIが生成したHTMLコードを **全文コピー&ペースト**
3. **Live Server** 拡張機能でプレビュー（右クリック → Open with Live Server）
4. 内容を自分の情報に **書き換え**:
   - 名前、所属、研究テーマ
   - 連絡先（メールアドレス）
   - 研究業績・発表リスト

### ポイント
- まずはAI生成コードを <span class="highlight">そのまま動かしてみる</span>
- 動作確認してから少しずつ修正

---

## AIでコードをカスタマイズ

### 追加の修正もAIに依頼できる

**デザイン変更:**

<div class="prompt-box">
「背景色を薄いグレー（#f5f5f5）に変更し、ヘッダーを青系（#0066cc）にしてください」
</div>

### コツ
- 変更したい部分の <span class="highlight">該当コードをAIに渡す</span> と精度が上がる

---

## AIでコードをカスタマイズ（続き）

**セクション追加:**

<div class="prompt-box">
「研究業績のセクションに、学会発表と論文のサブセクションを追加してください。箇条書きリスト形式でお願いします」
</div>

### その他の修正例
- レイアウト変更、フォント変更、レスポンシブ対応なども依頼可能

---

<!-- _class: section -->

# Git/GitHubで公開

---

## リポジトリ作成

### GitHub上で新規リポジトリを作成

1. GitHubにログイン
2. 右上の「+」→「New repository」
3. 設定:
   - **Repository name**: `自分のユーザー名.github.io`
     - 例: `matsuno-y.github.io`
   - <span class="teal">**Public**</span> を選択
   - **Add a README file** にチェック
4. 「Create repository」をクリック

> リポジトリ名を `ユーザー名.github.io` にすると <span class="highlight">GitHub Pagesの個人サイト</span> になる

---

## コミットとプッシュ

### GitHub Desktop での操作手順

1. **クローン**: File → Clone Repository → リポジトリを選択
2. **ファイル配置**: クローンしたフォルダに `index.html` をコピー
3. **変更確認**: GitHub Desktopに変更が表示される
4. **コミット**: Summary に「自己紹介ページを追加」→「Commit to main」
5. **プッシュ**: 「Push origin」をクリック

---

## GitHub Pagesで公開

### 設定手順

1. GitHubのリポジトリページを開く
2. <span class="teal">**Settings**</span> タブをクリック
3. 左メニューの <span class="teal">**Pages**</span> をクリック
4. Source を **「Deploy from a branch」** に設定
5. Branch を **「main」** 、フォルダを **「/ (root)」** に設定
6. 「Save」をクリック

### 公開URL
```
https://ユーザー名.github.io/
```
<span class="small">反映まで 1-2分 かかる場合がある</span>

---

<!-- _class: section -->

# 更新と反映

---

## Webページの更新フロー

### 修正から反映までの一連の流れ

```
VS Codeで修正 → GitHub Desktopで確認 → コミット → プッシュ → 自動反映
```

1. <span class="teal">**VS Codeで修正**</span>: `index.html` を編集・保存
2. <span class="teal">**GitHub Desktopで確認**</span>: 変更差分が自動表示
3. <span class="teal">**コミット**</span>: メッセージを入力してコミット
4. <span class="teal">**プッシュ → 確認**</span>: Push後、ブラウザで再読み込み

### コミットメッセージの例
- 「研究業績を更新」 / 「デザインを修正」 / 「連絡先セクションを追加」

---

<!-- _class: section -->

# 演習

---

<!-- _class: ai-exercise -->

## <span class="ai-badge">AI演習</span> AIでWebページを作成しGitHub Pagesで公開（40分）

| 時間 | 作業内容 |
|------|----------|
| 5分 | GitHubアカウント作成・GitHub Desktopセットアップ |
| 10分 | AIツールで自己紹介WebページのHTMLを生成 |
| 10分 | VS Codeで内容を自分の情報に修正 |
| 5分 | リポジトリ作成・クローン |
| 5分 | コミット・プッシュ・GitHub Pages設定 |
| 5分 | 公開確認・微修正 |

<span class="small">困ったときは手を挙げて質問してください。隣の人と相談してもOKです。</span>

---

<!-- _class: summary -->

## 課題

### 提出物
自己紹介WebページのGitHub PagesのURL

### 要件
- <span class="highlight">自分の情報</span> が正しく掲載されていること
- 最低限のセクション: 名前、所属、研究テーマ、連絡先
- <span class="teal">**GitHub Pagesで公開**</span> されアクセスできること

### 提出方法・締切
- 次回授業開始時まで（6/17）
- URLを提出フォームに入力

---

## 次回予告

### 第9回: データ分析と可視化（6/17）

- AIを使った <span class="teal">**データ分析**</span> と <span class="teal">**可視化**</span> の手法を学ぶ
- 論文品質のグラフ作成
- インタラクティブ可視化ツールの活用

### 準備しておくこと
- 自分の研究データがあれば持参
- 今日作成したWebページの <span class="highlight">完成版をプッシュ</span> しておく
