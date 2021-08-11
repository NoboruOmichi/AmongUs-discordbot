# AmongUsBot_discord

## 内容
- このプログラムはAmongUsをdiscordで行う際に、ミュート・解除、部屋の移動を半自動で行ってくれるbot
  - Herokuで実装しなくても、環境をPCで再現できれば誰かのPCでプログラムを実行すると使用できる 
  - 実装のチェックはローカル環境のデバッグで確かめる必要あり

## 基本操作
このプログラムは2つのテキスト「.start」・「.end」と、5つのリアクション「探索状態」・「エマージェンシー」・「スタートボタン」・「幽霊」・「生存者」を使用する。
  (リアクションは各々が作成し、リアクションのIDを取得する必要がある。)

1. 所定のテキストチャンネルに「.stert」を入力すると、botが起動し、専用のメッセージが発せられる。（同時にミーティング部屋に参加者が集められる）
   - 発せられたテキストに 設定したリアクション「生存者」・「スタートボタン」が付属する。（botがリアクションをつけている） 
   - 「生存者」リアクションに参加者はリアクションをつける（「生存者」のリアクションをクリックする）
     - 「生存者」のリアクションをつけるとロールに生存者が追加される
   - 全員がリアクションをつけるとAmongUsのゲーム開始と同時に「スタートボタン」のリアクションを誰かがクリックする。（全員が生存者になっていないと開始しない）
   - 「スタートボタン」のリアクションが消えると同時に「幽霊」と「エマージェンシー」のリアクションが現れる。
2. ***探索状態***
  - 探索者は全員探索者部屋に強制移動させられると同時に、強制ミュートになる。幽霊は幽霊部屋にミュート解除状態で移動させられる
  - AmongUs上でエマージェンシー状態になると、「エマージェンシー」のリアクションを誰かがクリックする。
    - 探索状態では「幽霊」のリアクションをクリックしてもロールは変更せずに、テキストに警告文が出る
    - （botは他人のリアクションを外すことができても、他人としてリアクションをつけることができないためこのようにしている）
  - 「エマージェンシー」のリアクションをクリックすると「エマージェンシー」が消え、「探索状態」のリアクションが現れ、会議状態に移行する。
3. ***会議状態***
  - エマージェンシー状態をクリックすると全員がミーティング部屋に移動される。（このとき、生存者はミュート解除、幽霊はマイクミュートの状態になる）
  - エマージェンシー状態でのみ「幽霊」のリアクションをクリックすると、幽霊のロールに代わる（同時にマイクがミュートになる）
  - 会議が終わると「探索状態」のリアクションを誰かがクリックし、探索状態に移行する。

4. ゲームが終わると誰かが所定のテキストチャンネルに「.end」と入力することですべてがリセットされる。（再度開始する際は「.start」で起動）

  
## プログラムの編集
- 編集する必要があるのはdiscordbot.pyのみ。(***botの設定を事前にやっておくこと（他サイト参照）***)
- 基本的に書き換える必要がある箇所は、IDとボットのトークンのみ。（botのトークンなどはHerokuでの実行説明や他サイトを参照してください。）
- 書き換えるIDは使用するサーバーのID、テキストチャンネルのID、ミーティング部屋のID、幽霊部屋のID、生存部屋のID、生存者・幽霊のロールのID、「探索状態」・「エマージェンシー」・「スタートボタン」・「幽霊」・「生存者」のリアクションのIDである。
  - ID取得にはサーバの管理者権限がないと無理だと思われる。
  - リアクションのIDはcheck_reactionID.pyを実行した状態でリアクションをつけるとIDがわかる
    - （check_reactionID.pyでIDを確認する際は、プログラム内のテキストチャンネルID（DEBUG_CHANNEL_ID）を書き換える必要あり）

- プログラムの実行は　python discord.py だけで実行できる。
<br />

## 以下はHerokuでdiscord.pyを実行するための手順
（サンプルのReadmeを引用）(https://github.com/DiscordBotPortalJP/discordpy-startup)
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

- Herokuでdiscord.pyを始めるテンプレートです。
- Use Template からご利用ください。
- 使い方はこちら： [Discord Bot 最速チュートリアル【Python&Heroku&GitHub】 - Qiita](https://qiita.com/1ntegrale9/items/aa4b373e8895273875a8)

## 各種ファイル情報

### discordbot.py
PythonによるDiscordBotのアプリケーションファイルです。

### requirements.txt
使用しているPythonのライブラリ情報の設定ファイルです。

### Procfile
Herokuでのプロセス実行コマンドの設定ファイルです。

### runtime.txt
Herokuでの実行環境の設定ファイルです。

### app.json
Herokuデプロイボタンの設定ファイルです。

### .github/workflows/flake8.yaml
GitHub Actions による自動構文チェックの設定ファイルです。

### .gitignore
Git管理が不要なファイル/ディレクトリの設定ファイルです。

### LICENSE
このリポジトリのコードの権利情報です。MITライセンスの範囲でご自由にご利用ください。

### README.md
このドキュメントです。
"# AmongUsBot_discord" 
