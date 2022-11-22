S：

代码规范化、统一格式

环境：node v16.13.0，npm v8.1.0，vue v3.2.37，vite v3.0.7

T：

配置eslint、prettier

A:

##### 1.安装依赖

```shell
pnpm i eslint -D 

# ESLint 专门解析 TypeScript 的解析器 
pnpm i @typescript-eslint/parser -D 

# 内置各种解析 TypeScript rules 插件 
pnpm i @typescript-eslint/eslint-plugin -D 
pnpm i eslint-formatter-pretty -D 
pnpm i eslint-plugin-json -D 
pnpm i eslint-plugin-prettier -D 
pnpm i eslint-plugin-vue -D 
pnpm i @vue/eslint-config-prettier -D 
pnpm i babel-eslint -D pnpm i prettier -D
```



##### 2.新建配置文件

.eslintrc.js

```javascript
module.exports = {
 root: true,
 env: {
  browser: true,
  es2020: true,
  node: true,
  jest: true,
 },
 globals: {
  ga: true,
  chrome: true,
  __DEV__: true,
 },
 // 解析 .vue 文件
 parser: "vue-eslint-parser",
 extends: [
  "plugin:json/recommended",
  "plugin:vue/vue3-essential",
  "eslint:recommended",
  "@vue/prettier",
 ],
 plugins: ["@typescript-eslint"],
 parserOptions: {
  parser: "@typescript-eslint/parser", // 解析 .ts 文件
 },
 rules: {
  "no-console": process.env.NODE_ENV === "production" ? "warn" : "off",
  "no-debugger": process.env.NODE_ENV === "production" ? "warn" : "off",
  "prettier/prettier": "error",
 },
};
```



.eslintignore

##### 3.VS配置

ctrl+shift+P打开workspace配置

添加Eslint校验配置：

```json
"eslint.validate": [
  "javascript",
  "javascriptreact",
  "html",
  "vue",
  "typescript",
 ]
```



重启VS

##### 4.git规范

- husky：操作git钩子的工具

```shell
npx husky add .husky/pre-commit "pnpm run lint"
```

lint命令：

```shell
"lint": "eslint --ext .ts,.tsx,.vue src", # --fix自动修复，但不会把修复后的结果纳入当前commit
```



此时进行commit操作都会运行lint命令进行代码规范。

（4）配置push之前通过单元测试的钩子

```shell
npx husky add .husky/pre-push "pnpm run test:run"
```

由于 vitest 默认是以伺服模式运行，所以需要写一个专门的脚本让测试运行在伺服模式下 packages.json

```shell
"scripts": {
	"test:run": "vitest run",
},
```

（5）校验commit message规范

- 安装commitlint

```shell
pnpm i -d @commitlint/config-conventional@"17.0.2" @commitlint/cli@"17.0.2"
```

- 根目录新建commitlint.config.js

```shell
module.exports = {
  extends: ["@commitlint/config-conventional"],
};
```

- 配置commitlint脚本

```shell
npx husky add .husky/commit-msg ""
```

修改.husky/commit-msg

```shell
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx --no -- commitlint --edit "$1"
```



#### Complete！！

