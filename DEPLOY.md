# GitHub Pages で公開する手順

参加者（社内・社外どちらでも）が開けるURLを発行できるようにする。所要10分ほど。
git はインストール済み。必要なのは GitHub アカウントだけ。

## 先に知っておくこと

**リポジトリは Public にする。** private リポジトリ + GitHub Pages は有料プラン限定のため。

Public にしても、**打合せの中身は一切公開されない。**

- 公開されるのは `index.html`（ツール本体）と `README.md` だけ。どちらもテンプレートで、社内情報は含まれない
- 件名・議題・参加者名・候補日程・回答内容は、すべてURLの `#` 以降に入っている
- **`#` 以降はブラウザからサーバーへ送信されない**（HTTPの仕様）。GitHubのアクセスログにも残らず、GitHub側からは誰がどんな打合せを調整したのか分からない

一方で、**コミットに使うメールアドレスは公開される。** 会社のアドレスを出したくない場合は、手順1で GitHub の noreply アドレスを使う。

## 1. git の名前とメールを設定

```bash
git config user.name "Kengo Miyazaki"
```

```bash
git config user.email "<GitHubユーザー名>@users.noreply.github.com"
```

`<GitHubユーザー名>` は自分のアカウント名に置き換える。この noreply アドレスを使えばメールアドレスは公開されない。
実際のアドレスを出して構わない場合は、そのアドレスをそのまま入れてもよい。

`--global` を付けなければ、この設定はこのフォルダだけに適用される（PC全体の設定は変わらない）。

## 2. コミットする

```bash
git add -A
```

```bash
git commit -m "Add meeting scheduler"
```

## 3. GitHub でリポジトリを作る

https://github.com/new を開いて、次のように設定する。

| 項目 | 設定 |
| --- | --- |
| Repository name | `mtg`（好きな名前。URLの一部になるので短い方がよい） |
| 公開設定 | **Public** |
| Add a README file | **チェックしない** |
| Add .gitignore / license | **どちらも None** |

「Create repository」を押す。空のリポジトリができる。

## 4. push する

```bash
git remote add origin https://github.com/<ユーザー名>/mtg.git
```

```bash
git push -u origin main
```

初回はブラウザが開いて GitHub へのログインと認可を求められる。許可すれば以降は自動で通る。

## 5. Pages を有効化する

リポジトリの **Settings** → 左メニュー **Pages** を開く。

- Source … 「Deploy from a branch」
- Branch … `main` と `/ (root)` を選ぶ
- Save を押す

1〜2分待って同じ画面を再読み込みすると、URLが表示される。

```
https://<ユーザー名>.github.io/mtg/
```

## 6. ツールに置き場所URLを登録する

上のURLを開き、**「⚙ あなたの設定」→「このファイルの置き場所URL」** にそのURLを貼る。
一度入れればブラウザに記憶されるので、次回以降は不要。

これで発行される個別URLはこうなる。

```
https://<ユーザー名>.github.io/mtg/#r=zVcvPSkJB...~0
```

社内でも社外でも、リンクを開くだけで回答画面が出る。ログインもアプリのインストールも不要。

## ツールを更新したとき

`index.html` を書き換えたら、同じ手順で push すれば1〜2分で反映される。

```bash
git add -A
git commit -m "変更内容の説明"
git push
```

**すでに配ったURLは、更新後もそのまま使える。** 候補日程や参加者を変えずにレイアウトや文言だけを直した場合、
回答コードも引き続き有効（イベント指紋は件名・候補・参加者から計算しているため）。

## URLについての注意

- **URL短縮サービスは使わないこと。** `#` 以降が失われると候補日程のデータが消えて開けなくなる
- URLは400文字前後。チャットやメール本文にはそのまま貼れる長さ
- 発行済みURLに期限はない。ただし候補日程や参加者を変更して再発行すると、古いURLと古い回答コードは無効になる（別のMTGの回答が混ざらないための安全機構）
- 誰でもURLを知れば回答画面を開ける。パスワードはかからないので、機密性の高い件名・議題を書く場合はその点だけ留意する
