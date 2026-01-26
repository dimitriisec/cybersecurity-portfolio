```markdown
# Algorithm for File Updates in Python

## Project description
In this project, you are working as a security specialist at a healthcare company.
Your job is to keep the allow list of IP addresses up to date.
This list controls who can access a restricted network that contains patient information.

Some employees no longer need access, and their IP addresses are listed in a separate **remove list**.
The goal is to write a Python script that:

- Reads the allow list from a file  
- Compares it with the remove list  
- Removes any matching IP addresses from the allow list  
- Updates the file so only authorized IPs remain  

This helps ensure that only authorized employees can reach the restricted system.

---

## Open the file that contains the allow list

```python
import_file = "allow_list.txt"

with open(import_file, "r") as file:
    file_contents = file.read()
```

**Explanation:**

- `import_file` stores the filename as a string  
- `open(import_file, "r")` opens the file in **read** mode  
- `with` ensures the file is properly closed after use  
- `file.read()` reads the entire content of the file into a single string  

This is the first step in reading the allow list and preparing it for updates.

---

## Read the file contents

To read the contents of a file in Python, you use `open()` together with `.read()` inside a `with` statement:

```python
with open("allow_list.txt", "r") as file:
    ip_string = file.read()
```

- `open("filename", "r")` — opens the file in read mode  
- `with` — ensures the file is automatically closed  
- `.read()` — returns the entire file content as one string  

The result is stored in a variable (for example, `ip_string`) for further processing.

---

## Convert the string into a list

When you read the file, all IP addresses are stored as one long string. To work with individual IPs, you need to split this string into a list:

```python
ip_addresses = ip_string.split()
```

- `.split()` splits the string on whitespace by default  
- The result is a list where each element is an IP address  

Now you can process each IP address individually.

---

## Iterate through the remove list

Assume you already have a list called `remove_list` that contains IPs to be removed.  
You can iterate through it using a `for` loop:

```python
for ip in remove_list:
    if ip in ip_addresses:
        ip_addresses.remove(ip)
```

- The loop goes through each IP in `remove_list`  
- The `if` condition checks whether that IP is present in `ip_addresses`  
- If it is, `.remove()` deletes it from the allow list  

This ensures that any IP address found in both lists is removed from the allow list.

---

## Update the file with the revised list of IP addresses

After filtering the IP addresses, you need to write the updated list back to the file:

```python
with open(import_file, "w") as file:
    file.write(" ".join(ip_addresses))
```

**Explanation:**

- Opening the file in `"w"` mode clears its existing contents  
- `" ".join(ip_addresses)` converts the list back into a single string, with spaces between IPs (you could also use `"\n"` if you want one IP per line)  
- `file.write()` saves the updated allow list to the file  

Now the file contains only the IP addresses that are still allowed access—those **not** present in the remove list.

---

## Summary

In this project, you built a simple Python algorithm to keep an IP allow list accurate and secure:

1. Read the allow list from a file  
2. Convert the file contents into a list of IP addresses  
3. Compare the allow list against a remove list  
4. Remove any matching IP addresses  
5. Write the updated list back to the original file  

This straightforward process helps protect a restricted healthcare network by ensuring that only the right employees maintain access based on their IP addresses.
```
