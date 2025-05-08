# VOICEVOX

[![版本发布](https://img.shields.io/github/v/release/VOICEVOX/voicevox?label=Release)](https://github.com/VOICEVOX/voicevox/releases)  
[![构建状态](https://github.com/VOICEVOX/voicevox/actions/workflows/build.yml/badge.svg)](https://github.com/VOICEVOX/voicevox/actions/workflows/build.yml)  
[![测试状态](https://github.com/VOICEVOX/voicevox/actions/workflows/test.yml/badge.svg)](https://github.com/VOICEVOX/voicevox/actions/workflows/test.yml)  
[![Discord社区](https://img.shields.io/discord/879570910208733277?color=5865f2&label=&logo=discord&logoColor=ffffff)](https://discord.gg/WMwWetrzuh)  

这是[VOICEVOX](https://voicevox.hiroshiba.jp/)的编辑器项目。  
（引擎部分参见[VOICEVOX ENGINE](https://github.com/VOICEVOX/voicevox_engine/)，核心库参见[VOICEVOX CORE](https://github.com/VOICEVOX/voicevox_core/)，整体架构详见[本文档](./docs/整体架构.md)。）

## 致用户

此页面为开发用文档。使用说明请参见[VOICEVOX官网](https://voicevox.hiroshiba.jp/)。

## 致有意贡献项目的开发者

VOICEVOX项目欢迎所有感兴趣的人参与贡献。  
我们准备了[贡献指南](./CONTRIBUTING.md)说明参与流程。

贡献不仅限于编程，还包括文档编写、测试用例生成、改进提案讨论等多种形式。  
特别设有新手友好任务，期待您的加入。

本编辑器采用Electron・TypeScript・Vue・Vuex等技术栈，整体结构可能较难理解。  
[代码导读](./docs/代码导读.md)文档介绍了项目结构，希望能为开发提供帮助。

在提交Issue解决方案的Pull Request时，为避免多人重复处理同一Issue，  
请在Issue中声明您开始工作，或先创建Draft状态的PR。

欢迎加入[VOICEVOX非官方Discord社区](https://discord.gg/WMwWetrzuh)参与开发讨论或日常交流。

### 设计规范

请参考[UX・UI设计方针](./docs/UX・UI设计方针.md)。

## 环境搭建

安装[.node-version](.node-version)中指定版本的Node.js。  
推荐使用Node.js版本管理工具（如[nvs](https://github.com/jasongin/nvs)或[Volta](https://volta.sh)），可便捷安装并自动切换版本。

安装Node.js后，请Fork并克隆[本仓库](https://github.com/VOICEVOX/voicevox.git)。

### 安装依赖库

执行以下命令安装/更新依赖：

```bash
npm i -g pnpm # 首次运行
pnpm i
```

## 运行

### 引擎准备

复制`.env.production`创建`.env`文件，在`VITE_DEFAULT_ENGINE_INFOS`中指定`executionFilePath`为  
[正式版VOICEVOX](https://voicevox.hiroshiba.jp/)内的`vv-engine/run.exe`即可运行。

Windows默认安装路径为`C:/Users/(用户名)/AppData/Local/Programs/VOICEVOX/vv-engine/run.exe`。  
注意路径分隔符应使用`/`而非`\`。

macOS用户需指定`/path/to/VOICEVOX.app/Resources/MacOS/vv-engine/run`。

Linux用户请使用[Releases](https://github.com/VOICEVOX/voicevox/releases/)中tar.gz包内的`vv-engine/run`命令。  
AppImage版可通过`$ /path/to/VOICEVOX.AppImage --appimage-mount`挂载文件系统。

若已单独启动引擎API服务器，则无需指定`executionFilePath`，  
但需将`executionEnabled`设为`false`（适用于已启动正式版VOICEVOX的情况）。

修改API端点需调整`VITE_DEFAULT_ENGINE_INFOS`中的`host`参数。

### 运行Electron

```bash
# 开发模式运行
pnpm run electron:serve

# 近似生产环境运行
pnpm run electron:serve --mode production

# 带参数运行
pnpm run electron:serve -- ...
```

语音合成引擎仓库：<https://github.com/VOICEVOX/voicevox_engine>

### 运行Storybook

可通过Storybook进行组件开发：

```bash
pnpm run storybook
```

main分支的Storybook部署于[VOICEVOX/preview-pages](https://github.com/VOICEVOX/preview-pages)：  
<https://voicevox.github.io/preview-pages/preview/branch-main/storybook/index.html>

### 运行浏览器版（开发中）

需先启动语音合成引擎，执行以下命令后访问显示的localhost地址：

```bash
pnpm run browser:serve
```

main分支的构建结果部署于[VOICEVOX/preview-pages](https://github.com/VOICEVOX/preview-pages)：  
<https://voicevox.github.io/preview-pages/preview/branch-main/editor/index.html>  
当前仍需在本地启动语音合成引擎。

## 构建

```bash
pnpm run electron:build
```

### 通过Github Actions构建

在fork的仓库中启用Actions，通过workflow_dispatch触发`build.yml`即可构建。  
产物将上传至Release页面。

## 测试

### 单元测试

执行`./tests/unit/`下的测试及Storybook测试：

```bash
pnpm run test:unit
pnpm run test-watch:unit # 监控模式
pnpm run test-ui:unit # 显示Vitest UI
pnpm run test:unit --update # 更新快照
```

> [!NOTE]  
> `./tests/unit`下的测试根据文件名区分运行环境：  
> - `.node.spec.ts`：Node.js环境  
> - `.browser.spec.ts`：浏览器环境（Chromium）  
> - `.spec.ts`：浏览器环境（happy-dom模拟）

### 浏览器端到端测试

执行不依赖Electron功能的UI/语音合成等端到端测试。

> [!NOTE]  
> 涉及引擎配置修改的测试仅在CI(Github Actions)中运行。

```bash
pnpm run test:browser-e2e
pnpm run test-watch:browser-e2e # 监控模式
pnpm run test-watch:browser-e2e --headed # 显示测试UI
pnpm run test-ui:browser-e2e # 显示Playwright UI
```

基于Playwright支持测试模式生成：  
**在浏览器版运行状态下**执行：

```bash
pnpm exec playwright codegen http://localhost:5173/ --viewport-size=1024,630
```

详见[Playwright文档的测试生成器](https://playwright.dev/docs/codegen-intro)。

### Storybook可视化回归测试

通过组件截图对比检测变更，显示差异部分。

> [!NOTE]  
> 该测试仅支持Windows平台。

```bash
pnpm run test:storybook-vrt
pnpm run test-watch:storybook-vrt # 监控模式
pnpm run test-ui:storybook-vrt # 显示Playwright UI
```

#### 快照更新

浏览器端到端测试和Storybook使用可视化回归测试。  
当前VRT测试仅限Windows平台，按以下步骤更新快照：

##### 通过Github Actions更新

1. 在fork的仓库设置中启用GitHub Actions  
2. 仓库设置 > Actions > General > Workflow permissions中选择Read and write permissions  
3. 提交包含`[update snapshots]`的commit：

   ```bash
   git commit -m "修改UI [update snapshots]"
   ```

4. Workflow完成后将自动提交新快照  
5. 拉取后推送空commit重新测试：

   ```bash
   git commit --allow-empty -m "（重新运行测试）"
   git push
   ```

> [!NOTE]  
> 可通过创建Token并添加到Secrets实现自动重试：  
> 1. 访问[Fine-granted Tokens](https://github.com/settings/personal-access-tokens/new)  
> 2. 输入名称，授予`用户名/voicevox`仓库的Contents读写权限  
> 3. 创建后复制Token字符串  
> 4. 在`用户名/voicevox`仓库的Settings > Secrets and variables > Actions中添加名为`PUSH_TOKEN`的Secret  

##### 本地更新

仅更新当前操作系统对应的快照：

```bash
pnpm run test:browser-e2e --update-snapshots
```

### Electron端到端测试

执行依赖Electron功能的引擎启停等端到端测试：

```bash
pnpm run test:electron-e2e
pnpm run test-watch:electron-e2e # 监控模式
```

## 生成依赖库许可信息

依赖库许可信息在Github Workflow构建时自动生成，也可手动生成：

```bash
# 从voicevox_engine获取licenses.json保存为engine_licenses.json

pnpm run license:generate -o voicevox_licenses.json
pnpm run license:merge -o public/licenses.json -i engine_licenses.json -i voicevox_licenses.json
```

## 代码格式化

提交PR前请执行格式化：

```bash
pnpm run fmt
```

## 代码检查（静态分析）

执行静态分析预防潜在问题，提交PR前请运行：

```bash
pnpm run lint
```

## 拼写检查

使用[typos](https://github.com/crate-ci/typos)进行拼写检查：

```bash
pnpm run typos
```

如需排除误判文件，请参照[配置文件说明](https://github.com/crate-ci/typos#false-positives)修改`_typos.toml`。

## 类型检查

执行TypeScript类型检查：

```bash
pnpm run typecheck
```

## Markdown检查

Markdown语法检查：

```bash
pnpm run markdownlint
```

## Shell脚本检查

ShellScript语法检查，安装方法参见[官方文档](https://github.com/koalaman/shellcheck#installing)：

```bash
shellcheck ./build/*.sh
```

## OpenAPI生成器

在语音合成引擎运行状态下执行：

```bash
curl http://127.0.0.1:50021/openapi.json >openapi.json

pnpm exec openapi-generator-cli generate \
    -i openapi.json \
    -g typescript-fetch \
    -o src/openapi/ \
    --additional-properties "modelPropertyNaming=camelCase,supportsES6=true,withInterfaces=true,typescriptThreePlus=true"

pnpm run fmt
```

### OpenAPI生成器版本升级

通过以下命令检查/安装新版本：

```bash
pnpm exec openapi-generator-cli version-manager list
```

## VS Code调试

开发构建时（如`serve`或`electron:serve`），vite会生成sourcemap实现源码映射。

复制`.vscode/launch.template.json`创建`.vscode/launch.json`，  
复制`.vscode/tasks.template.json`创建`.vscode/tasks.json`，  
即可通过VS Code启动开发构建并进行调试。

## 许可证

采用LGPL v3与无需公开源码的附加许可的双重授权。  
如需获取附加许可，请联系ヒホ：  
推特账号：[@hiho_karuta](https://x.com/hiho_karuta)
