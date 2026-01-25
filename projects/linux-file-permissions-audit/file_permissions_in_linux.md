# File Permissions in Linux

## Project Description

The research team at the organization needs updated file permissions for certain files and directories within the `projects` directory. Current permissions do not match the required authorization levels. Updating these permissions improves system security.

This project includes reviewing existing permissions and applying necessary changes.

---

## Checking File and Directory Details

To determine existing permissions, the following command was used:
ls -la projects/

This command lists all contents of the directory, including hidden files.  
The output showed:

- One directory: `drafts/`  
- One hidden file: `.project_x.txt`  
- Five project files  

The first column in the output contains a 10‑character permissions string.

---

## Understanding the Permissions String

The 10‑character string represents:

1. **1st character** — file type  
   - `d` = directory  
   - `-` = regular file  

2. **2nd–4th characters** — user permissions (r/w/x)

3. **5th–7th characters** — group permissions (r/w/x)

4. **8th–10th characters** — other permissions (r/w/x)

Example:  
`-rw-rw-r--` for `project_t.txt` means:

- Regular file (`-`)  
- User: read, write  
- Group: read, write  
- Other: read only  

---

## Changing File Permissions

### Removing Write Access for Other

The organization requires that **other** should not have write access to any files.

Example command: chmod o-w project_k.txt ls -la

---

### Restricting Access to Sensitive Files

`project_m.txt` should only be readable/writable by the user.

Example: chmod go-rw project_m.txt ls -la

---

## Changing Permissions on a Hidden File

`.project_x.txt` is archived and should not be writable by anyone.  
User and group should have read access.

Commands used: chmod u-w .project_x.txt chmod g-w .project_x.txt chmod g+r .project_x.txt

---

## Changing Directory Permissions

Only `researcher2` should have access to the `drafts` directory.  
No one else should have execute permissions.

Example: chmod g-x drafts/ ls -la

---

## Summary

To align permissions with organizational standards:

- `ls -la` was used to audit existing permissions  
- `chmod` was applied to remove unauthorized access  
- Sensitive files were restricted  
- Directory access was limited to specific users  

These changes improved the security posture of the research team’s file system.

