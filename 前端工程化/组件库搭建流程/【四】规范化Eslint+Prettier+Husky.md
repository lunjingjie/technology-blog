S：

代码规范化、统一格式

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



