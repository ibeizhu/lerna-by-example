# Lerna By Example
## 项目介绍
使用 Lerna 6+ 的一个案例仓库

观看这个视频 [10-minute walkthrough](https://youtu.be/1oxFYphTS4Y) 了解新的 lerna 如何工作的

这个仓库包含三个 package 和一个 project

- `bz-test-header` (a library of React components)
- `bz-test-footer` (a library of React components)
- `remixapp` (an app written using the Remix framework which depends on both `header` and `footer`)
  - 仓库是 private，避免和包一起发布

```
packages/
    bz-test-header/
        src/
            ...
        package.json
        rollup.config.json
        jest.config.js

    bz-test-footer/
        src/
            ...
        package.json
        rollup.config.json
        jest.config.js

    remixapp/
        app/
            ...
        public/
        package.json
        remix.config.js

package.json
```

## 安装依赖
```
npm install
```

package.json 中定义了 `workspaces` 字段，这是本地引用包（NPM/YARN/PNPM ）的内置解决方案，执行`npm install` 会自动链接包

`lerna.json` 中定义 `"useWorkspaces": true` 表示包交叉链接功能委托给包管理器，此项目使用 npm

> Lerna 历史上有自己的依赖管理解决方案：lerna bootstrap. 这是必需的，因为在 Lerna 首次发布时，没有可用的本地解决方案。如今，现代包管理器带有内置的“工作区”解决方案，因此强烈建议改用它。lerna bootstrap和其他相关命令将在 Lerna v7 中正式弃用。请参阅https://github.com/lerna/lerna/discussions/3410


## 可视化查看依赖
```
npx nx graph
```

## 构建
```
npm run build
```
执行 `npx lerna run build`

## 本地启动
```
npm run dev
```
`npm run dev` 会执行 `npx lerna run dev --scope=remixapp`命令，详解 package.json ,由于在 nx.json 配置了 dev dependsOn build，所以执行 `lerna run dev`之前，会先执行 `lerna run build`

## 发布包
```
npm run publish
```

执行 `npx lerna publish --no-private`, --no-private 表示 private 包不做发布（private在package.json中定义）