# Deployment Guide - Render

## Quick Deploy Steps

### 1. Sign Up / Log In to Render
- Go to [render.com](https://render.com)
- Sign up with your GitHub account (Hijanhv)

### 2. Create a New Web Service
- Click **"New +"** → **"Web Service"**
- Connect your GitHub repository: `Hijanhv/chatify`
- Click **"Connect"**

### 3. Configure the Service
Render will auto-detect the `render.yaml` file, but verify these settings:

**Basic Settings:**
- Name: `chatify` (or your preferred name)
- Region: `Oregon (US West)` (or closest to you)
- Branch: `main`
- Runtime: `Node`
- Build Command: `npm install && npm run build`
- Start Command: `npm run start`
- Plan: **Free**

### 4. Set Environment Variables
Click **"Environment"** tab and add these variables:

**Required:**
```
MONGO_URI=your_mongodb_connection_string
RESEND_API_KEY=your_resend_api_key
EMAIL_FROM=your_email_address
EMAIL_FROM_NAME=your_app_name
CLOUDINARY_CLOUD_NAME=your_cloudinary_name
CLOUDINARY_API_KEY=your_cloudinary_key
CLOUDINARY_API_SECRET=your_cloudinary_secret
ARCJET_KEY=your_arcjet_key
```

**Auto-configured (already in render.yaml):**
```
NODE_ENV=production
PORT=10000
CLIENT_URL=https://chatify.onrender.com (update if you use different name)
ARCJET_ENV=production
JWT_SECRET=auto-generated
```

### 5. Deploy
- Click **"Create Web Service"**
- Render will start building and deploying (takes 5-10 minutes)
- Once deployed, you'll get a URL like: `https://chatify.onrender.com`

### 6. Update CLIENT_URL (Important!)
After deployment:
- Copy your actual Render URL
- Go to **Environment** tab
- Update `CLIENT_URL` to your actual URL
- Save and redeploy

## Important Notes

### Free Tier Limitations
- **Sleeps after 15 minutes of inactivity**
- First request after sleep takes ~30 seconds to wake up
- 512 MB RAM
- Shared CPU

### MongoDB Setup
If you don't have MongoDB Atlas:
1. Go to [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. Create free cluster
3. Create database user
4. Whitelist all IPs (0.0.0.0/0) for Render
5. Get connection string

### Monitoring
- View logs in Render dashboard
- Check deployment status
- Monitor usage

## Troubleshooting

**Build fails:**
- Check Node version (should be >=20.0.0)
- Verify all dependencies are in package.json

**App crashes:**
- Check environment variables are set
- Verify MongoDB connection string
- Check logs for errors

**Socket.io not working:**
- Verify CLIENT_URL matches your Render URL exactly
- Check CORS settings

## Updating Your App

Push changes to GitHub:
```bash
git add .
git commit -m "Your update message"
git push origin main
```

Render auto-deploys on every push to main branch!
