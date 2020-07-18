# Python 3 開発環境構築 (Windows & VS Code)

## Python のインストール

### インストーラのダウンロード
* https://www.python.org/downloads/
* トップの "Download" ボタンを押すと 32bit版がダウンロードされるため、バージョンを選択し `Windows x86-64 executable installer`（64bit版）をダウンロードする

### Python のインストール

1. `python-3.x.x-amd64.exe` を実行
1. `Add Python 3.x to PATH` にチェックを入れる
1. `Install Now` でインストール実行


## 開発用ライブラリのインストール

### Flake8
`pip install flake8`
* コードを静的にチェック
  * pycodestyle
    * PEP8に準拠しているかチェック
  * pyflakes
    * エラーが発生しそうなコードをチェック
  * mccable
    * 循環的複雑度のチェック

### Black
`pip install black`
* コード整形
  * PEP8準拠

### autopep8
`pip install autopep8`
* コード整形
  * PEP8準拠
  * Visual Studio Code から利用


## Visual Studio Code の設定

### 拡張機能インストール
* Python (Microsoft)
* Pylance (Microsoft)
  * Preview版（2020/07/03現在）
    * Microsoft的には将来的に Python から Pylance へシフト意向
      https://forest.watch.impress.co.jp/docs/news/1262974.html
  * "IntelliSense"による強力な入力補完や型チェック、モジュールの自動インポート
  * コードチェック機能が Flake8 と重複するので一旦は無くてもいいかも…

### コードチェッカー変更 (Pylint → flake8)
VS Code 標準の Pylint はチェックが必要以上に厳しいので変更
* Pylint 無効化  
  `"python.linting.pylintEnabled": false`
* Python コードチェック有効化  
  `"python.linting.enabled": true`
* flake8 有効化  
  `"python.linting.flake8Enabled": true`
* ファイル保存時のチェック有効化  
  `"python.linting.lintOnSave": true`
* 自動整形フォーマット指定 (PEP8)  
  `"python.formatting.provider": autopep8`  
  * `右クリック＞ドキュメントのフォーマット (Shift + Alt + F)` で自動整形実行
* ファイル保存時の自動整形有効化  
  `"editor.formatOnSave": true`

#### PEP8 の1行あたりの文字数制限を無視する
1行が79文字を超えている場合のエラー (E501 line too long) を無視する
1. Settings で `flake8args` を検索
1. settings.json で編集
1. `"python.linting.flake8Args"` をユーザー設定にコピー
1. `.flake8Args": ["--ignore=E501"],` を記述


## 仮想環境 (venv)
{envname} は仮想環境の名称（任意）

### 仮想環境の作成
`> python -m venv {envname}`
* {envname} ディレクトリが作成される

### 仮想環境に入る
`> {envname}/Scripts/activate`
* CLI の入力行先頭に {envname} が表示される  
  `({envname}) ～～～ > `

### 仮想環境から抜ける
`> deactivate`

### 仮想環境の削除
{envname} ディレクトリを削除する


## 参考
* Python開発環境の整え方 - PyCon JP  
  https://gitpitch.com/pyconjp/slides/master?p=osc2020do
* VSCodeのPython開発環境でpylintの代わりにflake8を導入し自動整形を設定する - Qiita  
  https://qiita.com/psychoroid/items/2c2acc06c900d2c0c8cb
