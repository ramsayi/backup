---
title: ESLint规范代码格式
tags:
  - ESLint
categories:
  - 项目规范
  - ESLint
cover: '/assets/img/post/eslint.webp'
abbrlink: 89ef8535
date: 2022-09-03 15:13:10
---

```js
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true
  },
  extends: ['eslint:recommended', 'plugin:prettier/recommended'],
  parser: 'vue-eslint-parser',
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module'
  },
  plugins: ['vue'],
  rules: {
    indent: ['error', 2, { SwitchCase: 1 }], //强制统一缩进
    eqeqeq: ['error', 'always'], // 要求使用 === 和 !==
    'linebreak-style': ['error', 'windows'], //Windows的行结尾方式
    quotes: ['error', 'single'], //单引号
    semi: ['error', 'never'], //不加分号
    camelcase: 2 //强制驼峰法命名
  },
  // 全局的配置，通过eslint-loader传递给每个文件的配置
  globals: {
    document: true,
    window: true,
    uni: true,
    wx: true,
    ROUTES: true
  }
}

```

