# Google Apps Script 開発環境構築
* clasp
  * Google Apps Script CLIツール
    * https://github.com/google/clasp

* 検証環境
  * Windows 10 Pro

## Node.js & npm インストール

* Node.js インストーラ
  * https://nodejs.org/ja/
    * Windows x64 12.18.0 LTS

* Node.js と同時に npm もインストールされる
  ```
  > node -v
  v12.18.0

  > npm -v
  6.14.4
  ```

## clasp インストール

* インストール
  ```
  > npm install -g @google/clasp

  C:\Users\hoge\AppData\Roaming\npm\clasp ->  C:\Users\hoge\AppData\Roaming\npm\node_modules\@google\clasp\src\index.js
  npm WARN inquirer-autocomplete-prompt@1.0.1 requires a peer of inquirer@^5.0.0 || ^6.0.0 but none   is installed. You must install peer dependencies yourself.

  + @google/clasp@2.3.0
  added 160 packages from 92 contributors in 14.381s

  > clasp -v
  2.3.0
  ```

* 依存関係のあるパッケージがインストールされる
  ```
  > npm list

  C:\Users\hoge\AppData\Roaming\npm
  `-- @google/clasp@2.3.0
    +-- chalk@2.4.2 extraneous
      ・・・
    +-- googleapis@42.0.0 extraneous
    +-- UNMET PEER DEPENDENCY inquirer@7.2.0 extraneous
    +-- inquirer-autocomplete-prompt@1.0.1 extraneous
      ・・・
    `-- watch@1.0.2 extraneous

    npm ERR! peer dep missing: inquirer@^5.0.0 || ^6.0.0, required by inquirer-autocomplete-prompt@1.0.1
      ・・・
  ```

* WARN (UNMET PEER DEPENDENCY) が出たので、`inquirer@6.0.0` を追加
  ```
  > npm install inquirer@6.0.0

  npm notice created a lockfile as package-lock.json. You should commit this file.
  + inquirer@6.0.0
  removed 9 packages, updated 12 packages, moved 1 package and audited 151 packages in 2.061s

  5 packages are looking for funding
  run `npm fund` for details

  found 0 vulnerabilities
  ```

## Google Apps Script 連携

* Google Apps Script API 有効化
  * https://script.google.com/home/usersettings
    * Google Apps Script API を `オン` にする

* アカウント連携
  ```
  > clasp login
  ```

  ブラウザ起動後、Googleアカウントへログイン＆APIアクセス許可する
  ```
  【ブラウザ】
  Logged in! You may close this page.

  【CLI】
  Logging in globally...
  Authorize clasp by visiting this url:
  https://accounts.google.com/o/oauth2/v2/auth?・・・

  Authorization successful.

  Default credentials saved to: ~\.clasprc.json (C:\Users\hoge\.clasprc.json).
  ```

## GASプロジェクトのクローン・フェッチ
* `Webエディタ > ファイル > プロジェクトのプロパティ > 情報` から `スクリプトID` を確認しておく
```
> clasp clone [スクリプトID]
> clasp pull
```

## GASプロジェクトのプッシュ
* `.clasp.json` が存在するディレクトリで実行する
```
> clasp push
```

* アップロード可能なファイル
  * *.gs
  * *.html
  * `appscript.json`
* アップロードしないファイル
  * `.claspignore` ファイルに記述

## 参考
* claspを使い、Google Apps Scriptプロジェクトをgitでバージョン管理する - Qiita
  * https://qiita.com/rf_p/items/7492375ddd684ba734f8
* Google Apps Scriptの新しい3つの機能 その③ CLI Tool Clasp - Qiita
  * https://qiita.com/soundTricker/items/354a993e354016945e44
