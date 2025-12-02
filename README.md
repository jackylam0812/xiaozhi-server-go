# ✨ 小智 AI 聊天机器人后端服务（商业版）

小智 AI 是一个语音交互机器人，结合 Qwen、DeepSeek 等强大大模型，通过 MCP 协议连接多端设备（ESP32、Android、Python 等），实现高效自然的人机对话。

本项目是其后端服务，旨在提供一套 **商业级部署方案** —— 高并发、低成本、功能完整、开箱即用。

<p align="center">
  <img src="https://github.com/user-attachments/assets/aa1e2f26-92d3-4d16-a74a-68232f34cca3" alt="Xiaozhi Architecture" width="600">
</p>

项目初始基于 [虾哥的 ESP32 开源项目](https://github.com/78/xiaozhi-esp32?tab=readme-ov-file)，目前已形成完整生态，支持多种客户端协议兼容接入。

---

## ✨ 核心优势

| 优势         | 说明                                                   |
| ---------- | ---------------------------------------------------- |
| 🚀 高并发     | 单机支持 3000+ 在线，分布式可扩展至百万用户                            |
| 👥 用户系统    | 完整的用户注册、登录、权限管理能力                                    |
| 💰 支付集成    | 接入支付系统，助力商业闭环                                        |
| 🛠️ 模型接入灵活 | 支持通过 API 调用多种大模型，简化部署，支持定制本地部署                       |
| 📈 商业支持    | 提供 7×24 技术支持与运维保障                                    |
| 🧠 模型兼容    | 支持 ASR（豆包）、TTS（EdgeTTS）、LLM（OpenAI、Ollama）、图文解说（智谱）等 |

---

## ✅ 社区版功能清单

* [x] 支持 websocket 连接
* [x] 支持 PCM / Opus 格式语音对话
* [x] 支持大模型：ASR（豆包流式）、TTS（EdgeTTS/豆包）、LLM（OpenAI API、Ollama）
* [x] 支持语音控制调用摄像头识别图像（智谱 API）
* [x] 支持 auto/manual/realtime 三种对话模式，支持对话实时打断
* [x] 支持 ESP32 小智客户端、Python 客户端、Android 客户端连入，无需校验
* [x] OTA 固件下发
* [x] 支持 MCP 协议（客户端 / 本地 / 服务器），可接入高德地图、天气查询等
* [x] 支持语音控制切换角色声音
* [x] 支持语音控制切换预设角色
* [x] 支持语音控制播放音乐
* [x] 支持单机部署服务
* [x] 支持本地数据库 sqlite
* [x] 支持coze工作流 
* [x] 支持Docker部署
## ✅商务版功能清单
* [x] 社区版所有功能
* [x] 开发团队技术支持
* [x] 后续核心功能免费更新
* [x] 商务版管理后台，更多的功能选项
* [x] 支持多用户管理
* [x] 自定义修改欢迎界面
* [x] 自定义修改版权logo，使用自己公司的商务标识
* [x] 自定义修改Agent角色模板
* [x] 支持更多的模型
* [x] 支持 websocket 和 MQTT+UDP 两种通信协议
* [x] 支持 tts 流式生成及发送
* [x] 支持声音克隆
* [x] 支持知识库
* [x] 支持定制音色（cosyvoice2, indextts）
* [x] 支持通过 OTA 升级固件
* [x] 支持 Coze 工作流
* [x] 支持 Dify 工作流
* [x] 深度优化响应速度
* [x] 支持用户身份验证，激活绑定设备
* [x] 支持设备管理：解绑/禁用
* [x] 支持后台解绑设备
* [x] 支持用户自定义 Agent
* [x] 国际化多语言支持：中文、英语、日语、西班牙语、印尼语等
* [x] 支持MCP接入点
* [x] 支持网络数据库
* [x] 支持分布式部署
* [x] 支持本地部署大模型

商务版测试/体验地址：

https://xiaozhi.xf.bj.cn/login

---

## 🚀 快速开始

### 1. 下载 Release 版

> 推荐直接下载 Release 版本，无需配置开发环境：

👉 [点击前往 Releases 页面](https://github.com/AnimeAIChat/xiaozhi-server-go/releases)

* 选择你平台对应的版本（如 Windows: `windows-amd64-server.exe`）
* `.upx.exe` 是压缩版本，功能一致，体积更小，适合远程部署

---


### 2. 配置 `.config.yaml`

* 推荐复制一份 `config.yaml` 改名为 `.config.yaml`
* 按需求配置模型、WebSocket、OTA 地址等字段
* 不建议自行删减字段结构

#### WebSocket 地址配置（必配）

```yaml
web:
  websocket: ws://your-server-ip:8000
```

用于 OTA 服务下发给客户端的连接地址，ESP32 客户端会自动从此地址连接 WS，不再手动配置。

注：如果是局域网调试，your-server-ip要配置为**电脑在局域网中的IP**，且终端设备和电脑在同一网段，设备才能通过这个IP地址连到电脑上的服务。

#### OTA 地址配置（必配）

```text
http://your-server-ip:8080/api/ota/
```

> ESP32 固件内置 OTA 地址，确保该服务地址可用，**服务运行后可以在浏览器中输出此地址，确认服务可以访问**。

ESP32设备可以在联网界面修改OTA地址，从而在不重新刷固件的情况下，切换后端服务。

#### 配置ASR，LLM，TTS

根据配置文件的格式，配置好相关模型服务，尽量不要增减字段

---

## 💬 MCP 协议配置

参考：`src/core/mcp/README.md`

---

## 🧪 源码安装与运行

### 前置条件

* Go 1.24.2+
* Windows 用户需安装 CGO 和 Opus 库（见下文）

```bash
git clone https://github.com/AnimeAIChat/xiaozhi-server-go.git
cd xiaozhi-server-go
cp config.yaml .config.yaml
```

---

### Windows 安装 Opus 编译环境

安装 [MSYS2](https://www.msys2.org/)，打开MYSY2 MINGW64控制台，然后输入以下命令：

```bash
pacman -Syu
pacman -S mingw-w64-x86_64-gcc mingw-w64-x86_64-go mingw-w64-x86_64-opus
pacman -S mingw-w64-x86_64-pkg-config
```

设置环境变量（用于 PowerShell 或系统变量）：

```bash
set PKG_CONFIG_PATH=C:\msys64\mingw64\lib\pkgconfig
set CGO_ENABLED=1
```

尽量在MINGW64环境下运行一次 “go run ./src/main.go” 命令，确保服务正常运行

GO mod如果更新较慢，可以考虑设置go代理，切换国内镜像源。

---

### 运行项目

```bash
go mod tidy
go run ./src/main.go
```

### 编译发布版本

```bash
go build -o xiaozhi-server.exe src/main.go
```

### 测试
* 推荐使用ESP32硬件设备测试，可以最大程度避免兼容问题
* 推荐使用玄凤小智Android客户端，在设置界面增加本地服务的ota地址即可。安卓版本在Release页面发布，可选择最新版本
  <img width="221" height="470" alt="image" src="https://github.com/user-attachments/assets/145a6612-8397-439b-9429-325855a99101" />

  [xiaozhi-0.0.6.apk](https://github.com/AnimeAIChat/xiaozhi-server-go/releases/download/v0.1.0/xiaozhi-0.0.6.apk)
* 可使用其他兼容小智协议的客户端进行测试
---

## 📚 Swagger 文档

* 打开浏览器访问：`http://localhost:8080/swagger/index.html`

### 更新 Swagger 文档（每次修改 API 后都要运行）

```bash
cd src
swag init -g main.go
```

---

## ☁️ CentOS 源码部署指南

> 文档见：[Centos 8 安装指南](Centos_Guide.md)

---

## 🐧 Ubuntu 22.04 源码部署指南

### 1. 安装 Go 环境

```bash
# 下载 Go（以 1.24.2 为例，可根据需要调整版本）
GO_VERSION="1.24.2"
wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz

# 解压到 /usr/local
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz

# 配置环境变量（添加到 ~/.bashrc）
echo 'export GOROOT=/usr/local/go' >> ~/.bashrc
echo 'export GOPATH=$HOME/go' >> ~/.bashrc
echo 'export PATH=$PATH:$GOROOT/bin:$GOPATH/bin' >> ~/.bashrc
source ~/.bashrc

# 验证安装
go version
```

### 2. 安装编译依赖

项目使用了 CGO 调用 C 库（opus 音频编解码），需要安装以下依赖：

```bash
sudo apt update
sudo apt install -y build-essential libopus-dev pkg-config
```

### 3. 克隆项目并配置

```bash
git clone https://github.com/jackylam0812/xiaozhi-server-go.git
cd xiaozhi-server-go

# 复制配置文件
cp config.yaml .config.yaml

# 编辑配置文件，修改关键配置
nano .config.yaml
```

**必须修改的配置项：**

```yaml
web:
  websocket: ws://你的服务器IP:8000    # ESP32设备连接的WebSocket地址
  vision: http://你的服务器IP:8080/api/vision
```

### 4. 编译并运行

```bash
# 下载依赖
go mod tidy

# 方式一：直接运行（开发调试）
CGO_ENABLED=1 go run ./src/main.go

# 方式二：编译后运行（生产部署）
CGO_ENABLED=1 go build -o server ./src/main.go
./server
```

### 5. 配置防火墙（如需外网访问）

```bash
# 开放 WebSocket 端口 (8000) 和 Web 管理端口 (8080)
sudo ufw allow 8000/tcp
sudo ufw allow 8080/tcp
sudo ufw reload
```

### 6. 使用 systemd 管理服务（可选）

创建服务文件：

```bash
sudo nano /etc/systemd/system/xiaozhi.service
```

内容如下：

```ini
[Unit]
Description=Xiaozhi AI Server
After=network.target

[Service]
Type=simple
User=你的用户名
WorkingDirectory=/path/to/xiaozhi-server-go
ExecStart=/path/to/xiaozhi-server-go/server
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

启用并启动服务：

```bash
sudo systemctl daemon-reload
sudo systemctl enable xiaozhi
sudo systemctl start xiaozhi

# 查看状态
sudo systemctl status xiaozhi

# 查看日志
journalctl -u xiaozhi -f
```

### 7. 验证安装

- 访问管理后台：`http://你的服务器IP:8080`
- 默认管理员账号：`admin` / `123456`（请及时修改密码）
- ESP32 设备 OTA 地址设置为：`http://你的服务器IP:8080/api/ota/`

---

## Docker 环境部署

1. 准备`docker-compose.yml`,`.config.yaml`,二进制程序文件

👉 [点击前往 Releases 页面](https://github.com/AnimeAIChat/xiaozhi-server-go/releases)下载二进制程序文件

* 选择你平台对应的版本（默认使用 Liunx: `linux-amd64-server-upx`，如使用其他版本，需要修改docker-compose.yml）

2. 三个文件放到同一目录下，配置`docker-compose.yml`,`.config.yaml`

3. 运行`docker compose up -d`

---

## 💬 社区支持


欢迎提交 Issue、PR 或新功能建议！

<img src="https://github.com/Eric0308/assert/blob/main/xiaozhi/qr.jpg" width="450" alt="微信群二维码"> 
<img src="https://github.com/user-attachments/assets/074c6aec-cfb5-4a68-8fc2-2d08679e366b" width="450" alt="QQ群二维码">
---

## 🛠️ 定制开发

我们接受各种定制化开发项目，如果您有特定需求，欢迎通过微信联系洽谈。

<img src="https://github.com/user-attachments/assets/e2639bc3-a58a-472f-9e72-b9363f9e79a3" width="450" alt="群主二维码">

## 📄 License

本仓库遵循 `Xiaozhi-server-go Open Source License`（基于 Apache 2.0 增强版）
