# Part 1

https://www.gatsbyjs.com/docs/tutorial/part-one/

```bash
$ gatsby new [SITE_DIRECTORY_NAME] [URL_OF_STARTER_GITHUB_REPO]
```

## Hot Reloading

- `gatsby develop` でサーバーを起動しておく

### 1. Text の書き換え

`src/pages/index.html` の `Hello World!` を `Hello gatsby World!` に書き換える

- ブラウザで見てるコンテンツ内容が書き換わる
  - サーバーPushかなー

### 2. Style の書き換え

- 以下に書き換える

```jsx
export default function Home() {
  return <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
}
```

文字がパープルになって大きくなる。

### 3. font サイズを削ってメッセージ追加

```jsx
import React from "react"
export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <h1>Hello Gatsby!</h1>
      <p>What a world.</p>
    </div>
  );
}
```

### 4. 画像追加

```bash
import React from "react"

export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <h1>Hello Gatsby!</h1>
      <p>What a world.</p>
      <img src="https://source.unsplash.com/random/400x200" alt="" />
    </div>
  )
}
```

## JavaScript Function 内に HTML がある？

- React, JSX 触ったことがあればスキップ
- Hybrid HTML-in-JS は JSX と呼ばれる React 用の JavaScript の拡張Syntax　
- JSX から Pure JavaScript への書き換えが可能

```jsx
import React from "react"

export default function Home() {
  return <div>Hello world!</div>
}
```

これを Pure JS にすると

```javascript
import React from "react"

export default function Home() {
  return React.createElement("div", null, "Hello world!")
}
```

- `null` とかが出てきて直感的に何やってるか分かりづらい（個人的な感想）

## Component ってなんだ

Gatsby は React ベースなので、 Gatsby 内で Component って言ったら、React Component のことじゃ。特徴は以下

- 入力を受け付ける
- UI を表現する React 要素を返すことのできるコードの断片
- JSX で記載される
- CSS, HTML, JS が密結合

### 例: Button の例

HTML と JSX で Button の記述例を比較

```html
<button class="primary-button">Click me</button>
```

```jsx
<PrimaryButton>Click me</PrimaryButton>
```

## Page Component を使う

- `src/pages/*.js` は自動的に Page となる

## about 画面を作成する

- `localhost:8000/about`  の画面を構成したい

### 1. src/pages/about.js を記述する

```jsx
import React from "react"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <h1>About Gatsby</h1>
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

### 2. localhost:8000/about にアクセスする

```bash
$ curl http://localhost:8000/about
<!DOCTYPE html><html><head><meta charSet="utf-8"/><meta http-equiv="x-ua-compatible" content="ie=edge"/><meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"/><meta name="note" content="environment=development"/><script src="/socket.io/socket.io.js"></script></head><body><div id="___gatsby"></div><script src="/polyfill.js" nomodule=""></script><script src="/commons.js"></script></body></html>
```

- `about.js` は `/about` にマッピングされる

## Sub Component を使う

- Sub Component を使って使いまわしできる Component を構築する
- 試しにヘッダを構築してみる

### 1. src/components ディレクトリを作成する

### 2. header.js を作成する

```jsx
import React from "react"

export default function Header() {
  return <h1>This is a header.</h1>
}
```

### 3. about.js を変更する

```jsx
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

ところで、 `about` ページだけヘッダには `This is a header.` ではなく `About Gatsby` にしたい。

### 4. header.js を以下に変更

```jsx
import React from "react"

export default function Header(props) {
  return <h1>{props.headerText}</h1>
}
```

### 5. about.js を以下に変更

```jsx
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header headerText="About Gatsby" />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

### props ってなんだ

UI の Component で部品化して汎用化するのは良いけど、外部からデータを入れられないと仕方ないので、呼び出し側から動的に Component へデータを入力できる。これを `props` と呼んでいて、React によって提供される。

上記の例では `headerText` という prop が定義されており、呼び出し側の abtout.js が prop を通して header.js に値を渡す。

### 6. about.js を再度修正

header Component を再利用する

```jsx
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header headerText="About Gatsby" />
      <Header headerText="It's pretty cool" />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

`headerText`  が異なる Header Component を2つ配置。

## Link

Link Component を使う

### 1. Index.js を修正

```jsx
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <Link to="/contact/">Contact</Link>
      <Header headerText="Hello Gatsby!" />
      <p>What a world.</p>
      <img src="https://source.unsplash.com/random/400x200" alt="" />
    </div>
  )
}
```

`/contact/`  にアクセスすると 404 NotFound

### 2. src/pages/contact.js を作成

```jsx
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default function Contact() {
  return (
    <div style={{ color: `teal` }}>
      <Link to="/">Home</Link>
      <Header headerText="Contact" />
      <p>Send us a message!</p>
    </div>
  )
}
```

Link 先のページが作成され正常に読み込める。 `Link` Component はページ内の遷移を表現するもので、Gatsbyの制御下にない外部のリンクは `<a>`  タグを利用する。

## Gatsby Site の Deploy

- 例では surgey を使ってサイトの展開をしている
- たまたま Netlify を使っているのでそっちでDeployしてみる
