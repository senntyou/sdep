# sdep

[English Documentation](./README.en.md)

查看一个模块的依赖树.

## 快速开始

安装 sdep:

```
npm install sdep -g
```

使用:

```
sdep [options] <file>
```

## 参数

- `-q, --query <query>`: 查询某个字符串，过滤输出
- `-r, --regular`: 当查询某个字符串，过滤输出时，把查询字符串当作正则匹配
- `-i, --ignore`: 忽略 node_modules 下的文件
- `-d, --directory <directory>`: 包含所有模块的目录, 默认是 process.cwd()
- `-b, --base <base>`: 简写输出的基路径, 默认是 process.cwd()
- `--rc <rc>`: RequireJs 配置 for AMD modules
- `--wc <wc>`: Webpack 配置 for aliased modules
- `--tc <tc>`: TypeScript 配置
- `-f, --full`: 当使用查询某个字符串，过滤输出时，显示完整的依赖链

## 使用的第三方库

- [commander.js](https://github.com/tj/commander.js)
- [node-dependency-tree](https://github.com/dependents/node-dependency-tree)

## 示例

#### 查看一个文件的依赖结构

```
sdep example/index.js
```

```
example/index.js
├ example/css/css.css
├ example/css/scss.scss
├ example/css/less.less
├ example/jsx.jsx
| ├ node_modules/react/index.js
| | ├ node_modules/react/cjs/react.production.min.js
| | | └ node_modules/object-assign/index.js
| | └ node_modules/react/cjs/react.development.js
| |   ├ node_modules/object-assign/index.js
| |   └ node_modules/prop-types/checkPropTypes.js
| |     └ node_modules/prop-types/lib/ReactPropTypesSecret.js
| ├ node_modules/react-dom/index.js
| | ├ node_modules/react-dom/cjs/react-dom.production.min.js
| | | ├ node_modules/react/index.js
| | | | ├ node_modules/react/cjs/react.production.min.js
| | | | | └ node_modules/object-assign/index.js
| | | | └ node_modules/react/cjs/react.development.js
| | | |   ├ node_modules/object-assign/index.js
| | | |   └ node_modules/prop-types/checkPropTypes.js
| | | |     └ node_modules/prop-types/lib/ReactPropTypesSecret.js
| | | ├ node_modules/object-assign/index.js
| | | └ node_modules/scheduler/index.js
| | |   ├ node_modules/scheduler/cjs/scheduler.production.min.js
| | |   └ node_modules/scheduler/cjs/scheduler.development.js
| | └ node_modules/react-dom/cjs/react-dom.development.js
| |   ├ node_modules/react/index.js
| |   | ├ node_modules/react/cjs/react.production.min.js
| |   | | └ node_modules/object-assign/index.js
| |   | └ node_modules/react/cjs/react.development.js
| |   |   ├ node_modules/object-assign/index.js
| |   |   └ node_modules/prop-types/checkPropTypes.js
| |   |     └ node_modules/prop-types/lib/ReactPropTypesSecret.js
| |   ├ node_modules/object-assign/index.js
| |   ├ node_modules/prop-types/checkPropTypes.js
| |   | └ node_modules/prop-types/lib/ReactPropTypesSecret.js
| |   ├ node_modules/scheduler/index.js
| |   | ├ node_modules/scheduler/cjs/scheduler.production.min.js
| |   | └ node_modules/scheduler/cjs/scheduler.development.js
| |   └ node_modules/scheduler/tracing.js
| |     ├ node_modules/scheduler/cjs/scheduler-tracing.production.min.js
| |     └ node_modules/scheduler/cjs/scheduler-tracing.development.js
| └ example/wel.jsx
|   └ node_modules/react/index.js
|     ├ node_modules/react/cjs/react.production.min.js
|     | └ node_modules/object-assign/index.js
|     └ node_modules/react/cjs/react.development.js
|       ├ node_modules/object-assign/index.js
|       └ node_modules/prop-types/checkPropTypes.js
|         └ node_modules/prop-types/lib/ReactPropTypesSecret.js
└ example/async/index.js
  └ example/async/index.css
```

#### 查看一个文件包含 react 的依赖链

```
sdep example/index.js -q react
```

```
example/index.js
└ example/jsx.jsx
  └ node_modules/react/index.js
example/index.js
└ example/jsx.jsx
  └ node_modules/react-dom/index.js
example/index.js
└ example/jsx.jsx
  └ example/wel.jsx
    └ node_modules/react/index.js
```

#### 查看一个文件包含 less 或 scss 的依赖链

```
sdep example/index.js -q 'less|scss' -r
```

```
example/index.js
└ example/css/scss.scss
example/index.js
└ example/css/less.less
```
