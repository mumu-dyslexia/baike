# Dyslexia Baike

基于 [Hugo](https://gohugo.io/) 和 [Hextra](https://github.com/imfing/hextra) 主题构建的文档站点。

## 环境要求

- [Hugo](https://gohugo.io/installation/) v0.146.0+（需要 extended 版本）
- [Go](https://go.dev/dl/) 1.20+
- [Node.js](https://nodejs.org/)（用于编译 CSS）

## 安装依赖

```bash
npm install
```

## 常用命令

### npm

| 命令                | 说明                                                  |
| ------------------- | ----------------------------------------------------- |
| `npm run dev:theme` | 启动开发服务器，支持主题热加载和调试日志（端口 1313） |
| `npm run dev`       | 启动开发服务器，禁用快速渲染（端口 1313）             |
| `npm run build`     | 构建文档站点                                          |
| `npm run build:css` | 使用 PostCSS 和 Tailwind 编译 CSS                     |

### Task runner

需要先安装 [Task](https://taskfile.dev/installation/)。

| 命令         | 说明                                       |
| ------------ | ------------------------------------------ |
| `task dev`   | 启动开发服务器（运行 `npm run dev:theme`） |
| `task build` | 构建文档站点                               |
| `task css`   | 编译生产环境 CSS（会先执行 build）         |
