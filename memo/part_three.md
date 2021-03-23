# ネストコンポーネント

- Layout Component
- 複数のページで共有するコンポーネント
    - ヘッダとかフッター
    - ナビゲーションメニューとか

## Plugin を使う

- Typography.js
- 普通にインストールしようとするとNG

```bash
npm ERR! code ERESOLVE
npm ERR! ERESOLVE unable to resolve dependency tree
npm ERR!
...
```

- 以下のコマンドで解決

```bash
$ npm install gatsby-plugin-typography react-typography typography typography-theme-fairy-gates --save --legacy-peer-deps
```

- gatsby-config.jsは、Gatsbyが自動的に認識するもう1つの特別なファイル
- Pluginやサイト構成を追加する
    - gatsby-config はここ: https://www.gatsbyjs.com/docs/reference/config-files/gatsby-config/
- Typography.js に構成ファイルが必要

