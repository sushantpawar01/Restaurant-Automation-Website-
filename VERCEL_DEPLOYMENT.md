# Vercel Deployment Guide

This guide explains how to deploy your Restaurant Automation Website on Vercel.

## Project Structure
- **Frontend**: `food-del/frontend/` (React + Vite)
- **Admin**: `food-del/admin/` (React + Vite)
- **Backend**: `food-del/backend/` (Express.js)

## Pre-Deployment Checklist

### 1. Environment Variables
Create or update environment variables in Vercel dashboard:

**Backend (.env)**
```
MONGODB_URI=<your_mongodb_connection_string>
JWT_SECRET=<your_jwt_secret>
STRIPE_SECRET_KEY=<your_stripe_secret_key>
NODE_ENV=production
```

**Frontend (.env or .env.production)**
```
VITE_API_URL=<your_backend_api_url>
VITE_STRIPE_PUBLIC_KEY=<your_stripe_public_key>
```

### 2. Changes Made for Vercel

✅ **Backend (`food-del/backend/server.js`)**
- Added dynamic port configuration: `const port = process.env.PORT || 4000`
- Added export for Vercel serverless compatibility

✅ **Backend (`food-del/backend/package.json`)**
- Added `"build"` script for Vercel
- Added `"start"` script for production

✅ **Root Configuration**
- Created `vercel.json` for monorepo configuration

✅ **Environment Management**
- Created `.gitignore` to protect sensitive files

## Deployment Steps

### Option 1: Deploy Frontend & Admin on Vercel (Recommended)

1. **Deploy Frontend (Customer App)**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Select your GitHub repo
   - Set **Root Directory** to `food-del/frontend`
   - Add Environment Variables (VITE_API_URL, VITE_STRIPE_PUBLIC_KEY)
   - Deploy

2. **Deploy Admin Dashboard**
   - Create another Vercel project
   - Select same repo
   - Set **Root Directory** to `food-del/admin`
   - Add Environment Variables
   - Deploy

### Option 2: Deploy Backend on Vercel (Serverless Function)

**⚠️ Important Notes:**
- Vercel serverless functions have limitations with long-running operations
- For production, consider deploying backend on:
  - [Railway](https://railway.app)
  - [Render](https://render.com)
  - [Heroku](https://heroku.com)
  - [AWS/Google Cloud](https://cloud.google.com)

## Production Recommendations

### Database
- Use **MongoDB Atlas** (managed cloud service)
- Never hardcode connection strings

### Image/File Storage
- Replace local `multer` uploads with:
  - **Cloudinary** (free tier available)
  - **AWS S3**
  - **Vercel Blob Storage**

### API Configuration
- Update frontend API URL to production backend URL
- Add backend URL to CORS whitelist
- Use HTTPS only in production

### Environment Variables
```bash
# Backend
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/food-del
JWT_SECRET=your-secure-random-key
STRIPE_SECRET_KEY=sk_live_...
NODE_ENV=production

# Frontend
VITE_API_URL=https://your-backend-domain.com
VITE_STRIPE_PUBLIC_KEY=pk_live_...
```

## Troubleshooting

### Issue: Build fails
- Check Node.js version compatibility
- Verify all dependencies are in package.json
- Check for missing environment variables

### Issue: CORS errors
- Add frontend URL to CORS origin list in backend
- Check API endpoint configuration

### Issue: Database connection fails
- Verify MONGODB_URI is correct
- Check MongoDB Atlas IP whitelist
- Ensure connection string is in .env, not hardcoded

### Issue: Images not loading
- Replace local multer storage with cloud service
- Update image URLs to cloud CDN

## Useful Commands

```bash
# Test build locally
npm run build

# Test production build
npm run preview

# Deploy to Vercel
vercel deploy

# Deploy to production
vercel deploy --prod
```

## Security Checklist

- ✅ Never commit `.env` files
- ✅ Use strong JWT_SECRET (min 32 characters)
- ✅ Enable HTTPS only
- ✅ Implement rate limiting
- ✅ Validate all user inputs
- ✅ Use STRIPE_SECRET_KEY only on backend
- ✅ Set appropriate CORS origins
- ✅ Add API authentication middleware

---

For more help, refer to:
- [Vercel Docs](https://vercel.com/docs)
- [Express.js Production](https://expressjs.com/en/advanced/best-practice-performance.html)
- [MongoDB Atlas](https://docs.atlas.mongodb.com/)
