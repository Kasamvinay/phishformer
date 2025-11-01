# 🚂 Railway Deployment Guide for Phishing Detection Backend

## 📋 Prerequisites
- GitHub account
- Railway account (sign up at https://railway.app)
- Your backend code pushed to a GitHub repository

## 🎯 Step-by-Step Deployment Process

### Step 1: Prepare Your Repository

1. **Ensure all required files are in your repository:**
   - ✅ `app.py` (Flask application)
   - ✅ `requirements.txt` (Python dependencies)
   - ✅ `Procfile` (Railway start command)
   - ✅ `runtime.txt` (Python version)
   - ✅ `railway.json` (Railway configuration)
   - ✅ `saved_models/` folder with all model files

2. **Commit and push all changes to GitHub:**
   ```bash
   git add .
   git commit -m "Prepare for Railway deployment"
   git push origin main
   ```

### Step 2: Create Railway Project

1. **Go to Railway:** https://railway.app
2. **Sign in** with your GitHub account
3. **Click "New Project"**
4. **Select "Deploy from GitHub repo"**
5. **Choose your repository** (`phishformer`)
6. **Railway will automatically detect** it's a Python project

### Step 3: Configure Environment Variables

1. **In your Railway project dashboard**, click on your service
2. **Go to "Variables" tab**
3. **Add the following environment variables:**
   ```
   FLASK_ENV=production
   PORT=5000
   PYTHONUNBUFFERED=1
   ```

### Step 4: Deploy

1. **Railway will automatically start deploying** after you connect the repo
2. **Monitor the build logs** in the "Deployments" tab
3. **Wait for deployment to complete** (usually 3-5 minutes)
4. **Once deployed**, you'll see a green "Active" status

### Step 5: Get Your Backend URL

1. **In the Railway dashboard**, click on your service
2. **Go to "Settings" tab**
3. **Scroll to "Domains" section**
4. **Click "Generate Domain"**
5. **Copy the generated URL** (e.g., `https://your-app.up.railway.app`)

### Step 6: Update Frontend Configuration

1. **Open your frontend code** (deployed on Netlify)
2. **Find where you make API calls** (usually in a config file or API service file)
3. **Update the backend URL** from `http://localhost:5000` to your Railway URL
4. **Example:**
   ```javascript
   // Before
   const API_URL = 'http://localhost:5000';
   
   // After
   const API_URL = 'https://your-app.up.railway.app';
   ```
5. **Commit and push changes** to trigger Netlify rebuild

### Step 7: Test Your Deployment

1. **Open your frontend:** https://phish66.netlify.app
2. **Test the phishing detection feature**
3. **Check Railway logs** if you encounter any issues

## 🔧 Important Configuration Details

### CORS Configuration
Your backend is already configured to accept requests from:
- `https://phish66.netlify.app` (your production frontend)
- `http://localhost:3000` (local development)
- `http://localhost:5000` (local backend testing)

### Port Configuration
Railway automatically assigns a port via the `PORT` environment variable. Your `app.py` is configured to use this.

### Model Files
Ensure your `saved_models/` directory contains:
- `phishing_model.keras` or `phishing_model.h5`
- `scaler_url.pkl`
- `scaler_html.pkl`
- `feature_config.pkl`
- `metrics.pkl`

## 🐛 Troubleshooting

### Deployment Fails
- **Check build logs** in Railway dashboard
- **Verify all dependencies** are in `requirements.txt`
- **Ensure model files** are committed to Git (not too large)

### CORS Errors
- **Verify your frontend URL** is in the `ALLOWED_ORIGINS` list in `app.py`
- **Check Railway logs** for CORS-related errors

### Model Loading Errors
- **Ensure `saved_models/` folder** is in your repository
- **Check file sizes** - Railway has storage limits
- **Verify file paths** in `app.py`

### 502 Bad Gateway
- **Check if the app is running** in Railway logs
- **Verify PORT environment variable** is set
- **Check memory usage** - upgrade plan if needed

## 📊 Monitoring

1. **Railway Dashboard** - View deployment status, logs, and metrics
2. **Health Check Endpoint** - `https://your-app.up.railway.app/health`
3. **Metrics Endpoint** - `https://your-app.up.railway.app/metrics`

## 💰 Pricing

Railway offers:
- **Free tier**: $5 credit per month
- **Pro plan**: $20/month with more resources
- Your app should run fine on the free tier for testing

## 🔄 Continuous Deployment

Railway automatically redeploys when you push to your GitHub repository:
1. Make changes to your code
2. Commit and push to GitHub
3. Railway automatically detects changes and redeploys

## 🎉 You're Done!

Your backend is now live on Railway and connected to your Netlify frontend!

**Backend URL:** `https://your-app.up.railway.app`
**Frontend URL:** `https://phish66.netlify.app`

## 📝 Next Steps

1. **Test all API endpoints** thoroughly
2. **Monitor Railway logs** for any errors
3. **Set up custom domain** (optional)
4. **Configure alerts** for downtime (optional)
5. **Optimize performance** based on usage patterns

---

**Need Help?**
- Railway Docs: https://docs.railway.app
- Railway Discord: https://discord.gg/railway
- Check Railway logs for detailed error messages
