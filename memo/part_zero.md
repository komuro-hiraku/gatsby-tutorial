# Part 0

https://www.gatsbyjs.com/docs/tutorial/part-zero/

- node は Version.10 以降
  - v14.15.4
- npm はTutorial では 6.13.3. (自分の環境は6.14.10)
- あと git が必要

## Gatsby.js を インストール

```bash
$ npm install -g gatsby-cli
...
```

確認

```bash
$ gatsby --help
Usage: gatsby <command> [options]

Commands:
  gatsby develop                      Start development server. Watches files, rebuilds, and hot reloads if something changes
  gatsby build                        Build a Gatsby project.
  gatsby serve                        Serve previously built Gatsby site.
  gatsby info                         Get environment information for debugging and issue reporting
  gatsby clean                        Wipe the local gatsby environment including built assets and cache
  gatsby repl                         Get a node repl with context of Gatsby environment, see (https://www.gatsbyjs.com/docs/gatsby-repl/)
  gatsby recipes [recipe]             [EXPERIMENTAL] Run a recipe
  gatsby plugin <cmd> [plugins...]    Useful commands relating to Gatsby plugins
  gatsby new [rootPath] [starter]     Create new Gatsby project.
  gatsby telemetry                    Enable or disable Gatsby anonymous analytics collection.
  gatsby options [cmd] [key] [value]  View or set your gatsby-cli configuration settings.

Options:
  --verbose                Turn on verbose output                                                                                                                                 [boolean] [default: false]
  --no-color, --no-colors  Turn off the color in output                                                                                                                           [boolean] [default: false]
  --json                   Turn on the JSON logger                                                                                                                                [boolean] [default: false]
  -h, --help               Show help                                                                                                                                                               [boolean]
  -v, --version            Show the version of the Gatsby CLI and the Gatsby package in the current project
```

## Hello World

```bash
$ gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

- `new` : プロジェクト作成
- `hello-world` : プロジェクト名
- `https://github.com/gatsbyjs/gatsby-starter-hello-world` : 初期テンプレートのコードRepository

## 開発モードで起動

```bash
$ cd hello-world/
$ gatsby develop
success open and validate gatsby-configs - 0.012s
success load plugins - 0.062s
success onPreInit - 0.030s
success initialize cache - 0.008s
success copy gatsby files - 0.075s
success onPreBootstrap - 0.027s
success createSchemaCustomization - 0.003s
success Checking for changed pages - 0.002s
success source and transform nodes - 0.041s
success building schema - 0.147s
info Total nodes: 18, SitePage nodes: 1 (use --verbose for breakdown)
success createPages - 0.003s
success Checking for changed pages - 0.001s
success createPagesStatefully - 0.032s
success update schema - 0.018s
success write out redirect data - 0.002s
success onPostBootstrap - 0.003s
info bootstrap finished - 2.722s
success onPreExtractQueries - 0.001s
success extract queries from components - 0.079s
success write out requires - 0.010s
success run page queries - 0.040s - 2/2 49.85/s
⠀
You can now view gatsby-starter-hello-world in the browser.
⠀
  http://localhost:8000/
⠀
View GraphiQL, an in-browser IDE, to explore your site's data and schema
⠀
  http://localhost:8000/___graphql
⠀
Note that the development build is not optimized.
To create a production build, use gatsby build
⠀
success Building development bundle - 3.676s
```

`localhost:8000` で起動中。アクセス

```bash
$ curl http://localhost:8000/
<!DOCTYPE html><html><head><meta charSet="utf-8"/><meta http-equiv="x-ua-compatible" content="ie=edge"/><meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"/><meta name="note" content="environment=development"/><script src="/socket.io/socket.io.js"></script></head><body><div id="___gatsby"></div><script src="/polyfill.js" nomodule=""></script><script src="/commons.js"></script></body></html>
```

## VisualStudio Code Setup

基本的に Visual Studio Code で書く予定。Extensions をインストール

## Trouble Shooting

## npm version が古い

怒られる。

```bash
found 8 vulnerabilities (6 low, 2 high)
  run `npm audit fix` to fix them, or `npm audit` for details


   ╭─────────────────────────────────────────────────────────────────╮
   │                                                                 │
   │      New minor version of npm available! 6.13.4 → 6.14.11       │
   │   Changelog: https://github.com/npm/cli/releases/tag/v6.14.11   │
   │                Run npm install -g npm to update!                │
   │                                                                 │
   ╰─────────────────────────────────────────────────────────────────╯
```

### 謎のエラー

```bash
 ERROR

(node:20769) ExperimentalWarning: Package name self resolution is an experimental feature. This feature could change at any time
```

`ExperimentalWarning` だから無視して良いんだろうか。

#### gyp: No Xcode or CLT version detected!

```bash
> fsevents@1.2.13 install /YOUR_HOME/Develop/gatsby/hello-world/node_modules/fsevents
> node install.js

No receipt for 'com.apple.pkg.CLTools_Executables' found at '/'.

No receipt for 'com.apple.pkg.DeveloperToolsCLILeo' found at '/'.

No receipt for 'com.apple.pkg.DeveloperToolsCLI' found at '/'.

gyp: No Xcode or CLT version detected!
gyp ERR! configure error
gyp ERR! stack Error: `gyp` failed with exit code: 1
gyp ERR! stack     at ChildProcess.onCpExit (/YOUR_HOME/.nvm/versions/node/v14.15.4/lib/node_modules/npm/node_modules/node-gyp/lib/configure.js:351:16)
gyp ERR! stack     at ChildProcess.emit (events.js:315:20)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:277:12)
gyp ERR! System Darwin 19.6.0
gyp ERR! command "/YOUR_HOME/.nvm/versions/node/v14.15.4/bin/node" "/YOUR_HOME/.nvm/versions/node/v14.15.4/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /YOUR_HOME/Develop/gatsby/hello-world/node_modules/fsevents
gyp ERR! node -v v14.15.4
gyp ERR! node-gyp -v v5.1.0
gyp ERR! not ok
```

gyp がエラーだなー。謎。Xcode-select のインストールコマンドは実行済み。

```bash
$ xcode-select --install
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```

## 