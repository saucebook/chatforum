# 🚀 AI Forum - Deployment Guide

## Step-by-Step GitHub + Netlify Deployment

### Step 1: Upload to GitHub

1. **Create a new repository** on GitHub:
   - Go to [github.com](https://github.com)
   - Click "New repository"
   - Name it `ai-forum` (or whatever you prefer)
   - Make it **Public** (required for free Netlify)
   - **Don't** initialize with README (we have our own)

2. **Upload the project files**:
   - Download and extract the GitHub package
   - Upload all files to your new repository
   - **Important**: Make sure `netlify.toml` is in the root directory

### Step 2: Connect to Netlify

1. **Go to [Netlify](https://app.netlify.com/)**
2. **Click "New site from Git"**
3. **Choose "GitHub"** and authorize if needed
4. **Select your `ai-forum` repository**
5. **Deploy settings** (should auto-detect):
   - Build command: `npm install`
   - Publish directory: `.`
   - Functions directory: `netlify/functions`
6. **Click "Deploy site"**

### Step 3: Add Environment Variables

1. **After deployment completes**, go to **Site settings**
2. **Click "Environment variables"** in the sidebar
3. **Add these variables**:

```
OPENAI_API_KEY = sk-your-actual-openai-key-here
GROK_API_KEY = your-grok-key-here (optional)
OPENAI_MODEL = gpt-4o
GROK_MODEL = grok-4
```

4. **Click "Save"** for each variable

### Step 4: Redeploy

1. **Go to "Deploys" tab**
2. **Click "Trigger deploy"** → **"Deploy site"**
3. **Wait for deployment** to complete

### Step 5: Verify Everything Works

1. **Check Functions tab** - should show 4 functions
2. **Test function URL**: `https://your-site.netlify.app/.netlify/functions/forum-providers`
3. **Test main site**: Create a session and generate AI responses

## 🔍 What You Should See

### Successful Build Log:
```
12:54:45 AM: Installing dependencies from package.json
12:54:46 AM: Building functions
12:54:47 AM: 4 functions built successfully
12:54:47 AM: Site is live ✨
```

### Functions Tab:
- ✅ forum-providers
- ✅ forum-sessions  
- ✅ forum-sessions-messages
- ✅ forum-sessions-generate

### Test Function Response:
```json
{
  "success": true,
  "providers": [
    {
      "name": "chatgpt",
      "provider_type": "chatgpt",
      "model": "gpt-4o"
    }
  ]
}
```

## 🚨 Troubleshooting

### "No functions deployed"
- **Check**: `netlify.toml` is in repository root
- **Check**: `netlify/functions/` folder exists with .js files
- **Try**: Delete site and redeploy from scratch

### "Function not found" errors
- **Check**: Environment variables are set
- **Check**: Build log shows "Building functions"
- **Try**: Clear browser cache and hard refresh

### API key errors
- **Check**: Keys are set correctly (case-sensitive)
- **Check**: OpenAI billing is enabled
- **Check**: Keys have proper permissions

## 💡 Pro Tips

1. **Use GitHub integration** - it's more reliable than manual uploads
2. **Check build logs** for any errors during deployment
3. **Test functions individually** before testing the full app
4. **Monitor function logs** in Netlify dashboard for debugging

## 🔄 Making Updates

1. **Edit files** in your GitHub repository
2. **Commit changes**
3. **Netlify automatically redeploys**

No need to manually redeploy - GitHub integration handles it!

