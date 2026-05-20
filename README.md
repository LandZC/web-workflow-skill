# Web Workflow Skill

A complete web development workflow skill for Claude Code, covering requirements analysis, UI design, project scaffolding, code development, and Cloudflare Pages deployment.

[English](#english) | [中文](#中文)

---

## English

### Features

- **Full Coverage**: Requirements → UI Design → Development → Build → Deploy
- **Multiple Templates**: Next.js, Vite+Vue, Static HTML
- **Cloudflare Pages**: Pre-configured for zero-cost deployment
- **Flexible**: Works for new projects and existing projects

### Quick Start

#### For New Projects

1. Copy your desired template to your target directory:

```bash
# Next.js + Tailwind (Recommended)
cp -r templates/nextjs-tailwind/ ./my-project

# Vite + Vue
cp -r templates/vite-vue/ ./my-project

# Static HTML
cp -r templates/static-html/ ./my-project
```

2. Install dependencies:

```bash
cd my-project
npm install
```

3. Start development:

```bash
npm run dev
```

4. Build and deploy:

```bash
npm run build
wrangler pages deploy dist --project-name=your-project
```

### Templates

| Template | Best For | Tech Stack |
|----------|----------|------------|
| `nextjs-tailwind` | Most projects | Next.js 14, React, Tailwind CSS |
| `vite-vue` | Lightweight apps | Vite, Vue 3, Tailwind CSS |
| `static-html` | Simple pages | Plain HTML, Tailwind CDN |

### Workflow Phases

1. **Requirements Analysis** - Define what to build using EARS syntax
2. **UI Design** - Design the interface with aesthetic direction
3. **Project Initialization** - Set up scaffolding (new projects only)
4. **Code Development** - Implement features
5. **Build & Deploy** - Ship to Cloudflare Pages
6. **Testing & Verification** - Ensure quality

### Installation

Copy the `web-workflow` directory to your Claude Code skills folder:

```bash
cp -r web-workflow ~/.claude/skills/
```

---

## 中文

### 功能特点

- **完整覆盖**：需求分析 → UI设计 → 开发 → 构建 → 部署
- **多套模板**：Next.js、Vite+Vue、静态HTML
- **Cloudflare Pages**：预配置零成本部署
- **灵活适用**：支持新项目和现有项目

### 快速开始

#### 新项目

1. 复制模板到目标目录：

```bash
# Next.js + Tailwind（推荐）
cp -r templates/nextjs-tailwind/ ./my-project

# Vite + Vue
cp -r templates/vite-vue/ ./my-project

# 静态HTML
cp -r templates/static-html/ ./my-project
```

2. 安装依赖：

```bash
cd my-project
npm install
```

3. 启动开发：

```bash
npm run dev
```

4. 构建部署：

```bash
npm run build
wrangler pages deploy dist --project-name=your-project
```

### 模板列表

| 模板 | 适用场景 | 技术栈 |
|------|----------|--------|
| `nextjs-tailwind` | 大多数项目 | Next.js 14, React, Tailwind CSS |
| `vite-vue` | 轻量应用 | Vite, Vue 3, Tailwind CSS |
| `static-html` | 简单页面 | 纯HTML, Tailwind CDN |

### 工作流程

1. **需求分析** - 使用EARS语法定义需求
2. **UI设计** - 确定设计风格和配色方案
3. **项目初始化** - 搭建项目脚手架（仅新项目）
4. **代码开发** - 实现功能
5. **构建部署** - 部署到Cloudflare Pages
6. **测试验证** - 确保质量

### 安装方法

将 `web-workflow` 目录复制到Claude Code的skills文件夹：

```bash
cp -r web-workflow ~/.claude/skills/
```

## License

MIT
