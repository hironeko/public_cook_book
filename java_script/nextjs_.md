## 導入

```shell
npx create-next-app app-name
```

### tailwind をいれる

```shell
yarn add -D tailwindcss@latest postcss@latest autoprefixer@latest
npx tailwindcss init --full
touch pages/styles/tailwind.css
```

- 以下追記

pages以下に_app.tsxを作成する
```javascript
import './styles/tailwind.css'

function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}

export default App
```

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
  plugins: ['tailwindcss', ],
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