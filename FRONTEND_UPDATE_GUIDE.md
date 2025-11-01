# 🔗 Frontend Update Guide - Connect to Railway Backend

## 📍 Current Configuration

Your frontend is currently configured to use: `http://localhost:5000`

**Location:** `components\detection\url-scanner.tsx` (line 38)

## 🔧 Required Changes

After deploying your backend to Railway, you need to update the API URL in your frontend.

### Step 1: Get Your Railway Backend URL

1. Deploy backend to Railway (follow `RAILWAY_DEPLOYMENT_GUIDE.md`)
2. In Railway dashboard, go to Settings → Domains
3. Generate a domain (e.g., `https://phishformer-production.up.railway.app`)
4. Copy this URL

### Step 2: Update Frontend Code

**File to modify:** `components/detection/url-scanner.tsx`

**Current code (line 38):**
```typescript
const API_URL = "http://localhost:5000"
```

**Update to:**
```typescript
const API_URL = "https://your-railway-app.up.railway.app"
```

**Example:**
```typescript
const API_URL = "https://phishformer-production.up.railway.app"
```

### Step 3: Use Environment Variables (Recommended)

For better configuration management, use environment variables:

#### Option A: Create `.env.local` file (for local development)
```env
NEXT_PUBLIC_API_URL=http://localhost:5000
```

#### Option B: Create `.env.production` file (for production)
```env
NEXT_PUBLIC_API_URL=https://your-railway-app.up.railway.app
```

#### Update `url-scanner.tsx`:
```typescript
const API_URL = process.env.NEXT_PUBLIC_API_URL || "http://localhost:5000"
```

### Step 4: Configure Netlify Environment Variables

1. Go to Netlify dashboard: https://app.netlify.com
2. Select your site: `phish66`
3. Go to **Site settings** → **Environment variables**
4. Add new variable:
   - **Key:** `NEXT_PUBLIC_API_URL`
   - **Value:** `https://your-railway-app.up.railway.app`
5. Click **Save**
6. **Trigger a new deploy** (Site settings → Deploys → Trigger deploy)

## 🧪 Testing

### Test Locally
```bash
# Set environment variable
$env:NEXT_PUBLIC_API_URL="https://your-railway-app.up.railway.app"

# Run dev server
npm run dev

# Test the URL scanner feature
```

### Test Production
1. Visit https://phish66.netlify.app
2. Try scanning a URL
3. Check browser console for any errors
4. Verify the request goes to your Railway backend

## 🔍 Verify API Endpoints

Test these endpoints directly in your browser:

1. **Health Check:**
   ```
   https://your-railway-app.up.railway.app/health
   ```
   Should return: `{"status": "healthy", ...}`

2. **Metrics:**
   ```
   https://your-railway-app.up.railway.app/metrics
   ```
   Should return model performance metrics

3. **API Info:**
   ```
   https://your-railway-app.up.railway.app/
   ```
   Should return API information

## 🐛 Troubleshooting

### CORS Error
**Error:** `Access to fetch at 'https://...' from origin 'https://phish66.netlify.app' has been blocked by CORS policy`

**Solution:** Your backend is already configured with CORS for `https://phish66.netlify.app`. If you still see this error:
1. Check Railway logs for CORS-related errors
2. Verify the URL in `ALLOWED_ORIGINS` in `app.py` matches exactly
3. Ensure you're using HTTPS (not HTTP) for the Railway URL

### Network Error
**Error:** `Failed to fetch` or `Network request failed`

**Solution:**
1. Verify Railway backend is running (check Railway dashboard)
2. Test the health endpoint directly in browser
3. Check browser console for detailed error messages
4. Verify the API URL is correct (no trailing slash)

### 502 Bad Gateway
**Error:** `502 Bad Gateway`

**Solution:**
1. Check Railway logs for application errors
2. Verify the backend started successfully
3. Check if Railway service is active

## 📋 Deployment Checklist

- [ ] Backend deployed to Railway
- [ ] Railway domain generated and copied
- [ ] Frontend code updated with Railway URL
- [ ] Environment variables set in Netlify
- [ ] Code committed and pushed to GitHub
- [ ] Netlify rebuild triggered
- [ ] Health endpoint tested
- [ ] URL scanner tested on production site
- [ ] No CORS errors in browser console

## 🎯 Quick Reference

**Frontend (Netlify):** https://phish66.netlify.app
**Backend (Railway):** https://your-railway-app.up.railway.app
**File to update:** `components/detection/url-scanner.tsx`
**Line number:** 38

---

**Next Steps:**
1. Deploy backend to Railway
2. Update frontend with Railway URL
3. Test thoroughly
4. Monitor Railway logs for any issues
