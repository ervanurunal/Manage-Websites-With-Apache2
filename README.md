## Apache2 Web Server Configuration

---

### Overview

In this lab, I installed and configured **Apache2**, one of the most widely used web server applications in Linux environments. I deployed a company website, replaced the default Apache webpage, created a custom virtual host, enabled and disabled sites, activated Apache modules, and configured **Server Side Includes (SSI)** functionality.

This lab provided practical experience with:

* Installing Apache2
* Managing Apache services
* Understanding Virtual Hosts
* Configuring websites
* Enabling and disabling sites
* Working with Apache modules
* Configuring Server Side Includes
* Reloading and restarting services

---

### Tools & Technologies

* Linux Virtual Machine
* Apache2
* APT Package Manager
* Nano Text Editor
* Linux Terminal
* HTML / CSS
* Virtual Hosts
* Apache Modules
* Server Side Includes (SSI)

### Lab Type:
Linux Administration / Web Server Management / Networking

---
---

### Apache Directory Structure

| Directory                       | Purpose                       |
| ------------------------------- | ----------------------------- |
| `/var/www/`                     | Stores website files          |
| `/etc/apache2/sites-available/` | Available site configurations |
| `/etc/apache2/sites-enabled/`   | Enabled site configurations   |
| `/etc/apache2/mods-available/`  | Available modules             |
| `/etc/apache2/mods-enabled/`    | Enabled modules               |

Apache manages websites using configuration files and symbolic links between available and enabled sites.

---
---

### 1. Update Package Repository

Before installing software, update package information:

```bash
sudo apt update
```

![1](https://i.imgur.com/XwK4CiC.png)

---

### 2. Install Apache2

Install Apache2:

```bash
sudo apt install apache2
```

![2](https://i.imgur.com/QKn7BJd.png)

Apache automatically installs required dependencies.

---

### 3. Check Apache Service

Verify Apache status:

```bash
sudo service apache2 status
```

![3](https://i.imgur.com/rrQYMHe.png)

If Apache is not running:

```bash
sudo service apache2 start
```

![4](https://i.imgur.com/O64OlKF.png)

---

### 4. Verify Default Website

Open the server IP address in a browser.

Apache displays its default webpage, confirming the web server is functioning correctly.

---

### 5. Review Available Sites

View existing site configurations:

```bash
ls -l /etc/apache2/sites-available
```

![5](https://i.imgur.com/wt6igiy.png)

Common files:

```text
000-default.conf
default-ssl.conf
```

---

### 6. Move Website Files

Move company website files:

```bash
sudo mv /opt/devel/ourcompany /var/www/
```

Verify:

```bash
ls -l /var/www
```

![6](https://i.imgur.com/eay7WEi.png)

---

### 7. Create a New Virtual Host

Edit:

```bash
sudo nano /etc/apache2/sites-available/ourcompany.conf
```

Change:

```apache
DocumentRoot /var/www/html
```

To:

```apache
DocumentRoot /var/www/ourcompany
```

![7](https://i.imgur.com/rOEni5C.png)

---

### 8. Enable the New Site

Enable:

```bash
sudo a2ensite ourcompany.conf
```

![8](https://i.imgur.com/YWFmTzG.png)

Disable default:

```bash
sudo a2dissite 000-default.conf
```

![9](https://i.imgur.com/Q8LYiAp.png)

Apache uses symbolic links to manage active websites.

---

### 9. Reload Apache Configuration

Apply changes:

```bash
sudo service apache2 reload
```

![9](https://i.imgur.com/Fkp8Yas.png)

The company website should now appear.

---

### 10. Enable Server Side Includes (SSI)

The website uses SSI to display a footer. SSI requires the Apache **include** module.

Enable module:

```bash
sudo a2enmod include
```

![9](https://i.imgur.com/LQNiENb.png)

Restart Apache:

```bash
sudo service apache2 restart
```

![10](https://i.imgur.com/0gLkVcV.png)

---

### 11. Configure SSI in Virtual Host

Edit configuration:

```bash
sudo nano /etc/apache2/sites-available/ourcompany.conf
```

Add:

```apache
<Directory /var/www/ourcompany>
    Options +Includes
    XBitHack on
</Directory>
```

![11](https://i.imgur.com/eRtOrOB.png)


This allows Apache to process Server Side Includes.

---

### 12. Reload Apache Again

Apply configuration:

```bash
sudo service apache2 reload
```

The footer now appears correctly.

---
---

### Cybersecurity Relevance

Web servers are common targets for attackers. Understanding Apache configuration helps with:

* Secure web server deployment
* Log analysis
* Configuration management
* Access control
* Service monitoring
* Vulnerability reduction

Apache logs can also assist SOC analysts during incident investigations.

---
---

### Linux Commands Used

| Command       | Purpose                           |
| ------------- | --------------------------------- |
| `sudo`        | Execute commands as administrator |
| `apt update`  | Update package lists              |
| `apt install` | Install software                  |
| `ls`          | List files                        |
| `cp`          | Copy files                        |
| `mv`          | Move files                        |
| `nano`        | Edit files                        |
| `cat`         | View files                        |
| `service`     | Manage services                   |
| `a2ensite`    | Enable site                       |
| `a2dissite`   | Disable site                      |
| `a2enmod`     | Enable module                     |
| `a2dismod`    | Disable module                    |

---
---

### Key Concepts

| Concept            | Description                     |
| ------------------ | ------------------------------- |
| Apache2            | Linux web server software       |
| Virtual Host       | Multiple websites on one server |
| DocumentRoot       | Website file location           |
| Site Configuration | Apache website settings         |
| Module             | Additional Apache functionality |
| SSI                | Server Side Includes            |
| Reload             | Apply configuration changes     |
| Restart            | Reload software and modules     |

---
---

### Important Commands

```bash
sudo apt update
sudo apt install apache2
sudo service apache2 start
sudo service apache2 status
sudo mv /opt/devel/ourcompany /var/www/
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/ourcompany.conf
sudo nano /etc/apache2/sites-available/ourcompany.conf
sudo a2ensite ourcompany.conf
sudo a2dissite 000-default.conf
sudo service apache2 reload
sudo a2enmod include
sudo service apache2 restart
```

---
---

### Skills Demonstrated

* Linux Administration
* Apache Web Server Management
* Website Deployment
* Virtual Hosts
* Apache Modules
* Service Management
* Configuration File Editing
* Troubleshooting
* Basic Web Hosting

---
---

### Final Takeaway

This lab provided hands-on experience deploying and configuring an Apache2 web server. I practiced installing Apache, creating virtual hosts, enabling and disabling websites, activating modules, configuring Server Side Includes, and managing Linux services. These are foundational skills for IT Support, System Administration, and Cybersecurity roles.
