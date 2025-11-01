# ⚡ Quick Railway Deployment Checklist

## ✅ Pre-Deployment Checklist

- [ ] All code changes committed to GitHub
- [ ] `saved_models/` folder with all model files committed
- [ ] Railway account created and linked to GitHub
- [ ] Frontend URL noted: `https://phish66.netlify.app`

## 🚀 5-Minute Deployment

### 1. Push to GitHub
```bash
git add .
git commit -m "Ready for Railway deployment"
git push origin main
```

### 2. Deploy on Railway
1. Go to https://railway.app
2. Click "New Project" → "Deploy from GitHub repo"
3. Select your `phishformer` repository
4. Wait for automatic deployment (3-5 minutes)

### 3. Configure Domain
1. Click on your service in Railway dashboard
2. Go to "Settings" → "Domains"
3. Click "Generate Domain"
4. Copy the URL (e.g., `https://phishformer-production.up.railway.app`)

### 4. Update Frontend
Update your frontend API URL to point to the Railway URL:

**Find this in your frontend code:**
```javascript
// Common locations:
// - src/config/api.js
// - src/lib/api.ts
// - src/utils/api.js
// - .env.local or .env.production

const API_URL = 'https://your-railway-url.up.railway.app';
```

### 5. Test
1. Visit https://phish66.netlify.app
2. Try the phishing detection feature
3. Check Railway logs if issues occur

## 🔗 Important URLs

- **Railway Dashboard:** https://railway.app/dashboard
- **Frontend (Netlify):** https://phish66.netlify.app
- **Backend (Railway):** `https://[your-domain].up.railway.app`
- **Health Check:** `https://[your-domain].up.railway.app/health`

## 🆘 Quick Fixes

**CORS Error?**
→ Check that `https://phish66.netlify.app` is in `ALLOWED_ORIGINS` in `app.py`

**502 Bad Gateway?**
→ Check Railway logs for errors, ensure app is running

**Model Not Loading?**
→ Verify `saved_models/` folder is committed to Git

**Build Fails?**
→ Check `requirements.txt` has all dependencies

## 📞 Support

- Railway Docs: https://docs.railway.app
- Railway Status: https://status.railway.app
- View Logs: Railway Dashboard → Your Service → Deployments
