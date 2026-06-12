# Claude Code 全版本配置教程（终端 + 桌面版 + VSCode 插件版）
> 本教程涵盖 Claude Code 的三种使用方式。**令牌配置**为公共步骤，三个版本通用，只需配置一次。
>
> **ccswitch 配置**分为两个入口：**桌面版**走一个配置口，**终端版 + VSCode 插件版**走另一个配置口，请按需配置。

---

## 目录
+ [一、环境准备](#env-setup)
+ [二、创建令牌（三版本通用）](#create-token)
+ [三、安装与配置 ccswitch](#ccswitch)
    - [3A：终端版 + VSCode 插件版的 ccswitch 配置](#ccswitch-3a)
    - [3B：桌面版的 ccswitch 配置](#ccswitch-3b)
+ [四、安装 Claude Code](#install)
    - [方式 A：终端版（CLI）](#install-cli)
    - [方式 B：桌面版](#install-desktop)
    - [方式 C：VSCode 插件版](#install-vscode)
+ [五、验证与测试](#verify)
+ [六、常见问题与注意事项](#faq)

---

## 一、环境准备
> **说明**：终端版（CLI）和 VSCode 插件版需要 Node.js 环境；桌面版为独立应用，不依赖 Node.js，可跳过此步。
>

### 1. 检查 Node.js 环境
**Node.js >= 18.x**（推荐 20.x 或更高版本，npm >= 10.x）

`Win+R` 输入 `cmd` 打开终端，运行以下命令检查版本：

```bash
node -v
npm -v
```

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304009-5e825d0a-0f69-44e1-9f70-099deb365540.png)

### 2. 安装 / 更新 Node.js
若版本不满足要求，前往官网下载安装：

+ Node.js 官网（中文）：[https://nodejs.org/zh-cn/download/](https://nodejs.org/zh-cn/download/)

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304112-f3b99cbd-5741-469e-9e89-5cac4afed417.png)

下载安装包，安装即可。（若是更新 Node 需要先将原版本删除后再安装）

---

## 二、创建令牌（三版本通用）
> 此步骤为终端版、桌面版、VSCode 插件版 **共用**，只需操作一次。
>

### 1. 进入模型广场
打开向量引擎官方网站：[https://api.vectorengine.ai](https://api.vectorengine.ai)

进入 **模型广场**，选择需要使用的模型并查看对应分组。

**分组说明**：不同分组对应不同渠道和成本，分组倍率跟价格挂钩，价格越高的分组并发和稳定性越好。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781254761038-4f878e26-60a0-481c-a032-8696d50a038e.png)

### 2. 创建 API 令牌
打开 **控制台** -> **API 令牌** -> **添加令牌**，建议手动选择分组，比较稳定。

推荐分组（按优先级排序，令牌会优先使用前面的分组）：

| 优先级 | 分组名称 |
| --- | --- |
| 1 | default |
| 2 | 官转克劳德1 |
| 3 | claude code专属 |
| 4 | 官转克劳德2 |


选择后保存，**复制生成的密钥**，后面配置 ccswitch 时需要用到。![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781254793363-4a83e00f-da8a-49ff-8df5-66ee16101965.png)

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781254827459-73191be3-3a40-4f6d-a95f-1069e2739b91.png)

---

## 三、安装与配置 ccswitch
> **重要**：ccswitch 中 Claude Code 有 **两个配置入口**：
>
> + **终端版 + VSCode 插件版** → 对应 ccswitch 中的一个配置口（3A）
> + **桌面版** → 对应 ccswitch 中的另一个配置口（3B）
>
> 请根据你需要使用的版本，选择对应的配置进行操作。如果多个版本都要用，则两个都需要配置。
>

### 0. 下载安装 ccswitch
ccswitch 下载地址：[https://github.com/farion1231/cc-switch/releases](https://github.com/farion1231/cc-switch/releases)

进入页面往下拉，选择对应系统的安装包下载并安装。

> 备选：若 GitHub 打不开，使用夸克网盘下载：<[https://pan.quark.cn/s/d6152047213b](https://pan.quark.cn/s/d6152047213b)
>

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304391-dc936aba-c02f-497f-80f7-7cd4fef0f79c.png)

---

### 3A：终端版 + VSCode 插件版的 ccswitch 配置
> 此配置适用于 **终端版（CLI）** 和 **VSCode 插件版**，两者共享同一个 ccswitch 配置口。
>

#### 3A-1. 添加配置
打开 ccswitch，找到 **终端版/VSCode 插件版** 对应的 Claude Code 配置入口图标，点击右上角 **+** 号添加配置。![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255032208-5fea4ac2-13c2-4bc2-ae90-cba8c2fe324c.png)

进入配置页面，选择 **自定义配置**。![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255053809-244088e4-db3c-4fa3-8f58-07ce6fe3e5bc.png)

填写配置信息：

| 配置项 | 填写内容 |
| --- | --- |
| API Key | 第二步创建的令牌密钥（复制粘贴） |
| API 请求地址 | `https://api.vectorengine.ai`  (claude模型)或者 `https://api.vectorengine.ai/v1` （其他模型） |


![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255086691-2c23e925-66f9-45f0-9208-fd1d0a4611c6.png)

#### 3A-2. 配置模型
 点击 **获取模型列表**，选择令牌配置时对应的模型，点击 **保存并启用**。

| API 格式选项 | 原生支持 | 需额外路由 | 说明与适用场景 |
| --- | --- | --- | --- |
| **Anthropic Messages (原生)** | ✅ 是 | ❌ 否 | 直接使用 Anthropic 原生 Messages API 协议，适配 Claude 系列模型。 |
| **OpenAI Chat Completions (需开启路由)** | ❌ 否 | ✅ 是 | 使用 OpenAI `/v1/chat/completions` 协议来对接模型，需要中间层路由 / 转发服务做格式转换。适合gpt模型，和国产模型 |
| **OpenAI Responses API (需开启路由)** | ❌ 否 | ✅ 是 | 使用 OpenAI 新的 Responses API 协议，同样需要路由层做格式转换。 |
| **Gemini Native generateContent (需开启路由)** | ❌ 否 | ✅ 是 | 使用 Gemini 原生 `generateContent` 协议，需要路由 / 转发服务适配。适合 Gemini 模型 |


![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255118138-3cb9c48c-2ffa-460c-9b63-318cae0e5012.png)

#### 3A-3. 开启路由
 ⚠️  **claude模型及选的Anthropic Messages (原生)api格式不用开路由**

打开 **设置** -> 开启终端版/VSCode 插件版对应的 **Claude Code 路由**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255158314-62c76f99-870e-434d-9712-8336ab94eec4.png)

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255172147-f9ed4337-c9cd-488f-82e9-c60377a40669.png)

> 至此，终端版和 VSCode 插件版的 ccswitch 配置完成！
>

---

### 3B：桌面版的 ccswitch 配置
> 此配置适用于 **Claude Code 桌面版**，与终端版/VSCode 插件版是不同的配置入口。
>

#### 3B-1. 添加配置
打开 ccswitch，找到 **桌面版** 对应的 Claude Code 配置入口图标，点击右上角 **+** 号添加配置。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255223004-448296aa-8317-4dfd-a444-47074d039bc6.png)



进入配置页面，选择 **自定义配置**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255238817-d0e7d9c0-c7e1-4204-a630-e7c8bad07271.png)



填写配置信息：

| 配置项 | 填写内容 |
| --- | --- |
| API Key | 第二步创建的令牌密钥（复制粘贴） |
| API 请求地址 | `https://api.vectorengine.ai/v1` |


![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255255413-bb380ce8-fa28-47f7-8b29-1a4bcbe01086.png)

#### 3B-2. 配置模型映射
打开 **需要本地路由映射** -> 点击 **添加模型** -> 点击 **获取模型列表**，选择令牌配置时对应的模型，点击 **保存并启用**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255276295-89745e34-846d-42b3-9a06-f02827af3532.png)

#### 3B-3. 开启路由
打开 **设置** -> 开启桌面版对应的 **Claude Code 路由**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255288182-0a5fbdd3-8a3d-4398-82ff-818a2675fc0e.png)

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255299324-1e027900-7df9-4aa4-b27b-8685b3fdb3f3.png)

> 至此，桌面版的 ccswitch 配置完成！
>

---

## 四、安装 Claude Code
> 以下三种方式**任选其一或多选**，对应的 ccswitch 配置完成后即可使用。
>

### 方式 A：终端版（CLI）
适合喜欢命令行操作的用户，轻量快速，功能最全。

> **前提**：已完成 [3A 终端版/VSCode 插件版的 ccswitch 配置](#ccswitch-3a)。
>

#### A-1. 安装
打开终端，运行：

```bash
npm install -g @anthropic-ai/claude-code
```

> 如果安装速度慢，可以使用国内镜像源：
>

```bash
npm install -g @anthropic-ai/claude-code --registry=https://registry.npmmirror.com
```

#### A-2. 验证安装
```bash
claude --version
```

出现版本号即安装成功。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255320075-46abd623-f6d6-4dbb-9d87-1b331b318727.png)

#### A-3. 启动使用
在终端中进入你想要操作的项目目录，然后输入 `claude` 回车启动：

```bash
cd 你的项目路径
claude
```

启动后即可在聊天框中输入内容进行对话，Claude Code 会自动读取当前目录的项目文件作为上下文。

#### A-4. 常用命令
| 命令 | 说明 |
| --- | --- |
| `claude` | 启动交互式对话 |
| `claude "你的问题"` | 直接提问，无需进入交互模式 |
| `claude -p "问题"` | 单次提问（print 模式，不进入交互） |
| `claude config` | 打开配置界面 |
| `claude update` | 更新到最新版本 |
| `/help` | 在交互模式中查看帮助 |
| `/model` | 切换模型 |
| `/clear` | 清空对话历史 |
| `Esc` 两次 | 退出 Claude Code |


---

### 方式 B：桌面版
独立桌面应用，图形界面操作，适合不熟悉命令行的用户。

> **前提**：已完成 [3B 桌面版的 ccswitch 配置](#ccswitch-3b)。
>

#### B-1. 下载安装
前往官方下载页：<>（需要魔法）

选择对应系统版本下载安装。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255336112-5f078619-e96a-48e0-900b-e82a6ae744c9.png)

#### B-2. 登录配置
安装完成后打开 Claude Code 桌面版，需要跳过登录。

**桌面端配置（免登录）：**

1. **不点登录**，直接关闭登录弹窗![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20260611180706121.png)
2. 顶部菜单栏：`Help → Troubleshooting → Enable Developer Mode`，确认开启、重启软件
3. 重启后菜单栏出现 `Developer → Configure Third-Party Inference`
4. 填入 **Claude 中转 API 地址（**[https://api.vectorengine.ai）](https://api.vectorengine.ai）)** + API Key(令牌秘钥)**，点击 **apply changes**，彻底跳过账号登录直接聊天

> **注意**：确保 ccswitch 的桌面版 Claude Code 路由已开启（第 3B 步已完成），桌面版才能正常通过 ccswitch 转发请求。
>

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255360944-81b07803-cbd1-4a58-b50e-6238ef4619d3.png)

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255382918-633d35cd-d4d2-4d6c-bf88-3ed03c799ef5.png)

#### B-3. 选择项目目录
登录后选择一个本地项目文件夹，Claude Code 会以该目录为工作区进行代码操作。

#### B-4. 开始使用
在对话框中输入任务描述，Claude Code 即可帮你编写、修改代码。桌面版支持：

+ 图形化界面，操作直观
+ 文件浏览与编辑预览
+ 自动读取项目文件作为上下文

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255409762-0fb15220-ed52-4279-91f3-5a5c6ba7b4f6.png)

---

### 方式 C：VSCode 插件版
直接在编辑器内使用，与代码编辑无缝衔接，适合日常开发。

> **前提**：已完成 [3A 终端版/VSCode 插件版的 ccswitch 配置](#ccswitch-3a)。
>

#### C-1. 安装插件
打开 VSCode -> 侧边栏 **扩展**（快捷键 `Ctrl+Shift+X`）-> 搜索 **"Claude Code"** -> 找到 **Claude Code**（发布者为 Anthropic）-> 点击 **安装**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255421219-ad51564b-c98c-4df9-8a48-ba27db3df0ef.png)

> Cursor、Windsurf 等 VSCode 兼容编辑器也可使用同一插件。
>

#### C-2. 打开 Claude Code 面板
安装完成后，VSCode 侧边栏会出现 Claude Code 图标，点击打开即可。

首次打开时，插件会自动检测 Node.js 环境和 Claude Code CLI。如果尚未安装 CLI，插件会提示你安装。

#### C-3. 使用插件
在 Claude Code 面板的聊天框中输入问题即可开始使用。插件功能包括：

+ 支持选中代码后直接让 Claude 分析或修改
+ 自动读取当前工作区文件作为上下文
+ 支持内联代码编辑和 Diff 预览
+ 可以直接执行终端命令
+ 上下文感知当前打开的文件，提示更精准

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781255439299-97df2c6a-4d83-4918-a32d-5819ce49eb93.png)

> 如果安装后看不到 Claude Code 图标，请重启 VSCode。
>

---

## 五、验证与测试
无论使用哪个版本，完成安装后发送一条测试消息，收到正常回复即表示配置成功。

排查思路（如无法正常使用）：

1. 检查 ccswitch 是否已启动且对应版本的路由为开启状态
2. 检查令牌是否有效、余额是否充足
3. 检查模型映射是否已正确配置
4. 终端版 / VSCode 插件版：确认 Node.js 版本 >= 18.x
5. 桌面版：确认使用的是桌面版对应的 ccswitch 配置口
6. 插件版：尝试重启 VSCode

---

## 六、常见问题与注意事项
| 问题 | 说明 |
| --- | --- |
| 安装 Claude Code 时报错 | 确保 Node.js >= 18.x，并且网络可以访问 npm 仓库。可尝试使用国内镜像源安装。 |
| ccswitch 中两个配置口有什么区别？ | 桌面版走独立的配置口，终端版和 VSCode 插件版共享另一个配置口。使用哪个版本就配置哪个，都要用就两个都配。 |
| ccswitch 路由开启后仍无法连接 | 检查 API 请求地址是否正确填写为 `https://api.vectorengine.ai/v1`，以及模型映射是否已保存启用。确认你开启的路由和使用的版本对应。 |
| 备用请求地址 | `https://api.vectorengine.ai` 或 `https://api.vectorengine.cn` |
| 三个版本能同时使用吗？ | 可以。但需要在 ccswitch 中分别配置对应的配置口（终端版+VSCode 插件版配一个，桌面版配一个）。 |
| ccswitch 配置修改后需要重启吗？ | 修改模型或配置后，建议重启对应的客户端以确保生效。 |
| VSCode 插件找不到 | 确保 VSCode 版本较新（建议 1.80+），安装后需重启 VSCode。 |
| Claude Code 终端版如何更新 | 运行 `claude update` 或 `npm update -g @anthropic-ai/claude-code` |
| 使用时提示模型不可用 | 检查 ccswitch 中的模型映射是否包含你需要使用的模型，以及令牌分组是否有对应模型的权限。 |


---

> **总结**：只需完成 **创建令牌 -> 配置 ccswitch（按版本选配置口）** 两个步骤，然后根据个人喜好安装终端版 / 桌面版 / VSCode 插件版即可开始使用。
>

