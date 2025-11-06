# GitHub Pages Setup Guide

## Fixing 404 Errors on GitHub Pages - ROOT FIX

The 404 errors are caused by incorrect base paths when GitHub Pages serves from a subdirectory. 

## Root Fix Applied

I've implemented a **proper build-time fix** (not a runtime workaround):

1. **Gulp Build Task** (`fixGitHubPages`): Fixes all paths in HTML files during build
2. **GitHub Actions Workflow**: Automatically builds and deploys with correct paths
3. **No JavaScript workarounds**: Paths are fixed at build time, not runtime

## GitHub Pages Configuration

### Automatic Deployment (Recommended)

1. Go to your repository Settings → Pages
2. Under "Source", select **"GitHub Actions"** (not "Deploy from a branch")
3. The workflow will automatically:
   - Build CSS
   - Fix all paths for GitHub Pages
   - Deploy to GitHub Pages

Your site will be available at: `https://yourusername.github.io/009-skydash/`

### Manual Build (Optional)

If you want to build manually:

```bash
cd template
npm install
export GITHUB_REPOSITORY="yourusername/009-skydash"  # Optional
npx gulp fixGitHubPages
```

Then configure GitHub Pages to serve from `/template` folder.

## Files Modified

- `template/gulpfile.js` - Added `fixGitHubPages` build task
- `.github/workflows/deploy-gh-pages.yml` - GitHub Actions workflow for automatic deployment
- `template/index.html` - Removed JavaScript workaround (clean HTML)

## Testing

After deploying:
1. Visit your GitHub Pages URL
2. Open browser DevTools (F12) → Network tab
3. Check that all resources (CSS, JS, images) load with status 200
4. Verify the page displays correctly

## Troubleshooting

If you still see 404 errors:

1. **Check the base path**: Open DevTools Console and run:
   ```javascript
   document.querySelector('base').href
   ```
   It should show your repository path (e.g., `/009-skydash/`)

2. **Clear browser cache**: Hard refresh (Ctrl+F5 or Cmd+Shift+R)

3. **Verify file structure**: Make sure all files are in the correct location relative to your GitHub Pages source folder

4. **Check GitHub Pages build**: Go to Settings → Pages and verify the site is published

## Additional Notes

- The base path script runs immediately when the page loads, before any resources are requested
- It automatically detects whether you're on GitHub Pages or local development
- For local development with `gulp serve`, it will use relative paths (`./`)

