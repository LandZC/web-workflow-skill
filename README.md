# Web Workflow Skill

> A complete web development workflow skill for Claude Code, covering requirements analysis, UI design, project scaffolding, code development, and Cloudflare Pages deployment.

[English](#english) | [中文](#中文)

---

## English

### Why This Skill?

Building a web project involves many steps: defining requirements, designing UI, setting up the project, writing code, and deploying. This skill automates the entire workflow, so you can focus on what matters - building your product.

**Key Benefits:**
- Zero-cost deployment to Cloudflare Pages
- Pre-built templates for popular frameworks
- Structured workflow from design to production
- Works with both new projects and existing codebases

### Project Structure

```
web-workflow/
├── SKILL.md                    # Main skill definition (Claude Code reads this)
├── README.md                   # This file
├── LICENSE                     # MIT License
└── templates/
    ├── nextjs-tailwind/        # Next.js 14 + Tailwind CSS template
    │   ├── package.json
    │   ├── next.config.js      # Pre-configured for static export
    │   ├── tailwind.config.js
    │   ├── postcss.config.js
    │   ├── tsconfig.json
    │   └── src/
    │       └── app/
    │           ├── layout.tsx
    │           ├── page.tsx
    │           └── globals.css
    ├── vite-vue/               # Vite + Vue 3 template
    │   ├── package.json
    │   ├── vite.config.js      # Pre-configured with relative paths
    │   ├── tailwind.config.js
    │   ├── postcss.config.js
    │   ├── index.html
    │   └── src/
    │       ├── main.js
    │       ├── App.vue
    │       └── style.css
    └── static-html/            # Simple HTML template (no build step)
        └── index.html          # Uses Tailwind CDN
```

### Installation

#### Option 1: Manual Installation

1. Download or clone this repository:
```bash
git clone https://github.com/LandZC/web-workflow-skill.git
```

2. Copy to Claude Code skills directory:
```bash
# Linux/macOS
cp -r web-workflow ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse web-workflow ~/.claude/skills/
```

3. Restart Claude Code to load the skill.

#### Option 2: Copy Specific Files

If you only need certain templates, copy only what you need:
```bash
# Just the Next.js template
cp -r templates/nextjs-tailwind /path/to/your/project
```

### Quick Start

#### Creating a New Project

**Step 1: Choose a Template**

| Template | Best For | Tech Stack | Build Step |
|----------|----------|------------|------------|
| `nextjs-tailwind` | Most projects, SSR/SSG needed | Next.js 14, React 18, Tailwind CSS | Required |
| `vite-vue` | Lightweight SPAs | Vite 5, Vue 3, Tailwind CSS | Required |
| `static-html` | Landing pages, simple sites | HTML, Tailwind CDN | None |

**Step 2: Initialize Project**

```bash
# Example: Create a new Next.js project
cp -r ~/.claude/skills/web-workflow/templates/nextjs-tailwind ./my-awesome-project
cd my-awesome-project
npm install
```

**Step 3: Start Development**

```bash
npm run dev
# Open http://localhost:3000 (Next.js) or http://localhost:5173 (Vite)
```

**Step 4: Build & Deploy**

```bash
# Build for production
npm run build

# Deploy to Cloudflare Pages
wrangler pages deploy dist --project-name=my-awesome-project
# Or for Next.js (output is in 'out' directory):
wrangler pages deploy out --project-name=my-awesome-project
```

### Template Details

#### Next.js + Tailwind (`nextjs-tailwind`)

**Features:**
- App Router (Next.js 14)
- Static site generation (SSG)
- Tailwind CSS for styling
- TypeScript support
- Pre-configured for Cloudflare Pages

**File Structure:**
```
src/
├── app/
│   ├── layout.tsx      # Root layout with metadata
│   ├── page.tsx        # Home page
│   └── globals.css     # Global styles + Tailwind directives
├── components/         # Your components (create this)
└── lib/               # Utilities (create this)
```

**Key Configuration:**
```javascript
// next.config.js - Already configured for static export
module.exports = {
  output: 'export',        // Static HTML export
  images: {
    unoptimized: true,     // Required for static export
  },
  trailingSlash: true,     // Better for static hosting
};
```

**Customization:**
1. Update `src/app/layout.tsx` - Change metadata (title, description)
2. Update `src/app/page.tsx` - Build your homepage
3. Add components in `src/components/`
4. Update `tailwind.config.js` - Customize colors, fonts, etc.

#### Vite + Vue (`vite-vue`)

**Features:**
- Vue 3 with Composition API
- Vite for fast development
- Tailwind CSS for styling
- Pre-configured relative paths

**File Structure:**
```
src/
├── main.js            # Entry point
├── App.vue            # Root component
├── style.css          # Tailwind imports
├── components/        # Your components (create this)
└── views/             # Page components (create this)
```

**Key Configuration:**
```javascript
// vite.config.js - Already configured for relative paths
export default defineConfig({
  base: './',           // Relative paths for Cloudflare Pages
  plugins: [vue()],
  build: {
    outDir: 'dist',
  },
});
```

#### Static HTML (`static-html`)

**Features:**
- No build step required
- Uses Tailwind CDN
- Direct deployment
- Perfect for landing pages

**Usage:**
```bash
# Just edit index.html and deploy
cp -r templates/static-html ./landing-page
# Edit landing-page/index.html
wrangler pages deploy landing-page --project-name=landing
```

### Workflow with Claude Code

When you invoke this skill in Claude Code, it follows a structured workflow:

#### Phase 1: Requirements Analysis
- Analyzes your request
- Creates user stories with EARS syntax
- Generates `requirements.md`

#### Phase 2: UI Design
- Defines aesthetic direction
- Creates color palette and typography
- Generates `design.md`

#### Phase 3: Project Initialization
- Copies appropriate template
- Configures project settings
- Installs dependencies

#### Phase 4: Code Development
- Implements features based on requirements
- Follows best practices
- Provides progress updates

#### Phase 5: Build & Deploy
- Builds for production
- Deploys to Cloudflare Pages
- Provides deployment URL

#### Phase 6: Testing & Verification
- Runs quality checks
- Verifies functionality
- Reports any issues

### Prerequisites

- **Node.js** 18 or higher
- **npm** or **yarn** or **pnpm**
- **Wrangler CLI** (for deployment):
  ```bash
  npm install -g wrangler
  ```
- **Cloudflare Account** (free tier works)

### Configuration

#### Cloudflare Pages Setup

1. Create a Cloudflare account at https://dash.cloudflare.com
2. Install Wrangler CLI: `npm install -g wrangler`
3. Login: `wrangler login`
4. Deploy: `wrangler pages deploy dist --project-name=your-project`

#### Custom Domain (Optional)

1. Go to Cloudflare Pages dashboard
2. Select your project
3. Go to Custom domains
4. Add your domain and follow DNS setup instructions

### Troubleshooting

#### Build Errors

**"Module not found"**
```bash
# Solution: Reinstall dependencies
rm -rf node_modules package-lock.json
npm install
```

**"Type error"**
```bash
# Solution: Check TypeScript config
# Ensure tsconfig.json includes your files
```

#### Deployment Issues

**404 after deployment**
- Check build output directory (`dist` or `out`)
- Ensure `base: './'` in vite.config.js
- Verify `output: 'export'` in next.config.js

**Assets not loading**
- Use relative paths, not absolute
- Check browser console for 404 errors
- Verify build output structure

### Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit changes: `git commit -m 'Add my feature'`
4. Push to branch: `git push origin feature/my-feature`
5. Open a Pull Request

### License

MIT License - see [LICENSE](LICENSE) for details.

---

## 中文

### 为什么需要这个 Skill？

构建一个 Web 项目涉及多个步骤：定义需求、设计 UI、搭建项目、编写代码和部署。这个 skill 自动化了整个工作流程，让你可以专注于真正重要的事情——构建产品。

**核心优势：**
- 零成本部署到 Cloudflare Pages
- 预置热门框架模板
- 从设计到生产的结构化工作流
- 支持新项目和现有项目

### 项目结构

```
web-workflow/
├── SKILL.md                    # 主 skill 定义（Claude Code 读取这个）
├── README.md                   # 说明文档
├── LICENSE                     # MIT 许可证
└── templates/
    ├── nextjs-tailwind/        # Next.js 14 + Tailwind CSS 模板
    ├── vite-vue/               # Vite + Vue 3 模板
    └── static-html/            # 简单 HTML 模板（无需构建）
```

### 安装方法

#### 方法一：手动安装

1. 下载或克隆此仓库：
```bash
git clone https://github.com/LandZC/web-workflow-skill.git
```

2. 复制到 Claude Code skills 目录：
```bash
# Linux/macOS
cp -r web-workflow ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse web-workflow ~/.claude/skills/
```

3. 重启 Claude Code 以加载 skill。

#### 方法二：仅复制需要的模板

如果只需要特定模板，只复制需要的部分：
```bash
# 只需要 Next.js 模板
cp -r templates/nextjs-tailwind /path/to/your/project
```

### 快速开始

#### 创建新项目

**第一步：选择模板**

| 模板 | 适用场景 | 技术栈 | 需要构建 |
|------|----------|--------|----------|
| `nextjs-tailwind` | 大多数项目，需要 SSR/SSG | Next.js 14, React 18, Tailwind CSS | 是 |
| `vite-vue` | 轻量级 SPA | Vite 5, Vue 3, Tailwind CSS | 是 |
| `static-html` | 落地页、简单站点 | HTML, Tailwind CDN | 否 |

**第二步：初始化项目**

```bash
# 示例：创建新的 Next.js 项目
cp -r ~/.claude/skills/web-workflow/templates/nextjs-tailwind ./my-awesome-project
cd my-awesome-project
npm install
```

**第三步：开始开发**

```bash
npm run dev
# 打开 http://localhost:3000（Next.js）或 http://localhost:5173（Vite）
```

**第四步：构建并部署**

```bash
# 构建生产版本
npm run build

# 部署到 Cloudflare Pages
wrangler pages deploy dist --project-name=my-awesome-project
# Next.js 输出在 'out' 目录：
wrangler pages deploy out --project-name=my-awesome-project
```

### 模板详情

#### Next.js + Tailwind (`nextjs-tailwind`)

**功能特点：**
- App Router（Next.js 14）
- 静态站点生成（SSG）
- Tailwind CSS 样式
- TypeScript 支持
- 已配置好 Cloudflare Pages

**关键配置：**
```javascript
// next.config.js - 已配置为静态导出
module.exports = {
  output: 'export',        // 静态 HTML 导出
  images: {
    unoptimized: true,     // 静态导出必需
  },
  trailingSlash: true,     // 更适合静态托管
};
```

**自定义步骤：**
1. 更新 `src/app/layout.tsx` - 修改元数据（标题、描述）
2. 更新 `src/app/page.tsx` - 构建首页
3. 在 `src/components/` 添加组件
4. 更新 `tailwind.config.js` - 自定义颜色、字体等

#### Vite + Vue (`vite-vue`)

**功能特点：**
- Vue 3 Composition API
- Vite 快速开发
- Tailwind CSS 样式
- 已配置相对路径

**关键配置：**
```javascript
// vite.config.js - 已配置相对路径
export default defineConfig({
  base: './',           // 相对路径，适合 Cloudflare Pages
  plugins: [vue()],
  build: {
    outDir: 'dist',
  },
});
```

#### 静态 HTML (`static-html`)

**功能特点：**
- 无需构建步骤
- 使用 Tailwind CDN
- 直接部署
- 适合落地页

**使用方法：**
```bash
# 编辑 index.html 然后部署
cp -r templates/static-html ./landing-page
# 编辑 landing-page/index.html
wrangler pages deploy landing-page --project-name=landing
```

### Claude Code 工作流程

在 Claude Code 中使用此 skill 时，它遵循结构化的工作流程：

#### 阶段 1：需求分析
- 分析你的请求
- 使用 EARS 语法创建用户故事
- 生成 `requirements.md`

#### 阶段 2：UI 设计
- 定义美学方向
- 创建配色方案和排版
- 生成 `design.md`

#### 阶段 3：项目初始化
- 复制合适的模板
- 配置项目设置
- 安装依赖

#### 阶段 4：代码开发
- 根据需求实现功能
- 遵循最佳实践
- 提供进度更新

#### 阶段 5：构建并部署
- 构建生产版本
- 部署到 Cloudflare Pages
- 提供部署 URL

#### 阶段 6：测试验证
- 运行质量检查
- 验证功能
- 报告任何问题

### 前置要求

- **Node.js** 18 或更高版本
- **npm** 或 **yarn** 或 **pnpm**
- **Wrangler CLI**（用于部署）：
  ```bash
  npm install -g wrangler
  ```
- **Cloudflare 账户**（免费套餐即可）

### 配置说明

#### Cloudflare Pages 设置

1. 在 https://dash.cloudflare.com 创建 Cloudflare 账户
2. 安装 Wrangler CLI：`npm install -g wrangler`
3. 登录：`wrangler login`
4. 部署：`wrangler pages deploy dist --project-name=your-project`

#### 自定义域名（可选）

1. 进入 Cloudflare Pages 控制台
2. 选择你的项目
3. 进入 Custom domains
4. 添加你的域名并按照 DNS 设置说明操作

### 常见问题

#### 构建错误

**"Module not found"**
```bash
# 解决方案：重新安装依赖
rm -rf node_modules package-lock.json
npm install
```

**"Type error"**
```bash
# 解决方案：检查 TypeScript 配置
# 确保 tsconfig.json 包含你的文件
```

#### 部署问题

**部署后 404**
- 检查构建输出目录（`dist` 或 `out`）
- 确保 vite.config.js 中有 `base: './'`
- 验证 next.config.js 中有 `output: 'export'`

**资源无法加载**
- 使用相对路径，不要用绝对路径
- 检查浏览器控制台的 404 错误
- 验证构建输出结构

### 贡献指南

欢迎贡献！请按照以下步骤：

1. Fork 仓库
2. 创建功能分支：`git checkout -b feature/my-feature`
3. 提交更改：`git commit -m 'Add my feature'`
4. 推送到分支：`git push origin feature/my-feature`
5. 创建 Pull Request

### 许可证

MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。
