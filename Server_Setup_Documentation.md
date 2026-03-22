### LAMP Stack Setup
This Markdown file serves as documentation for my LAMP Server setup.

## Introduction
* A LAMP stack server is a server that utilizes Linux, Apache, MySQL, and PHP to host database websites. This type of server is common because it utilizes free, open source software.

## Installation Steps
This section will include installation steps for Apache, MySQL, and PHP.

# Apache
* First, we need to check that our VM is running the latest upgrades for all packages.
* To do so, run ``` sudo apt update ``` then ``` sudo apt -y upgrade ```.
* Once everything has been upgraded, use the following command to install Apache: ``` apt search apache2 | head ```.
* Verify the file is the correct one for our purposes using ``` apt show apache2 ```.
* Now, we can install the package using ``` sudo apt install apache2 ```.

# MySQL
* To beginning, check the VM is running the latest upgrades for all packages.
* Next, install MySQL using ``` sudo apt install mysql-server ```. If we want to check the specific version we are installing, use ``` apt policy mysql-server ```. After installing, we can check this again using ``` mysql --version ```.
* The installation should have our server up and running. To check the server's status, use ``` systemctl status mysql ```. The installation will ask a series of questions for the initial set-up. For most questions, we will answer yes. For security, we will enter a lower setting for our testing purposes.

# PHP
* Use ``` apt show php libapache2-mod-php ``` to examine the package we are installing.
* to install use ``` sudo apt install php libapache2-mod-php ``` and ``` sudo systemctl restart apache 2 ``` to restart the Apache2 program.
* To check the version of PHP we have installed, use ``` php -v ```.
* We need to check the status of Apache2 after restarting using ``` systemctl status apache2 ```.

## Configuration
This section will include specific configuration steps for Apache, MySQL, and PHP.

# Apache
This covers the configurations need to change the initial webpage from the Apache default to my own webpage.
* First, navigate to the document root using ``` cd /var/www/html/ ```.
* Then, we rename the original index using ``` sudo mv index.html index.original.html ```.
* Lastly, we edit the file using tilde ``` sudo tilde index.html ```

# MySQL
These changes were necessary to link MySQL and PHP:
* First, we need to change some ownership and permissions:
* ``` cd /var/www ```
* ``` sudo touch login.php ```
* ``` sudo chmod 640 login.php ```
* ``` sudo chown :www-data login.php ```
* ``` ls -l login.php ```
* ``` sudo tilde login.php ```

* Edit login.php to include the following (filling in user/password where applicable):
* ``` <?php // login.php ```
* ``` $db_hostname = "localhost"; ```
* ``` $db_database = "opacdb"; ```
* ``` $db_username = "opacuser"; ```
* ``` $db_password = "XXXXXXXXX"; ```
* ``` ?> ```

* Next, create a new file to create a basic OPAC page by navigating to the root and creating a file named opac.php.
* Insert the basic text from the textbook.
* test the file's syntax to ensure they are working properly: ``` sudo php -f /var/www/login.php ``` and ``` sudo php -f /var/www/html/opac.php ```.
* Use a web-based browser to view the server, inserting the opac.php file name after the external IP.

# PHP
These configurations allowed the Apache server to serve .php files.
* Navigate to ``` cd /etc/apache2/mods-available/ ```
* Create a backup of the configuration file, using ``` cd cp dir.conf dir.conf.bak ```
* Now, edit the file using ``` sudo tilde dir.conf ```
* In the file, we want to edit it so that the ``` index.php ``` displays before the ``` index. html ```
* Now to check our changes, use ``` apachectl configtest ``` to display configtest commands
* We want to check the config file's syntax, so use ``` apachectl -t ```, which should display ``` Syntax Ok ``` if everything was done correctly.
* Lastly, we want to reload Apache and check it's status using ``` sudo systemctl reload apache2 ``` and ``` systemctl status apache2 ```

## Verification
This section will discuss verification methods for each component.

# Apache
* To verify that the webpage is displaying your changes, use either a graphical browser or a text-based browser.
* Use w3m to browse graphically. Install it using ``` sudo apt install w3m ```. Then, navigate to the website using ``` w3m localhost ```.
* To use a graphical browser, locate the server's external IP in Google Cloud Console, then click on it to launch the webpage.

# MySQL
* To ensure our configurations have properly paired PHP and MySQL, check the file's syntax using ``` sudo php -f /var/www/login.php ``` and ``` sudo php -f /var/www/html/opac.php ```.
* Then, use a web-based browser to view the server, inserting the opac.php file name after the external IP. This should display our desired page.

# PHP
* To check our changes made to connect PHP to the Apache server, use ``` apachectl configtest ``` to display configtest commands
* Mainly, we want to check the config file's syntax, so use ``` apachectl -t ```, which should display ``` Syntax Ok ``` if everything was done correctly.
* Lastly, we want to reload Apache and check it's status using ``` sudo systemctl reload apache2 ``` and ``` systemctl status apache2 ```.

## Challenges
* For Apache: I didn't have many challenges installing, configuring, or verifying my Apache server. The steps were straightforward and easy to follow. I did enjoy learning about loopback ip addresses and document roots, as I felt like these concepts helped me understand how information is organized and retrieved via the server.
* For MySQL: When I was trying to log in as my opacuser, I was confused by the password. I thought I had set something up wrong! After a quick google search, I learned that the password was working as intended, and doesn't display any visual indication that the password is being input as a security protocol.
* For PHP: I had troubles getting my index.php to display properly in using a graphical browser. One of the main problems I linked this to was that I had accidentally editted the dir.config.bak file instead of the dir.config file like I was supposed to. Other than that, I had to refresh the webpage about ten times before any changes actually showed.
