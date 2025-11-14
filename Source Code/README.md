# 🎓 University Exam Paper Management System

A secure, role-based exam paper management system with version control and approval workflow.

---

## 🚀 Quick Start (For Developers)

### **1. Clone & Install**
```bash
git clone <repository-url>
cd "file web"
npm install
```

### **2. Start Development**
```bash
# Terminal 1: Start emulator
npm run emulator

# Terminal 2: Create test users (first time only)
node seed-simple.js

# Terminal 2: Start app
npm run dev
```

### **3. Access**
- **App**: http://localhost:3000
- **Emulator UI**: http://localhost:4000
- **Login**: `lecturer1@test.com` / `test123456`

**✅ That's it! No Firebase Cloud setup needed for development!**

---

## 📚 Documentation

| File | Purpose | Who Needs It |
|------|---------|--------------|
| **TEAM_SETUP.md** | Complete setup guide | New team members |
| **EMULATOR_GUIDE.md** | How to use emulator | All developers |
| **TEST_ACCOUNTS.md** | All test account credentials | Everyone |
| **TROUBLESHOOTING.md** | Fix common issues | When stuck |
| **SECURITY.md** | Security architecture | Technical reference |

**Start here:** [TEAM_SETUP.md](./TEAM_SETUP.md)

---

## 🎯 Features

### **Role-Based Access Control**
- **Exam Unit Admin**: Approve users, manage departments, final approval
- **HOS (Head of School)**: Review & approve department exam papers
- **Lecturers**: Upload exam papers, submit for review

### **Workflow**
```
Lecturer uploads → HOS reviews → Exam Unit approves → Ready for printing
```

### **Version Control**
- Track all file versions
- View file timeline
- Download any version
- See who changed what

### **Security**
- AES-256-GCM encryption
- Role-based permissions
- Department isolation
- Audit trails

---

## 🏗️ Architecture

### **Local Development (What You Use)**
```
Your Computer:
├── React Frontend (localhost:3000)
├── Firebase Emulator (localhost:4000)
│   ├── Auth Emulator (localhost:9099)
│   ├── Firestore Emulator (localhost:8080)
│   └── Storage Emulator (localhost:9199)
└── Temporary test data

✅ No internet connection to Firebase Cloud
✅ Each developer has own isolated environment
✅ Fast testing (no deploy needed)
```

### **Production (When Deployed)**
```
Internet:
├── React Frontend (https://file-share-f8260.web.app)
├── Firebase Cloud
│   ├── Firebase Authentication
│   ├── Cloud Firestore
│   └── Cloud Storage
└── Real user data

⚠️ Only team lead deploys to production
⚠️ Requires Firebase project access
```

---

## 🗂️ Database Structure

### **Collections:**

#### **users/**
```javascript
{
  email: "lecturer1@test.com",
  displayName: "Dr. Ali Rahman",
  role: "lecturer",  // pending | lecturer | hos | exam_unit
  department: "cs-dept",
  subjects: ["cs101", "cs201"],
  status: "approved"
}
```

#### **departments/**
```javascript
{
  name: "Computer Science",
  code: "CS",
  description: "Department of Computer Science"
}
```

#### **files/**
```javascript
{
  fileName: "CS101_Final_Exam.pdf",
  fileSize: 2048000,
  createdBy: "user_id",
  createdByName: "Dr. Ali Rahman",
  departmentId: "cs-dept",
  subjectCode: "CS101",
  workflowStatus: "PENDING_HOS_REVIEW",
  version: 2,
  encryptionKey: "...",
  downloadURL: "gs://...",
  downloads: 5,
  downloadHistory: [...]
}
```

#### **fileVersions/**
```javascript
{
  fileId: "file001",
  version: 2,
  description: "Fixed formatting issues",
  uploadedBy: "user_id",
  uploadedAt: Timestamp
}
```

#### **feedback/**
```javascript
{
  fileId: "file001",
  reviewerRole: "hos",
  action: "APPROVED",
  comments: "Looks good",
  createdAt: Timestamp
}
```

---

## 🔄 Workflow States

| Status | Description | Next Action |
|--------|-------------|-------------|
| `DRAFT` | Lecturer created, not submitted | Submit for review |
| `PENDING_HOS_REVIEW` | Waiting for HOS review | HOS approve/reject |
| `NEEDS_REVISION` | HOS requested changes | Lecturer uploads new version |
| `PENDING_EXAM_UNIT` | HOS approved, awaiting final | Exam Unit approve/reject |
| `APPROVED` | Final approval | Ready for printing |

---

## 👥 User Roles & Permissions

| Action | Lecturer | HOS | Exam Unit |
|--------|----------|-----|-----------|
| Upload files | ✅ | ❌ | ❌ |
| Submit for review | ✅ | ❌ | ❌ |
| View own files | ✅ | - | - |
| View department files | ❌ | ✅ | ✅ |
| Review files | ❌ | ✅ | ✅ |
| Approve/Reject | ❌ | ✅ | ✅ |
| Final approval | ❌ | ❌ | ✅ |
| Manage users | ❌ | ❌ | ✅ |
| Manage departments | ❌ | ❌ | ✅ |
| Version history | ✅ | ✅ | ✅ |
| File timeline | ✅ | ✅ | ✅ |

---

## 🛠️ Tech Stack

**Frontend:**
- React 18
- React Router
- TailwindCSS
- Lucide Icons

**Backend:**
- Firebase Authentication
- Cloud Firestore
- Firebase Storage
- Firebase Hosting

**Security:**
- AES-256-GCM Encryption
- Role-based access control
- Firestore Security Rules

**Development:**
- Vite (Build tool)
- Firebase Emulator Suite
- ESLint

---

## 📦 Project Structure

```
file web/
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── FileCard.jsx
│   │   ├── Navbar.jsx
│   │   └── ...
│   ├── pages/              # Page components
│   │   ├── Dashboard.jsx
│   │   ├── Upload.jsx
│   │   ├── HOSReview.jsx
│   │   ├── ExamUnitReview.jsx
│   │   ├── AdminPanel.jsx
│   │   └── ...
│   ├── services/           # Business logic
│   │   ├── authService.js
│   │   ├── firestoreService.js
│   │   ├── storageService.js
│   │   └── encryptionService.js
│   └── utils/              # Helper functions
│
├── firebase.json           # Firebase & Emulator config
├── firestore.rules         # Database security rules
├── firestore.indexes.json  # Database indexes
├── seed-simple.js          # Create test data
├── package.json            # Dependencies
│
└── Documentation/
    ├── TEAM_SETUP.md       # Setup guide for team
    ├── EMULATOR_GUIDE.md   # Emulator usage
    ├── TEST_ACCOUNTS.md    # Test credentials
    ├── TROUBLESHOOTING.md  # Common issues
    └── SECURITY.md         # Security details
```

---

## 🧪 Test Accounts

All passwords: `test123456`

| Email | Role | Department |
|-------|------|------------|
| `examunit@test.com` | Exam Unit | - |
| `hos.cs@test.com` | HOS | Computer Science |
| `hos.me@test.com` | HOS | Mechanical Engineering |
| `hos.ee@test.com` | HOS | Electrical Engineering |
| `lecturer1@test.com` | Lecturer | Computer Science |
| `lecturer2@test.com` | Lecturer | Mechanical Engineering |
| `lecturer3@test.com` | Lecturer | Electrical Engineering |

See [TEST_ACCOUNTS.md](./TEST_ACCOUNTS.md) for full details.

---

## 🚀 Deployment (Production)

**Only team lead should deploy:**

```bash
# Build production version
npm run build

# Deploy to Firebase Hosting
firebase deploy --only hosting

# Deploy everything (hosting + rules + indexes)
firebase deploy
```

**Live URL:** https://file-share-f8260.web.app

---

## 🔐 Security Notes

- Files encrypted with AES-256-GCM before upload
- Encryption keys stored in Firestore
- Role-based access via Firestore Security Rules
- Department isolation enforced
- Audit trail for all actions
- See [SECURITY.md](./SECURITY.md) for details

---

## 🐛 Troubleshooting

**Common issues:**

- **Port 8080 in use**: Kill the process using `taskkill` (see TROUBLESHOOTING.md)
- **Can't login**: Make sure you ran `node seed-simple.js`
- **Emulator not starting**: Check if Java processes are hung
- **Changes not showing**: Hard refresh browser (Ctrl+Shift+R)

See [TROUBLESHOOTING.md](./TROUBLESHOOTING.md) for full guide.

---

## 📝 Development Workflow

### **Daily Routine:**
```bash
# Morning: Start emulator
npm run emulator

# Start React app
npm run dev

# Code all day...
# Save → Browser auto-refreshes → Test

# Evening: Stop everything
Ctrl+C (both terminals)
```

### **Feature Development:**
```bash
# Create feature branch
git checkout -b feature/my-feature

# Develop & test locally

# Commit & push
git add .
git commit -m "Added feature"
git push origin feature/my-feature

# Create Pull Request
# Wait for review & merge
```

---

## 🆘 Need Help?

1. **Check documentation** (files above)
2. **Check browser console** (F12 → Console)
3. **Check Emulator UI** (http://localhost:4000)
4. **See TROUBLESHOOTING.md**
5. **Ask team lead**

---

## 📄 License

[Add your license here]

---

## 👥 Team

[Add team members here]

---

**Built for efficient and secure exam paper management** 🎓🔒

**Version:** 2.0 (with Firebase Emulator support)  
**Last Updated:** November 11, 2025
