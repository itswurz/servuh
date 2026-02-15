# Quick Reference Card

## 🚀 Deploy in 5 Minutes

### Step 1: Create Repository
1. Go to https://github.com/new
2. Name: `discord-analytics`
3. Public ✓
4. Add README ✓
5. Create!

### Step 2: Add index.html
1. Click "Add file" → "Create new file"
2. Name: `index.html`
3. Paste the HTML code
4. **IMPORTANT:** Change line 495:
   ```javascript
   const API_URL = 'https://YOUR-SERVEO-URL.serveo.net';
   ```
5. Commit!

### Step 3: Enable Pages
1. Settings → Pages
2. Source: `main` / `(root)`
3. Save!
4. Wait 2 minutes

### Step 4: Visit Your Site
```
https://YOUR-USERNAME.github.io/discord-analytics/
```

---

## 🔧 Essential Commands

### Start Your Services (Termux)
```bash
cd discord-analytics

# Terminal 1: Bot
python bot.py

# Terminal 2: API
python api.py

# Terminal 3: Tunnel
ssh -R 80:localhost:8000 serveo.net
```

### Check Status
```bash
# Bot running?
ps aux | grep bot.py

# API running?
curl http://localhost:8000/stats

# Tunnel running?
ps aux | grep ssh
```

### Stop Everything
```bash
pkill -f bot.py
pkill -f api.py
pkill -f ssh
```

---

## 🌐 Important URLs

### Your API (Local)
```
http://localhost:8000/stats
http://localhost:8000/top-words
http://localhost:8000/top-skulls
```

### Your API (Public via Serveo)
```
https://something.serveo.net/stats
https://something.serveo.net/top-words
https://something.serveo.net/top-skulls
```

### Your Dashboard (GitHub Pages)
```
https://YOUR-USERNAME.github.io/discord-analytics/
```

---

## 🐛 Quick Fixes

### Dashboard shows "Please configure API URL"
→ Edit `index.html` line 495 with your serveo URL

### "Failed to connect to API"
→ Check serveo tunnel is running: `ps aux | grep ssh`

### No data showing
→ Send messages in Discord first to populate database

### GitHub Pages shows 404
→ Wait 2 minutes, or check Settings → Pages is enabled

### Tunnel URL changed
→ Update `index.html` line 495 with new serveo URL

---

## 📝 File Locations

```
Termux:
~/discord-analytics/
├── bot.py          # Discord bot
├── api.py          # Flask API
├── messages.db     # SQLite database
└── index.html      # Frontend (copy to GitHub)

GitHub:
discord-analytics/
├── index.html      # Your dashboard
└── README.md       # Repository description
```

---

## ⚡ Pro Tips

1. **Bookmark your GitHub Pages URL** for easy access
2. **Keep serveo terminal open** or it disconnects
3. **Test locally first** before pushing to GitHub
4. **Check browser console (F12)** for errors
5. **Use tmux** to keep everything running in background

---

## 🎯 Common Customizations

### Change refresh rate (line 497):
```javascript
const REFRESH_INTERVAL = 30000;  // milliseconds
```

### Change word count (line 527):
```javascript
fetch(`${API_URL}/top-words?limit=20`)  // change 20
```

### Change skull period (line 541):
```javascript
fetch(`${API_URL}/top-skulls?limit=10&days=7`)  // change 7
```

### Change colors (line 678):
```javascript
const colors = ['#667eea', '#764ba2', ...];  // add colors
```

---

## 📞 Need Help?

1. Check browser console (F12) for errors
2. Verify API responds: `curl YOUR-SERVEO-URL/stats`
3. Check all services running: `bash status.sh`
4. Read GITHUB_PAGES_GUIDE.md for detailed troubleshooting

---

## ✅ Checklist

Before going live, verify:

- [ ] Discord bot is running and logging messages
- [ ] Flask API responds to `http://localhost:8000/stats`
- [ ] Serveo tunnel is active and shows URL
- [ ] `index.html` has correct API URL (line 495)
- [ ] GitHub Pages is enabled (Settings → Pages)
- [ ] Dashboard loads at `https://username.github.io/discord-analytics/`
- [ ] Data appears in word cloud and lists
- [ ] Auto-refresh works (check console logs)

---

## 🎉 Success Looks Like

```
Browser Console:
Discord Analytics Dashboard initialized
API URL: https://abc123.serveo.net
Auto-refresh enabled (every 30 seconds)

Dashboard Shows:
✓ Colorful word cloud
✓ List of top 20 words with counts
✓ List of top 10 skull reactions
✓ "Last updated" timestamp
✓ Auto-updates every 30 seconds
```

You're all set! 🚀
