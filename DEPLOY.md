# GitHub Pages で公開する手順

| | |
| --- | --- |
| リポジトリ | https://github.com/K3ngo/MTG_setting |
| 公開後のURL | `https://K3ngo.github.io/MTG_setting/` |

## 済んでいること

- [x] `index.html`（ツール本体）の作成
- [x] git の初期化（ブランチ `main`）
- [x] 作者情報の設定 … `Kengo Miyazaki <K3ngo@users.noreply.github.com>`
      （noreply アドレスなので実際のメールアドレスは公開されない。GitHubの貢献グラフには反映される）
- [x] 初回コミット `c8f247a`
- [x] リモート `origin` の登録

## 残っている作業

### 1. push する

```bash
git push -u origin main
```

初回はブラウザが開いて GitHub のログインと認可を求められる。許可すれば以降は自動で通る。

### 2. Pages を有効化する

https://github.com/K3ngo/MTG_setting/settings/pages を開いて、次のように設定する。

- Source … **Deploy from a branch**
- Branch … **main** と **/ (root)**
- Save を押す

1〜2分待って同じ画面を再読み込みすると、公開URLが表示される。

### 3. ツールに置き場所URLを登録する

`https://K3ngo.github.io/MTG_setting/` を開き、
**「⚙ あなたの設定」→「このファイルの置き場所URL」** に次を貼る。

```
https://K3ngo.github.io/MTG_setting/
```

一度入れればブラウザに記憶されるので、次回以降は不要。これで発行される個別URLはこうなる。

```
https://K3ngo.github.io/MTG_setting/#r=zVcvPSkJB...~0
```

社内でも社外でも、リンクを開くだけで回答画面が出る。ログインもアプリのインストールも不要。

## Public リポジトリでも打合せの中身は公開されない

公開されるのは `index.html`（ツール本体）と `README.md`・`DEPLOY.md` だけで、どれもテンプレート。
実際の打合せデータは含まれない。

- 件名・議題・参加者名・候補日程・回答内容は、すべてURLの `#` 以降に入っている
- **`#` 以降はブラウザからサーバーへ送信されない**（HTTPの仕様）。GitHubのアクセスログにも残らないので、
  GitHub側からは誰がどんな打合せを調整したのか分からない

## ツールを更新したとき

`index.html` を書き換えたら push すれば1〜2分で反映される。

```bash
git add -A
git commit -m "変更内容の説明"
git push
```

**すでに配ったURLは更新後もそのまま使える。** 候補日程や参加者を変えずにレイアウトや文言だけ直した場合、
回答コードも引き続き有効（イベント指紋は件名・候補・参加者から計算しているため）。

## URLについての注意

- **URL短縮サービスは使わないこと。** `#` 以降が失われると候補日程のデータが消えて開けなくなる
- URLは400文字前後。チャットやメール本文にはそのまま貼れる長さ
- 発行済みURLに期限はない。ただし候補日程や参加者を変更して再発行すると、古いURLと古い回答コードは
  無効になる（別のMTGの回答が混ざらないための安全機構）
- 誰でもURLを知れば回答画面を開ける。パスワードはかからないので、機密性の高い件名・議題を書く場合は
  その点だけ留意する
