# Linux File Permissions Audit

This project demonstrates how to audit and modify file and directory permissions in a Linux environment. The goal is to ensure that users on the research team have appropriate access while preventing unauthorized access to sensitive files.

The project includes a permissions review, explanation of Linux permission strings, and step‑by‑step examples of modifying permissions using the `chmod` command.

---

## 📄 Included Documents

- **scenario.md** — description of the fictional scenario  
- **file_permissions_in_linux.md** — full analysis and permission changes  
- **current_file_permissions.md** — initial permissions audit (to be added)
- **file_permissions_in_linux.docx**
- **current_file_permissions.docx** — initial permissions audit (to be added) — full analysis and permission changes

---

## 🎯 Objectives

- Review existing file and directory permissions  
- Interpret Linux permission strings  
- Apply correct authorization using `chmod`  
- Remove unauthorized access  
- Strengthen system security through proper permission management  

---

## 🧩 Skills Demonstrated

- Linux command‑line operations  
- File system permission auditing  
- Understanding of user/group/other access  
- Applying permission changes with symbolic and numeric modes  
- Security hardening through least privilege  

---

## 🛡️ Summary of Findings

The audit revealed several inconsistencies between required and actual permissions.  
Using `ls -la`, existing permissions were reviewed, and corrections were applied using `chmod` to:

- Remove unauthorized write access  
- Restrict sensitive files to user‑only access  
- Adjust permissions on hidden files  
- Limit directory access to specific users  

These changes aligned the file system with organizational authorization standards.
