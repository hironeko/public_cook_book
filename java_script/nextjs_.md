## 導入

```shell
npx create-next-app app-name
```

### tailwind をいれる

```shell
yarn add tailwindcss -D
npx tailwindcss init --full
touch styles/tailwind.css
```

- 以下追記

- tailwind.config.js
```javascript
const colors = require('tailwindcss/colors')

module.exports = {
  purge: ['./components/**/*.jsx', './pages/**/*.jsx'], // 追記
  // 以下省略
}
```

- postcss.config.js

```javascript
module.exports = {
  plugins: ['tailwindcss', 'postcss-preset-env'],
}
```

- styles/global.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```shell
yarn dev
```