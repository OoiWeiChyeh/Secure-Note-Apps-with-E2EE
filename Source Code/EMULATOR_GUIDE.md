# 🔥 Firebase Emulator - Local Development Guide

## 🎯 What is Firebase Emulator?

Firebase Emulator lets you run Firebase services (Auth, Firestore, Storage) **on your own computer (localhost)** instead of using the cloud. This means:

- ✅ **Instant testing** - No deploy needed!
- ✅ **Free forever** - No Firebase billing
- ✅ **Safe development** - Can't break production
- ✅ **Team collaboration** - Each developer has their own database
- ✅ **Offline development** - Works without internet (after first setup)

---

## 🚀 Quick Start (First Time Setup)

### **1. Install Firebase CLI** (if not already installed)
```bash
npm install -g firebase-tools
firebase login
```

### **2. Clone & Install**
```bash
git clone <repository-url>
cd "file web"
npm install
```

### **3. Start Firebase Emulators** (Terminal 1)
```bash
npm run emulator
```

**You'll see:**
```
✔ All emulators ready! It is now safe to connect your app.
┌─────────────┬────────────────┬─────────────────────────────────┐
│ Emulator    │ Host:Port      │ View in Emulator UI             │
├─────────────┼────────────────┼─────────────────────────────────┤
│ Auth        │ localhost:9099 │ http://localhost:4000/auth      │
│ Firestore   │ localhost:8080 │ http://localhost:4000/firestore │
│ Storage     │ localhost:9199 │ http://localhost:4000/storage   │
└─────────────┴────────────────┴─────────────────────────────────┘
```

### **4. Populate Test Data** (Terminal 2 - First time only)
```bash
npm run seed
```

**You'll see:**
```
✅ Seed completed successfully!

📝 Test Accounts Created:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Email                 | Password      | Role
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
examunit@test.com     | test123456    | exam_unit
hos.cs@test.com       | test123456    | hos
lecturer1@test.com    | test123456    | lecturer
...
```

### **5. Start React App** (Terminal 2)
```bash
npm run dev
```

**You'll see:**
```
  VITE v5.0.8  ready in 350 ms

  ➜  Local:   http://localhost:3000/
  ➜  press h + enter to show help
```

### **6. Open Your Browser**
- **React App**: http://localhost:3000
- **Emulator UI**: http://localhost:4000 (view database like phpMyAdmin!)

---

## 📖 Daily Workflow

### **Morning - Start Work**

#### **Terminal 1: Start Emulators**
```bash
cd "file web"
npm run emulator
```
*Keep this running all day!*

#### **Terminal 2: Start React App**
```bash
cd "file web"
npm run dev
```
*Keep this running all day!*

#### **First Time Today? Add Test Data (Terminal 3)**
```bash
npm run seed
```
*Only needed once per day or when you restart emulators*

---

### **During Development**

```
1. Edit code in VS Code
2. Save file (Ctrl+S)
3. Browser auto-refreshes (2 seconds)
4. Test immediately!
5. Repeat!
```

**No build, no deploy, instant feedback!** 🚀

---

### **View Data in Emulator UI**

Open: http://localhost:4000

You can see:
- **Authentication** tab → All users
- **Firestore** tab → All database collections (like phpMyAdmin!)
- **Storage** tab → All uploaded files
- **Logs** tab → See what's happening

**Just like phpMyAdmin but for Firebase!**

---

### **End of Day - Stop Everything**

In both terminals: **Press Ctrl+C**

```
Terminal 1: Ctrl+C (stops emulators)
Terminal 2: Ctrl+C (stops React app)
```

**All data deleted!** (This is good - clean slate tomorrow)

---

## 👥 Team Collaboration

### **How Multiple Developers Work Together**

```
Developer A (Your PC):
├── npm run emulator → OWN local database
├── npm run dev      → OWN React app
└── npm run seed     → OWN test data

Developer B (Teammate's laptop):
├── npm run emulator → OWN local database
├── npm run dev      → OWN React app
└── npm run seed     → OWN test data

No conflicts! Everyone has their own environment!
```

### **When Your Feature is Ready**

```bash
# Save your work
git add .
git commit -m "Added HOS dashboard feature"
git push

# Team lead reviews and deploys to production
npm run build
firebase deploy
```

---

## 🔐 Test Accounts

After running `npm run seed`, you can login with:

### **1 Exam Unit Admin**
| Email | Password | Role | Purpose |
|-------|----------|------|---------|
| `examunit@test.com` | `test123456` | Exam Unit | Admin, approve users, final review |

### **3 HOS (Head of School)**
| Email | Password | Department | Name |
|-------|----------|------------|------|
| `hos.cs@test.com` | `test123456` | Computer Science | Dr. Ahmad bin Hassan |
| `hos.me@test.com` | `test123456` | Mechanical Engineering | Prof. Sarah Abdullah |
| `hos.ee@test.com` | `test123456` | Electrical Engineering | Dr. Raj Kumar |

### **3 Lecturers**
| Email | Password | Department | Subjects |
|-------|----------|------------|----------|
| `lecturer1@test.com` | `test123456` | Computer Science | CS101, CS201 |
| `lecturer2@test.com` | `test123456` | Mechanical Engineering | ME101, ME201 |
| `lecturer3@test.com` | `test123456` | Electrical Engineering | EE101, EE201 |

**All passwords:** `test123456`  
**See full details:** `TEST_ACCOUNTS.md`

---

## 🆚 Localhost vs Production

### **When You Run Locally (localhost:3000)**
```
Your Code → Firebase Emulator (YOUR computer)
            ↓
            Temporary database
            Temporary users
            Temporary files
            
When you stop emulator: ALL DELETED ✅
```

### **When Deployed (file-share-f8260.web.app)**
```
Your Code → Firebase Cloud (Google servers)
            ↓
            Real database
            Real users
            Real files
            
Permanent! ✅
```

**They're completely separate!** You can't accidentally break production.

---

## ⚠️ Important Notes

### **Data is Temporary**
```
Start emulator → Fresh empty database
Run seed       → Add test data
Stop emulator  → ALL DATA DELETED
Next day       → Run seed again
```

This is **GOOD** because:
- ✅ Clean slate every time
- ✅ No pollution from old tests
- ✅ Consistent test environment

### **Production is Safe**
- Emulator only works on localhost
- Can't accidentally affect real users
- Deploy to production only when ready

---

## 🐛 Troubleshooting

### **Problem: Port already in use**
```
Error: Port 8080 is not available
```

**Solution:**
```bash
# Kill the process using that port
netstat -ano | findstr :8080
taskkill /PID <process_id> /F
```

### **Problem: Can't connect to emulator**
```
Error: Connection refused
```

**Solution:**
1. Make sure emulator is running: `npm run emulator`
2. Check http://localhost:4000 loads
3. Restart both terminals

### **Problem: No test data**
```
Login shows "Invalid credentials"
```

**Solution:**
```bash
# Run seed script
npm run seed
```

### **Problem: Emulator won't start**
```
Error: firebase-tools not found
```

**Solution:**
```bash
# Install Firebase CLI globally
npm install -g firebase-tools
firebase login
```

---

## 📊 URLs Reference

| Service | URL | What is it? |
|---------|-----|-------------|
| **React App** | http://localhost:3000 | Your application |
| **Emulator UI** | http://localhost:4000 | View database/users |
| **Firestore** | localhost:8080 | Database backend |
| **Auth** | localhost:9099 | Login backend |
| **Storage** | localhost:9199 | File storage backend |
| **Production** | https://file-share-f8260.web.app | Live site |

---

## 🎯 Common Commands

```bash
# Start emulator
npm run emulator

# Start React app
npm run dev

# Add test data
npm run seed

# Build for production
npm run build

# Deploy to production
firebase deploy

# View emulator data
# Open: http://localhost:4000
```

---

## 💡 Tips & Tricks

### **Tip 1: Keep Emulator Running**
Don't restart emulator between code changes. Just keep it running!

### **Tip 2: Use Emulator UI**
http://localhost:4000 is your best friend. View all data visually!

### **Tip 3: Check Console**
Your browser console will show:
```
🔥 Firebase Emulator Mode Enabled
📍 Auth: http://localhost:9099
📍 Firestore: http://localhost:8080
...
```

### **Tip 4: Git Workflow**
```bash
# Create feature branch
git checkout -b feature/new-dashboard

# Develop with emulator (fast!)
# Make changes, test immediately

# When done
git push

# Create pull request
# Team reviews
# Merge to main
# Deploy to production
```

---

## ❓ Need Help?

**Can't figure something out?**

1. Check this guide first
2. Check http://localhost:4000 (emulator UI)
3. Check browser console (F12)
4. Check terminal for errors
5. Ask team lead

---

## 🎉 Success Checklist

Before you start developing, verify:

- [ ] Emulator running (Terminal 1)
- [ ] React app running (Terminal 2)
- [ ] Can access http://localhost:3000
- [ ] Can access http://localhost:4000
- [ ] Can login with test account
- [ ] Can see test data
- [ ] Browser console shows "Firebase Emulator Mode Enabled"

**All checked? You're ready to code!** 🚀

---

**Questions?** Ask your team lead or check the Firebase Emulator docs:
https://firebase.google.com/docs/emulator-suite

