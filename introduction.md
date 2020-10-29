# 介紹

Deno 是一個具有預設安全及有良好開發體驗的 JavaScript/TypeScript 運行環境。

Deno 基於V8、Rust、Tokio上。

## 功能亮點

- 預設安全性。除非啟用否則無法訪問檔案、網路或運行環境
- 原生支援Typescript
- 單一的可執行檔 (`deno`)
- 內建實用工具，例如 依賴檢查工具 (`deno info`)及程式碼格式化工具 (`deno fmt`)
- 擁有一套經過審查且[保證與Deno相容的標準模組](https://github.com/denoland/deno/tree/master/std)
- 腳本可以被單獨封裝到一個JavaScript檔案

## 哲學

Deno的目標是為現代程式設計師提供高效能且安全的腳本環境。  
Deno只有單一的可執行檔，並且該執行檔可以運行任何Deno程式，
包含了運行環境及套件管理工具，只要一個URL，就能運行[解壓縮後不超過15MB](https://github.com/denoland/deno/releases)的Deno可執行檔。  
Deno使用與瀏覽器相容的加載模組(URL)。  
除此之外，對於過去使用Python與Bash的腳本，Deno將是一個優秀的替代品。

## Goals

- Only ship a single executable (`deno`).
- Provide Secure Defaults.
  - Unless specifically allowed, scripts can't access files, the environment, or
    the network.
- Browser compatible: The subset of Deno programs which are written completely
  in JavaScript and do not use the global `Deno` namespace (or feature test for
  it), ought to also be able to be run in a modern web browser without change.
- Provide built-in tooling like unit testing, code formatting, and linting to
  improve developer experience.
- Does not leak V8 concepts into user land.
- Be able to serve HTTP efficiently.

## Comparison to Node.js

- Deno does not use `npm`.
  - It uses modules referenced as URLs or file paths.
- Deno does not use `package.json` in its module resolution algorithm.
- All async actions in Deno return a promise. Thus Deno provides different APIs
  than Node.
- Deno requires explicit permissions for file, network, and environment access.
- Deno always dies on uncaught errors.
- Uses "ES Modules" and does not support `require()`. Third party modules are
  imported via URLs:

  ```javascript
  import * as log from "https://deno.land/std@$STD_VERSION/log/mod.ts";
  ```

## Other key behaviors

- Remote code is fetched and cached on first execution, and never updated until
  the code is run with the `--reload` flag. (So, this will still work on an
  airplane.)
- Modules/files loaded from remote URLs are intended to be immutable and
  cacheable.
