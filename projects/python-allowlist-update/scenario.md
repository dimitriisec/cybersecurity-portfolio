# Scenario

You are a security professional working at a healthcare company. As part of your responsibilities, you must regularly update a file that identifies which employees are allowed to access a restricted subnetwork containing personal patient records.

Access is controlled by IP address:

- The **allow list** contains IP addresses permitted to access the restricted system.
- The **remove list** contains IP addresses belonging to employees who no longer require access.

Your task is to create an algorithm in Python that:

1. Reads the allow list from a file  
2. Compares it against the remove list  
3. Identifies any matching IP addresses  
4. Removes those IPs from the allow list  
5. Updates the allow list file with the revised contents  

This ensures that only authorized employees maintain access to sensitive patient information.
