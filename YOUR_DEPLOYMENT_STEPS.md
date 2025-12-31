# Your Deployment Steps - Ready to Deploy Now!

## ✅ Already Configured:

1. ✅ **Gemini API Key**: Already added to .env
2. ✅ **Secret Key**: Auto-generated and added to .env
3. ✅ **PDF File**: Will be deployed from your repository
4. ✅ **All code fixes**: Applied and ready

## 🔑 What You Still Need:

### Google OAuth Credentials (Required for Login)

You need to get these 2 values:
- `GOOGLE_CLIENT_ID`
- `GOOGLE_CLIENT_SECRET`

**How to get them (5 minutes):**

1. Go to: https://console.cloud.google.com/apis/credentials

2. **If you don't have a project:**
   - Click "CREATE PROJECT"
   - Name: "Ask Lagronian"
   - Click "CREATE"

3. **Enable Google+ API:**
   - Go to: https://console.cloud.google.com/apis/library
   - Search for "Google+ API"
   - Click "ENABLE"

4. **Configure OAuth Consent Screen:**
   - Go to: https://console.cloud.google.com/apis/credentials/consent
   - User Type: External
   - Click "CREATE"
   - Fill in:
     - App name: Ask Lagronian
     - User support email: Your email
     - Developer contact: Your email
   - Click "SAVE AND CONTINUE"
   - Click "SAVE AND CONTINUE" (skip scopes)
   - Add test users: Your email
   - Click "SAVE AND CONTINUE"

5. **Create OAuth Client ID:**
   - Go to: https://console.cloud.google.com/apis/credentials
   - Click "CREATE CREDENTIALS" → "OAuth 2.0 Client ID"
   - Application type: Web application
   - Name: Ask Lagronian Web Client
   - Authorized redirect URIs:
     - Add: `http://localhost:5000/authorize` (for testing)
     - Add: `https://your-app-name.vercel.app/authorize` (you'll update this after deployment)
   - Click "CREATE"
   - **COPY both Client ID and Client Secret** (you'll need these!)

6. **Update your local .env file:**
   - Open `.env` file
   - Replace `your_google_client_id_here` with your Client ID
   - Replace `your_google_client_secret_here` with your Client Secret

## 🚀 Deploy to Vercel (5 minutes):

### Step 1: Commit and Push Your Changes

```bash
cd Ask-Lagronian-Campus-Chatmate

# Add all changes
git add .

# Commit
git commit -m "Fix: Update for Vercel deployment with all fixes"

# Push to GitHub
git push origin main
```

### Step 2: Deploy on Vercel

**Option A: Vercel Dashboard (Easier)**

1. Go to: https://vercel.com/new

2. Sign in with GitHub

3. Click "Import" next to your repository: `LA-Colico/Ask-Lagronian-Campus-Chatmate`

4. Configure Project:
   - Framework Preset: **Other**
   - Root Directory: `./` (leave as is)
   - Build Command: (leave empty)
   - Output Directory: (leave empty)

5. **Add Environment Variables** (Click "Environment Variables"):

   Add these 4 variables:

   | Name | Value |
   |------|-------|
   | `GEMINI_API_KEY` | `AIzaSyCQ4-7u5HoQXEvQWPBDpnriWCokxnwntW4` |
   | `SECRET_KEY` | `da1415910c29a0576217bcfd4bcb9029549538a2b4028a440ac03a5b691ef40c` |
   | `GOOGLE_CLIENT_ID` | (paste your Client ID here) |
   | `GOOGLE_CLIENT_SECRET` | (paste your Client Secret here) |

6. Click **"Deploy"**

7. Wait 2-3 minutes for deployment to complete

8. You'll get a URL like: `https://ask-lagronian-campus-chatmate.vercel.app`

**Option B: Vercel CLI (Advanced)**

```bash
# Install Vercel CLI
npm install -g vercel

# Login
vercel login

# Deploy
cd Ask-Lagronian-Campus-Chatmate
vercel

# Add environment variables
vercel env add GEMINI_API_KEY
# Paste: AIzaSyCQ4-7u5HoQXEvQWPBDpnriWCokxnwntW4

vercel env add SECRET_KEY
# Paste: da1415910c29a0576217bcfd4bcb9029549538a2b4028a440ac03a5b691ef40c

vercel env add GOOGLE_CLIENT_ID
# Paste your Client ID

vercel env add GOOGLE_CLIENT_SECRET
# Paste your Client Secret

# Deploy to production
vercel --prod
```

### Step 3: Update OAuth Redirect URI

After deployment, you'll get a URL like: `https://your-app-name.vercel.app`

1. Go back to: https://console.cloud.google.com/apis/credentials

2. Click on your OAuth Client ID

3. Under "Authorized redirect URIs":
   - Add: `https://your-actual-vercel-url.vercel.app/authorize`
   - (Replace with your actual Vercel URL)

4. Click "SAVE"

### Step 4: Test Your Deployment! 🎉

1. Visit your Vercel URL: `https://your-app-name.vercel.app`

2. You should see the homepage

3. Click "Sign In"

4. Login with your Google account

5. Test the chatbot - send a message!

## 📋 Deployment Checklist:

- [ ] Got Google OAuth Client ID and Client Secret
- [ ] Updated local `.env` with OAuth credentials
- [ ] Committed and pushed changes to GitHub
- [ ] Deployed to Vercel
- [ ] Added all 4 environment variables in Vercel
- [ ] Updated OAuth redirect URI with Vercel URL
- [ ] Tested homepage loads
- [ ] Tested login works
- [ ] Tested chatbot responds

## 🔧 Troubleshooting:

### "redirect_uri_mismatch" Error
- Make sure you added the exact Vercel URL to OAuth redirect URIs
- Must use HTTPS (not HTTP)
- Must end with `/authorize`

### "Failed to get user info"
- Add yourself as a test user in OAuth consent screen
- Try logging in with the test user email

### Build Failed on Vercel
- Check all 4 environment variables are added
- No extra spaces in the values
- Check build logs in Vercel dashboard

### Chatbot Doesn't Respond
- Check Gemini API key is correct
- View function logs in Vercel dashboard
- Make sure API key has no usage limits

### PDF Not Loading
- Pull latest changes from GitHub: `git pull origin main`
- The PDF should be in the repository
- Check filename is exactly: `Lagro High School - Data .pdf`

## 📊 What's Next?

After successful deployment:

1. **Share your chatbot**: Send the Vercel URL to users
2. **Monitor usage**: Check Vercel Analytics
3. **Check API limits**: Monitor Gemini API usage
4. **Add custom domain** (optional): In Vercel project settings

## 🎯 Your Environment Variables:

For reference, here are your values:

```env
GEMINI_API_KEY=AIzaSyCQ4-7u5HoQXEvQWPBDpnriWCokxnwntW4
SECRET_KEY=da1415910c29a0576217bcfd4bcb9029549538a2b4028a440ac03a5b691ef40c
GOOGLE_CLIENT_ID=(get from Google Cloud Console)
GOOGLE_CLIENT_SECRET=(get from Google Cloud Console)
```

**IMPORTANT:** Never share these values publicly or commit the `.env` file to GitHub!

---

## 🚀 You're Ready!

Everything is configured and ready to deploy. Just:
1. Get your OAuth credentials (5 min)
2. Update `.env` locally
3. Push to GitHub
4. Deploy on Vercel
5. Update OAuth redirect URI
6. Test!

**Total time: ~15 minutes** ⏱️

Good luck with your deployment! 🎉
