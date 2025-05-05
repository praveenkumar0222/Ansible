# **Study Material: Day 6 - Ansible Variables and Variable Precedence**

---

## **Table of Contents**
1. **Introduction to Ansible Variables**
   - What are Ansible Variables?
   - Why Use Variables?
2. **Types of Variables in Ansible**
   - Playbook Variables
   - Inventory Variables
   - Role Variables
   - Host Variables
   - Group Variables
   - Extra Variables
3. **Variable Precedence**
   - Understanding Variable Precedence
   - Precedence Hierarchy
4. **Using Variables in Playbooks**
   - Example: Using Variables in a Playbook
   - Best Practices for Using Variables
5. **Conclusion and Next Steps**

---

## **1. Introduction to Ansible Variables**

### **What are Ansible Variables?**
Variables in Ansible are used to store values that can be reused throughout your playbooks, roles, and inventory. They make your playbooks more flexible and reusable.

### **Why Use Variables?**
- **Reusability**: Variables allow you to reuse values across multiple playbooks and roles.
- **Flexibility**: Variables make it easy to customize playbooks for different environments.
- **Maintainability**: Using variables makes your playbooks easier to maintain and update.

---

## **2. Types of Variables in Ansible**

### **Playbook Variables**
- Defined within a playbook using the `vars` keyword.
- Example:
  ```yaml
  - hosts: all
    vars:
      http_port: 80
    tasks:
      - name: Ensure Apache is installed
        apt:
          name: apache2
          state: present
  ```

### **Inventory Variables**
- Defined in the inventory file for specific hosts or groups.
- Example:
  ```ini
  [webservers]
  web1.example.com http_port=80
  web2.example.com http_port=8080
  ```

### **Role Variables**
- Defined within a role in the `vars` directory.
- Example:
  ```yaml
  # roles/web_server/vars/main.yml
  http_port: 80
  ```

### **Host Variables**
- Defined for specific hosts in the inventory file.
- Example:
  ```ini
  [webservers]
  web1.example.com http_port=80
  web2.example.com http_port=8080
  ```

### **Group Variables**
- Defined for groups of hosts in the inventory file.
- Example:
  ```ini
  [webservers:vars]
  http_port=80
  ```

### **Extra Variables**
- Defined at runtime using the `--extra-vars` option.
- Example:
  ```bash
  ansible-playbook -i inventory.ini playbook.yml --extra-vars "http_port=8080"
  ```

---

## **3. Variable Precedence**

### **Understanding Variable Precedence**
Variable precedence determines which value is used when the same variable is defined in multiple places. Ansible follows a specific hierarchy to resolve variable precedence.

### **Precedence Hierarchy**
1. **Extra Variables**: Highest precedence.
2. **Playbook Variables**: Defined in the playbook using `vars`.
3. **Role Variables**: Defined in the `vars` directory of a role.
4. **Inventory Variables**: Defined in the inventory file.
5. **Host Variables**: Defined for specific hosts in the inventory file.
6. **Group Variables**: Defined for groups of hosts in the inventory file.
7. **Role Defaults**: Defined in the `defaults` directory of a role. Lowest precedence.

---

## **4. Using Variables in Playbooks**

### **Example: Using Variables in a Playbook**
```yaml
---
- name: Configure Web Server
  hosts: webservers
  vars:
    http_port: 80
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present

    - name: Configure Apache to listen on the specified port
      lineinfile:
        path: /etc/apache2/ports.conf
        regexp: '^Listen '
        line: 'Listen {{ http_port }}'
        state: present
      notify: Restart Apache

  handlers:
    - name: Restart Apache
      service:
        name: apache2
        state: restarted
```

### **Best Practices for Using Variables**
- **Use Descriptive Names**: Use meaningful names for variables to make your playbooks easier to understand.
- **Avoid Hardcoding**: Use variables instead of hardcoding values in your playbooks.
- **Use Defaults**: Define default values for variables in the `defaults` directory of a role.
- **Document Variables**: Document the purpose and usage of variables in the `README.md` file of your role.

---

## **5. Conclusion and Next Steps**

### **What We Learned**
- **Ansible Variables**: Used to store values that can be reused throughout your playbooks, roles, and inventory.
- **Types of Variables**: Playbook variables, inventory variables, role variables, host variables, group variables, and extra variables.
- **Variable Precedence**: Determines which value is used when the same variable is defined in multiple places.
- **Using Variables in Playbooks**: Example of using variables to configure a web server.

### **Next Steps**
- **Day 7**: Advanced variable techniques, including using `set_fact` and `register`.
- **Day 8**: Using Ansible for configuration management and deployment.

---

## **Images and Tables**

### **Variable Precedence Hierarchy**
1. **Extra Variables**
2. **Playbook Variables**
3. **Role Variables**
4. **Inventory Variables**
5. **Host Variables**
6. **Group Variables**
7. **Role Defaults**

### **Example Playbook Using Variables**
```yaml
---
- name: Configure Web Server
  hosts: webservers
  vars:
    http_port: 80
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present

    - name: Configure Apache to listen on the specified port
      lineinfile:
        path: /etc/apache2/ports.conf
        regexp: '^Listen '
        line: 'Listen {{ http_port }}'
        state: present
      notify: Restart Apache

  handlers:
    - name: Restart Apache
      service:
        name: apache2
        state: restarted
```

---

## **References**
- [Ansible Documentation](https://docs.ansible.com/)
- [Ansible Variables Guide](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html)
- [Ansible Variable Precedence](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence)

---

This study material provides a comprehensive guide to Ansible variables, including types of variables, variable precedence, and best practices. It is designed to help you understand the core concepts and apply them in real-world scenarios.




Study Material: Day 6 - Ansible Variables and Variable Precedence
________________________________________
Table of Contents
1.	Introduction to Ansible Variables 
o	What are Ansible Variables?
o	Why Use Variables?
2.	Types of Variables in Ansible 
o	Playbook Variables
o	Inventory Variables
o	Role Variables
o	Host Variables
o	Group Variables
o	Extra Variables
3.	Variable Precedence 
o	Understanding Variable Precedence
o	Precedence Hierarchy
4.	Using Variables in Playbooks 
o	Example: Using Variables in a Playbook
o	Best Practices for Using Variables
5.	Conclusion and Next Steps
________________________________________
1. Introduction to Ansible Variables
What are Ansible Variables?
Variables in Ansible are used to store values that can be reused throughout your playbooks, roles, and inventory. They make your playbooks more flexible and reusable.
Why Use Variables?
•	Reusability: Variables allow you to reuse values across multiple playbooks and roles.
•	Flexibility: Variables make it easy to customize playbooks for different environments.
•	Maintainability: Using variables makes your playbooks easier to maintain and update.
________________________________________
2. Types of Variables in Ansible
Playbook Variables
•	Defined within a playbook using the vars keyword.
•	Example: 
•	- hosts: all
•	  vars:
•	    http_port: 80
•	  tasks:
•	    - name: Ensure Apache is installed
•	      apt:
•	        name: apache2
•	        state: present
Inventory Variables
•	Defined in the inventory file for specific hosts or groups.
•	Example: 
•	[webservers]
•	web1.example.com http_port=80
•	web2.example.com http_port=8080
Role Variables
•	Defined within a role in the vars directory.
•	Example: 
•	# roles/web_server/vars/main.yml
•	http_port: 80
Host Variables
•	Defined for specific hosts in the inventory file.
•	Example: 
•	[webservers]
•	web1.example.com http_port=80
•	web2.example.com http_port=8080
Group Variables
•	Defined for groups of hosts in the inventory file.
•	Example: 
•	[webservers:vars]
•	http_port=80
Extra Variables
•	Defined at runtime using the --extra-vars option.
•	Example: 
•	ansible-playbook -i inventory.ini playbook.yml --extra-vars "http_port=8080"
________________________________________
3. Variable Precedence
Understanding Variable Precedence
Variable precedence determines which value is used when the same variable is defined in multiple places. Ansible follows a specific hierarchy to resolve variable precedence.
Precedence Hierarchy
1.	Extra Variables: Highest precedence.
2.	Playbook Variables: Defined in the playbook using vars.
3.	Role Variables: Defined in the vars directory of a role.
4.	Inventory Variables: Defined in the inventory file.
5.	Host Variables: Defined for specific hosts in the inventory file.
6.	Group Variables: Defined for groups of hosts in the inventory file.
7.	Role Defaults: Defined in the defaults directory of a role. Lowest precedence.
________________________________________
4. Using Variables in Playbooks
Example: Using Variables in a Playbook
---
- name: Configure Web Server
  hosts: webservers
  vars:
    http_port: 80
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present

    - name: Configure Apache to listen on the specified port
      lineinfile:
        path: /etc/apache2/ports.conf
        regexp: '^Listen '
        line: 'Listen {{ http_port }}'
        state: present
      notify: Restart Apache

  handlers:
    - name: Restart Apache
      service:
        name: apache2
        state: restarted
Best Practices for Using Variables
•	Use Descriptive Names: Use meaningful names for variables to make your playbooks easier to understand.
•	Avoid Hardcoding: Use variables instead of hardcoding values in your playbooks.
•	Use Defaults: Define default values for variables in the defaults directory of a role.
•	Document Variables: Document the purpose and usage of variables in the README.md file of your role.
________________________________________
5. Conclusion and Next Steps
What We Learned
•	Ansible Variables: Used to store values that can be reused throughout your playbooks, roles, and inventory.
•	Types of Variables: Playbook variables, inventory variables, role variables, host variables, group variables, and extra variables.
•	Variable Precedence: Determines which value is used when the same variable is defined in multiple places.
•	Using Variables in Playbooks: Example of using variables to configure a web server.
Next Steps
•	Day 7: Advanced variable techniques, including using set_fact and register.
•	Day 8: Using Ansible for configuration management and deployment.
________________________________________
Images and Tables
Variable Precedence Hierarchy
1.	Extra Variables
2.	Playbook Variables
3.	Role Variables
4.	Inventory Variables
5.	Host Variables
6.	Group Variables
7.	Role Defaults
Example Playbook Using Variables
---
- name: Configure Web Server
  hosts: webservers
  vars:
    http_port: 80
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present

    - name: Configure Apache to listen on the specified port
      lineinfile:
        path: /etc/apache2/ports.conf
        regexp: '^Listen '
        line: 'Listen {{ http_port }}'
        state: present
      notify: Restart Apache

  handlers:
    - name: Restart Apache
      service:
        name: apache2
        state: restarted
________________________________________
References
•	Ansible Documentation
•	Ansible Variables Guide
•	Ansible Variable Precedence
________________________________________
This study material provides a comprehensive guide to Ansible variables, including types of variables, variable precedence, and best practices. It is designed to help you understand the core concepts and apply them in real-world scenarios.

