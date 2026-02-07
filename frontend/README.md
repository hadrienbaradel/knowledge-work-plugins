# Frontend Plugin

Frontend development and verification tools for Claude Code.

## Overview

The frontend plugin helps you write, test, and verify UI code with comprehensive browser testing workflows and SEO optimization. Verify frontend changes in Chrome, ensure responsive design, optimize content for search engines, and validate factual accuracy.

## Skills

### frontend-verification

Comprehensive verification workflow that:
- Reviews code quality before testing
- Launches development server
- Opens Chrome for visual testing
- Tests desktop viewport
- Tests mobile viewports (phone and tablet)
- Checks accessibility
- Runs performance audits
- Provides detailed checklists

**Use when:**
- After writing new UI components
- After modifying existing frontend code
- After changing responsive layouts
- After fixing visual bugs
- Before committing frontend changes

**Example usage:**
```
"Verify the login page in Chrome and mobile"
"Test the new navigation menu across viewports"
"Check if the dashboard is responsive"
```

### seo-verification

Complete SEO audit and content verification that:
- Checks meta tags and technical SEO setup
- Analyzes keyword optimization
- Verifies content quality and readability
- Fact-checks claims with authoritative sources
- Validates schema markup (JSON-LD)
- Assesses E-E-A-T signals (Experience, Expertise, Authoritativeness, Trustworthiness)
- Audits images and internal/external links
- Tests mobile-friendliness and page speed
- Provides automated audit scripts

**Use when:**
- After publishing new articles or blog posts
- Before launching landing pages
- After updating existing content
- When optimizing for search engines
- Before submitting content for review
- After making significant content changes

**Example usage:**
```
"Audit the SEO of the lice removal guide article"
"Verify the blog post has proper meta tags and facts are sourced"
"Check if the landing page is optimized for search engines"
"Fact-check all claims in the medical article"
```

## Installation

This plugin is part of the knowledge-work-plugins repository. Install via Claude Code:

```bash
claude install frontend
```

Or add to your `.claude.json`:

```json
{
  "plugins": [
    "frontend@knowledge-work-plugins"
  ]
}
```

## Requirements

- Node.js and npm (for running dev servers)
- Google Chrome (for testing)
- Optional: Firefox, Safari for cross-browser testing
- Optional: Playwright for automated testing
- Optional: axe-core-cli for accessibility audits

## Configuration

No configuration required. The plugin detects your dev server setup from `package.json`.

Supported frameworks:
- React (Create React App, Vite, Next.js)
- Vue (Vue CLI, Vite)
- Svelte (SvelteKit, Vite)
- Angular
- Any framework with a local dev server

## Features

### Automated Browser Launch
- Automatically opens Chrome to your local dev server
- Supports custom ports and URLs
- Cross-platform (macOS, Linux, Windows)

### Mobile Testing
- Guides through Chrome DevTools device emulation
- Tests common mobile viewports (iPhone, iPad, etc.)
- Verifies touch targets and responsive behavior

### Verification Checklists
- Pre-launch code review
- Visual inspection
- Functional testing
- Console error checking
- Accessibility validation
- Performance checks

### Automation Scripts
- Quick setup for Playwright visual regression
- Accessibility audits with axe-core
- Lighthouse performance checks
- CI/CD integration templates

## Best Practices

1. **Run verification after every UI change** - Catch visual bugs early
2. **Test on real devices when possible** - DevTools emulation is good but not perfect
3. **Automate regression tests** - Use Playwright for critical user flows
4. **Check accessibility** - Use automated tools + manual keyboard testing
5. **Monitor performance** - Set budgets and track over time

## Troubleshooting

### Port conflicts
If your dev server port is in use:
```bash
lsof -ti:3000 | xargs kill -9
```

### Chrome won't open
Verify Chrome is installed:
```bash
# macOS
ls /Applications/ | grep Chrome

# Linux
which google-chrome
```

### Changes not reflecting
Clear build cache:
```bash
rm -rf .next/ dist/ build/
npm run dev
```

## Contributing

This is a personal fork of knowledge-work-plugins. To contribute:

1. Make changes in your local plugin directory
2. Test thoroughly with real projects
3. Commit and push to your fork
4. Consider contributing improvements back to the upstream repo

## License

Apache 2.0 - See LICENSE file for details
