# 🔒 Linux Non-Interactive User Setup

A step-by-step guide to creating a **non-interactive user** in Linux. Useful for service accounts, automation, CI/CD agents, and secure background operations.

---

## 🎯 Objective

Create a user with a **non-interactive shell** (`/usr/sbin/nologin`) to restrict login access while allowing system-level or automated tasks.
This ensures enhanced security and prevents unnecessary interactive login permissions.

---

## 📋 Prerequisites

* Linux server access
* `sudo` privileges
* Basic understanding of Linux user management
* SSH access

---

## 🔧 Technologies Used

* Linux user management (`useradd`, `userdel`, `grep`)
* SSH
* System administration basics

---

## 🚀 Steps to Create a Non-Interactive User

### **1. SSH into the Server**

```bash
ssh user@app-server-ip
# OR
ssh user@server-name
```

---

### **2. Create User With Non-Interactive Shell**

```bash
sudo useradd -m -s /usr/sbin/nologin username
```

Explanation:

* `-s`: Assign shell (here, `/usr/sbin/nologin` prevents login)
* `-m`: Create home directory under `/home/username`

---

### **3. Verify User Creation**

```bash
grep username /etc/passwd
```

You should see something like:

```
username:x:1002:1002::/home/username:/usr/sbin/nologin
```

---

## 🛠️ Verification & Troubleshooting

### **⚠️ Permission denied?**

Ensure you have `sudo` rights.

### **👤 User already exists?**

```bash
cat /etc/passwd | grep username
```

### **❌ Shell not found?**

Verify that `/usr/sbin/nologin` exists:

```bash
ls /usr/sbin/nologin
```

---

## 📘 Additional Useful Commands

### **List all non-interactive users**

```bash
grep nologin /etc/passwd
```

### **Check user details**

```bash
id username
```

### **Remove a user (with home directory)**

```bash
sudo userdel -r username
```

---

## 🔐 Best Practices for Service Accounts

* ✔️ Do **not** give `sudo` access to service users in production.
* ✔️ Use **SSH keys with restricted permissions** if automation requires secure remote execution.
* ✔️ Keep service accounts **non-interactive** to maintain security and prevent unauthorized access.
* ✔️ Document each service user and its purpose for auditing.

> সার্ভার-অপারেশন/অটোমেশন এর জন্য কখনোই ইন্টারঅ্যাকটিভ লগইন দরকার নেই — সার্ভিস অ্যাকাউন্টগুলোকে non-interactive shell দিয়ে সীমাবদ্ধ রাখা সিকিউরিটি ও অর্ডার বজায় রাখে।

---

## 📄 License

Feel free to use or modify this README for your organization or personal projects.

---

If you want, I can also add **badges, contribution guide, folder structure, or screenshots section**!
