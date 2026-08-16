\# 🌐 Page 06: Apache, PHP \& MySQL Installation



\---



\# Objective



Install and configure Apache Web Server, PHP, and MySQL (MariaDB) on Ubuntu Desktop. This environment will host the DVWA (Damn Vulnerable Web Application) used to generate attack logs for Splunk.



\---



\# Prerequisites



\- Ubuntu Desktop 24.04.4 LTS installed

\- Internet connection available

\- SSH server installed

\- User has sudo privileges



\---



\# Software Overview



| Software | Purpose |

| --- | --- |

| Apache2 | Web Server |

| PHP | Server-side scripting |

| MariaDB | Database Server |

| PHP Extensions | Required for DVWA |



\---



\# Step 1: Update Package Repository



Open Terminal and run:



```bash

sudo apt update

```



\---



\# Step 2: Install Apache



```bash

sudo apt install apache2 -y

```



\---



\# Step 3: Verify Apache Service



```bash

sudo systemctl status apache2

```



Expected Output



```

Active: active (running)

```



Press



```

q

```



to exit.



\---



\# Step 4: Enable Apache at Boot



```bash

sudo systemctl enable apache2

```



\---



\# Step 5: Verify Apache in Browser



Find Ubuntu IP address:



```bash

hostname -I

```



Example



```

192.168.70.144

```



Open a browser on Ubuntu and visit:



```

<http://localhost>

```



Or from another VM:



```

http://<Ubuntu-IP>

```



Example



```

<http://192.168.70.144>

```



Expected Page



```

Apache2 Ubuntu Default Page

```



\---



\# Step 6: Install MariaDB



```bash

sudo apt install mariadb-server -y

```



\---



\# Step 7: Verify MariaDB Service



```bash

sudo systemctl status mariadb

```



Expected Output



```

Active: active (running)

```



Press



```

q

```



\---



\# Step 8: Enable MariaDB at Boot



```bash

sudo systemctl enable mariadb

```



\---



\# Step 9: Secure MariaDB



Run



```bash

sudo mysql\_secure\_installation

```



Recommended Configuration



```

Set root password?            Y



Remove anonymous users?       Y



Disallow root login remotely? Y



Remove test database?         Y



Reload privilege tables?      Y

```



\---



\# Step 10: Install PHP



```bash

sudo apt install php libapache2-mod-php php-mysql -y

```



\---



\# Step 11: Install Required PHP Extensions



```bash

sudo apt install php-gd php-curl php-mbstring php-xml php-zip php-cli php-imagick php-ldap php-imap -y

```



\---



\# Step 12: Verify PHP Version



```bash

php -v

```



Expected Output



```

PHP 8.x.x

```



\---



\# Step 13: Create PHP Test File



```bash

echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php

```



\---



\# Step 14: Restart Apache



```bash

sudo systemctl restart apache2

```



\---



\# Step 15: Test PHP



Open



```

<http://localhost/info.php>

```



Or



```

http://<Ubuntu-IP>/info.php

```



Expected Result



```

PHP Information Page

```



\*PHP Information Page\*



!image.png



\---



\# Step 16: Verify Listening Ports



```bash

sudo ss -tulpn

```



Verify



| Service | Port |

| --- | --- |

| Apache | 80 |

| SSH | 22 |

| MariaDB | 3306 |



\---



\# Step 17: Verify Installed Packages



Apache Version



```bash

apache2 -v

```



MariaDB Version



```bash

mysql --version

```



PHP Version



```bash

php -v

```



\---



\# Step 18: Verify Database Login



```bash

sudo mysql

```



Expected Prompt



```sql

MariaDB \[(none)]>

```



Exit



```sql

exit;

```



\---



\# Expected Result



Ubuntu should now have:



\- Apache Web Server running

\- PHP installed and working

\- MariaDB running

\- PHP extensions installed

\- Web server accessible from the network



\---



\# Verification Checklist



\- \[ ]  Apache Installed

\- \[ ]  Apache Running

\- \[ ]  Apache Starts Automatically

\- \[ ]  MariaDB Installed

\- \[ ]  MariaDB Running

\- \[ ]  PHP Installed

\- \[ ]  PHP Working

\- \[ ]  PHP Test Page Accessible



\---



\# Commands Summary



```bash

sudo apt update



sudo apt install apache2 -y



sudo systemctl status apache2



sudo systemctl enable apache2



sudo apt install mariadb-server -y



sudo systemctl status mariadb



sudo systemctl enable mariadb



sudo mysql\_secure\_installation



sudo apt install php libapache2-mod-php php-mysql -y



sudo apt install php-gd php-curl php-mbstring php-xml php-zip php-cli php-imagick php-ldap php-imap -y



php -v



echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php



sudo systemctl restart apache2



sudo ss -tulpn



apache2 -v



mysql --version



php -v



sudo mysql

```



\---



\# Troubleshooting



\### Apache is not running



```bash

sudo systemctl restart apache2

sudo systemctl status apache2

```



\### MariaDB is not running



```bash

sudo systemctl restart mariadb

sudo systemctl status mariadb

```



\### PHP page downloads instead of opening



Restart Apache:



```bash

sudo systemctl restart apache2

```



\### Cannot access Apache from another VM



Check the Ubuntu IP:



```bash

hostname -I

```



Verify all VMs are using the \*\*NAT\*\* network.



\---

