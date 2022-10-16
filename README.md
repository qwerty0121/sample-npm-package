# sample-npm-package

## 概要

GitHub Packagesにnpmパッケージを公開するサンプルプロジェクト。

## GitHubの個人用アクセストークンを作成

GitHub Packages上のnpmパッケージを公開またはインストールするためには、GitHubの個人用アクセストークンが必要になる。

作成方法は以下のサイトの通り。  
[個人用アクセス トークンの作成](https://docs.github.com/ja/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

個人アクセストークンのスコープは以下の通りとする。
* repo
* write:packages

個人アクセストークンを利用してnpmパッケージの公開やインストールをするためには、`~/.npmrc`に個人用アクセストークンを含める必要がある。  
そのため、以下のコマンドを実行する。
```bash
echo "//npm.pkg.github.com/:_authToken={access-token}" >> ~/.npmrc
```

## npmパッケージを公開

npmパッケージを公開する手順は以下の通り。

1. 以下のコマンドでnpmパッケージをレジストリに公開する
    ```bash
    npm publish --registry=https://npm.pkg.github.com
    ```

## npmパッケージのインストール

npmパッケージをインストールする手順は以下の通り。

1. npmパッケージを利用するプロジェクトに`.npmrc`ファイルを作成し、以下を追記する
    ```
    @{scope}:registry=https://npm.pkg.github.com
    ```
   * 上記を追記することによって、指定したスコープのnpmパッケージについてはGitHub Packagesからインストールするようになる。
1. 以下のコマンドでnpmパッケージをインストールする
    ```bash
    npm install @{scope}/{package-name}
    ```

実際にGitHub Packagesに公開したnpmパッケージをインストールした例は以下のリポジトリを参照。  
[sample-npm-package-use](https://github.com/qwerty0121/sample-npm-package-use)

## 参考サイト

* [GitHub Packagesで社内用npmパッケージを配布して使ってみた](https://zenn.dev/odiak/articles/950f05a34e9c84)
* [npmについてのまとめ](https://qiita.com/rihofujino/items/818ce07e5eb72acafd5a#scope%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
* [About scopes](https://docs.npmjs.com/about-scopes)
* [個人用アクセス トークンの作成](https://docs.github.com/ja/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
* [GitHub Package Registry を npm で使う](https://qiita.com/nall/items/5e94f37288c3e796a85e#%E4%B8%8B%E6%BA%96%E5%82%99)
