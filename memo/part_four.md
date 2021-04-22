# Data in Gatsby

- Gatsby data layer は GraphQL 使ってるよ
- これ見ておくといいよ
  - https://www.howtographql.com/

## Data とは

- CS的には `42` とか `{pizza: true}` とか
- Gatsby的には, **React Component 以外のすべて**
- テキストとかImageを Component 内に直接書いてたので問題ない
- ただ必要に応じて外に保存したデータを Component に取り込みたい場合がある
- Gatsby Data Layer を使おう

## Using Unstructured Data vs GraphQL

- **Q. Gatsby にデータを取り込みたい場合、GraphQLやプラグインを使わないといけないか？**
  - A. 100% No.
  - createPages API を使える
  - GraphQLデータレイヤを通さずに非構造データを Gatsby に取り込める
  - 小さなサイトとかには最適。大規模で複雑なやつは GraphQL を使おう
    - https://www.gatsbyjs.com/docs/how-to/querying-data/using-gatsby-without-graphql/
  
- **非構造データとGraphQLはどちらをいつ使うのか**
  - 小さいサイトを構築する際は createPages API を使って非構造データを取り込む
  - 大きくなってきたら以下の手順で複雑なサイトの構築に進むか、データレイヤを利用する
1. Plugin ライブラリをチェックし、すでに既存のものが存在し、データを変換できるかをチェック
2. 存在しなければ Plugin オーサリングガイドを読んで自身で作るのです

## How Gatsby’s data layer uses GraphQL to pull data into components

- Gatsby の React Component にデータをLoadする方法はたくさんあって、その中の一つが GraphQL
- GaphQL を使って Component にデータを宣言できる

## 以降作成

https://www.gatsbyjs.com/docs/tutorial/part-four/#create-a-new-example-site

