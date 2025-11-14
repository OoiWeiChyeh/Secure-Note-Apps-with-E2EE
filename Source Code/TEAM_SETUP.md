# 👥 Team Development Setup Guide

Quick setup guide for team members joining this project.

---

## 🚀 One-Time Setup (5 minutes)

### **1. Clone Repository**
```bash
git clone <repository-url>
cd "file web"
```

### **2. Install Node Packages**
```bash
npm install
```

### **3. Verify Setup**
Check if everything is installed:
```bash
node --version    # Should show v16 or higher
npm --version     # Should show v8 or higher
```

**That's it for local development!** 🎉

---

### **🔐 Optional: Only If You Need to Deploy**

**Skip this if you're only developing locally!**

If you need to deploy changes to production:

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login to Firebase
firebase login
```

**Note:** You'll also need project access from the team lead.
Ask them to add you at: https://console.firebase.google.com/project/file-share-f8260/settings/iam

---

## 🎯 Daily Workflow (Every Time You Work)

### **Step 1: Pull Latest Changes**
```bash
git pull origin main
```

### **Step 2: Start Firebase Emulator** (Terminal 1)
```bash
npm run emulator
```
Keep this running! You'll see:
```
✔ All emulators ready!
┌─────────────┬────────────────┐
│ Emulator    │ Host:Port      │
├─────────────┼────────────────┤
│ Auth        │ localhost:9099 │
│ Firestore   │ localhost:8080 │
│ Storage     │ localhost:9199 │
│ UI          │ localhost:4000 │
└─────────────┴────────────────┘
```

### **Step 3: Create Test Users** (Terminal 2 - FIRST TIME ONLY)
```bash
node seed-simple.js
```
Creates 7 test users. You'll see:
```
✅ Seed completed!
examunit@test.com | test123456 | exam_unit
hos.cs@test.com   | test123456 | hos
...
```

### **Step 4: Start React App** (Terminal 2)
```bash
npm run dev
```
Opens at http://localhost:3000

### **Step 5: Start Coding! 🎉**
- Edit code in `src/`
- Save file (Ctrl+S)
- Browser auto-refreshes
- Test immediately!

---

## 🔐 Test Accounts

All passwords: `test123456`

| Email | Role | Use For |
|-------|------|---------|
| `examunit@test.com` | Exam Unit | Admin, approve users, final review |
| `hos.cs@test.com` | HOS | Review CS department files |
| `hos.me@test.com` | HOS | Review ME department files |
| `hos.ee@test.com` | HOS | Review EE department files |
| `lecturer1@test.com` | Lecturer | Upload files (CS dept) |
| `lecturer2@test.com` | Lecturer | Upload files (ME dept) |
| `lecturer3@test.com` | Lecturer | Upload files (EE dept) |

See `TEST_ACCOUNTS.md` for full details.

---

## 📊 URLs

| Service | URL | Purpose |
|---------|-----|---------|
| **React App** | http://localhost:3000 | Your development app |
| **Emulator UI** | http://localhost:4000 | View database/users (like phpMyAdmin) |
| **Production** | https://file-share-f8260.web.app | Live site (don't test here!) |

---

## 🔄 Git Workflow

### **Working on a Feature:**
```bash
# 1. Create feature branch
git checkout -b feature/my-feature

# 2. Make changes, test locally

# 3. Commit changes
git add .
git commit -m "Added my feature"

# 4. Push to GitHub
git push origin feature/my-feature

# 5. Create Pull Request on GitHub
# Wait for code review and approval
```

### **Updating Your Local Copy:**
```bash
# Pull latest changes from main
git checkout main
git pull origin main

# Restart emulator if database changed
# (Ctrl+C in emulator terminal, then npm run emulator)
```

---

## ⚠️ Important Rules

### **✅ DO:**
- Work on feature branches
- Test with emulator (localhost)
- Commit working code
- Ask for code review
- Pull latest changes before starting work

### **❌ DON'T:**
- Work directly on `main` branch
- Test on production (https://file-share-f8260.web.app)
- Commit `node_modules/` or `dist/`
- Deploy without team lead approval
- Share Firebase credentials publicly

---

## 🐛 Common Issues

### **Issue: Port already in use**
```bash
# Kill processes using emulator ports
netstat -ano | findstr ":8080"
taskkill /PID <process-id> /F

# Then restart emulator
npm run emulator
```

### **Issue: Emulator UI not loading (localhost:4000)**
- Make sure emulator is running (Terminal 1)
- Wait 10 seconds after starting
- Check `netstat -ano | findstr ":4000"`

### **Issue: Can't login with test accounts**
- Did you run `node seed-simple.js`?
- Check http://localhost:4000/auth - should see 7 users
- Restart emulator and seed again

### **Issue: Changes not showing**
- Hard refresh browser: Ctrl+Shift+R
- Check terminal for React errors
- Make sure `npm run dev` is running

See `TROUBLESHOOTING.md` for more help.

---

## 📚 Documentation

- `EMULATOR_GUIDE.md` - Complete emulator usage guide
- `TEST_ACCOUNTS.md` - All test account details
- `TROUBLESHOOTING.md` - Common issues and fixes
- `START_HERE.md` - Project overview

---

## 🆘 Need Help?

1. Check `TROUBLESHOOTING.md`
2. Check browser console (F12) for errors
3. Check Emulator UI (http://localhost:4000)
4. Ask team lead
5. Check Firebase docs: https://firebase.google.com/docs/emulator-suite

---

## ✅ Setup Checklist

Before starting development, verify:

### **Required for Local Development:**
- [ ] Node.js installed (`node --version`)
- [ ] Repository cloned
- [ ] `npm install` completed
- [ ] Can start emulator (`npm run emulator`)
- [ ] Can seed users (`node seed-simple.js`)
- [ ] Can start React app (`npm run dev`)
- [ ] Can access http://localhost:3000
- [ ] Can access http://localhost:4000
- [ ] Can login with `lecturer1@test.com` / `test123456`
- [ ] Browser console shows "🔥 Firebase Emulator Mode Enabled"

### **Only If You Need to Deploy:**
- [ ] Firebase CLI installed (`firebase --version`)
- [ ] Logged into Firebase (`firebase login`)
- [ ] Have Firebase project access (ask team lead)

**All required items checked? You're ready to code!** 🚀

---

## 🎉 Welcome to the Team!

Happy coding! Remember:
- Test locally with emulator
- Commit often
- Ask questions
- Have fun! 😊

