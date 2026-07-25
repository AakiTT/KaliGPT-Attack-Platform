<div align="center">

# KaliGPT-Attack Platform 🛡️


[![Go Version](https://img.shields.io/badge/Go-1.21+-00ADD8?style=flat-square&logo=go)](https://golang.org)
[![React](https://img.shields.io/badge/React-18.2-61DAFB?style=flat-square&logo=react)](https://reactjs.org)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](CONTRIBUTING.md)

**基于AI的自主渗透测试平台 | AI-Powered Autonomous Penetration Testing Platform**

[English](#english) | [中文](#chinese)

</div>

---

<a name="chinese"></a>


## 📖 项目简介


KaliGPT-Attack Platform 是一个创新的AI驱动的自主渗透测试工具，采用独特的**三模块架构**（推理、生成、解析），有效解决了传统LLM在长时间渗透测试过程中的上下文丢失问题。该工具支持Web UI和MCP-stdio两种工作模式，能够自主决策、执行渗透测试任务，并实时反馈结果。
![外部图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ZQgABwTC9I59Z22xEnprcfcUpgEOGwx2bOic0pYcLsUBV2iaJsSsSWvSPvsrLsjKUVykuVgzU4bL0KibaeE6YRJfQ/640?wx_fmt=png&from=appmsg&watermark=1)

### ✨ 核心特性

- 🧠 **三模块AI架构** - 推理模块（Lead Tester）、生成模块（Junior Tester）、解析模块，分工明确，有效缓解上下文丢失
- 🌲 **PTT任务树** - Penetration Testing Task Tree，清晰维护任务层级和执行状态
- 🔄 **双模式支持** - Web UI（可视化界面）+ MCP-stdio（命令行集成）
- ⚡ **实时流式输出** - SSE技术实现AI推理和工具执行的实时反馈
- 🤖 **自主执行** - AI自动决策下一步操作，无需人工干预
- 🔍 **智能漏洞分析** - 自动提取、分类和报告发现的安全漏洞
- 🛠️ **丰富的工具集成** - 支持Nmap、SQLMap、Nikto、Gobuster、Hydra等主流渗透测试工具
- 🎨 **现代化UI** - 基于React + TailwindCSS + Framer Motion的精美界面，支持深色/浅色主题

---

### 三模块架构详解

#### 1️⃣ 推理模块 (Reasoning Module - Lead Tester)

- **职责**：维护PTT任务树，决策下一步任务
- **输入**：用户目标、工具执行结果、当前PTT状态
- **输出**：下一步任务建议、优先级排序
- **关键功能**：
  - PTT初始化和动态更新
  - 任务可行性评估
  - 攻击路径规划
  - 风险评估

#### 2️⃣ 生成模块 (Generation Module - Junior Tester)

- **职责**：将抽象任务转换为具体可执行命令
- **输入**：推理模块的子任务描述
- **输出**：具体的工具调用命令和参数
- **关键功能**：
  - 任务扩展（Chain of Thought）
  - 命令生成和参数优化
  - 工具选择和组合
  - 执行策略制定

#### 3️⃣ 解析模块 (Parsing Module)

- **职责**：提取和分析工具输出信息
- **输入**：工具输出、源代码、HTTP响应等
- **输出**：结构化的发现、漏洞报告
- **关键功能**：
  - 工具输出智能解析
  - 漏洞识别和分类
  - 信息提取和关联
  - 结果去重和聚合

---

## 🚀 快速开始

### 前置要求

- **Go** 1.21 或更高版本
- **Node.js** 16+ 和 npm/yarn
- **Kali Linux** 或安装了渗透测试工具的系统
- **OpenAI兼容的API** (OpenAI、DeepSeek、SiliconFlow等)

####  运行

**Web模式（推荐）：**

```bash
./kaligpt-attack -mode web -addr :8080
```

然后访问 `http://localhost:8080`

**MCP-stdio模式：**

```bash
./kaligpt-attack -mode mcp-stdio
```

---

## 💻 使用指南

### Web UI 模式

1. **启动服务**

   ```bash
   ./kaligpt-attack -mode web
   ```

2. **访问界面**

   - 打开浏览器访问 `http://localhost:8080`
   - 首次使用需要在"系统设置"中配置API Key

3. **开始渗透测试**

   - 进入"LLM助手"页面

   - 输入目标和测试需求，例如：

     ```
     请对目标网站 http://example.com 进行全面的安全测试
     ```

   - AI将自动规划任务树并执行测试

4. **查看结果**

   - 实时查看AI推理过程
   - 查看工具执行输出
   - 查看攻击链可视化
   - 导出测试报告

### MCP-stdio 模式

适合集成到其他工具（如Claude Desktop、Cursor等）：

```bash
# 在MCP配置文件中添加
{
  "mcpServers": {
    "kaligpt": {
      "command": "/path/to/kaligpt-attack",
      "args": ["-mode", "mcp-stdio"],
      "env": {
        "KALIGPT_API_KEY": "your-api-key"
      }
    }
  }
}
```


## 🛠️ 支持的工具

| 工具         | 类别     | 描述               | 状态 |
| ------------ | -------- | ------------------ | ---- |
| **Nmap**     | 扫描     | 网络映射和端口扫描 | ✅    |
| **Masscan**  | 扫描     | 超快速端口扫描     | ✅    |
| **HTTPx**    | Web      | HTTP探测和指纹识别 | ✅    |
| **SQLMap**   | Web      | SQL注入检测和利用  | ✅    |
| **Nikto**    | Web      | Web服务器漏洞扫描  | ✅    |
| **Gobuster** | Web      | 目录/文件暴力破解  | ✅    |
| **WPScan**   | Web      | WordPress安全扫描  | ✅    |
| **Hydra**    | 暴力破解 | 网络登录暴力破解   | ✅    |

更多工具持续集成中...

---


## 🎯 使用场景

### 1. 自动化渗透测试

```
用户输入：对 http://testsite.com 进行完整的安全评估

AI执行流程：
1. 推理模块：规划测试任务树（信息收集 → 漏洞扫描 → 漏洞利用）
2. 生成模块：生成具体命令（nmap、nikto、sqlmap等）
3. 解析模块：分析结果，提取漏洞信息
4. 推理模块：根据发现调整任务树，继续深入测试
```

### 2. 漏洞验证

```
用户输入：验证 http://example.com/login.php 是否存在SQL注入

AI执行流程：
1. 生成模块：生成SQLMap测试命令
2. 执行器：运行SQLMap
3. 解析模块：分析输出，确认漏洞
4. 推理模块：生成详细报告
```

### 3. 安全培训

- 观察AI的渗透测试思路
- 学习工具使用方法
- 理解攻击链构建过程

---

## 🔒 安全说明

⚠️ **重要提示**

- 本工具仅用于**授权的安全测试**
- 未经授权对他人系统进行渗透测试是**违法行为**
- 使用本工具产生的一切后果由使用者自行承担
- 建议在隔离的测试环境中使用

---

## 🗺️ 未来规划

### 短期目标 (1-3个月)

- [ ] **增强AI能力**
  - [ ] 优化提示词工程，提升决策准确性
  - [ ] 实现多轮对话上下文优化

- [ ] **工具集成**
  - [ ] 集成Metasploit框架
  - [ ] 添加Burp Suite集成
  - [ ] 支持自定义工具配置

- [ ] **报告生成**
  - [ ] 自动生成PDF/HTML报告
  - [ ] 漏洞评分和风险评估
  - [ ] 修复建议生成

- [ ] **用户体验**
  - [ ] 任务模板库
  - [ ] 历史任务复用
  - [ ] 实时协作功能

### 中期目标 (3-6个月)

- [ ] **智能化提升**
  - [ ] 基于历史数据的学习优化
  - [ ] 自动化漏洞利用链构建
  - [ ] 智能绕过WAF/IDS

- [ ] **企业功能**
  - [ ] 多用户支持
  - [ ] 权限管理系统
  - [ ] 任务调度和队列
  - [ ] API接口开放

- [ ] **性能优化**
  - [ ] 分布式任务执行
  - [ ] 结果缓存机制
  - [ ] 大规模目标支持

### 长期目标 (6-12个月)

- [ ] **AI Agent进化**
  - [ ] 多Agent协作系统
  - [ ] 自主学习和策略优化
  - [ ] 零日漏洞发现能力

- [ ] **生态建设**
  - [ ] 插件市场
  - [ ] 社区工具贡献
  - [ ] 知识库共享

- [ ] **合规与认证**
  - [ ] 符合OWASP标准
  - [ ] 安全审计日志
  - [ ] 合规性报告

---


## ⭐ Star History

如果这个项目对你有帮助，请给我们一个 Star ⭐️


---

<div align="center">


**Made with ❤️ by KaliGPT Team**

[⬆ 回到顶部](#kaligpt-attack-)

</div>

---

<a name="english"></a>

## English Version

### 📖 Introduction

KaliGPT-Attack is an innovative AI-driven autonomous penetration testing tool featuring a unique **three-module architecture** (Reasoning, Generation, Parsing) that effectively addresses context loss issues in traditional LLMs during extended penetration testing sessions. The tool supports both Web UI and MCP-stdio modes, enabling autonomous decision-making, task execution, and real-time feedback.

### ✨ Key Features

- 🧠 **Three-Module AI Architecture** - Clear division of labor between Reasoning (Lead Tester), Generation (Junior Tester), and Parsing modules
- 🌲 **PTT Task Tree** - Penetration Testing Task Tree for clear task hierarchy and execution status
- 🔄 **Dual Mode Support** - Web UI (visual interface) + MCP-stdio (CLI integration)
- ⚡ **Real-time Streaming** - SSE technology for live AI reasoning and tool execution feedback
- 🤖 **Autonomous Execution** - AI automatically decides next steps without manual intervention
- 🔍 **Intelligent Vulnerability Analysis** - Automatic extraction, classification, and reporting of security vulnerabilities
- 🛠️ **Rich Tool Integration** - Support for mainstream penetration testing tools like Nmap, SQLMap, Nikto, Gobuster, Hydra
- 🎨 **Modern UI** - Beautiful interface based on React + TailwindCSS + Framer Motion with dark/light theme support

### 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/kk12-30/KaliGPT.git
cd KaliGPT

# Configure
cp config.example.yaml config.yaml
# Edit config.yaml with your API key

# Build
./build.sh  # Linux/Mac
# or
build.bat   # Windows

# Run
./kaligpt-attack -mode web -addr :8080
```

Visit `http://localhost:8080` to start using KaliGPT-Attack!


**⭐ If you find this project helpful, please give it a star! ⭐**

</div>


