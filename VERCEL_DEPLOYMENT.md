# 🚀 Vercel Deployment Guide for CineFindr

This guide will help you deploy your CineFindr application to Vercel.

## 📋 Prerequisites

- A GitHub account with your CineFindr repository
- A Vercel account (sign up at [vercel.com](https://vercel.com))
- A TMDB API key (get one at [themoviedb.org](https://www.themoviedb.org/settings/api))

## 🎯 Deployment Steps

### Step 1: Connect Repository to Vercel

1. Go to [vercel.com](https://vercel.com) and sign in
2. Click **"Add New..."** → **"Project"**
3. Import your GitHub repository: `Shashank-V-A/CineFindr`
4. Click **"Import"**

### Step 2: Configure Project Settings

In the project configuration:

1. **Framework Preset**: Select **"Next.js"** (should auto-detect)

2. **Root Directory**: Set to `apps/web`
   - Click **"Edit"** next to Root Directory
   - Enter: `apps/web`

3. **Build and Output Settings**:
   - Build Command: `npm run build` (default)
   - Output Directory: `.next` (default)
   - Install Command: `npm install` (default)

### Step 3: Environment Variables

Add the following environment variables in Vercel:

1. Click **"Environment Variables"** section
2. Add these variables:

   ```
   TMDB_API_KEY=your_tmdb_api_key_here
   ```

   **Note**: Get your TMDB API key from https://www.themoviedb.org/settings/api

3. Optionally, if you need to connect to a database:
   ```
   DATABASE_URL=your_database_connection_string
   REDIS_URL=your_redis_connection_string
   ```

### Step 4: Deploy

1. Click **"Deploy"** button
2. Wait for the build to complete (usually 2-5 minutes)
3. Once deployed, Vercel will provide you with a URL like: `https://cinefindr-xyz.vercel.app`

### Step 5: Custom Domain (Optional)

1. Go to your project settings → **Domains**
2. Add your custom domain (e.g., `cinefindr.vercel.app`)
3. Follow Vercel's DNS configuration instructions

## 🔧 Configuration Details

### How It Works

Your Next.js application includes API routes in `apps/web/src/app/api/` that handle:
- Movie/TV show search (`/api/search`)
- Title details (`/api/titles/[id]`)
- Genres (`/api/genres`)
- Streaming providers (`/api/titles/[id]/providers`)
- And more...

These API routes run as serverless functions on Vercel, calling the TMDB API directly. No separate backend deployment needed!

### Project Structure

```
CineFindr/
├── apps/
│   └── web/              ← Vercel deploys this directory
│       ├── src/
│       │   ├── app/
│       │   │   ├── api/  ← Serverless API routes
│       │   │   └── ...   ← Next.js pages
│       │   └── ...
│       └── package.json
```

## ✅ Post-Deployment Checklist

- [ ] Verify the site loads at your Vercel URL
- [ ] Test search functionality
- [ ] Check movie/TV show details pages
- [ ] Verify images load correctly (TMDB images)
- [ ] Test genre filtering
- [ ] Check streaming provider links

## 🐛 Troubleshooting

### Build Fails

- **Error: "Cannot find module"**: Make sure Root Directory is set to `apps/web`
- **Error: "Build command failed"**: Check that all dependencies are in `apps/web/package.json`

### API Routes Not Working

- Verify `TMDB_API_KEY` is set correctly in Environment Variables
- Check Vercel function logs: Project → Deployments → Select deployment → Functions tab

### Images Not Loading

- Verify `next.config.js` has correct image domain configuration for `image.tmdb.org`
- Check browser console for CORS errors

### Environment Variables Not Working

- After adding environment variables, redeploy the project
- Use `NEXT_PUBLIC_` prefix only for variables that need to be accessible in the browser

## 📚 Additional Resources

- [Vercel Documentation](https://vercel.com/docs)
- [Next.js Deployment Guide](https://nextjs.org/docs/deployment)
- [Vercel Environment Variables](https://vercel.com/docs/concepts/projects/environment-variables)

## 🔄 Updating Your Deployment

After pushing changes to GitHub:

1. Vercel automatically detects new commits
2. Creates a new deployment preview
3. Once build succeeds, you can promote it to production

Or manually trigger:
- Go to Vercel dashboard → Your Project → Deployments
- Click **"Redeploy"**

---

🎉 **Congratulations!** Your CineFindr app is now live on Vercel!

