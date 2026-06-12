## 1.下载与安装
### 1-1openclaw安装
<font style="color:rgb(52, 64, 84);">首先确保你已经安装了 Node.js 环境，然后在终端执行：</font>

```plain
npm i -g openclaw
```

初始化openclaw

```plain
openclaw onboard
```

### 1-2.ccswitch下载
ccswitch下载链接：[https://github.com/farion1231/cc-switch/releases/tag/v3.15.0](https://github.com/farion1231/cc-switch/releases/tag/v3.15.0)  

页面拉取到最下面，选择Windows版本安装包，下载安装即可。

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1779771152448-2c77912a-4345-4752-adc0-8bade3d6e075.png)

## 2.配置ccswitch
### 2-1.打开ccswitch，选择小龙虾图标新建配置
![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1779773308151-9d0d0ba8-9e34-4a48-b885-27e5010cd87f.png)

### 2-2.选择自定义配置
![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1779773353202-5f2d6f6c-3df6-4465-be91-a4b1e05bc091.png)

### 2-3.填写配置
![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1779773761470-ab61d7eb-2507-4a4b-9527-36f43fd8465c.png)

官网链接：https://api.vectorengine.ai

api协议：一般默认<font style="color:#DF2A3F;">OpenAI Completions 格式</font>  对应  api端点：https://api.vectorengine.ai/v1

claude模型可选 Anthropic Messages格式 对应 api端点为：https://api.vectorengine.ai

### 2-4.获取模型
![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1779774153596-ef296ff5-827a-43bd-8d16-b09d7108a93e.png)

填写apikey 后添加模型，并获取模型列表，若成功获取列表说明前面填写正确。

建议一个配置使用一个模型，（因为不同模型一般分组不同）

### 2-5. 测试并添加
![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1779776520911-dec2cd8d-7d38-4cbf-b723-34a2c3f5423c.png)

## 3.测试与使用
### 3-1.打开终端，输入下面命令，开启openclaw网关
```plain
 openclaw gateway  
```

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1779775190983-1c6cdb75-67bf-4d3d-a277-d00652f9963d.png)

### 3-2.重新开一个终端（开启网关终端不关），输入下面命令进入openclaw自带可视化网页端。
```plain
 openclaw dashboard  
```

![](https://cdn.nlark.com/yuque/0/2026/png/68353871/1779775376290-474a2a2e-9f3b-4617-aee8-532354985b17.png)

下拉框选择刚刚配置的模型，对话测试，回应及成功。

