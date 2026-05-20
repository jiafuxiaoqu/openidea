Open In IDEA

一个可以通过浏览器快速打开本地 IDE 项目的工具，支持从 Web 页面、浏览器插件等场景，一键唤起本地 IntelliJ IDEA / Android Studio 等 JetBrains IDE。

# Spring Boot Open In IDEA — 一键从浏览器跳转到 Controller 源码

**Developer Toolchain · Spring Boot · IntelliJ IDEA**

在浏览器 Network 面板看到请求时，**一键** 精准定位到 Spring Boot 项目中对应的 Controller 方法，无需手动搜索类和方法。

---

## ✨ 核心功能

- 实时捕获浏览器发出的业务请求（自动过滤静态资源）
- 页面右下角可拖拽浮窗，展示所有接口请求
- 点击「📂 打开 IDEA」按钮，自动跳转到对应 Controller 方法所在行
- 智能匹配 Spring MVC 注解（@GetMapping、@PostMapping 等）
- 自动剥离代理前缀（`/dev-api`、`/admin-api`、`/gateway/...` 等）
- 支持 Ant 风格路径匹配（`{id}`、` * `、` ** `）

---

## 🛠 工作原理

整个流程由三个组件组成，形成完整闭环：

1. **Chrome 扩展** 通过 `chrome.webRequest` 监听网络请求
2. **本地 HTTP 通信** 将请求发送到 IDEA 插件（默认端口 38523）
3. **IDEA 插件** 扫描项目中所有 Controller 注解，精准匹配并跳转

---

## 📦 两个核心组件

### 1. Chrome Extension（浏览器端）
项目名称：`spring-boot-open-in-ide-extension`

- 右下角可拖拽浮窗，不影响正常操作
- 自动过滤静态资源（CSS、JS、图片等）
- 支持最小化、清空列表
- 可自定义 IDEA 插件端口

### 2. IDEA Plugin（开发工具端）
项目名称：`open-in-idea-plugin`

- 支持所有 Spring MVC 映射注解
- 类级别 + 方法级别路径自动拼接
- 自动处理路径前缀差异
- Settings 面板可开关插件、修改端口
- 支持 IDEA 2023.3+（Java 17+）


---

## 🚀 快速安装

### 第一步：安装 IDEA 插件

1. 克隆 `open-in-idea-plugin` 仓库
2. IDEA → **Settings → Plugins → ⚙️ → Install Plugin from Disk...**
3. 安装后重启 IDEA，在 **Settings → Tools → Open In IDEA** 中启用

### 第二步：安装 Chrome 扩展

1. 克隆 `spring-boot-open-in-ide-extension` 仓库
2. 打开 Chrome 浏览器，访问 `chrome://extensions/`
3. 开启右上角**开发者模式**
4. 点击「加载已解压的扩展程序」，选择扩展文件夹
5. 安装完成，工具栏出现扩展图标

> **注意**：IDEA 插件和 Chrome 扩展需使用相同端口（默认 38523），修改后两端都要同步更新。

---

## ❓ 常见问题（FAQ）

**点击按钮无反应？**  
请确认：IDEA 已打开对应后端项目、插件已启用、端口被正确占用。

**提示“未找到匹配的 Controller”？**  
检查项目是否正确、索引是否完成、HTTP Method 是否匹配、是否使用了自定义组合注解（暂不支持）。

**同时打开多个项目时如何处理？**  
同一端口只能被一个 IDEA 实例占用，可为不同项目配置不同端口。

**支持复杂路径前缀吗？**  
完全支持。插件会逐段剥离前缀进行匹配，兼容各类网关和代理配置。

---

## 技术栈

- **IDEA 插件**：IntelliJ Platform SDK + Kotlin
- **Chrome 扩展**：Manifest V3 + TypeScript
- **通信协议**：本地 HTTP

---

## 贡献与反馈

欢迎提交 Issue 和 Pull Request！

项目主页：https://openidea.kwkwonline.us.kg

---

**让前后端联调更丝滑 🚀**