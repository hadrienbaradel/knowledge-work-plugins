---
name: frontend-verification
description: Verify frontend code by testing in Chrome desktop and mobile views. Use after writing or modifying frontend code to ensure visual correctness, responsive behavior, and functionality across viewports.
---

# Frontend Verification Skill

Comprehensive frontend testing workflow that automatically verifies code changes by opening Chrome, testing desktop and mobile views, and providing a detailed verification checklist.

## When to Use This Skill

Use this skill after:
- Writing new UI components or pages
- Modifying existing frontend code (HTML, CSS, JavaScript, React, Vue, etc.)
- Updating responsive layouts or media queries
- Changing styles, animations, or interactions
- Fixing visual bugs or UI issues
- Implementing new features with visual components

## Verification Workflow

### 1. Pre-Launch Code Review

Before opening the browser, perform a quick code audit:

**HTML/JSX Structure:**
- [ ] Semantic HTML elements used appropriately
- [ ] Proper heading hierarchy (h1 → h2 → h3)
- [ ] Alt text on all images
- [ ] ARIA labels for interactive elements
- [ ] Form inputs have associated labels
- [ ] No inline styles (use CSS classes)

**CSS/Styling:**
- [ ] Responsive units (rem, em, %, vh/vw) instead of fixed px
- [ ] Mobile-first media queries
- [ ] CSS custom properties for theme values
- [ ] No !important flags (or well-justified)
- [ ] Consistent naming convention (BEM, utility classes, etc.)

**JavaScript/Framework:**
- [ ] Console.log statements removed
- [ ] Error handling for async operations
- [ ] Loading states for data fetching
- [ ] No hardcoded API endpoints or credentials
- [ ] Event listeners properly cleaned up
- [ ] Accessibility: keyboard navigation works

### 2. Development Server Launch

**Determine the dev server command:**
- Next.js: `npm run dev` (usually port 3000)
- Vite/React: `npm run dev` (usually port 5173)
- Vue: `npm run serve` (usually port 8080)
- Create React App: `npm start` (usually port 3000)
- Custom: Check package.json scripts

**Launch sequence:**
```bash
# Start the dev server in the background
npm run dev &

# Wait for server to be ready (adjust URL as needed)
sleep 3
curl -s http://localhost:3000 > /dev/null && echo "Server ready"

# Open Chrome with the application
open -a "Google Chrome" http://localhost:3000
```

### 3. Desktop View Testing

Once Chrome opens, verify the following:

**Visual Inspection:**
- [ ] Layout matches design/expectations
- [ ] All images load correctly
- [ ] Fonts render properly (no flash of unstyled text)
- [ ] Colors match design system
- [ ] Spacing and alignment correct
- [ ] Animations play smoothly
- [ ] No horizontal scroll at default viewport

**Functional Testing:**
- [ ] All links navigate correctly
- [ ] Buttons trigger expected actions
- [ ] Forms validate input properly
- [ ] Dropdown menus work
- [ ] Modals/dialogs open and close
- [ ] Hover states appear correctly
- [ ] Click interactions work

**Console Check:**
- [ ] No JavaScript errors in console (F12 → Console)
- [ ] No 404 errors for resources
- [ ] No CORS errors
- [ ] No React/Vue warnings

**Performance Check:**
- [ ] Initial page load feels fast
- [ ] No layout shift during load
- [ ] Images lazy-load if applicable
- [ ] Smooth scrolling

### 4. Mobile View Testing

**Using Chrome DevTools Device Emulation:**

```bash
# Open Chrome DevTools with device toolbar enabled
# Keyboard: Cmd+Option+I (Mac) or F12 (Windows/Linux)
# Then: Cmd+Shift+M (Mac) or Ctrl+Shift+M (Windows/Linux)
```

**Test Common Mobile Viewports:**

1. **iPhone 12 Pro (390 × 844)**
   - [ ] Navigation menu accessible (hamburger menu works)
   - [ ] Text readable without zooming
   - [ ] Buttons/tap targets minimum 44×44px
   - [ ] No horizontal scroll
   - [ ] Images scale appropriately

2. **iPhone SE (375 × 667)** - Small screen test
   - [ ] Content doesn't overflow
   - [ ] Font sizes still readable
   - [ ] Forms usable on small screen

3. **iPad Air (820 × 1180)** - Tablet test
   - [ ] Layout adapts appropriately (not just stretched mobile)
   - [ ] Multi-column layouts work if designed

4. **Responsive Width Test**
   - [ ] Drag viewport from 320px to 1920px
   - [ ] No awkward breakpoints where layout breaks
   - [ ] Elements resize/reflow smoothly

**Touch Interaction Testing:**
- [ ] Tap targets are large enough (min 44×44px)
- [ ] No hover-dependent functionality (must work on touch)
- [ ] Swipe gestures work if implemented
- [ ] Pinch-to-zoom works (unless intentionally disabled)

**Mobile-Specific Issues:**
- [ ] Fixed positioning works (header/footer don't overlap content)
- [ ] Keyboard appearance doesn't break layout
- [ ] Safe areas respected (iPhone notch, etc.)

### 5. Cross-Browser Testing Commands

**Open in multiple browsers for thorough testing:**

```bash
# macOS
open -a "Google Chrome" http://localhost:3000
open -a "Safari" http://localhost:3000
open -a "Firefox" http://localhost:3000

# Linux
google-chrome http://localhost:3000 &
firefox http://localhost:3000 &

# Windows (PowerShell)
Start-Process "chrome" "http://localhost:3000"
Start-Process "firefox" "http://localhost:3000"
```

**Critical browsers to test:**
- Chrome (most users)
- Safari (different rendering engine, iOS users)
- Firefox (standards compliance)

### 6. Automated Testing Scripts

For repeated verification, use these helper scripts:

**Quick Visual Regression (requires Playwright):**
```bash
# Install if needed
npm install -D @playwright/test

# Create quick test
cat > tests/visual-check.spec.js << 'EOF'
import { test, expect } from '@playwright/test';

test('homepage visual check', async ({ page }) => {
  await page.goto('http://localhost:3000');

  // Desktop screenshot
  await page.setViewportSize({ width: 1920, height: 1080 });
  await expect(page).toHaveScreenshot('homepage-desktop.png');

  // Mobile screenshot
  await page.setViewportSize({ width: 390, height: 844 });
  await expect(page).toHaveScreenshot('homepage-mobile.png');
});
EOF

npx playwright test --update-snapshots
```

**Accessibility Audit (using axe-core):**
```bash
npm install -D @axe-core/cli

# Run accessibility audit
npx axe http://localhost:3000 --exit
```

**Lighthouse Performance Check:**
```bash
# Install if needed
npm install -g lighthouse

# Run Lighthouse
lighthouse http://localhost:3000 --view --only-categories=performance,accessibility,best-practices
```

### 7. Final Verification Checklist

Before marking the task complete:

**Code Quality:**
- [ ] Code linted (no ESLint errors)
- [ ] TypeScript types correct (if applicable)
- [ ] No unused imports or variables
- [ ] Comments added for complex logic

**Functionality:**
- [ ] All user flows tested end-to-end
- [ ] Error states handled gracefully
- [ ] Loading states implemented
- [ ] Success/failure messages shown

**Responsive Design:**
- [ ] Works on mobile (320px+)
- [ ] Works on tablet (768px+)
- [ ] Works on desktop (1024px+)
- [ ] Works on large screens (1920px+)

**Accessibility:**
- [ ] Keyboard navigation works
- [ ] Screen reader friendly
- [ ] Color contrast passes WCAG AA
- [ ] Focus states visible

**Performance:**
- [ ] No console errors
- [ ] No memory leaks
- [ ] Images optimized
- [ ] Bundle size reasonable

**Browser Compatibility:**
- [ ] Tested in Chrome
- [ ] Tested in Safari (or similar webkit)
- [ ] Tested in Firefox (optional but recommended)

## Common Issues and Solutions

### Issue: "Address already in use" (port conflict)

```bash
# Find and kill process on port 3000 (adjust port as needed)
lsof -ti:3000 | xargs kill -9

# Or use a different port
PORT=3001 npm run dev
```

### Issue: Changes not reflecting in browser

```bash
# Clear build cache and restart
rm -rf .next/ # Next.js
rm -rf dist/ # Vite
rm -rf build/ # CRA
npm run dev
```

### Issue: Chrome not opening

```bash
# macOS: Check if Chrome is installed
ls /Applications/ | grep Chrome

# Linux: Check Chrome path
which google-chrome

# Windows: Check Program Files
dir "C:\Program Files\Google\Chrome\Application\chrome.exe"
```

### Issue: Mobile viewport not matching real device

- Chrome DevTools emulation is good but not perfect
- For critical mobile testing, use real devices or BrowserStack
- Test on actual iOS and Android devices before production

## Quick Reference: Browser DevTools Shortcuts

**Chrome/Firefox:**
- `F12` or `Cmd+Option+I`: Open DevTools
- `Cmd+Shift+M` (Mac) / `Ctrl+Shift+M`: Toggle device toolbar
- `Cmd+Shift+C`: Inspect element
- `Cmd+Option+J`: Console
- `Cmd+R`: Reload
- `Cmd+Shift+R`: Hard reload (clear cache)

**Safari:**
- `Cmd+Option+I`: Web Inspector
- `Cmd+Option+C`: Console
- Settings → Advanced → "Show Develop menu" to enable dev tools

## Integration with CI/CD

For automated verification in pipelines:

```yaml
# .github/workflows/frontend-test.yml
name: Frontend Verification
on: [push, pull_request]

jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm ci
      - run: npm run build
      - run: npm run test
      - run: npx playwright test
      - run: npm run lint
```

## Best Practices

1. **Test Early, Test Often**: Run verification after every significant change
2. **Use Real Devices**: DevTools emulation is good for development, but test on real phones before release
3. **Automate When Possible**: Set up Playwright/Cypress for regression testing
4. **Document Edge Cases**: If something is tricky to test, add notes for future verification
5. **Performance Budget**: Set thresholds (e.g., "page load < 2s") and fail if exceeded
6. **Accessibility First**: Use automated tools (axe, Lighthouse) but also manual keyboard testing

## Workflow Automation

**Create a verification script:**

```bash
#!/bin/bash
# save as verify-frontend.sh

echo "🔍 Starting Frontend Verification..."

# 1. Code quality
echo "✓ Running linter..."
npm run lint || exit 1

# 2. Type check (if TypeScript)
if [ -f "tsconfig.json" ]; then
  echo "✓ Type checking..."
  npx tsc --noEmit || exit 1
fi

# 3. Unit tests
echo "✓ Running tests..."
npm test -- --watchAll=false || exit 1

# 4. Build check
echo "✓ Building production..."
npm run build || exit 1

# 5. Start dev server
echo "✓ Starting dev server..."
npm run dev &
DEV_PID=$!
sleep 5

# 6. Open Chrome
echo "✓ Opening Chrome..."
open -a "Google Chrome" http://localhost:3000

# 7. Run accessibility audit
echo "✓ Running accessibility audit..."
npx axe http://localhost:3000

echo "✅ Automated checks passed!"
echo "📱 Please manually verify mobile views in Chrome DevTools"
echo "🛑 Press Ctrl+C when done to stop dev server"

# Wait for user
wait $DEV_PID
```

Make it executable:
```bash
chmod +x verify-frontend.sh
./verify-frontend.sh
```
