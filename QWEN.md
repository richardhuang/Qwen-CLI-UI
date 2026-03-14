# Qwen CLI UI 项目指南

## 项目概述

**Qwen CLI UI** 是一个基于 Qwen Code 的可视化 Web 界面，提供 AI 辅助编程功能。该项目允许用户通过浏览器随时随地进行 AI 编程，支持实时对话、文件管理、终端执行等功能。

### 核心特性

- 🌐 **响应式 Web 界面** - 支持桌面、平板、手机等各类设备
- 🤖 **AI 辅助编程** - 集成 Qwen Code CLI，提供智能代码建议
- 💬 **实时聊天** - 与 Qwen Code AI 进行编程对话
- 📁 **项目管理** - 可视化文件浏览器，实时监控项目文件
- 💻 **集成终端** - 在浏览器中执行命令，支持多终端会话
- 🔐 **用户认证** - JWT 认证系统，支持多用户登录
- ⚙️ **个性化设置** - 主题、字体、API 配置等

### 技术栈

#### 前端技术
- **React 18.2.0** - 现代化 UI 框架
- **Vite 4.4.0** - 快速开发构建工具
- **Tailwind CSS 3.3.0** - 样式框架
- **React Router DOM 6.15.0** - 路由管理
- **Socket.IO Client 4.7.0** - WebSocket 实时通信
- **CodeMirror 6.x** - 代码编辑器（语法高亮、多语言支持）
- **xterm.js 5.3.0** - 终端模拟器
- **Lucide React** - 图标库

#### 后端技术
- **Node.js + Express 4.18.0** - 服务器框架
- **SQLite3 5.1.0** - 轻量级数据库
- **JWT 9.0.0** - 身份认证
- **bcrypt 5.1.0** - 密码加密
- **node-pty 0.10.1** - 真正的伪终端支持
- **Socket.IO 4.7.0** - WebSocket 通信

## 项目结构

```
Qwen-CLI-UI/
├── src/                      # 前端源代码
│   ├── components/          # React 组件
│   │   ├── Chat.jsx         # 聊天界面组件
│   │   ├── FileExplorer.jsx # 文件浏览器组件
│   │   ├── Login.jsx        # 登录/注册组件
│   │   ├── Settings.jsx     # 设置组件
│   │   ├── Sidebar.jsx      # 侧边栏组件
│   │   └── Terminal.jsx     # 终端组件
│   ├── contexts/            # React Context
│   │   ├── AuthContext.jsx  # 认证上下文
│   │   ├── SocketContext.jsx # WebSocket 上下文
│   │   └── ProjectContext.jsx # 项目上下文
│   ├── utils/               # 工具函数
│   ├── App.jsx              # 主应用组件
│   └── main.jsx             # 应用入口
├── server/                   # 后端源代码
│   ├── index.js             # 服务器主文件
│   ├── database/            # SQLite 数据库文件
│   └── package.json         # 后端依赖
├── projects/                 # 项目文件存储目录
│   ├── ll/
│   ├── my_proj/
│   ├── proj_3/
│   ├── test_proj/
│   └── test-project/
├── dist/                     # 构建输出目录
├── scripts/                  # 辅助脚本
├── index.html                # HTML 模板
├── vite.config.js            # Vite 配置
├── tailwind.config.js        # Tailwind 配置
├── postcss.config.js         # PostCSS 配置
├── package.json              # 前端依赖
├── env.example               # 环境变量示例
├── start.sh                  # 启动脚本
├── README.md                 # 项目说明
├── DEMO.md                   # 功能演示文档
└── TERMINAL_GUIDE.md         # 终端使用指南
```

## 开发环境配置

### 前置要求

- Node.js 20 或更高版本
- npm 或 yarn

### 安装依赖

```bash
# 安装所有依赖（前端和后端）
npm run install-all

# 或分别安装
npm install                    # 安装前端依赖
cd server && npm install      # 安装后端依赖
```

### 环境变量配置

```bash
# 复制环境变量示例文件
cp env.example .env

# 编辑 .env 文件，配置以下关键参数：
PORT=4008                      # 服务器端口
JWT_SECRET=your-secret-key     # JWT 密钥（请修改为随机字符串）
OPENAI_API_KEY=your_api_key    # Qwen API 密钥
OPENAI_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
OPENAI_MODEL=qwen3-coder-plus
```

### 启动开发服务器

```bash
# 使用启动脚本（推荐）
./start.sh

# 或手动启动
npm run dev                    # 同时启动前后端开发服务器
```

开发服务器将在以下地址运行：
- **前端**: http://localhost:4009/
- **后端 API**: http://localhost:4008/

## 构建和部署

### 生产构建

```bash
# 构建前端静态文件
npm run build

# 构建输出到 dist/ 目录
```

### 生产运行

```bash
# 构建后运行
npm run preview

# 或直接运行后端服务器（需要先构建）
cd server && npm start
```

### 一键启动（生产模式）

```bash
# 先构建
npm run build

# 然后运行
npm run server
```

## 核心功能说明

### 1. 用户认证系统

- **注册/登录**: 新用户需要先注册账户
- **JWT 认证**: 使用 JSON Web Token 进行身份验证
- **会话持久化**: 自动保存登录状态
- **密码加密**: 使用 bcrypt 加密存储密码

### 2. AI 聊天功能

- 与 Qwen Code AI 进行编程对话
- 获取代码建议和重构建议
- 解答编程问题
- 支持多种 Qwen 模型选择

### 3. 项目管理

- 创建新项目
- 选择现有项目
- 项目文件存储在 `./projects/` 目录
- 每个项目有独立的工作目录

### 4. 文件浏览器

- 浏览项目文件结构
- 在线编辑代码文件
- 支持多种编程语言的语法高亮
- 自动保存编辑内容

### 5. 终端集成

- **多终端会话**: 支持创建多个独立终端
- **node-pty 实现**: 真正的伪终端支持
- **工作目录隔离**: 每个终端自动设置到项目目录
- **WebSocket 通信**: 单端口 WebSocket 架构
- **终端管理**:
  - 创建/关闭终端
  - 重命名终端
  - 切换终端会话
  - 调整终端大小

### 6. 设置管理

- API 密钥配置
- Base URL 配置
- 模型选择
- 主题设置
- 字体大小调整
- 自动保存开关
- 通知设置

## 开发规范

### 代码风格

- **React**: 使用函数组件和 Hooks
- **CSS**: 使用 Tailwind CSS 工具类
- **命名**: 遵循 React 命名规范（PascalCase 组件，camelCase 变量）
- **模块化**: 组件、Context、工具函数分离

### 文件组织

- 组件按功能分类放在 `src/components/`
- 全局状态使用 Context API
- 工具函数放在 `src/utils/`
- 后端 API 路由在 `server/index.js`

### 数据库结构

#### users 表
- id: 用户 ID
- username: 用户名（唯一）
- password_hash: 密码哈希
- created_at: 创建时间
- last_login: 最后登录时间
- is_active: 是否激活

#### settings 表
- id: 设置 ID
- user_id: 用户 ID（外键）
- api_key: Qwen API 密钥
- base_url: API 基础 URL
- model: 使用的模型
- theme: 主题
- font_size: 字体大小
- enable_auto_save: 是否自动保存
- enable_notifications: 是否启用通知
- max_history_length: 最大历史长度

#### projects 表
- id: 项目 ID
- user_id: 用户 ID（外键）
- name: 项目名称
- path: 项目路径（唯一）
- created_at: 创建时间
- last_accessed: 最后访问时间

## API 端点

### 用户认证
- `POST /api/auth/register` - 注册
- `POST /api/auth/login` - 登录
- `POST /api/auth/logout` - 登出
- `GET /api/auth/me` - 获取当前用户信息

### 项目管理
- `GET /api/projects` - 获取项目列表
- `POST /api/projects` - 创建项目
- `DELETE /api/projects/:id` - 删除项目
- `PUT /api/projects/:id` - 更新项目

### 设置管理
- `GET /api/settings` - 获取用户设置
- `PUT /api/settings` - 更新用户设置

### 终端管理
- `GET /api/terminal/sessions` - 获取终端会话列表
- `POST /api/terminal/create` - 创建终端
- `POST /api/terminal/rename` - 重命名终端
- `POST /api/terminal/destroy` - 关闭终端

### WebSocket 事件
- `terminal:connect` - 连接到终端
- `terminal:input` - 发送终端输入
- `terminal:data` - 接收终端输出
- `terminal:resize` - 调整终端大小
- `terminal:close` - 关闭终端连接

## 常见任务

### 添加新功能

1. 前端组件放在 `src/components/`
2. 后端 API 添加到 `server/index.js`
3. 数据库表修改需要更新 `server/index.js` 中的初始化代码
4. 更新 `README.md` 和 `DEMO.md` 文档

### 调试

- **前端**: 打开浏览器开发者工具
- **后端**: 查看终端输出或使用 `console.log`
- **数据库**: 使用 SQLite 工具查看 `server/database/qwen_code_ui.db`

### 修复问题

1. 检查控制台错误信息
2. 查看服务器日志
3. 验证环境变量配置
4. 确认依赖已正确安装

## 重要注意事项

### 安全性

1. **JWT 密钥**: 生产环境必须修改 `JWT_SECRET`
2. **API 密钥**: 不要将包含敏感信息的 `.env` 文件提交到 Git
3. **密码加密**: 使用 bcrypt 加密存储密码
4. **路径验证**: 终端创建时验证项目路径权限

### 性能优化

1. **按需渲染**: 只渲染活跃的终端组件
2. **连接复用**: WebSocket 连接在所有终端间共享
3. **内存管理**: 终端关闭时自动清理资源
4. **数据库索引**: 确保常用查询字段有索引

### 限制和已知问题

1. **会话持久化**: 终端会话存储在内存中，服务重启后会丢失
2. **进程管理**: 终端进程在会话关闭时自动清理
3. **网络连接**: 需要稳定的 WebSocket 连接
4. **浏览器兼容**: 需要支持 WebSocket 和现代 JavaScript 的浏览器

## 相关资源

- [Qwen Code](https://github.com/QwenLM/qwen-code) - 为 Qwen3-Coder 优化的 CLI 工作流
- [Gemini CLI UI](https://github.com/cruzyjapan/Gemini-CLI-UI) - 本项目的灵感来源
- [React 官方文档](https://react.dev/)
- [Vite 官方文档](https://vitejs.dev/)
- [Tailwind CSS 官方文档](https://tailwindcss.com/)
- [Socket.IO 官方文档](https://socket.io/docs/v4/)

## 许可证

本项目基于 [GPL-3.0](LICENSE) 许可证开源。

## 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

---

**最后更新**: 2026年3月14日
**项目状态**: ✅ 生产就绪
