# Table Formats

This document describes the structure of the two tables used in the SQL security investigation project. These tables belong to the organization’s internal database and contain authentication logs and employee information.

---

## 1. `log_in_attempts` Table

The **log_in_attempts** table stores information about every login attempt made within the organization.

### **Columns**

| Column Name  | Description |
|--------------|-------------|
| **event_id** | Unique identification number assigned to each login event |
| **username** | Username of the employee attempting to log in |
| **login_date** | Date when the login attempt occurred |
| **login_time** | Time when the login attempt occurred |
| **country** | Country from which the login attempt originated |
| **ip_address** | IP address of the employee’s device |
| **success** | Indicates whether the login attempt succeeded (`TRUE`) or failed (`FALSE`) |

### **Column Order in MariaDB**

```
event_id
username
login_date
login_time
country
ip_address
success
```

---

## 2. `employees` Table

The **employees** table stores information about employees and the devices assigned to them.

### **Columns**

| Column Name  | Description |
|--------------|-------------|
| **employee_id** | Unique identification number assigned to each employee |
| **device_id** | Identification number of the device assigned to the employee |
| **username** | Employee’s username |
| **department** | Department where the employee works |
| **office** | Office location of the employee |

### **Column Order in MariaDB**

```
employee_id
device_id
username
department
office
```
