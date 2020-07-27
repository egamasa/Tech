# CentOS 7 on WSL 2 セットアップ

## 動作環境

* Windows 10 バージョン 2004、ビルド 19041 以降


## WSL有効化

* Intel VT／AMD-V 有効化  
  BIOS／UEFI→CPU設定

* 「Linux 用 Windows サブシステム」有効化
  ```powershell
  # PowerShell（管理者として実行）
  dism.exe /online /enable-feature /  featurename:Microsoft-Windows-Subsystem-Lin ux /all /norestart
  ```

* 「仮想マシン プラットフォーム」有効化
  ```powershell
  # PowerShell（管理者として実行）
  dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
  ```

* WSL 有効化完了
  ```
  PS > wsl

  Linux 用 Windows サブシステムには、ディストリビューションがインストールされていません。
  ディストリビューションは Microsoft Store にアクセスしてインストールすることができます:
  ```


## WSL 2 Linux カーネルの更新

* WSL 2 Linux カーネル更新プログラム パッケージのダウンロード・インストール  
  https://docs.microsoft.com/ja-jp/windows/wsl/wsl2-kernel

* WSL 2 を規定バージョンに設定
  ```powershell
  # PowerShell（管理者として実行）
  wsl --set-default-version 2

  WSL 2 との主な違いについては、https://aka.ms/wsl2 を参照してください
  ```


## CentOS 7 インストール

* `CentOS7.zip` ダウンロード  
  https://github.com/yuk7/CentWSL

* ファイル配置
  1. `C:\Users\{ユーザ名}\AppData\Local\Packages\CentOS7` ディレクトリを作成
  1. `CentOS7.zip` を解凍
  1. `CentOS7.exe` および `rootfs.tar.gz` を作成したディレクトリに配置

* CentOS 7 インストール  
  `CentOS7.exe` を管理者権限で実行
  ```
  Installing...
  Installation Complete!
  Press any key to continue...
  ```

* CentOS 7 インストール完了
  ```
  PS > wsl -l -v

  NAME       STATE           VERSION
  * CentOS7    Stopped         2
  ```

## Cent OS 7 の実行
  * WSL ランチャー
    ```powershell
    wsl -d CentOS7
    ```
  * `CentOS7.exe` を起動


## CentOS 7 設定

* root パスワード設定
  ```bash
  passwd root
  ```

* 作業ユーザ作成
  ```bash
  useradd {ユーザ名}
  passwd {ユーザ名}
  gpasswd -a {ユーザ名} wheel
  ```

* デフォルトユーザ変更  
  CentOS7.exe 実行時のログインユーザを root から作業ユーザへ変更
  ```bat
  rem コマンド プロンプト（管理者として実行）
  chdir %USERPROFILE%\AppData\Local\Packages\CentOS7
  %USERPROFILE%\AppData\Local\Packages\CentOS7> CentOS7.exe config --default-user {ユーザ名}
  ```


## 参考
* Windows 10 用 Windows Subsystem for Linux のインストール ガイド - Microsoft Docs
  https://docs.microsoft.com/ja-jp/windows/wsl/install-win10

* WSLでCentOSが利用できたかも？（CentOS 7） - torutkのブログ
  https://torutk.hatenablog.jp/entry/2019/11/24/110818
