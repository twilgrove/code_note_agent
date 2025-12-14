
-----

# 🤖 Code Note Agent (v0.7.3)

> **声明 / Credits**
>
> 本项目代码及文档由 **Google Gemini** (Model 2.0 Flash Experimental) 协助生成与维护。
>
> The code and documentation of this project were generated with the assistance of Google Gemini.

## 📖 项目简介

**Code Note Agent** 是一个轻量级、**单文件 (Single-file)** 的网页端代码批量处理工具。它利用现代浏览器的 **File System Access API**，允许用户直接挂载本地文件夹，批量调用大语言模型（LLM）对代码进行中文注释、逻辑解释或重构。

**v0.7.3 版本核心升级**：重点优化了多模型切换体验，实现了**API Key 分服务商独立存储**以及**任务状态自动恢复**，让“换个模型重跑”变得丝滑无感。

## ✨ 核心特性 (v0.7.3 新增)

  * **🔐 多账号 Key 隔离 (Multi-Key Isolation)**：
      * 系统会自动根据服务商（DeepSeek/Gemini/豆包等）**分别存储**您的 API Key。
      * 切换服务商时，会自动填充对应的 Key，无需反复粘贴。
  * **⏯️ 智能断点续连 (Auto-Resume)**：
      * 只要您已经挂载了输入/输出目录，切换服务商并重新连接成功后，**“启动任务”按钮会自动解锁**。
      * 无需重新选择文件夹，真正实现无缝切换。
  * **⚡️ 豆包 (Doubao) 深度适配**：
      * 提供专属的 **Endpoint ID** 输入框。
      * 连接时自动发送轻量级探测请求，验证接入点有效性，不再只是简单的保存配置。

## 🌟 通用功能

  * **📂 本地直连**：浏览器直接读写本地硬盘，代码不经过第三方中转服务器，隐私安全。
  * **🧠 全模型支持**：
      * **DeepSeek** (默认推荐，高性价比)
      * **Doubao (豆包)** (火山引擎专用接口)
      * **Google Gemini** / **Kimi (Moonshot)**
      * **Ollama** (本地模型支持)
      * **Custom** (兼容所有 OpenAI 格式接口)
  * **🛡️ 智能抗干扰**：内置指数退避算法，自动处理 HTTP 429 限流错误，带有倒计时冷却提示。
  * **⏱️ 实时监控**：精准显示处理进度百分比及任务实时耗时。

## 🚀 快速开始

### 1\. 环境要求

必须使用支持 File System Access API 的现代浏览器：

  * ✅ **Google Chrome** (推荐)
  * ✅ **Microsoft Edge**
  * ❌ Firefox / Safari (暂不支持)

### 2\. 使用步骤

1.  **打开工具**：双击下载的 `index.html` 文件。
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
  * **网络请求**：所有代码数据仅在您的浏览器与目标 AI 服务商（如 https://www.google.com/search?q=api.deepseek.com）之间直接传输。

## 🛠️ 技术栈

  * **Core**: Vanilla JavaScript (ES6+)
  * **UI**: HTML5 + CSS3 (Flexbox/Grid)
  * **API**: Fetch API (Async/Await) + File System Access API

-----

**License**
MIT License (开源免费，随意修改)
