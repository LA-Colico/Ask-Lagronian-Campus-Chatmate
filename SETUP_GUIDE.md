# Setup Guide for Ask Lagronian Campus Chatmate

This guide will help you set up the improved Ask Lagronian application with Google OAuth authentication.

## Quick Start Summary

The application now has:
- **Public Homepage** at `http://localhost:5000/`
- **Login Required** for the chatbot
- **Google OAuth** authentication
- **Functional Navigation** menu

## Step-by-Step Setup

### 1. Install Dependencies

```bash
cd asklagronian
pip install -r requirements.txt
```

### 2. Set Up Google OAuth

#### A. Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select existing
3. Project name: "Ask Lagronian" (or your choice)

#### B. Enable Required APIs

1. In your project, go to "APIs & Services" → "Library"
2. Search for "Google+ API" and enable it
3. Also enable "Google OAuth2 API"

#### C. Create OAuth Credentials

1. Go to "APIs & Services" → "Credentials"
2. Click "Create Credentials" → "OAuth 2.0 Client ID"
3. Configure consent screen if prompted:
   - User Type: External
   - App name: Ask Lagronian
   - User support email: Your email
   - Developer contact: Your email
4. Create OAuth Client ID:
   - Application type: Web application
   - Name: Ask Lagronian Web Client
   - Authorized redirect URIs:
     - `http://localhost:5000/authorize` (for local development)
     - `http://127.0.0.1:5000/authorize` (alternative local)
5. Click "Create"
6. **IMPORTANT**: Copy the Client ID and Client Secret

### 3. Configure Environment Variables

1. Copy the example file:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` and fill in your credentials:
   ```
   GEMINI_API_KEY=your_gemini_api_key_from_makersuite
   SECRET_KEY=any_random_long_string_here
   GOOGLE_CLIENT_ID=your_client_id_from_step_2
   GOOGLE_CLIENT_SECRET=your_client_secret_from_step_2
   ```

### 4. Add Your School PDF

Make sure you have "Lagro High School - Data .pdf" in the root directory. This file is excluded from git for privacy.

### 5. Run the Application

```bash
python app.py
```

### 6. Test the Application

1. Open browser: `http://localhost:5000`
2. You should see the homepage
3. Click "Sign In" button
4. Login with any Google account
5. You'll be redirected to the chatbot page

## Features Overview

### Public Pages (No Login)
- **Homepage** (`/`): Welcome page with school info
  - About Lagro High School
  - Programs (STEM, HUMSS, ABM, TVL)
  - Contact information
  - Navigation to login

### Protected Pages (Login Required)
- **Chatbot** (`/chatbot`): AI assistant
  - Only accessible after Google login
  - Conversation history
  - User profile displayed

### Navigation
- **Home** button: Returns to homepage
- **Ask Assistant**: Goes to chatbot (requires login)
- **Logout**: Sign out and clear session
- Other menu items currently disabled (Achievements, Analytics, etc.)

## Troubleshooting

### OAuth Error: "redirect_uri_mismatch"
- Go to Google Cloud Console → Credentials
- Edit your OAuth Client
- Add `http://localhost:5000/authorize` to Authorized redirect URIs
- Save and try again

### "GEMINI_API_KEY not found"
- Check your `.env` file exists
- Verify the API key is correct
- No quotes needed around the values

### "Failed to get user info"
- Check Google Cloud Console → OAuth consent screen
- Make sure your email is added as a test user
- Try using an incognito window

### PDF File Not Loading
- Ensure `Lagro High School - Data .pdf` is in the root directory
- Check the filename matches exactly (including spaces)
- Look at console logs for error messages

## Development vs Production

### Local Development
- Redirect URI: `http://localhost:5000/authorize`
- Use `.env` file for credentials
- Debug mode enabled

### Production (Vercel/Other)
- Update redirect URI in Google Cloud Console
- Set environment variables in hosting platform
- Disable debug mode
- Use HTTPS redirect URI

## Next Steps

1. Test all authentication flows
2. Customize the homepage content
3. Add more features to disabled menu items
4. Deploy to production

## Support

For issues:
- Check the application logs in `app.log`
- Review console output when running `python app.py`
- Verify all environment variables are set correctly

---

**Developed by Lanz Andrei Colico**
