##### 安装依赖

```js
npm i @iconify/iconify
npm i @iconify/json vite-plugin-purge-icons -D
```

##### vite.config.js配置

```js
import PurgeIcons from 'vite-plugin-purge-icons';

export default defineConfig({
  plugins: [PurgeIcons({})],
});

```

##### 在main.js引入

```js
import '@purge-icons/generated';
```



