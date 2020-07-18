# RubyGems SSL証明書エラーの対応方法

`gem install` 等を実行しようとすると、SSL接続でエラー
```
> gem update --system
Updating rubygems-update
ERROR:  While executing gem ... (Gem::RemoteFetcher::FetchError)
    SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://api.rubygems.org/api/v1/dependencies?gems=rubygems-update)
```

* RubyGems のアップデートを行うことで、クライアント側証明書も更新されるとのこと（RubyGems Guides）  
https://guides.rubygems.org/ssl-certificate-update/#installing-using-update-packages


## RubyGems アップデート

1. RubyGems サイトから、`rubygems-update` をダウンロード  
    https://rubygems.org/gems/rubygems-update/
    * 右下の `リンク集：ダウンロード` から `rubygems-update-x.x.x.gem` ファイルをダウンロードする

1. rubygems-update インストール
    ```
    > gem install --local .\rubygems-update-x.x.x.gem
    ```
    * `rubygems-update-x.x.x.gem` ファイルを指定し、ローカルからインストールする

1. rubygems-update 実行
    ```
    > update_rubygems --no-ri --no-rdoc
    ```

1. RubyGems バージョン確認
    ```
    > gem -v
    x.x.x
    ```
    * バージョンが更新されていればOK


## 備考
Ruby 2.1.9 の場合、利用可能な RubyGems の最新バージョンは 2.7.10 のようです。  
（RubyGems サイトで gem のバージョン履歴を選択して、`必要Rubyバージョン` の項目で確認可能）  
rubygems-update にも 必要Rubyバージョンの制約があるので、Ruby 自体も出来る限り新しいものを使うほうが良いですね。
