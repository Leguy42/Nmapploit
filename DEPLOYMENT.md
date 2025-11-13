# Nmap Exploit Analyzer - Web Deployment Guide

## Quick Start: Deploy in 3 Minutes

### Option 1: Vercel (Recommended - Fastest & Free)

**Step 1:** Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/nmap-exploit-analyzer.git
git push -u origin main
```

**Step 2:** Deploy to Vercel
1. Go to https://vercel.com
2. Click "New Project"
3. Select your GitHub repository
4. Click "Deploy"
5. Share the auto-generated link with anyone!

**Example link:** `https://nmap-exploit-analyzer-abc123.vercel.app`

---

### Option 2: Netlify (Free & Easy)

**Step 1:** Connect GitHub
1. Go to https://netlify.com
2. Click "New site from Git"
3. Connect GitHub account
4. Select repository
5. Build settings auto-configured ✓

**Step 2:** Deploy
- Netlify automatically deploys on every push
- Share the auto-generated URL

**Example link:** `https://nmap-exploit-analyzer.netlify.app`

---

### Option 3: GitHub Pages (Free)

**Step 1:** Update vite.config.ts
```typescript
export default {
  base: '/nmap-exploit-analyzer/',
  // ... rest of config
}
```

**Step 2:** Deploy
```bash
npm run build
git add dist/
git commit -m "Deploy to GitHub Pages"
git push
```

**Step 3:** Enable in Settings
- Go to repo Settings → Pages
- Select "main branch /docs folder" (if built to docs/)
- Your site: `https://YOUR_USERNAME.github.io/nmap-exploit-analyzer`

---

### Option 4: Docker Container (Self-Hosted)

**Dockerfile:**
```dockerfile
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM node:18-alpine
WORKDIR /app
RUN npm install -g serve
COPY --from=builder /app/dist ./dist
EXPOSE 3000
CMD ["serve", "-s", "dist", "-l", "3000"]
```

**Build & Run:**
```bash
docker build -t nmap-analyzer .
docker run -p 3000:3000 nmap-analyzer
```

---

### Option 5: AWS S3 + CloudFront (Scalable)

**Deploy to S3:**
```bash
npm run build

# Install AWS CLI if needed: brew install awscli

aws s3 sync dist/ s3://your-bucket-name/ --delete
aws cloudfront create-invalidation --distribution-id YOUR_DIST_ID --paths "/*"
```

---

## Local Build & Test Before Deploying

**Build for production:**
```bash
npm install
npm run build
```

**Test the build locally:**
```bash
npm run preview
```

Then visit `http://localhost:4173` to see your app.

---

## Deployment Checklist

- [ ] All dependencies installed: `npm install`
- [ ] Build successful: `npm run build`
- [ ] Local preview works: `npm run preview`
- [ ] Git repository created and pushed
- [ ] Hosting platform connected (Vercel/Netlify)
- [ ] Auto-deployment enabled
- [ ] Link tested in new browser/incognito
- [ ] Link shared with users

---

## Post-Deployment Configuration

### Custom Domain (Optional)
- **Vercel:** Settings → Domains → Add domain
- **Netlify:** Site settings → Domain management → Add domain
- Both support free HTTPS

### Analytics
- **Vercel:** Built-in analytics in dashboard
- **Netlify:** Built-in analytics in dashboard
- **Custom:** Add tracking code to index.html

### Environment Variables
If you add environment variables later:

```bash
# .env file (add to .gitignore)
VITE_API_KEY=your_key_here
```

In code:
```javascript
const apiKey = import.meta.env.VITE_API_KEY;
```

---

## Troubleshooting

**Build fails:**
```bash
rm -rf node_modules package-lock.json
npm install
npm run build
```

**Blank page after deploy:**
- Check browser console for errors (F12)
- Verify CSS loading (check Network tab)
- Ensure all assets have correct paths

**Link shares don't work:**
- Use HTTPS link (not HTTP)
- Test in incognito/private window
- Ensure deployment finished (check status)

---

## Share Your App

Once deployed, share links like:
- **Anyone can use:** Just send the link!
- **Paste scan data** or **upload .txt files** directly
- **No installation needed** - works on any device with a browser

Example: `https://your-app-link.vercel.app`

---

## Performance Tips

The built app is already optimized:
- ✓ Code splitting by Vite
- ✓ CSS minified & tree-shaken
- ✓ React optimized production build
- ✓ Gzip compression on most hosts

Average file size: ~200KB (minified + gzipped)
Page load time: <2 seconds on average connection

---

## Questions?

- Vercel docs: https://vercel.com/docs
- Netlify docs: https://docs.netlify.com
- Vite docs: https://vitejs.dev/guide/static-deploy.html
