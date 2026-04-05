# Entry Nine

## Requirements
* First, review the Wordpress documentation to familiarize ourselves with the regular process.
* Next, check for updates (entry two has the steps).
* Now, we need to check the versions of our MySQL and PHP programs to see if they are compatible with Wordpress's requirements:
``` php --version ```, ``` mysql --version ```, (Ubuntu version) ``` cat /etc/issue.net ```
* Install new PHP modules:
``` sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl ```
* Restart Apache2 and MySQL:
``` sudo systemctl restart apache2 ```, ``` sudo systemctl restart mysql ```

## Installation
* Move to the document root, then download WordPress:
``` cd /var/www/html ```, ``` sudo wget https://wordpress.org/latest.zip ```
* Install the unzip command:
``` sudo apt install unzip ```
* Unzip the wordpress file:
``` sudo unzip latest.zip ```

## Wordpress database and user
* Log in as the root MySQL user:
``` sudo mysql -u root ```
* Create a new user (edit the password for security):
``` create user 'wordpress'@'localhost' identified by '#########'; ```
* Create a new database:
``` create database wordpress; ```
* Grant privileges to the user:
``` grant all privileges on wordpress.* to 'wordpress'@'localhost'; ```
* Show the database:
``` show databases; ```
* Exit:
``` \q ```

## Configuration
* Navigate to the wordpress directory:
``` cd /var/www/html/wordpress ```
* Rename the sample config file:
``` sudo cp wp-config-sample.php wp-config.php ```
* Edit the config file using tilde to include the username, password, and database we just created in MySQL

### Optional Setting
* I chose to rename my wordpress directory to my-library:
``` sudo mv /var/www/html/wordpress /var/www/html/my-library ```

## Finish installation
* Navigate to the external IP, then set up the wordpress username and password.
* Now, it's time to play around with themes with the goal of making the website more visually appealing.

## Reflection
* At first, I did not realize I didn't have the unzip command installed. But, this was pretty easy to remedy as we have learned how to install programs before.
* I thought it was interesting that we downloaded the zip file from the Wordpress.org website directly, as this seems different from our previous methods of downloading programs.
* It was really interesting to see examples of library websites that utilize Wordpress for their client-side interface. This makes our experience more valuable, because our workflow is simply a modification of a workflow real systems librarians have done to set up their library's front-end.
