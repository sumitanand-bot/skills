# Web Artifacts Builder Steering

## Metadata

- **Name**: web-artifacts-builder
- **Description**: Suite of tools for creating elaborate, multi-component claude.ai HTML artifacts using modern frontend web technologies (React, Tailwind CSS, shadcn/ui). Use for complex artifacts requiring state management, routing, or shadcn/ui components - not for simple single-file HTML/JSX artifacts.

## Triggers

Use this steering when:
- User wants to create complex frontend artifacts
- User needs React with state management or routing
- User requests shadcn/ui components
- User mentions "multi-component" or "elaborate" HTML artifacts
- User wants to build Claude.ai artifacts with modern frontend stack

## Instructions

To build powerful frontend claude.ai artifacts, follow these steps:
1. Initialize the frontend repo using `scripts/init-artifact.sh`
2. Develop your artifact by editing the generated code
3. Bundle all code into a single HTML file using `scripts/bundle-artifact.sh`
4. Display artifact to user
5. (Optional) Test the artifact

**Stack**: React 18 + TypeScript + Vite + Parcel (bundling) + Tailwind CSS + shadcn/ui

### Design & Style Guidelines

**VERY IMPORTANT**: To avoid what is often referred to as "AI slop", avoid using excessive centered layouts, purple gradients, uniform rounded corners, and Inter font.

### Step 1: Initialize Project

```bash
bash scripts/init-artifact.sh <project-name>
cd <project-name>
```

This creates a fully configured project with:
- ✅ React + TypeScript (via Vite)
- ✅ Tailwind CSS 3.4.1 with shadcn/ui theming system
- ✅ Path aliases (`@/`) configured
- ✅ 40+ shadcn/ui components pre-installed
- ✅ All Radix UI dependencies included
- ✅ Parcel configured for bundling

### Step 2: Develop Your Artifact

Edit the generated files. See project structure for guidance.

### Step 3: Bundle to Single HTML File

```bash
bash scripts/bundle-artifact.sh
```

This creates `bundle.html` - a self-contained artifact with all JavaScript, CSS, and dependencies inlined.

**Requirements**: Your project must have an `index.html` in the root directory.

**What the script does**:
- Installs bundling dependencies
- Creates `.parcelrc` config with path alias support
- Builds with Parcel (no source maps)
- Inlines all assets into single HTML

### Step 4: Share Artifact with User

Share the bundled HTML file in conversation so they can view it as an artifact.

### Step 5: Testing (Optional)

Only perform if necessary or requested. Use available tools (Playwright, Puppeteer) to test. Avoid testing upfront as it adds latency.

## Resources

- `skills/web-artifacts-builder/scripts/init-artifact.sh` - Project initialization
- `skills/web-artifacts-builder/scripts/bundle-artifact.sh` - HTML bundling
- `skills/web-artifacts-builder/scripts/shadcn-components.tar.gz` - Pre-packaged components
- **shadcn/ui docs**: https://ui.shadcn.com/docs/components
