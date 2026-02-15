# GitHub Pages Deployment Guide

Complete guide to deploy your Discord Analytics frontend on GitHub Pages.

## 📋 What You're Deploying

A single-file frontend dashboard that:
- ✅ Displays top 20 most used words
- ✅ Shows top 10 skull-reacted messages
- ✅ Renders an interactive word cloud
- ✅ Auto-refreshes every 30 seconds
- ✅ Works entirely client-side (perfect for GitHub Pages)
- ✅ Fetches data from your public Flask API

---

## 🚀 Step 1: Create GitHub Repository

### Option A: Via GitHub Website

1. Go to https://github.com
2. Click the **+** icon (top right) → **New repository**
3. Repository settings:
   - **Name:** `discord-analytics` (or any name you want)
   - **Description:** "Discord server analytics dashboard"
   - **Visibility:** Public (required for free GitHub Pages)
   - **Initialize:** ✅ Check "Add a README file"
4. Click **Create repository**

### Option B: Via GitHub CLI (if you have it)

```bash
gh repo create discord-analytics --public --description "Discord analytics dashboard"
```

---

## 📁 Step 2: Add Your HTML File

### Option A: Via GitHub Website (Easiest)

1. In your new repository, click **Add file** → **Create new file**

2. Name the file: `index.html`

3. Copy the entire contents of the `index.html` file I provided

4. **IMPORTANT:** Before saving, find this line (around line 495):
   ```javascript
   const API_URL = 'https://your-serveo-url.serveo.net';
   ```

5. **Replace it** with your actual serveo URL:
   ```javascript
   const API_URL = 'https://abc123.serveo.net';
   ```

6. Scroll down and click **Commit changes**

### Option B: Via Git Command Line

```bash
# Clone your repo
git clone https://github.com/YOUR_USERNAME/discord-analytics.git
cd discord-analytics

# Copy the index.html file into this directory
# Then edit the API_URL line

# Commit and push
git add index.html
git commit -m "Add analytics dashboard"
git push origin main
```

---

## ⚙️ Step 3: Enable GitHub Pages

1. In your repository, click **Settings** (top menu bar)

2. Scroll down the left sidebar and click **Pages**

3. Under **Source**:
   - **Branch:** Select `main` (or `master`)
   - **Folder:** Select `/ (root)`

4. Click **Save**

5. Wait 1-2 minutes for GitHub to build your site

6. You'll see a green box that says:
   ```
   ✓ Your site is published at https://YOUR_USERNAME.github.io/discord-analytics/
   ```

7. **Click that URL** to visit your dashboard!

---

## 🔧 Step 4: Configure Your API URL

If you forgot to update the API URL in Step 2:

1. Go to your repository
2. Click on `index.html`
3. Click the **pencil icon** (Edit this file)
4. Find line 495:
   ```javascript
   const API_URL = 'https://your-serveo-url.serveo.net';
   ```
5. Change it to your actual serveo URL
6. Click **Commit changes**
7. Wait 1-2 minutes for GitHub Pages to rebuild

---

## 🧪 Step 5: Test Your Dashboard

### Test Locally First

Before deploying, you can test the HTML file locally:

1. Open `index.html` in your browser (just double-click it)
2. Make sure your Flask API is running in Termux
3. Make sure serveo tunnel is active
4. The dashboard should load data

### Test on GitHub Pages

1. Visit your GitHub Pages URL: `https://YOUR_USERNAME.github.io/discord-analytics/`

2. Open browser DevTools (F12)

3. Check the Console tab for any errors

4. You should see:
   ```
   Discord Analytics Dashboard initialized
   API URL: https://your-serveo-url.serveo.net
   ```

5. If it works, you'll see:
   - Word cloud rendering
   - Top 20 words list populated
   - Top 10 skull reactions

### Common Issues & Fixes

**Problem:** "Failed to connect to API"
- **Fix:** Check that your serveo tunnel is running: `ssh -R 80:localhost:8000 serveo.net`
- **Fix:** Verify API URL is correct in `index.html`
- **Fix:** Test API directly: `curl https://your-url.serveo.net/top-words`

**Problem:** "CORS error" in browser console
- **Fix:** Your Flask API already has CORS enabled, but verify `api.py` has:
  ```python
  from flask_cors import CORS
  CORS(app)
  ```

**Problem:** Word cloud not showing
- **Fix:** Make sure you have word data (send some messages in Discord first)
- **Fix:** Check browser console for JavaScript errors

**Problem:** Page shows "Please configure your API URL"
- **Fix:** You forgot to update line 495 in `index.html`

---

## 📊 Understanding What You Built

### File Structure
```
discord-analytics/
├── index.html          # Your entire dashboard (single file!)
└── README.md           # GitHub repository description
```

### How It Works

1. **Browser loads `index.html`** from GitHub Pages
2. **JavaScript fetches data** from your Flask API via serveo tunnel
3. **Data is rendered** in real-time:
   - Word list shows top 20 words
   - Word cloud visualizes word frequency
   - Skull list shows most-reacted messages
4. **Auto-refresh** every 30 seconds to get latest data

### Data Flow
```
Discord Server
    ↓ (messages sent)
Discord Bot (bot.py in Termux)
    ↓ (logs to SQLite)
SQLite Database (messages.db)
    ↓ (queries)
Flask API (api.py in Termux)
    ↓ (tunneled via serveo)
Public Internet
    ↓ (fetched by browser)
GitHub Pages (index.html)
    ↓ (displays)
Your Users' Browsers
```

---

## 🔄 Updating Your Dashboard

### Update API URL

1. Go to your repo on GitHub
2. Click `index.html` → Edit (pencil icon)
3. Change the API URL on line 495
4. Commit changes
5. Wait 1-2 minutes for rebuild

### Update Design/Features

1. Edit `index.html` locally or on GitHub
2. Commit changes
3. GitHub Pages automatically rebuilds (1-2 minutes)
4. Refresh your browser to see changes

### Force Rebuild

If changes aren't showing:
1. Make a small change (add a space somewhere)
2. Commit
3. Or go to Settings → Pages → Change source to "None", save, then change back to "main"

---

## 🎨 Customization Ideas

### Change Refresh Interval

Find line 497:
```javascript
const REFRESH_INTERVAL = 30000;  // 30 seconds
```

Change to:
```javascript
const REFRESH_INTERVAL = 60000;  // 60 seconds (1 minute)
const REFRESH_INTERVAL = 10000;  // 10 seconds
```

### Change Number of Words Shown

Find line 527:
```javascript
const response = await fetch(`${API_URL}/top-words?limit=20`);
```

Change `limit=20` to `limit=30` or any number you want.

### Change Skull Reactions Time Period

Find line 541:
```javascript
const response = await fetch(`${API_URL}/top-skulls?limit=10&days=7`);
```

Change `days=7` to `days=1` (today only) or `days=30` (last month).

### Change Color Scheme

The word cloud colors are on line 678:
```javascript
const colors = ['#667eea', '#764ba2', '#f093fb', '#4facfe', '#43e97b'];
```

Add or change hex color codes!

---

## 🌐 Sharing Your Dashboard

Your dashboard is now live at:
```
https://YOUR_USERNAME.github.io/discord-analytics/
```

Share this URL with:
- Your Discord server members
- Friends who want to see the analytics
- Anyone! (it's public)

**Note:** They can only VIEW data. They cannot access your API directly or your Discord bot.

---

## 🔒 Privacy & Security Notes

### What's Public
- ✅ The dashboard HTML/CSS/JavaScript code
- ✅ Analytics data (word counts, skull reactions)
- ✅ Discord usernames that appear in messages

### What's Private
- ✅ Your Discord bot token (stays in Termux)
- ✅ Your SQLite database (stays in Termux)
- ✅ Your Termux/phone

### Security Best Practices
- Don't commit sensitive data to GitHub
- Don't put your Discord bot token in `index.html`
- Your API only exposes analytics, not raw messages
- Consider adding rate limiting to your Flask API if it gets popular

---

## 🐛 Troubleshooting

### GitHub Pages shows 404

**Causes:**
- File is not named `index.html` (case-sensitive!)
- GitHub Pages is not enabled
- Wrong branch selected (should be `main` or `master`)

**Fix:**
- Check filename is exactly `index.html`
- Go to Settings → Pages and verify it's enabled
- Make sure branch is set to `main`

### Dashboard loads but shows no data

**Check:**
```bash
# 1. Is your bot running?
ps aux | grep bot.py

# 2. Is your API running?
curl http://localhost:8000/stats

# 3. Is serveo tunnel running?
ps aux | grep ssh
```

**Fix:**
```bash
# Restart everything
cd ~/discord-analytics
bash stop.sh
bash start.sh

# Start serveo tunnel
ssh -R 80:localhost:8000 serveo.net
```

### Word cloud is blank

**Causes:**
- No messages in database yet
- JavaScript error
- Word cloud library didn't load

**Fix:**
- Send some messages in Discord first
- Check browser console (F12) for errors
- Verify internet connection for CDN libraries

---

## 📱 Mobile Optimization

The dashboard is already mobile-responsive! Test it on your phone:

1. Open your GitHub Pages URL on mobile browser
2. Word cloud adjusts to smaller screen
3. Cards stack vertically
4. Text sizes scale appropriately

---

## 🎉 You're Done!

You now have:
- ✅ Discord bot logging messages (Termux)
- ✅ Flask API serving data (Termux)
- ✅ Public tunnel via serveo (SSH)
- ✅ Beautiful dashboard on GitHub Pages
- ✅ Auto-refreshing analytics
- ✅ Shareable public URL

**Your complete stack:**
```
Discord → Bot → SQLite → Flask API → Serveo Tunnel → GitHub Pages → Users
```

Enjoy your analytics dashboard! 🚀

---

## 🔮 Next Steps

- Add more endpoints to your Flask API
- Create charts with Chart.js
- Add user-specific statistics
- Build a mobile app version
- Set up a proper VPS for 24/7 uptime
- Add authentication for private dashboards

Have fun! 🎮
