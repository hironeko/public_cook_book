## install

```shell
npx create-nuxt-app nuxt-ts-jest                                                                                                                                 (master) ✖
create-nuxt-app v2.11.1
✨  Generating Nuxt.js project in nuxt-ts-jest
? Project name nuxt-ts-jest
? Project description My gnarly Nuxt.js project
? Author name none
? Choose the package manager Yarn
? Choose UI framework Tailwind CSS
? Choose custom server framework None (Recommended)
? Choose Nuxt.js modules (Press <space> to select, <a> to toggle all, <i> to invert selection)
? Choose linting tools (Press <space> to select, <a> to toggle all, <i> to invert selection)
? Choose test framework Jest
? Choose rendering mode Single Page App
? Choose development tools (Press <space> to select, <a> to toggle all, <i> to invert selection)
```

## ディレクトリの移動

- src ディレクトリを作成しそこに下記 file 郡を移行

```shell
── src
│   ├── assets
│   ├── components
│   ├── layouts
│   ├── middleware
│   ├── pages
│   ├── plugins
│   ├── static
│   └── store
...
```

- 以下の状態にする

```shell

├── README.md
├── jest.config.js
├── node_modules
├── nuxt.config.js
├── package.json
├── src
├── test
└── yarn.lock
```

## nuxt.config.js の編集

```javascript
export default {
  mode: "spa",
  srcDir: "src"
  // 省略
}
```

## ts 化対応

```shell
yarn add -D @nuxt/typescript-build @nuxt/types
```

## nuxt.config.js の編集

```javascript
export default {
  // 省略

  buildModules: [
    "@nuxt/typescript-build",
    // Doc: https://github.com/nuxt-community/nuxt-tailwindcss
    "@nuxtjs/tailwindcss"
  ]

  // 省略
}
```

## 型定義ファイルの作成と tsconfig.json の作成

- types ディレクトリを作成

```typescript
declare module "*.vue" {
  import Vue from "vue"
  export default Vue
}
```

```json
{
  "compilerOptions": {
    "target": "es2018",
    "module": "esnext",
    "moduleResolution": "node",
    "lib": ["esnext", "esnext.asynciterable", "dom"],
    "esModuleInterop": true,
    "allowJs": true,
    "sourceMap": true,
    "strict": true,
    "noEmit": true,
    "baseUrl": "./",
    "paths": {
      "~/*": ["src/*"],
      "@/*": ["src/*"]
    },
    "types": ["@types/node", "@nuxt/types"]
  },
  "files": ["shims-vue.d.ts"],
  "exclude": ["node_modules"]
}
```

## typescript-runtime を入れて設定

```shell
yarn add @nuxt/typescript-runtime
```

- package.json の修正

```json
{
  // 省略
  "scripts": {
    "dev": "nuxt-ts",
    "build": "nuxt-ts build",
    "start": "nuxt-ts start",
    "generate": "nuxt-ts generate",
    "test": "jest"
  }
  // 省略
}
```

## ts で test を書くために準備

```shell
yarn add -D ts-jest @types/jest
```

- 設定を変更

```javascript
module.exports = {
  moduleNameMapper: {
    "^@/(.*)$": "<rootDir>/src/$1",
    "^~/(.*)$": "<rootDir>/src/$1",
    "^vue$": "vue/dist/vue.common.js"
  },
  moduleFileExtensions: ["js", "vue", "json", "ts"],
  transform: {
    "^.+\\.ts$": "<rootDir>/node_modules/ts-jest",
    "^.+\\.js$": "<rootDir>/node_modules/babel-jest",
    ".*\\.(vue)$": "<rootDir>/node_modules/vue-jest"
  },
  testMatch: ["<rootDir>/test/**/*.(js|jsx|ts|tsx)"],
  // collectCoverage: true,
  collectCoverageFrom: [
    "<rootDir>/components/**/*.vue",
    "<rootDir>/pages/**/*.vue"
  ],
  testPathIgnorePatterns: ["<rootDir>/.nuxt/", "<rootDir>/node_modules/"],
  preset: "ts-jest",
  globals: {
    "ts-jest": {
      tsConfig: "tsconfig.json"
    }
  }
}
```
