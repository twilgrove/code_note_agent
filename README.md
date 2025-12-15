
-----

# 🤖 Code Note Agent (v0.7.3)

> **声明 / Credits**
>
> 本项目代码及文档由 **Google Gemini** (Model 2.0 Flash Experimental) 协助生成与维护。
>
> The code and documentation of this project were generated with the assistance of Google Gemini.

## 📖 项目简介

**Code Note Agent** 是一个轻量级、**单文件 (Single-file)** 的网页端代码批量处理工具。它利用现代浏览器的 **File System Access API**，允许用户直接挂载本地文件夹，调用大语言模型（LLM）对代码进行批量中文注释、逻辑解释或重构。

***

## 📅 版本演进 (Changelog)

### **v0.7.3 (Current) - 终极体验优化**
* ✨ **多账号隔离**：实现了 API Key 按服务商（DeepSeek/Gemini/豆包等）独立存储。切换服务商时自动恢复对应的 Key，无需重复输入。
* 🚀 **无缝热切换**：增加了断点检测功能。在任务中途切换模型并重新连接后，无需重新挂载文件夹，“启动”按钮自动解锁，实现丝滑切换。

### **v0.7.1 ~ v0.7.2 - 交互容错修复**
* 🐛 **死锁修复**：修复了连接失败后按钮状态无法重置的问题。现在修改 Key 或 ID 会立即重置连接状态，允许随时重试。
* 🛡️ **实弹验证**：针对豆包（Doubao），连接时增加轻量级探测请求（Ping），确保 Endpoint ID 有效且 Key 正确后才允许通过，杜绝无效配置。

### **v0.7.0 - 豆包深度适配 (UI重构)**
* 🏗️ **UI 分离**：针对火山引擎架构特点，为豆包设计了独立的 **Endpoint ID** 输入框，隐藏了不适用的“获取模型列表”下拉框。
* 🧹 **逻辑清理**：移除了因浏览器 CORS 限制导致无效的自动列表获取逻辑，改为更可靠的手动指定模式。

### **v0.6.0 - 交互逻辑重构**
* 🔒 **步骤锁定机制**：引入了 Step 1 (连接) -> Step 2 (挂载) -> Step 3 (启动) 的严格状态流转，防止误操作。
* 🖥️ **控制台优化**：重写了日志输出逻辑，支持不同类型的日志（成功/警告/错误）高亮显示。

### **v0.5.0 - 国产模型生态扩展**
* 🥟 **接入豆包**：增加了对字节跳动豆包（火山引擎）的支持，解决了 Endpoint ID 与标准模型名不一致的配置问题。
* 🌍 **CORS 兼容性探索**：初步探索了不同厂商 API 的跨域策略。

### **v0.4.0 - 多模型架构支持**
* 🔌 **协议泛化**：重构了底层请求逻辑，兼容 OpenAI 格式接口。
* 🤝 **新成员加入**：正式支持 DeepSeek（深度求索）和 Kimi (月之暗面)，大幅降低了使用成本并提升了中文理解能力。

### **v0.3.0 - 稳定性与环境检测**
* 🚦 **环境自检**：增加了对 `File System Access API` 的浏览器兼容性检测（Chrome/Edge）。
* 📊 **可视化进度**：引入了进度条和百分比显示，解决了批量处理时“不知道还要多久”的焦虑。

### **v0.2.0 - 智能限流与列表获取**
* 📜 **模型列表拉取**：实现了连接时自动获取账号下可用模型列表的功能。
* 🧊 **冷却机制**：增加了指数退避算法（Exponential Backoff），遇到 API 429 限流错误时自动倒计时等待，防止任务中断。

### **v0.1.0 - 原型诞生**
* 🌱 **MVP 发布**：基于 Google Gemini API 和 File System API 构建了首个单文件版本，实现了本地代码读取、AI 处理、本地写入的最小可行性闭环。

## 🌟 通用功能

  * **📂 本地直连**：浏览器直接读写本地硬盘，代码不经过第三方中转服务器，隐私安全。
  * **🧠 全模型支持**：
      * **DeepSeek** (默认推荐，高性价比)
      * **Doubao** (火山引擎)
      * **Kimi** (月之暗面)
      * **Gemini** (Google)
      * **Ollama** (本地模型支持)
      * **Custom**(兼容所有 OpenAI 格式接口) 
  * **🛡️ 智能抗干扰**：内置指数退避算法，自动处理 HTTP 429 限流错误，带有倒计时冷却提示。
  * **⏱️ 实时监控**：精准显示处理进度百分比及任务实时耗时。

## 🚀 快速开始

### 1\. 环境要求

必须使用支持 File System Access API 的现代浏览器：

  * ✅ **Google Chrome** (推荐)
  * ✅ **Microsoft Edge**
  * ❌ Firefox / Safari (暂不支持)

### 2\. 使用步骤

1.  **打开工具**：双击下载的 `code_note_agent.html` 文件。
2.  **Step 1: 连接大脑**
      * 选择 AI 服务商。
      * 输入 API Key（会自动保存）。
      * 如果是豆包，还需输入 Endpoint ID。
      * 点击 **“⚡ 连接并验证”**。
3.  **Step 2: 挂载文件**
      * 点击 **“📂 选择源代码文件夹”**（Input）。
      * 点击 **“💾 选择输出文件夹”**（Output）。
4.  **Step 3: 启动**
      * 点击 **“🚀 启动智能注释 Agent”**。
      * 观察控制台日志，等待处理完成。

## ⚙️ 模型配置速查表

| 服务商            | Base URL (默认)                                    | 鉴权填空说明                                |
| :---------------- | :------------------------------------------------- | :------------------------------------------ |
| **DeepSeek**      | `https://api.deepseek.com`                         | 输入 `sk-` 开头的 API Key                   |
| **Doubao (豆包)** | `https://ark.cn-beijing.volces.com/api/v3`         | **特殊**：输入 `ep-2024...` 格式的接入点 ID |
| **Gemini**        | `https://generativelanguage.googleapis.com/v1beta` | 输入 Google AI Studio Key                   |
| **Kimi**          | `https://api.moonshot.cn/v1`                       | 输入 Moonshot API Key                       |
| **Ollama**        | `http://localhost:11434/v1`                        | 本地运行通常留空即可                        |

## 🔒 安全说明

  * **零后端**：本工具是纯静态 HTML/JS 页面。
  * **Key 存储**：API Key 仅保存在您本地浏览器的 `localStorage` 中。
  * **网络请求**：所有代码数据仅在您的浏览器与目标 AI 服务商之间直接传输。

## 🛠️ 技术栈

  * **Core**: Vanilla JavaScript (ES6+)
  * **UI**: HTML5 + CSS3 (Flexbox/Grid)
  * **API**: Fetch API (Async/Await) + File System Access API

-----

**License**
MIT License (开源免费，随意修改)
