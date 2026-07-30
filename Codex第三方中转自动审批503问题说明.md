# Codex 第三方中转自动审批 503 问题说明

## 1. 问题概述

当 Codex 使用 OpenAI 官方服务时，自动审批功能可能向服务端发送如下模型标识：

```text
codex-auto-review
```

它是 Codex 自动审批流程使用的内部模型或路由标识，不是用户通常选择的公开主模型。

使用第三方中转 API 时，中转服务可能不认识这个内部标识，而是把它当作普通公开模型名称继续向上游请求。由于上游没有名为 `codex-auto-review` 的可用模型或渠道，请求会失败。

常见错误如下：

```text
Automatic approval review failed:
unexpected status 503 Service Unavailable
模型 codex-auto-review 无可用渠道（distributor）
```

这类错误与本地文件权限、沙箱权限或主模型本身的代码能力无关。即使 `gpt-5.6-sol` 等主模型可以正常使用，自动审批仍可能失败，因为主任务和审批任务使用了不同的模型标识。

## 2. 调用过程

### 2.1 官方服务

```text
Codex 发起需要审批的操作
-> Codex 发送 model=codex-auto-review
-> OpenAI 服务识别内部路由
-> 服务端选择实际审批模型和审批策略
-> 返回允许或拒绝的审批结论
```

官方服务最终使用的基础模型不一定等于当前主模型。实际模型由服务端根据版本、安全策略、成本和延迟等因素决定，客户端通常不可见。

### 2.2 不兼容的第三方中转

```text
Codex 发起需要审批的操作
-> Codex 发送 model=codex-auto-review
-> 中转将其当成普通模型名
-> 中转或上游找不到对应渠道
-> 返回 503 Service Unavailable
```

因此，普通对话和编码请求可能一直正常，只有触发自动审批时才出现 503，看起来像“有时可以、有时不行”。

## 3. 如何确认是这个问题

同时满足以下特征时，基本可以确认：

1. 当前主模型可以正常对话、编程和调用普通工具。
2. 只有需要 `require_escalated` 的命令或自动审批操作失败。
3. 错误正文包含 `codex-auto-review`、`无可用渠道` 或类似说明。
4. 第三方中转日志中的请求 JSON 包含：

```json
{
  "model": "codex-auto-review"
}
```

如果失败日志中没有这个模型字段，则 503 可能来自中转限流、额度不足、上游节点异常或其他路由问题，应继续检查中转日志。

## 4. 解决方案

### 4.1 推荐顺序

按稳定性和安全隔离程度排序：

1. 让第三方中转原生支持 `codex-auto-review`，并将它正确映射到兼容的审批模型。
2. 自动审批请求使用 OpenAI 官方服务，普通主任务继续使用中转。
3. 在 Codex 客户端覆盖自动审批模型，使其直接使用中转已经支持的当前主模型。
4. 关闭自动审批，改为由用户手动批准需要提升权限的操作。

### 4.2 客户端覆盖方案

已验证的客户端方案是修改当前主模型的模型元数据：

```json
"auto_review_model_override": "gpt-5.6-sol"
```

这表示当主模型为 `gpt-5.6-sol` 时，自动审批也直接请求 `gpt-5.6-sol`，不再向中转发送 `codex-auto-review`。

修复后的调用过程为：

```text
主任务：model=gpt-5.6-sol
审批任务：model=gpt-5.6-sol
```

主模型不是 `gpt-5.6-sol` 时，应把覆盖值改为用户当前实际可用的主模型，不要照抄固定模型名。

## 5. 配置实施原则

Codex 的普通 `config.toml` 没有通用的顶层模型别名字段。不要随意添加以下未经支持的配置：

```toml
model_aliases = {}
auto_review_model = "gpt-5.6-sol"
```

正确做法是：

1. 读取 `~/.codex/config.toml`，确定当前 `model` 和 `model_provider`。
2. 使用 `codex debug models --bundled` 获取当前 Codex 版本的完整模型目录。
3. 保留完整模型条目，在当前主模型条目中设置 `auto_review_model_override`。
4. 将结果保存为单独的模型目录文件，例如：

```text
~/.codex/model-catalog-overrides.json
```

5. 在 `~/.codex/config.toml` 中添加：

```toml
model_catalog_json = "/absolute/path/to/model-catalog-overrides.json"
```

Windows 示例：

```toml
model_catalog_json = "C:\\Users\\用户名\\.codex\\model-catalog-overrides.json"
```

6. 运行 `codex debug models`，确认当前主模型的有效元数据包含正确的 `auto_review_model_override`。
7. 重启 Codex 桌面应用或新建任务，使模型目录重新加载。

不要只创建一个字段不完整的最小模型条目。不同 Codex 版本会要求 `display_name`、`supported_reasoning_levels`、`shell_type` 等完整字段，最可靠的方法是基于当前版本的完整内置目录生成覆盖文件。

## 6. 验证方法

不要仅凭配置文件存在就判断修复成功，应执行一次无副作用的真实审批测试。

测试条件：

```text
approval_policy = on-request
approvals_reviewer = auto_review
sandbox = read-only
```

测试命令：

```powershell
Write-Output 'auto-review-ok'
```

测试时必须明确使用：

```text
sandbox_permissions = require_escalated
```

成功标准：

1. 请求确实进入自动审批流程。
2. 自动审批没有返回 `codex-auto-review` 503。
3. 命令退出码为 `0`。
4. 命令输出为 `auto-review-ok`。
5. 测试过程中没有创建、修改或删除文件。

## 7. 可直接发给 Codex 的修复提示词

将下面整段发送给出现问题的 Codex：

```text
请修复自定义/中转 API 下自动审批请求 `codex-auto-review` 返回 503 的问题。

要求：
1. 读取 `~/.codex/config.toml`，确定当前 `model` 和 `model_provider`，不要修改 API 地址、密钥或主模型。
2. 检查当前 Codex 是否支持模型元数据字段 `auto_review_model_override`，不要修改或补丁 Codex 可执行文件。
3. 修改任何配置前先创建带时间戳的备份。不要输出或泄露 API 密钥、访问令牌或完整认证配置。
4. 保留现有模型目录；如果没有自定义模型目录，以 `codex debug models --bundled` 的完整结果为基础生成 `~/.codex/model-catalog-overrides.json`。
5. 在当前主模型对应的模型条目中，将 `auto_review_model_override` 设置为当前主模型自身。例如当前模型是 `gpt-5.6-sol`，则设置：
   `"auto_review_model_override": "gpt-5.6-sol"`
6. 在 `~/.codex/config.toml` 中设置 `model_catalog_json` 指向该文件。正确处理 Windows 和 Unix 路径，不要覆盖其他配置。
7. 使用 `codex debug models` 验证当前主模型的 `auto_review_model_override` 已生效，并确认其他模型条目仍然保留。
8. 做一次无副作用的真实测试：使用 `approval_policy=on-request`、`approvals_reviewer=auto_review`、只读沙箱，明确以 `require_escalated` 请求运行 `Write-Output 'auto-review-ok'`。不要创建、修改或删除测试文件。
9. 确认测试获得自动审批、退出码为 0、输出为 `auto-review-ok`，并且不再出现 `codex-auto-review` 的 503。
10. 最后报告修改的文件、有效映射和测试结果，并提醒我重启 Codex 或新建任务。

如果当前 Codex 版本不支持 `auto_review_model_override`，不要猜测配置字段，也不要修改可执行文件。请停止修改，恢复备份，并说明应改为在中转端配置模型映射，或关闭自动审批后使用手动批准。
```

## 8. 风险与限制

### 8.1 审批隔离减弱

官方默认设计使用独立的审批路由。将 `auto_review_model_override` 指向当前主模型后，主任务和审批任务可能由同一个模型执行。虽然审批流程仍使用独立提示词和策略，但模型层面的职责隔离弱于官方默认路由。

在高风险、生产环境或处理敏感数据的场景中，优先让中转正确支持独立审批模型，或者改用人工审批。

### 8.2 模型切换

覆盖配置通常绑定某个主模型条目。用户切换到其他模型后，新模型可能仍使用默认的 `codex-auto-review`，从而再次出现 503。每个需要使用的主模型都应单独检查和配置。

### 8.3 Codex 升级

自定义模型目录基于生成时的 Codex 内置模型元数据。Codex 升级后，模型字段、上下文窗口、能力声明或内置模型列表可能变化，应重新执行以下流程：

```text
重新导出内置模型目录
-> 重新加入 auto_review_model_override
-> 验证完整模型列表
-> 重新执行无副作用审批测试
```

### 8.4 中转稳定性

即使映射正确，中转仍可能因额度、并发限制、上游账号失效或节点故障返回 503。修复后若再次失败，应检查失败请求中的实际 `model` 字段：

- 如果仍是 `codex-auto-review`，说明覆盖未加载或当前主模型没有配置覆盖。
- 如果已经是当前主模型，说明问题转为中转渠道可用性故障，不再是内部审批路由兼容问题。

## 9. 结论

该问题的本质不是“主模型没有审批能力”，而是第三方中转不认识 Codex 的内部审批模型标识。客户端覆盖方案通过让审批请求直接使用中转已支持的主模型解决兼容问题；长期更稳妥的方案仍是让中转服务正确实现 `codex-auto-review` 的独立路由，或使用官方服务完成审批。
