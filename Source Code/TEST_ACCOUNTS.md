# 🔐 Test Accounts Reference

## Quick Login Credentials

All passwords: `test123456`

---

## 👥 Users Overview

**Total: 7 users**
- 1 Exam Unit Admin
- 3 HOS (Head of School)
- 3 Lecturers

---

## 📋 Complete Account List

### **1️⃣ Exam Unit Admin (1)**

| Email | Password | Role | Department | Purpose |
|-------|----------|------|------------|---------|
| `examunit@test.com` | `test123456` | Exam Unit | - | Admin access, approve users, final review |

---

### **2️⃣ HOS - Head of School (3)**

| Email | Password | Role | Department | Name |
|-------|----------|------|------------|------|
| `hos.cs@test.com` | `test123456` | HOS | Computer Science | Dr. Ahmad bin Hassan |
| `hos.me@test.com` | `test123456` | HOS | Mechanical Engineering | Prof. Sarah Abdullah |
| `hos.ee@test.com` | `test123456` | HOS | Electrical Engineering | Dr. Raj Kumar |

---

### **3️⃣ Lecturers (3)**

| Email | Password | Role | Department | Subjects | Name |
|-------|----------|------|------------|----------|------|
| `lecturer1@test.com` | `test123456` | Lecturer | Computer Science | CS101, CS201 | Dr. Ali Rahman |
| `lecturer2@test.com` | `test123456` | Lecturer | Mechanical Engineering | ME101, ME201 | Dr. Siti Nurhaliza |
| `lecturer3@test.com` | `test123456` | Lecturer | Electrical Engineering | EE101, EE201 | Dr. Kumar Subramaniam |

---

## 🏫 Departments Structure

### **Computer Science (CS)**
- **HOS**: Dr. Ahmad bin Hassan (`hos.cs@test.com`)
- **Lecturer**: Dr. Ali Rahman (`lecturer1@test.com`)
- **Subjects**:
  - CS101: Introduction to Programming
  - CS201: Data Structures and Algorithms

---

### **Mechanical Engineering (ME)**
- **HOS**: Prof. Sarah Abdullah (`hos.me@test.com`)
- **Lecturer**: Dr. Siti Nurhaliza (`lecturer2@test.com`)
- **Subjects**:
  - ME101: Engineering Mechanics
  - ME201: Thermodynamics

---

### **Electrical Engineering (EE)**
- **HOS**: Dr. Raj Kumar (`hos.ee@test.com`)
- **Lecturer**: Dr. Kumar Subramaniam (`lecturer3@test.com`)
- **Subjects**:
  - EE101: Circuit Analysis
  - EE201: Digital Electronics

---

## 🎯 Test Scenarios

### **Scenario 1: Lecturer Uploads Exam Paper**
1. Login as `lecturer1@test.com` (CS Dept)
2. Upload exam paper for CS101
3. Submit for HOS review

### **Scenario 2: HOS Reviews Paper**
1. Login as `hos.cs@test.com`
2. Review paper from Dr. Ali Rahman
3. Approve or Reject with comments

### **Scenario 3: Exam Unit Final Approval**
1. Login as `examunit@test.com`
2. Review HOS-approved papers
3. Final approval for printing

### **Scenario 4: Cross-Department Testing**
- ME Lecturer uploads → ME HOS reviews
- EE Lecturer uploads → EE HOS reviews
- Test department isolation

---

## 🔄 Workflow Example

```
Lecturer (lecturer1@test.com)
    ↓ Upload CS101 Exam Paper
    ↓ Submit for Review
    
HOS CS (hos.cs@test.com)
    ↓ Review Paper
    ↓ Approve with Comments
    
Exam Unit (examunit@test.com)
    ↓ Final Review
    ↓ Approve
    
✅ Paper Ready for Printing
```

---

## 📊 Access Matrix

| Feature | Exam Unit | HOS | Lecturer |
|---------|-----------|-----|----------|
| Upload Files | ❌ | ❌ | ✅ |
| Submit for Review | ❌ | ❌ | ✅ |
| Review Department Files | ✅ | ✅ (own dept) | ❌ |
| Approve/Reject | ✅ | ✅ (own dept) | ❌ |
| Final Approval | ✅ | ❌ | ❌ |
| Approve Users | ✅ | ❌ | ❌ |
| Manage Departments | ✅ | ❌ | ❌ |
| View All Files | ✅ | ❌ | ❌ |
| Version History | ✅ | ✅ | ✅ (own files) |
| File Timeline | ✅ | ✅ | ✅ (own files) |

---

## 🚀 Quick Test Commands

### **Start Emulator & Seed Data**
```bash
# Terminal 1
npm run emulator

# Terminal 2
npm run seed
npm run dev
```

### **Access Points**
- App: http://localhost:3000
- Emulator UI: http://localhost:4000

---

## 💡 Testing Tips

1. **Test Each Role**: Login as each user type to verify permissions
2. **Test Workflow**: Upload → HOS Review → Exam Unit Approval
3. **Test Department Isolation**: HOS CS can't see ME files
4. **Test Version Control**: Upload new version, check history
5. **View in Emulator UI**: http://localhost:4000 to see all data

---

## 📝 Notes

- All accounts created automatically by `npm run seed`
- Data is temporary (deleted when emulator stops)
- Run `npm run seed` again to recreate accounts
- Production deployment will need real users
- Change passwords in production!

---

**Last Updated:** November 11, 2025  
**Password for ALL accounts:** `test123456`  
**Total Users:** 7 (1 Admin + 3 HOS + 3 Lecturers)

