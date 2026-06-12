# CODEX 全版本配置教程（终端 + 桌面版 + VSCode 插件版）
> 本教程涵盖 Codex 的三种使用方式。**令牌配置**和 **ccswitch 配置**为公共步骤，三个版本通用，只需配置一次。
>

---

## 目录
+ 一、环境准备
+ 二、创建令牌（三版本通用）
+ 三、安装与配置 ccswitch（三版本通用）
+ 四、安装 Codex
    - 方式 A：终端版
    - 方式 B：桌面版
    - 方式 C：VSCode 插件版
+ 五、验证与测试
+ 六、常见问题与注意事项

---

## 一、环境准备
⚠️ **说明**：终端版和 VSCode 插件版需要 Node.js 环境；桌面版为独立应用，不依赖 Node.js，可跳过此步。

### 1. 检查 Node.js 环境
**Node.js ≥ 22.x**（npm ≥ 10.x）

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

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304194-13f807e7-e53a-485f-91f1-f770e41d07d4.png)

### 2. 创建 API 令牌
打开 **控制台** → **API 令牌** → **添加令牌**，建议手动选择分组，比较稳定。

推荐分组（按优先级排序，令牌会优先使用前面的分组）：

| 优先级 | 分组名称 |
| --- | --- |
| 1 | codex 专属 |
| 2 | default |
| 3 | 官转 |
| 4 | 官转 openai |


选择后保存，**复制生成的密钥**，后面配置 ccswitch 时需要用到。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304300-fc08de73-38b7-4433-9731-3c3f33928bdb.png)

---

## 三、安装与配置 ccswitch（三版本通用）
> 此步骤为终端版、桌面版、VSCode 插件版 **共用**，只需操作一次。
>

### 1. 下载安装 ccswitch
ccswitch v3.16 下载地址：[https://github.com/farion1231/cc-switch/releases/tag/v3.16.1](https://github.com/farion1231/cc-switch/releases/tag/v3.16.1)

进入页面往下拉，选择对应系统的安装包下载并安装。

> 备选：若 GitHub 打不开，使用夸克网盘下载：[https://pan.quark.cn/s/d6152047213b](https://pan.quark.cn/s/d6152047213b)（选择 3.16 版本）
>

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304391-dc936aba-c02f-497f-80f7-7cd4fef0f79c.png)

### 2. 添加配置
打开 ccswitch，选择 **Codex 图标**，点击右上角 **＋** 号添加配置。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304469-7f791e92-b34c-4fc6-8be2-5ccb257c7ed2.png)

进入配置页面，选择 **自定义配置**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304616-ec5caa4d-a5e9-496f-87a5-d5a444797d21.png)

填写配置信息：

| 配置项 | 填写内容 |
| --- | --- |
| API Key | 第二步创建的令牌密钥（复制粘贴） |
| API 请求地址 | `https://api.vectorengine.ai/v1` |


![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304729-4e95a508-930a-4be5-a0c0-cfa7a22ff0b9.png)

### 3. 配置模型映射
打开 **需要本地路由映射** → 点击 **添加模型** → 点击 **获取模型列表**，选择令牌配置时对应的模型，点击 **保存并启用**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304798-643880e0-298c-4319-96e3-75f1ebfbfe67.png)

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145304902-959d9b24-ac32-4e0d-a545-fe98f4f2cd93.png)

### 4. 开启路由
打开 **设置** → 开启 **Codex 路由**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145305106-2967c9ef-e848-49ea-8883-93feaa466c72.png)

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145305195-eae91888-d50c-4b85-a0d2-64eb3633794e.png)

> ✅ 至此，公共配置完成！下面根据你需要的版本，选择对应安装方式即可。
>

---

## 四、安装 Codex
> 以下三种方式**任选其一或多选**，ccswitch 配置完成后均可直接使用。
>

### 方式 A：终端版
适合喜欢命令行操作的用户，轻量快速。

#### A-1. 安装
打开终端，运行：

```bash
npm install -g @openai/codex
```

#### A-2. 验证安装
```bash
codex --version
```

出现版本号即安装成功。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145305290-be47c558-d9fc-4477-ba72-35d4f4fc5cef.png)

#### A-3. 启动使用
终端输入 `codex` 回车启动，在聊天框输入内容即可对话。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145305382-25e872aa-9ff1-423e-8bfa-84086a4c0770.png)

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145305486-c89b7f72-b390-4f8e-b874-429af8a87c9e.png)

---

### 方式 B：桌面版
独立桌面应用，支持多线程并行开发、Git worktree 管理，功能最全面。

#### B-1. 下载安装
前往官方下载页：[https://developers.openai.com/codex/app](https://developers.openai.com/codex/app)（需要魔法）

选择 **Windows** 版本下载安装。也可从 [Microsoft Store](https://apps.microsoft.com/detail/9plm9xgg6vks) 获取。

#### B-2. 登录配置
安装完成后打开 Codex 桌面版，登录方式选择 **使用 API Key 登录**（填写   **令牌秘钥 **）。

> ⚠️ **注意**：确保 ccswitch 的 Codex 路由已开启（第三步已完成），桌面版才能正常通过 ccswitch 转发请求。
>

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781256581979-56ff051e-4670-41dc-b2d1-b8541432e90e.png)

#### B-3. 选择项目目录
登录后选择一个本地项目文件夹，Codex 会以该目录为工作区进行代码操作。

#### B-4. 开始使用
在对话框中输入任务描述，Codex 即可帮你编写、修改代码。桌面版支持：

+ 多线程并行处理
+ Git worktree 隔离
+ 文件浏览与编辑预览

---

### 方式 C：VSCode 插件版
直接在编辑器内使用，与代码编辑无缝衔接，适合日常开发。

#### C-1. 安装插件
打开 VSCode → 侧边栏 **扩展**（快捷键 `Ctrl+Shift+X`）→ 搜索 **"Codex"** → 找到 **Codex — OpenAI's coding agent**（发布者为 OpenAI）→ 点击 **安装**。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1781145964637-39bc22b5-3a02-46e3-a777-f4717ed7189a.png)

> 💡 Cursor、Windsurf 等 VSCode 兼容编辑器也可使用同一插件。
>

#### C-2. 登录配置
安装后插件会若提示登录，选择 **使用 API Key 登录**（与桌面版相同，复制令牌密钥即可）。

> ⚠️ **注意**：确保 ccswitch 的 Codex 路由已开启（第三步已完成）。
>

#### C-3. 使用插件
安装完成后，VSCode 右侧边栏会出现 Codex 图标，点击打开即可使用。

+ 支持选中代码后直接让 Codex 分析或修改
+ 默认为 Agent 模式，可自动读写文件、运行命令
+ 上下文感知当前打开的文件，提示更精准

> 如果安装后看不到 Codex 图标，请重启 VSCode。
>

---

## 五、验证与测试
无论使用哪个版本，完成安装后发送一条测试消息，收到正常回复即表示配置成功。

排查思路（如无法正常使用）：

1. ✅ 检查 ccswitch 是否已启动且路由为开启状态
2. ✅ 检查令牌是否有效、余额是否充足
3. ✅ 检查模型映射是否已正确配置
4. ✅ 终端版：确认 Node.js 版本 ≥ 22.x
5. ✅ 桌面版 / 插件版：尝试重启应用或 VSCode

---

## 六、常见问题与注意事项
| 问题 | 说明 |
| --- | --- |
| 使用 GPT 模型时不需要路由？ | 使用 GPT 模型时，可以不开「需要本地路由映射」开关，此时不需打开路由也能使用 Codex，但输入 `/model` 切换模型时，仅能选择官方固定的 Codex 配置模型。 |
| 备用请求地址 | `https://api.vectorengine.ai` 或 `https://api.vectorengine.cn` |
| 三个版本能同时使用吗？ | 可以。终端版、桌面版、VSCode 插件版共享同一份 ccswitch 配置，互不冲突。 |
| ccswitch 配置修改后需要重启吗？ | 修改模型或供应商后，建议重启对应的 Codex 客户端以确保生效。 |


---

> 📌 **总结**：只需完成 **创建令牌 → 配置 ccswitch** 两个公共步骤，然后根据个人喜好安装终端版 / 桌面版 / VSCode 插件版即可开始使用。
>

