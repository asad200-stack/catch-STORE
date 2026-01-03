# 🚀 Deployment Guide

This guide will help you deploy the Multi-Tenant SaaS Store Platform to Railway.

## Prerequisites

- GitHub account
- Railway account (sign up at [railway.app](https://railway.app))
- PostgreSQL database (Railway provides this)

## Step 1: Prepare Your Repository

1. Push your code to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```

## Step 2: Set Up Railway Project

1. Go to [Railway Dashboard](https://railway.app/dashboard)
2. Click "New Project"
3. Select "Deploy from GitHub repo"
4. Choose your repository
5. Railway will automatically detect Next.js

## Step 3: Add PostgreSQL Database

1. In your Railway project, click "New"
2. Select "Database" → "Add PostgreSQL"
3. Railway will create a PostgreSQL instance
4. Copy the `DATABASE_URL` from the PostgreSQL service variables

## Step 4: Configure Environment Variables

In your Railway project settings, add these environment variables:

### Required Variables

- `DATABASE_URL`: Your PostgreSQL connection string (from step 3)
- `JWT_SECRET`: Generate with `openssl rand -base64 32` or use a strong random string
- `APP_URL`: Your Railway app URL (e.g., `https://your-app.railway.app`)
- `STORAGE_PATH`: `/app/storage` (for Railway) or use S3

### Optional Variables

- `MAX_FILE_SIZE_MB`: `10` (default)
- `MAX_IMAGE_SIZE_MB`: `5` (default)

## Step 5: Deploy

Railway will automatically:
1. Install dependencies (`npm ci`)
2. Generate Prisma client (`prisma generate`)
3. Run migrations (`prisma migrate deploy`)
4. Build the app (`npm run build`)
5. Start the server (`npm start`)

## Step 6: Verify Deployment

1. Wait for the deployment to complete (check the "Deployments" tab)
2. Click on your service to get the public URL
3. Visit the URL and test:
   - Register a new account
   - Create a store
   - Add products
   - View the public storefront

## Step 7: Seed Demo Data (Optional)

To seed the database with demo data:

1. Connect to your Railway database via Railway's PostgreSQL service
2. Or use Railway CLI:
   ```bash
   railway run npm run db:seed
   ```

## Troubleshooting

### Database Connection Issues

- Verify `DATABASE_URL` is correct
- Check that PostgreSQL service is running
- Ensure SSL mode is set correctly in connection string

### Build Failures

- Check build logs in Railway dashboard
- Verify all environment variables are set
- Ensure `package.json` scripts are correct

### Migration Issues

- Check that `DATABASE_URL` is accessible
- Verify Prisma schema is valid
- Run `prisma migrate deploy` manually if needed

## Production Checklist

- [ ] Set strong `JWT_SECRET`
- [ ] Configure proper `APP_URL`
- [ ] Set up file storage (S3 recommended for production)
- [ ] Enable HTTPS (Railway does this automatically)
- [ ] Set up monitoring and logging
- [ ] Configure backup strategy for database
- [ ] Review security settings

## Custom Domain (Optional)

1. In Railway project settings, go to "Settings" → "Domains"
2. Add your custom domain
3. Configure DNS records as instructed
4. Railway will provision SSL certificate automatically

## Scaling

Railway automatically handles:
- Horizontal scaling
- Load balancing
- SSL certificates
- Health checks

For high traffic, consider:
- Using Railway's paid plans
- Setting up database connection pooling
- Using CDN for static assets
- Implementing caching strategies

---

**Need Help?** Check Railway's [documentation](https://docs.railway.app) or open an issue in the repository.

