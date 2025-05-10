# 贡献者指南

## 开始之前

首先，感谢你对VOICEVOX项目的关注。我们欢迎你积极参与。

实际上，当你想要参与时，任何社区都有规则，若你不理解这些规则，可能会觉得有些障碍。

这份指南旨在尽可能清晰地记录这些部分，以便为新贡献者提供一个容易参与的环境。由于这份文档详细解释了参与方式，可能对有经验的开发者来说某些部分不需要阅读。不过，我们欢迎有意愿贡献的开发者，阅读文档后加入项目。

## 负责人

| 角色               | 负责人                             |
| ------------------ | ---------------------------------- |
| 产品负责人         | @Hiroshiba                         |
| 维护者             | @Hiroshiba、@y-chan、@qryxip       |
| 汉化             | @WERTYUS11       |

## 参与心态

VOICEVOX项目属于集体开发型的开源软件。希望参与的你需要注意以下几点：

- 提建议时，若能与[VOICEVOX的目标](docs/使命・价值・愿景.md)对照，沟通会更顺畅。

- 关于具体的工作内容，需要在社区中讨论并达成共识。项目方针有时也会拒绝某些提案。

- 集体开发的乐趣之一，就是通过讨论共同创造。在与他人合作时，相较于独立工作，沟通需要更加细致，务必尊重每一位参与者。

- 参与项目与年龄、国籍、背景、性别等无关。我们不容忍任何形式的歧视。

- 项目尊重原创作者及其作品。在贡献时，务必遵守版权及许可证规定，避免提交抄袭的代码。

- 你提交的代码将按照项目定义的许可证处理。

- 若涉及到与隐私相关的实现，或可能对计算机造成危害的代码，必须在实施之前进行慎重讨论，并达成共识。

## 如何贡献

这份文档主要面向那些希望帮助改进程序的贡献者，提供了“参与方式”的指南。

VOICEVOX的贡献方式如下：

- 作为用户使用
- 发布文章或视频进行推广
- 帮助改进程序
- 编写文档等

程序分为三个部分，选择你感兴趣的部分进行参与。

| 项目类别          | 项目页面                                                     | 主要功能                       |
| ----------------- | ------------------------------------------------------------ | ------------------------------ |
| VOICEVOX          |主要功能                       |
| ----------------- | ------------------------------------------------------------ | ------------------------------ |
| VOICEVOX          | [项目链接](https://github.com/VOICEVOX/voicevox/)            | 主要是用户界面（编辑器部分）    |
| VOICEVOX_ENGINE            | 主要是用户界面（编辑器部分）    |
| VOICEVOX_ENGINE   | [项目链接](https://github.com/VOICEVOX/voicevox_engine/)     | 主要是Web API实现部分           |
| VOICEVOX_CORE     | [项目链接 | 主要是Web API实现部分           |
| VOICEVOX_CORE     | [项目链接](https://github.com/VOICEVOX/voicevox_core/)       | 主要是语音合成与库实现部分      |

如果你想了解整个结构，可以参考[此文档](docs/整体结构.md)。

## 初学者友好任务

如果你希望学习编程开发，或者希望在开源开发社区中实践，建议你参与已在社区的“初学者友好任务”。

这些任务通常被认为是“难度较低，但非常需要的任务”，你可以在参与的过程中一边学习一边贡献。

| 项目类别          | 初学者友好任务页面                                                                                                   |
| ----------------- | -------------------------------------------------------------------------------------------------------------------- |
| VOICEVOX          | [初学者友好任务](https://github.com/VOICEVOX/voicevox/issues?q=is%3Aissue+is%3Aopen+label%3A初心者歓迎タスク)         |
| VOICEVOX_ENGINE   | [初学者友好任务](https://github.com/VOICEVOX/voicevox_engine/issues?q=is%3Aissue+is%3Aopen+label%3A初心者歓迎タスク)  |
| VOICEVOX_CORE     | [初学者友好任务](https://github.com/VOICEVOX/voicevox_core/issues?q=is%3Aissue+is%3Aopen+label%3A初心者歓迎タスク)    |

## 准备工作

以下是为Windows用户准备的，假设你将要搭建VOICEVOX（编辑器）的环境。首先，构建VOICEVOX的测试版环境。

### 1. 安装VOICEVOX产品版

- 首先安装[VOICEVOX的产品版](https://voicevox.hiroshiba.jp/)，通过安装产品版，你可以获得可用的VOICEVOX引擎。

### 2. 设置开发环境

- 必要工具：

  - [Node.js](https://nodejs.org/en/download/releases/)\
    下载并安装文档中指定版本的Node.js，版本信息可以参考[这里](https://github.com/VOICEVOX/voicevox/blob/main/.node-version)。

- 需要的工具：
  - [Git](https://git-scm.com/downloads)
  - [Visual Studio Code](https://code.visualstudio.com/)
  - [GitHub CLI](https://github.com/cli/cli#installation)
  - [typos](https://github.com/crate-ci/typos#install) （如果需要进行拼写检查）
  - [Tortoise Git](https://tortoisegit.org/download/)（如果希望通过资源管理器进行操作）

### 3. Fork项目

- 通过Fork操作，将项目复制到自己的GitHub仓库。点击[这里](https://github.com/VOICEVOX/voicevox/fork)进行Fork。

### 4. 克隆源码（获取代码）

- 将你的GitHub仓库中的代码克隆到本地工作目录。

#### 4.1 使用命令行

- 使用GitHub命令行（GitHub CLI）：

```bash
gh repo clone https://github.com/(你的GitHub用户名)/voicevox.git
```

- 使用Git命令行（Git CLI）：

```bash
git clone git@github.com:(你的GitHub用户名)/voicevox.git
```

#### 4.2 使用图形界面

- 使用Visual Studio Code或Tortoise Git等工具克隆代码。

- 克隆地址为`git@github.com:(你的GitHub用户名)/voicevox.git`或`https://github.com/(你的GitHub用户名)/voicevox.git`。

### 5. 下载所需的程序

- 打开你在第4步中获取的文件夹，并在命令行中执行以下命令以准备环境，自动下载所需的工具。

```bash
npm install -g pnpm
pnpm i
```

### 6. 配置引擎

- 复制`.env.production`文件并将其重命名为`.env`，然后在编辑器中打开，修改`VITE_DEFAULT_ENGINE_INFOS`中的`executionFilePath`为第一步中安装的引擎路径。例如：

```ini
VITE_APP_NAME=voicevox
VITE_DEFAULT_ENGINE_INFOS=`[
    {
        "uuid": "074fc39e-678b-4c13-8916-ffca8d505d1d",
        "name": "VOICEVOX Engine",
        "executionEnabled": true,
        "executionFilePath": "C:/Users/(你的用户名)/AppData/Local/Programs/VOICEVOX/vv-engine/run.exe",
        "executionArgs": [],
        "host": "http://127.0.0.1:50021"
    }
]`
```

### 7. 启动开发环境

- 执行`pnpm run electron:serve`命令。如果一切配置正确，开发环境应该能够成功启动。

## 项目贡献步骤

### 1. 提出建议与调整

首先，如果有任何以下内容，请创建一个Issue：

- 想要修改程序的规格
- 希望添加新功能
- 确认存在bug

#### 1.1 提出建议

提出时，考虑你想建议的是VOICEVOX的哪个部分。同时，尽可能简单地描述“改善的点”或“可能受影响的点”。

#### 1.2 讨论

在这个阶段，你将与相关人员讨论实现的限制、影响范围、优先级等，确保讨论清晰并达成共识。

#### 1.3 开始工作

在现有的Issue上标明“我将着手进行”，确保不会与其他贡献者重复工作。

### 2. 创建分支

- 在你的工作目录中创建一个新的分支。

### 3. 编写代码

- 按照约定进行命名，尽量遵循代码规范。

### 4. 进行预先测试

- 在提交代码前，确保代码已通过测试，符合编码规范，并且没有引入额外的警告或错误。

### 5. 提交代码

- 在个人仓库中进行提交，并在提交信息中简洁明了地描述所做的改动。然后，通过Pull Request提交代码。

### 6. 代码审查

- 项目维护者或社区成员会对你的代码进行审查，若有问题，会提出修改建议。

### 7. 解决冲突

- 如果合并时出现代码冲突，需要手动解决冲突，并重新进行测试。

---

这样，你就完成了对VOICEVOX项目的贡献步骤冲突，并重新进行测试。


