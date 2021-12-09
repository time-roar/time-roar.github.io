# Vue

## vue  安装

- 安装vue-cli

```shell
npm i -g @vue/cli
```

- 创建项目

```shell
vue create timeroar-auth-front
```

- 如下提示选择手动配置

```shell
Vue CLI v4.5.15
? Please pick a preset:
  Default ([Vue 2] babel, eslint)
  Default (Vue 3) ([Vue 3] babel, eslint)
> Manually select features
```

- 可选如下配置

```shell
? Check the features needed for your project:
 (*) Choose Vue version //选择vue版本
 (*) Babel	//使用babel
 ( ) TypeScript //不用ts
 ( ) Progressive Web App (PWA) Support //不用pwa
 (*) Router //使用vue-router
 (*) Vuex //使用vuex	
 (*) CSS Pre-processors //使用css预处理
>(*) Linter / Formatter //使用代码格式化 !强烈建议开启
 ( ) Unit Testing
 ( ) E2E Testing
```

- 选择3.0

```shell
? Choose a version of Vue.js that you want to start the project with
  2.x
> 3.x
```

- 不使用history路由

```shell
 Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) n
```

- 如果你能科学,你可以选node-sass,否则建议选dart-sass

```shell
? Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default): (Use arrow keys)
> Sass/SCSS (with dart-sass)
  Sass/SCSS (with node-sass)
  Less
  Stylus
```

- 使用Eslint标准格式化方案

```shell
? Pick a linter / formatter config:
  ESLint with error prevention only
  ESLint + Airbnb config
> ESLint + Standard config
  ESLint + Prettier
```

- 配置校验方式

```shell
? Pick additional lint features: (Press <space> to select, <a> to toggle all, <i> to invert selection)
>(*) Lint on save  //保存校验
 ( ) Lint and fix on commit //保存提交都需要校验
```

- 创建es独立配置文件

```shell
? Where do you prefer placing config for Babel, ESLint, etc.?
> In dedicated config files
  In package.json
```

- 是否存储预设?

```shell
 Save this as a preset for future projects? (y/N)
```

- 升级vue到最新版使其支持 script setup语法

```shell
npm i vue@3.2.8 vue-router@4.0.11 vuex@4.0.2
```

- 导入element-plus

```shell
vue add element-plus
```

