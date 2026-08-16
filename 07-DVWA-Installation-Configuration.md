    \# 🎯 Page 7: Installing and Configuring DVWA (Damn Vulnerable Web Application)



\---



\# Objective



Install and configure Damn Vulnerable Web Application (DVWA) on Ubuntu Desktop. DVWA will be used as the target application for demonstrating various web attacks, including SQL Injection, Cross-Site Scripting (XSS), Broken Access Control, and Remote Code Execution.



\---



\# Prerequisites



\- Ubuntu Desktop 24.04 LTS

\- Apache2 installed

\- PHP installed

\- MariaDB installed

\- Internet connectivity

\- User with sudo privileges



\---



\# Software Required



| Software | Purpose |

| --- | --- |

| Git | Download DVWA |

| DVWA | Vulnerable Web Application |



\---



\# Step 1: Install Git



Update the package list.



```bash

sudo apt update

```



Install Git.



```bash

sudo apt install git -y

```



Verify installation.



```bash

git --version

```



Expected Output



```

git version 2.x.x

```



\---



\# Step 2: Download DVWA



Navigate to the web root.



```bash

cd /var/www/html

```



Remove the default Apache page.



```bash

sudo rm index.html

```



Clone the DVWA repository.



```bash

sudo git clone https://github.com/digininja/DVWA.git

```



Verify.



```bash

ls

```



Expected Output



```

DVWA

```



\---



\# Step 3: Set File Permissions



```bash

sudo chown -R www-data:www-data /var/www/html/DVWA

```



```bash

sudo chmod -R 755 /var/www/html/DVWA

```



\---



\# Step 4: Configure DVWA



Navigate to the configuration directory.



```bash

cd /var/www/html/DVWA/config

```



Copy the sample configuration.



```bash

sudo cp config.inc.php.dist config.inc.php

```



Verify.



```bash

ls

```



Expected Output



```

config.inc.php

```



\---



\# Step 5: Create the Database



Open MariaDB.



```bash

sudo mysql

```



Create the database.



```sql

CREATE DATABASE dvwa;

```



Create a dedicated user.



```sql

CREATE USER 'dvwa'@'localhost' IDENTIFIED BY '<DVWA_DB_PASSWORD>';

```



Grant permissions.



```sql

GRANT ALL PRIVILEGES ON dvwa.\* TO 'dvwa'@'localhost';

```



Reload privileges.



```sql

FLUSH PRIVILEGES;

```



Exit MariaDB.



```sql

EXIT;

```



\---



\# Step 6: Configure Database Credentials



Edit the DVWA configuration.



```bash

sudo nano /var/www/html/DVWA/config/config.inc.php

```



Locate the following lines and update them.



```php

$\_DVWA\['db\_server'] = '127.0.0.1';

$\_DVWA\['db\_database'] = 'dvwa';

$\_DVWA\['db\_user'] = 'dvwa';

$\_DVWA\['db\_password'] =  '<DVWA_DB_PASSWORD>';

```



Save the file.



Press



```

Ctrl + O

Enter

Ctrl + X

```



\---



\# Step 7: Create Writable Directories



```bash

sudo chmod -R 777 /var/www/html/DVWA/hackable/uploads

```



```bash

sudo chmod -R 777 /var/www/html/DVWA/config

```



\---



\# Step 8: Restart Apache



```bash

sudo systemctl restart apache2

```



Verify.



```bash

sudo systemctl status apache2

```



Expected Output



```

Active: active (running)

```



\---



\# Step 9: Open DVWA



Find the Ubuntu IP.



```bash

hostname -I

```



Example



```

192.168.70.144

```



Open a browser.



```

<http://localhost/DVWA>

```



or



```

http://<Ubuntu-IP>/DVWA

```



Example



```

<http://192.168.70.144/DVWA>

```



The DVWA login page should appear.



\*DVWA Login Page\*



!image.png



\---



\# Step 10: Initialize the Database



Click



```

Create / Reset Database

```



Wait for the initialization to complete.



You should be redirected to the login page.



\---



\# Step 11: Login to DVWA



Default credentials.



Username



```

admin

```



Password



```

password

```



Click



```

Login

```



\---



\# Step 12: Set Security Level



Navigate to



```

DVWA Security

```



Select



```

Low

```



Click



```

Submit

```



This setting makes vulnerabilities easier to demonstrate during the lab.



\---



\# Step 13: Verify Available Modules



Confirm the following modules are visible.



\- SQL Injection

\- XSS (Reflected)

\- XSS (Stored)

\- Command Injection

\- File Inclusion

\- File Upload

\- Brute Force

\- CSRF

\- Weak Session IDs

\- Authentication Bypass



\---



\# Expected Result



DVWA should:



\- Load successfully.

\- Connect to MariaDB.

\- Allow administrator login.

\- Operate with Security Level set to Low.

\- Be accessible from Kali Linux.



\---



\# Verification Checklist



\- \[ ]  Git Installed

\- \[ ]  DVWA Downloaded

\- \[ ]  Database Created

\- \[ ]  Configuration Updated

\- \[ ]  Apache Restarted

\- \[ ]  DVWA Login Page Accessible

\- \[ ]  Database Initialized

\- \[ ]  Login Successful

\- \[ ]  Security Level Set to Low



\---



\# Commands Summary



```bash

sudo apt update



sudo apt install git -y



cd /var/www/html



sudo rm index.html



sudo git clone <https://github.com/digininja/DVWA.git>



sudo chown -R www-data:www-data /var/www/html/DVWA



sudo chmod -R 755 /var/www/html/DVWA



cd /var/www/html/DVWA/config



sudo cp config.inc.php.dist config.inc.php



sudo mysql



sudo nano /var/www/html/DVWA/config/config.inc.php



sudo chmod -R 777 /var/www/html/DVWA/hackable/uploads



sudo chmod -R 777 /var/www/html/DVWA/config



sudo systemctl restart apache2



hostname -I

```



\---



\# Troubleshooting



\### Apache does not start



```bash

sudo systemctl restart apache2

sudo systemctl status apache2

```



\### Database connection error



Verify the database credentials in:



```

/var/www/html/DVWA/config/config.inc.php

```



\### Permission denied



```bash

sudo chown -R www-data:www-data /var/www/html/DVWA

sudo chmod -R 755 /var/www/html/DVWA

```



\### Blank page



Check the Apache error log.



```bash

sudo tail -f /var/log/apache2/error.log

```



\---



\# Learning Outcome



After completing this page, the learner will be able to:



\- Install DVWA from GitHub.

\- Configure a PHP web application.

\- Create and configure a MariaDB database.

\- Prepare a vulnerable web application for penetration testing.

\- Verify application accessibility from another virtual machine.



\---



\#

