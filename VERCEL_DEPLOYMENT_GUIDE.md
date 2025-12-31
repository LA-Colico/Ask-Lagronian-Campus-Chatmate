# Vercel Deployment Guide for Ask Lagronian

This guide will help you deploy the Ask Lagronian chatbot to Vercel.

## Prerequisites

1. A Vercel account (sign up at https://vercel.com)
2. The Vercel CLI installed (optional but recommended)
3. Google Gemini API key
4. Google OAuth credentials

## Step 1: Prepare Environment Variables

You need to set up the following environment variables in Vercel:

### Required Environment Variables:

1. **GEMINI_API_KEY**
   - Get from: https://makersuite.google.com/app/apikey
   - This is your Google Gemini API key

2. **SECRET_KEY**
   - Generate a random secret key
   - You can use Python to generate one:
     ```python
     import secrets
     print(secrets.token_hex(32))
     ```

3. **GOOGLE_CLIENT_ID**
   - Get from: https://console.cloud.google.com/apis/credentials
   - Your Google OAuth Client ID

4. **GOOGLE_CLIENT_SECRET**
   - Get from: https://console.cloud.google.com/apis/credentials
   - Your Google OAuth Client Secret

## Step 2: Set Up Google OAuth for Production

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Select your project (or create a new one)
3. Navigate to "APIs & Services" → "Credentials"
4. Edit your OAuth 2.0 Client ID
5. Add your Vercel domain to "Authorized redirect URIs":
   - `https://your-app-name.vercel.app/authorize`
   - Replace `your-app-name` with your actual Vercel app name
6. Save the changes

## Step 3: Deploy to Vercel

### Option A: Deploy via Vercel Dashboard (Recommended)

1. Go to https://vercel.com/dashboard
2. Click "Add New" → "Project"
3. Import your GitHub repository:
   - If not connected, authorize Vercel to access your GitHub
   - Select the repository: `LA-Colico/Ask-Lagronian-Campus-Chatmate`
4. Configure the project:
   - **Framework Preset**: Other
   - **Root Directory**: ./
   - **Build Command**: Leave empty (not needed for Flask)
   - **Output Directory**: Leave empty
5. Add Environment Variables:
   - Click "Environment Variables"
   - Add all 4 required variables (see Step 1)
   - Make sure to add them for all environments (Production, Preview, Development)
6. Click "Deploy"
7. Wait for the deployment to complete

### Option B: Deploy via Vercel CLI

1. Install Vercel CLI:
   ```bash
   npm install -g vercel
   ```

2. Login to Vercel:
   ```bash
   vercel login
   ```

3. Navigate to your project directory:
   ```bash
   cd Ask-Lagronian-Campus-Chatmate
   ```

4. Deploy:
   ```bash
   vercel
   ```

5. Follow the prompts:
   - Set up and deploy: Y
   - Which scope: Select your account
   - Link to existing project: N (first time) or Y (subsequent deploys)
   - Project name: ask-lagronian (or your choice)
   - Directory: ./ (press Enter)

6. Add environment variables:
   ```bash
   vercel env add GEMINI_API_KEY
   vercel env add SECRET_KEY
   vercel env add GOOGLE_CLIENT_ID
   vercel env add GOOGLE_CLIENT_SECRET
   ```

7. Deploy to production:
   ```bash
   vercel --prod
   ```

## Step 4: Update Google OAuth Redirect URI

After deployment, you'll receive a URL like: `https://your-app-name.vercel.app`

1. Go back to Google Cloud Console
2. Navigate to your OAuth 2.0 Client ID
3. Add the production redirect URI:
   - `https://your-app-name.vercel.app/authorize`
4. Save

## Step 5: Test Your Deployment

1. Visit your Vercel URL: `https://your-app-name.vercel.app`
2. Click "Sign In"
3. Login with your Google account
4. Test the chatbot functionality

## Important Notes

### About the PDF File

The `Lagro High School - Data.pdf` file is excluded from deployment (see `.vercelignore`).

**Options:**

1. **Upload to Gemini Files API** (Recommended):
   - Upload the PDF once to Gemini
   - Store the file URI in an environment variable
   - Modify the code to use the stored URI

2. **Store in Cloud Storage**:
   - Upload to AWS S3, Google Cloud Storage, or similar
   - Download and process on first request

3. **Embed in Code**:
   - Convert PDF content to text
   - Include directly in the system instruction

For now, the app will work without the PDF, but responses may be less specific.

### Serverless Limitations

Vercel uses serverless functions, which means:

1. **No persistent file system**: Files written during runtime don't persist
2. **Stateless**: Each request may run on a different instance
3. **Cold starts**: First request after inactivity may be slower
4. **Time limits**: Functions timeout after 10 seconds (Hobby plan) or 60 seconds (Pro plan)

The app has been configured to handle these limitations:
- Removed file logging (uses console logging instead)
- PDF loads on-demand per request
- Session state managed via Flask sessions

### Troubleshooting

**Build Failed:**
- Check that all environment variables are set correctly
- Review build logs in Vercel dashboard
- Ensure `requirements.txt` is up to date

**OAuth Error:**
- Verify redirect URI matches exactly in Google Console
- Check that GOOGLE_CLIENT_ID and GOOGLE_CLIENT_SECRET are correct
- Make sure you're using HTTPS URLs (not HTTP)

**Chatbot Not Responding:**
- Check that GEMINI_API_KEY is valid
- Review function logs in Vercel dashboard
- Verify API key has proper permissions

**PDF Not Loading:**
- This is expected if PDF is not deployed
- See "About the PDF File" section above for solutions

### Monitoring and Logs

1. View logs in Vercel Dashboard:
   - Go to your project
   - Click on "Deployments"
   - Select a deployment
   - Click "View Function Logs"

2. Monitor usage:
   - Check Vercel Analytics
   - Monitor Gemini API usage at Google Cloud Console

### Cost Considerations

1. **Vercel:**
   - Hobby plan: Free with limitations
   - Pro plan: $20/month with higher limits

2. **Google Gemini API:**
   - Free tier available
   - Check current pricing at https://ai.google.dev/pricing

3. **Google Cloud (OAuth):**
   - OAuth is free
   - No charges for authentication

## Next Steps

1. Set up custom domain (optional)
2. Configure analytics
3. Set up monitoring alerts
4. Implement PDF solution (see notes above)
5. Test thoroughly with different user scenarios

## Support

For issues:
- Check Vercel documentation: https://vercel.com/docs
- Review Google Gemini docs: https://ai.google.dev/docs
- Check project logs in Vercel dashboard

---

**Deployment checklist:**
- [ ] All environment variables added to Vercel
- [ ] Google OAuth redirect URI updated with Vercel URL
- [ ] Project successfully deployed
- [ ] Login functionality tested
- [ ] Chatbot responses working
- [ ] No console errors in browser
- [ ] Mobile responsiveness verified
