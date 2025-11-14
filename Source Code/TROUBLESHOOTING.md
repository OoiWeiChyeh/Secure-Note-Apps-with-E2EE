# 🔧 Troubleshooting Guide

Common issues and solutions for Firebase Emulator setup.

---

## ❌ Problem: "Port 8080 is not open" or "Port taken"

### **Error Message:**
```
!  firestore: Port 8080 is not open on localhost
Error: Could not start Firestore Emulator, port taken.
```

### **Cause:**
Another application is using port 8080. Common culprits:
- XAMPP (Apache or MySQL)
- Previous emulator instance that didn't close properly
- Other development servers
- Oracle services

### **Solution:**

#### **Option 1: Kill the Process (Quick Fix)**

**Step 1: Find what's using port 8080**
```powershell
netstat -ano | findstr :8080
```

You'll see something like:
```
TCP    127.0.0.1:8080    0.0.0.0:0    LISTENING    12345
                                                    ↑ PID
```

**Step 2: Kill the process**
```powershell
taskkill /PID 12345 /F
```

Replace `12345` with the actual PID from step 1.

**Step 3: Try again**
```bash
npm run emulator
```

---

#### **Option 2: Change Emulator Ports**

If you want to keep the other app running, change the emulator ports:

**Edit `firebase.json`:**
```json
{
  "emulators": {
    "auth": {
      "port": 9099
    },
    "firestore": {
      "port": 8081    ← Change from 8080 to 8081
    },
    "storage": {
      "port": 9199
    },
    "ui": {
      "enabled": true,
      "port": 4000
    }
  }
}
```

**Then update `src/firebase.js`:**
```javascript
connectFirestoreEmulator(db, 'localhost', 8081);  // Change to 8081
```

---

#### **Option 3: Stop XAMPP (If Using)**

If you're using XAMPP:
1. Open XAMPP Control Panel
2. Stop Apache
3. Stop MySQL
4. Try `npm run emulator` again

---

## ❌ Problem: "Cannot find module 'firebase/app'"

### **Error Message:**
```
Error: Cannot find module 'firebase/app'
```

### **Solution:**
```bash
npm install
```

The node_modules weren't installed. Run this in your project directory.

---

## ❌ Problem: Emulator starts but app can't connect

### **Symptoms:**
- Emulator UI (http://localhost:4000) works
- React app runs but can't login/register
- Console shows connection errors

### **Solution:**

**Check if emulator mode is enabled:**

Open browser console (F12) and look for:
```
🔥 Firebase Emulator Mode Enabled
📍 Auth: http://localhost:9099
📍 Firestore: http://localhost:8080
📍 Storage: http://localhost:9199
```

If you don't see this:
1. Make sure you're on `http://localhost:3000` (NOT `https://`)
2. Clear browser cache and hard refresh (Ctrl+Shift+R)
3. Restart React app (`npm run dev`)

---

## ❌ Problem: "No test users found" after seeding

### **Symptoms:**
- Ran `npm run seed` successfully
- Can't login with test accounts
- Emulator UI shows no users

### **Solution:**

**Make sure emulator is running FIRST:**
```bash
# Terminal 1: Start emulator (must be running!)
npm run emulator

# Wait for "All emulators ready" message

# Terminal 2: Then seed data
npm run seed
```

**Order matters!** Emulator must be running before you seed.

---

## ❌ Problem: Data disappears after stopping emulator

### **Symptoms:**
- Created test users
- Stopped emulator
- Restarted emulator
- All data gone

### **This is NORMAL!**

Emulator data is **temporary**. This is by design:
- ✅ Clean slate every time
- ✅ No old test data pollution
- ✅ Consistent testing

**Solution:** Run `npm run seed` again after restarting emulator.

---

## ❌ Problem: "EADDRINUSE" or "Port already in use"

### **Error Message:**
```
Error: listen EADDRINUSE: address already in use :::3000
```

### **Cause:**
React dev server port (3000) is in use.

### **Solution:**

**Kill the process:**
```powershell
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

Or just close the terminal running `npm run dev` and start again.

---

## ❌ Problem: Firebase CLI not found

### **Error Message:**
```
'firebase' is not recognized as an internal or external command
```

### **Solution:**

**Install Firebase CLI globally:**
```bash
npm install -g firebase-tools
firebase login
```

Then try again.

---

## ❌ Problem: Emulator UI shows "Unable to connect"

### **Symptoms:**
- http://localhost:4000 loads but shows errors
- Can't see authentication/firestore tabs

### **Solution:**

1. **Check if emulators are actually running:**
   ```bash
   # Should show processes on ports 8080, 9099, 9199, 4000
   netstat -ano | findstr "8080 9099 9199 4000"
   ```

2. **Restart emulators:**
   ```bash
   # Kill all Firebase processes
   taskkill /F /IM java.exe
   taskkill /F /IM node.exe
   
   # Start fresh
   npm run emulator
   ```

---

## ❌ Problem: Changes not reflecting in browser

### **Symptoms:**
- Changed code
- Saved file
- Browser not updating

### **Solution:**

1. **Hard refresh:** Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
2. **Clear cache:** Browser DevTools → Application → Clear Storage
3. **Restart dev server:** Stop `npm run dev` and start again

---

## ❌ Problem: "Permission denied" errors

### **Error Message:**
```
Error: EACCES: permission denied
```

### **Solution (Windows):**

**Run terminal as Administrator:**
1. Right-click PowerShell/Command Prompt
2. "Run as administrator"
3. Navigate to project: `cd "D:\file web"`
4. Try again: `npm run emulator`

---

## ❌ Problem: Seed script fails with auth errors

### **Error Message:**
```
Error creating user: auth/email-already-exists
```

### **This is NORMAL!**

It means users already exist. Either:
1. **Ignore it** - Users are already created
2. **Restart emulator** - Fresh database
3. **Check Emulator UI** - http://localhost:4000/auth to see users

---

## 🔍 General Debugging Steps

When something goes wrong:

### **1. Check Console (F12)**
Look for errors in browser console. Red text = problems!

### **2. Check Emulator UI**
Visit http://localhost:4000 and check:
- Authentication tab → Are users there?
- Firestore tab → Is data there?
- Logs tab → Any errors?

### **3. Check Terminal Output**
Look for error messages in terminals running:
- `npm run emulator`
- `npm run dev`
- `npm run seed`

### **4. Restart Everything**
The "turn it off and on again" approach:
```bash
# Kill all processes
Ctrl+C in both terminals

# Restart emulator
npm run emulator

# Restart React
npm run dev

# Re-seed if needed
npm run seed
```

### **5. Check Ports**
Make sure these ports are free:
```powershell
netstat -ano | findstr "3000 4000 8080 9099 9199"
```

If any are in use, kill those processes or change ports.

---

## 📞 Still Having Issues?

### **Check These:**

- [ ] Node.js installed? (`node --version`)
- [ ] npm works? (`npm --version`)
- [ ] Firebase CLI installed? (`firebase --version`)
- [ ] Logged into Firebase? (`firebase login`)
- [ ] In correct directory? (`cd "D:\file web"`)
- [ ] Ran `npm install`?
- [ ] Emulator running before seeding?
- [ ] Using localhost:3000 (not production URL)?

### **Get Help:**

1. Read the full error message
2. Check this guide for that error
3. Check Firebase docs: https://firebase.google.com/docs/emulator-suite
4. Ask your team lead

---

## 💡 Pro Tips

### **Tip 1: Always check port conflicts first**
Most issues are port conflicts. Before starting emulator:
```powershell
netstat -ano | findstr "8080"
```

### **Tip 2: Use Task Manager**
Windows Task Manager → Details tab → Sort by "PID" to find and kill processes.

### **Tip 3: Create a restart script**
Save time with a PowerShell script:
```powershell
# restart-emulator.ps1
taskkill /F /IM java.exe /T 2>$null
taskkill /F /IM node.exe /T 2>$null
Start-Sleep -Seconds 2
cd "D:\file web"
npm run emulator
```

### **Tip 4: Keep terminals organized**
- Terminal 1: Emulator (keep running)
- Terminal 2: React app (keep running)
- Terminal 3: Commands (seed, etc.)

---

## ✅ Success Checklist

Before reporting a problem, verify:

- [ ] Emulator running (Terminal 1)
- [ ] React app running (Terminal 2)
- [ ] http://localhost:4000 accessible
- [ ] http://localhost:3000 accessible
- [ ] Browser console shows "🔥 Firebase Emulator Mode Enabled"
- [ ] Can see test users at http://localhost:4000/auth
- [ ] Can login with `lecturer1@test.com` / `test123456`

**All checked?** If still not working, see specific error above.

---

**Last Updated:** November 11, 2025  
**Most Common Issue:** Port 8080 already in use (see top of guide)

