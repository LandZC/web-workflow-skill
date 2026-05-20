---
name: web-workflow
description: Complete web development workflow from design to deployment. Covers requirements analysis, UI design, project scaffolding, code development, and Cloudflare Pages deployment. Use when building new web projects or developing features in existing web projects.
alwaysApply: false
---

## When to use this skill

Use this skill for **complete web development workflow** when you need to:

- Build a new web project from scratch (Next.js, Vite, Vue, React, etc.)
- Develop features in existing web projects
- Design and implement UI interfaces
- Deploy to Cloudflare Pages with CloudBase integration
- Initialize project scaffolding with proper configuration

**Do NOT use for:**
- Mini-program development (use miniprogram-development skill)
- Backend-only services (use cloudrun-development skill)
- Quick bug fixes that don't require full workflow

---

## How to use this skill (for a coding agent)

1. **Determine project type first**
   - New project: Follow Phase 1-5 completely
   - Existing project: Skip to Phase 3 (Development) or Phase 4 (Build & Deploy)

2. **Follow the workflow phases**
   - Each phase must be completed before moving to next
   - Get user confirmation at key checkpoints

3. **Use templates for new projects**
   - Available templates in `templates/` directory
   - Copy template and customize based on requirements

4. **Deploy to Cloudflare Pages**
   - Always use Cloudflare Pages for deployment
   - Configure proper build commands and output directories

---

# Web Workflow - Complete Development Process

## Overview

This skill provides a complete web development workflow covering:
1. Requirements Analysis & Task Planning
2. UI Design & Specification
3. Project Initialization (for new projects)
4. Code Development & Debugging
5. Build & Deploy to Cloudflare Pages

---

## Phase 1: Requirements Analysis

**Purpose:** Understand what needs to be built and create clear acceptance criteria.

**Steps:**
1. Analyze user's request and clarify ambiguities
2. Define user stories and acceptance criteria using EARS syntax
3. Save requirements to `specs/[project-name]/requirements.md`

**EARS Syntax Format:**
```
While <optional precondition>, when <optional trigger>, the <system> shall <response>
```

**Output:**
```markdown
# Requirements Document

## Introduction
[Project description]

## Requirements

### Requirement 1 - [Name]
**User Story:** As a [user], I want [feature] so that [benefit]

#### Acceptance Criteria
1. While [precondition], when [trigger], the system shall [response]
2. ...
```

---

## Phase 2: UI Design

**Purpose:** Design the visual interface and user experience.

**Steps:**
1. Analyze user needs and core interaction logic
2. Define aesthetic direction (reference ui-design skill for detailed rules)
3. Create high-fidelity UI specification
4. Save to `specs/[project-name]/design.md`

**Design Specification Format:**
```markdown
# Design Specification

## Purpose Statement
[2-3 sentences about problem/users/context]

## Aesthetic Direction
[Choose one: Brutally minimal / Maximalist chaos / Retro-futuristic / Organic / Luxury / Playful / Editorial / Art deco / Soft pastel / Industrial]

## Color Palette
- Primary: [hex code]
- Secondary: [hex code]
- Accent: [hex code]
- Background: [hex code]
- Text: [hex code]

## Typography
- Heading: [font name]
- Body: [font name]

## Layout Strategy
[Asymmetric/Diagonal/Overlapping approach]

## Key Screens
1. [Screen 1]: [Description]
2. [Screen 2]: [Description]
```

---

## Phase 3: Project Initialization (New Projects Only)

**Purpose:** Set up project scaffolding with proper configuration.

**Available Templates:**

### Template 1: Next.js + Tailwind (Recommended for most projects)
```bash
# Location: templates/nextjs-tailwind/
# Features: Next.js 14, Tailwind CSS, App Router, CloudBase SDK ready
```

### Template 2: Vite + Vue/React (Lightweight option)
```bash
# Location: templates/vite-vue/ or templates/vite-react/
# Features: Vite, Vue 3/React 18, Tailwind CSS, minimal setup
```

### Template 3: Static HTML (Simplest)
```bash
# Location: templates/static-html/
# Features: Plain HTML/CSS/JS, no build step needed
```

**Initialization Steps:**
1. Choose appropriate template based on requirements
2. Copy template to target directory
3. Update `package.json` with project name and dependencies
4. Configure `vite.config.js` or `next.config.js` as needed
5. Set up CloudBase SDK integration if required

---

## Phase 4: Code Development

**Purpose:** Implement the actual code based on requirements and design.

**Development Rules:**

### File Structure
```
project/
├── src/              # Source code
├── public/           # Static assets
├── package.json      # Dependencies
├── vite.config.js    # Vite config (if using Vite)
└── next.config.js    # Next.js config (if using Next.js)
```

### Code Standards
1. **Components:** Split into reusable components in `src/components/`
2. **Pages:** Organize by routes in `src/pages/` or `app/`
3. **Styles:** Use Tailwind CSS utility classes
4. **Icons:** Use lucide-react (Web) or professional icon libraries
5. **State:** Use React hooks or Zustand for state management

### CloudBase Integration (if needed)
```javascript
// Initialize CloudBase
import cloudbase from "@cloudbase/js-sdk";

const app = cloudbase.init({
  env: "your-env-id"  // Use envQuery tool to get this
});

const auth = app.auth();
const db = app.database();
```

### Development Workflow
1. Start dev server: `npm run dev`
2. Implement features incrementally
3. Test each feature before moving to next
4. Fix issues immediately when found

---

## Phase 5: Build & Deploy to Cloudflare Pages

**Purpose:** Build the project and deploy to production.

### Build Configuration

#### For Next.js Projects
```javascript
// next.config.js
module.exports = {
  output: 'export',  // Static export for Cloudflare Pages
  images: {
    unoptimized: true,  // Required for static export
  },
};
```

#### For Vite Projects
```javascript
// vite.config.js
export default defineConfig({
  base: './',  // Relative paths for Cloudflare Pages
  build: {
    outDir: 'dist',
  },
});
```

### Build Steps
1. Install dependencies: `npm install`
2. Run build: `npm run build`
3. Verify build output directory:
   - Next.js: `out/`
   - Vite: `dist/`

### Deploy to Cloudflare Pages

**Option A: Via Wrangler CLI (Recommended)**
```bash
# Install Wrangler if not installed
npm install -g wrangler

# Login to Cloudflare
wrangler login

# Deploy
wrangler pages deploy dist --project-name=your-project-name
```

**Option B: Via Cloudflare Dashboard**
1. Go to Cloudflare Pages dashboard
2. Click "Create a project"
3. Connect to Git repository or upload direct
4. Configure build settings:
   - Build command: `npm run build`
   - Build output directory: `dist` or `out`
5. Deploy

### Post-Deployment
1. Verify deployment URL works
2. Test all critical functionality
3. Check console for errors
4. Share deployment URL with user

---

## Phase 6: Testing & Verification

**Purpose:** Ensure everything works correctly.

**Testing Checklist:**
1. [ ] All pages load correctly
2. [ ] Navigation works as expected
3. [ ] Forms submit properly
4. [ ] API calls succeed (if applicable)
5. [ ] Responsive design works on mobile
6. [ ] No console errors
7. [ ] Performance is acceptable

**Testing Tools:**
- Use Playwright for automated testing (if configured)
- Manual testing in browser
- Check Cloudflare Pages analytics

---

## Quick Reference Commands

### Development
```bash
npm run dev          # Start dev server
npm run build        # Build for production
npm run preview      # Preview build locally
```

### Deployment
```bash
wrangler pages deploy dist --project-name=xxx  # Deploy to Cloudflare
wrangler pages project list                     # List projects
wrangler pages deployment list --project-name=xxx  # List deployments
```

### CloudBase (if using)
```bash
# Use envQuery tool to get environment info
# Use manageHosting for static hosting operations
```

---

## Troubleshooting

### Common Issues

**Build fails with "Module not found"**
- Run `npm install` to ensure all dependencies are installed

**Cloudflare Pages shows 404**
- Check build output directory is correct
- Ensure `base: './'` in vite.config.js for relative paths

**Static assets not loading**
- Verify `publicPath` or `base` is configured correctly
- Use relative paths (`./`) instead of absolute paths

**CloudBase SDK errors**
- Verify environment ID is correct using envQuery tool
- Ensure SDK is initialized before making calls

---

## Template Usage Guide

When creating a new project from template:

1. **Copy template directory**
   ```bash
   cp -r templates/nextjs-tailwind/ ./my-new-project
   cd my-new-project
   ```

2. **Update project configuration**
   - Edit `package.json`: Update name, description
   - Edit config files: Set correct paths and options

3. **Install dependencies**
   ```bash
   npm install
   ```

4. **Start development**
   ```bash
   npm run dev
   ```

5. **When ready to deploy**
   ```bash
   npm run build
   wrangler pages deploy dist --project-name=your-project
   ```
