# Entry Seven
This entry will discuss the installation process for MySQL and how I configured it to work with PHP for my Apache server.

## Set-Up
* To beginning, check the VM is running the latest upgrades for all packages.
* Next, install MySQL using ``` sudo apt install mysql-server ```. If we want to check the specific version we are installing, use ``` apt policy mysql-server ```. After installing, we can check this again using ``` mysql --version ```.
* The installation should have our server up and running. To check the server's status, use ``` systemctl status mysql ```. The installation will ask a series of questions for the initial set-up. For most questions, we will answer yes. For security, we will enter a lower setting for our testing purposes.

## Running MySQL for the first time
* log in using ``` sudo mysql - u root ```
* show databases using ``` show databases; ```
* to exit MySQL, use ``` \q ```

## Create a User Account
* ``` create user 'opacuser'@'localhost' identified by 'XXXXXXXXX'; ``` where 'opacuser' is the username and 'XXXXXXXXX' indicates the password (changed per user).
* Log in using ``` mysql -u opacuser -p ```. When inputting the password, there will be no visual indication that the password is going through, but it will register all keystrokes.

## Edit the User Prompt
* ``` tilde ~/.bashrc ```
* Add the following line to the bottom of .bashrc: ``` export MYSQL_PS1="[\d]> " ```
* Save and exit.

## Practice Database Creation
* The following will create the database, display the database, and allow a specified user to access the newly created database:

* ``` create database opacdb default character set utf8mb4 collate utf8mb4_0900_ai_ci; show databases; grant all privileges on opacdb.* to 'opacuser'@'localhost'; ```

* If we want to grant only a specific privelege, they are: Create, Drop, Delete, Insert, Select, Updae, and Grant Option.

### Create a Table in a Database
* Log in as a user. To view databases, use ``` show databases; ```. To view a specific database, ``` use database_name ```. In our case, we want to view the created database ```opacdb ```.
* This database is empty because we just created it. Let's create a table using the following command line prompts:
* ``` create table books ( id int unsigned not null auto_increment, author varchar(150) not null, title varchar(150) not null, copyright year not null, primary key (id) ); ```
* View the table using ``` show tables ``` then ``` describe books ```.

### Add Records to a Database Table
* Example for inserting data:
* ``` insert into books (author, title, copyright) values ('Jennifer Egan', 'The Candy House', '2022'), ('Imbolo Mbue', 'How Beautiful We Were', '2021'),  ('Lydia Millet', 'A Children\'s Bible', '2020'), ('Julia Phillips', 'Disappearing Earth', '2019'); ```
* Notice that the format is ``` insert into table_name (value1, value2, value3) values ```  then all data entries are in parenthesis and follow the same fomat as the values to tell the machine where to fit the correct values in at.
* We can view these records after creation using ``` select * from books; ```

### Commands for MySQL
* ``` select value from table_name; ``` will display data from records in a table matching the value input. Display multiple values seperated by a comma. Specify specific values using ``` where value like '%specific_value%' ```. Wildcard selects all
* ``` alter table table_name add value after value; ``` adds a new value to the table. Existing records will need to be updated.
* ``` update table_name set value=`specifidata` where id=number; ``` will update a piece of data to have a new value added to it.
* ``` delete fom table_name where value='specificdata'; ``` delete a value from a record in the table
* ``` insert into table_name (value1, value 2, value 3) value ``` followed by new records to add to the table.
* View examples from the textbook for Week 9 for more specific examples.

## Pair PHP and MySQL
* Install ``` sudo apt install php-mysql ```
* Restart Apache and MySQL using ``` sudo systemctl restart apache2 ``` and ``` sudo systemctl restart mysql ```

### Authenticate PHP/MySQL
* First, we need to change some ownership and permissions:
* ``` cd /var/www ```
  ``` sudo touch login.php ```
  ``` sudo chmod 640 login.php ```
  ``` sudo chown :www-data login.php ```
  ``` ls -l login.php ```
  ``` sudo tilde login.php ```
* Edit login.php to include the following (filling in user/password where applicable):
* ``` <?php // login.php ```
* ``` $db_hostname = "localhost"; ```
* ``` $db_database = "opacdb"; ```
* ``` $db_username = "opacuser"; ```
* ``` $db_password = "XXXXXXXXX"; ```
* ``` ?> ```
* Next, create a new file to create a basic OPAC page by navigating to the root and creating a file named opac.php.
* Insert the basic text from the textbook.
* test the file's syntac to ensure they are working properly: ``` sudo php -f /var/www/login.php ``` and ``` sudo php -f /var/www/html/opac.php ```.
* Use a web-based browser to view the server, inserting the opac.php file name after the external IP.

# Reflections
* When I was trying to log in as my opacuser, I was confused by the password. I thought I had set something up wrong! After a quick google search, I learned that the password was working as intended, and doesn't display any visual indication that the password is being input as a security protocol.
* I find learning MySQL to be really interesting. It's cool to see how different layers are connected, like database > table > record > value. This relates to what we learned at the beginning of the course concerning how information is organized in systems.

