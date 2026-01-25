# Apply Filters to SQL Queries

## Project Description

My organization is actively enhancing its system security. As part of my role, I am responsible for safeguarding the infrastructure, identifying and investigating potential vulnerabilities, and ensuring employee devices remain up to date.  
This document demonstrates how SQL filtering techniques were applied to investigate key security‑related events.

---

# 1. Retrieve After‑Hours Failed Login Attempts

A potential security incident occurred outside standard business hours (after **18:00**).  
All failed login attempts during this period required investigation.

### SQL Query

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = FALSE;
```

### Returned Records (sample)

| event_id | username | login_date  | login_time | country | ip_address       | success |
|----------|----------|-------------|------------|---------|------------------|---------|
| 2        | apatel   | 2022‑05‑10  | 20:27:27   | CAN     | 192.168.205.12   | 0       |
| 18       | pwashing | 2022‑05‑11  | 19:28:50   | US      | 192.168.66.142   | 0       |
| 20       | tshah    | 2022‑05‑12  | 18:56:36   | MEXICO  | 192.168.109.50   | 0       |
| 28       | aestrada | 2022‑05‑09  | 19:28:12   | MEXICO  | 192.168.27.57    | 0       |
| 34       | drosas   | 2022‑05‑11  | 21:02:04   | US      | 192.168.45.93    | 0       |
| 42       | cgriffin | 2022‑05‑09  | 23:04:05   | US      | 192.168.4.157    | 0       |
| 52       | cjackson | 2022‑05‑10  | 22:07:07   | CAN     | 192.168.58.57    | 0       |

### Analysis

The query filters for:

- `login_time > '18:00'` — after‑hours activity  
- `success = FALSE` — failed attempts  

This isolates suspicious login attempts requiring further review.

---

# 2. Retrieve Login Attempts on Specific Dates

A suspicious event occurred on **2022‑05‑09**.  
To investigate, login attempts from **May 9** and **May 8** were reviewed.

### SQL Query

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

### Returned Records (sample)

| event_id | username | login_date  | login_time | country | ip_address       | success |
|----------|----------|-------------|------------|---------|------------------|---------|
| 1        | jrafael  | 2022‑05‑09  | 04:56:27   | CAN     | 192.168.243.140  | 1       |
| 3        | dkot     | 2022‑05‑09  | 06:47:41   | USA     | 192.168.151.162  | 1       |
| 4        | dkot     | 2022‑05‑08  | 02:00:39   | USA     | 192.168.178.71   | 0       |
| 8        | bisles   | 2022‑05‑08  | 01:30:17   | US      | 192.168.119.173  | 0       |

### Analysis

The `OR` operator ensures both dates are included.  
This helps identify patterns or anomalies across consecutive days.

---

# 3. Retrieve Login Attempts Outside of Mexico

A review of login activity revealed concerns about attempts originating from outside Mexico.

### SQL Query

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

### Returned Records (sample)

| event_id | username | login_date  | login_time | country | ip_address       | success |
|----------|----------|-------------|------------|---------|------------------|---------|
| 1        | jrafael  | 2022‑05‑09  | 04:56:27   | CAN     | 192.168.243.140  | 1       |
| 2        | apatel   | 2022‑05‑10  | 20:27:27   | CAN     | 192.168.205.12   | 0       |
| 3        | dkot     | 2022‑05‑09  | 06:47:41   | USA     | 192.168.151.162  | 1       |
| 4        | dkot     | 2022‑05‑08  | 02:00:39   | USA     | 192.168.178.71   | 0       |

### Analysis

`NOT country LIKE 'MEX%'` excludes:

- `MEX`  
- `MEXICO`  
- any variation beginning with `MEX`

This ensures all non‑Mexico login attempts are returned.

---

# 4. Retrieve Employees in Marketing (East Building)

The Marketing department in the East building required system upgrades.

### SQL Query

```sql
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';
```

### Returned Records (sample)

| employee_id | device_id      | username | department | office    |
|-------------|----------------|----------|------------|-----------|
| 1000        | a320b137c219   | elarson  | Marketing  | East‑170  |
| 1052        | a192b174c940   | jdarosa  | Marketing  | East‑195  |
| 1075        | x573y883z772   | fbautist | Marketing  | East‑267  |
| 1088        | k8651965m233   | rgosh    | Marketing  | East‑157  |
| 1103        | NULL           | randerss | Marketing  | East‑460  |
| 1156        | a184b775c707   | dellery  | Marketing  | East‑417  |
| 1163        | h6791515j339   | cwilliam | Marketing  | East‑216  |

### Analysis

- `department = 'Marketing'` filters by department  
- `office LIKE 'East%'` filters by building  
- Combined with `AND`, only employees meeting both conditions are returned  

---

# 5. Retrieve Employees in Finance or Sales

These departments required a separate security update.

### SQL Query

```sql
SELECT *
FROM employees
WHERE department = 'Finance' OR department = 'Sales';
```

### Returned Records (sample)

| employee_id | device_id      | username | department | office     |
|-------------|----------------|----------|------------|------------|
| 1003        | d394e816f943   | sgilmore | Finance    | South‑153  |
| 1007        | h1741497j413   | wjaffrey | Finance    | North‑406  |
| 1008        | 1858j583k571   | abernard | Finance    | South‑170  |

### Analysis

The `OR` operator ensures employees from **either** department are included.

---

# 6. Retrieve All Employees Not in IT

A security update was required for all departments except Information Technology.

### SQL Query

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

### Returned Records (sample)

| employee_id | device_id      | username | department       | office      |
|-------------|----------------|----------|------------------|-------------|
| 1000        | a320b137c219   | elarson  | Marketing        | East‑170    |
| 1001        | b239c825d303   | bmoreno  | Marketing        | Central‑276 |
| 1002        | c116d593e558   | tshah    | Human Resources  | North‑434   |

### Analysis

`NOT` excludes the IT department, returning all other employees.

---

# Summary

Across all tasks, SQL filtering techniques were used to:

- Investigate suspicious login attempts  
- Identify after‑hours failed logins  
- Review activity on specific dates  
- Filter by geographic location  
- Retrieve employee device data by department and office  
- Exclude specific departments  

Operators used:

- `AND`  
- `OR`  
- `NOT`  
- `LIKE` with `%` wildcard  

These filters enabled precise extraction of relevant security data for further analysis.

---
