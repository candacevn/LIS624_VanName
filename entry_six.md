# Entry Six

## Installing PHP
- Use ``` apt show php libapache2-mod-php ``` to examine the package we are installing.
- to install use ``` sudo apt install php libapache2-mod-php ``` and ``` sudo systemctl restart apache 2 ``` to restart the Apache2 program.
- To check the version of PHP we have installed, use ``` php -v ```
- We need to check the status of Apache2 after restarting using ``` systemctl status apache2 ```.

## System info
- To check that php is working on the Apache2 server, we will create a .php file to display system info.
- First, navigate to the root using ``` cd /var/www/html/ ```.
- Here, create a file using ``` sudo tilde info.php ```.
- In the created file, insert ``` <?php phpinfo(); ?> ```.
- Now, use a text- or web-based browser to display the file.
- After seeing the file displayed in the browser, delete it using ``` sudo rm index.php ``` as it contains sensitive information.

## Configuring to default PHP 
- Navigate to ``` cd /etc/apache2/mods-available/ ```
- Create a backup of the configuration file, using ``` cd cp dir.conf dir.conf.bak ```
- Now, edit the file using ``` sudo tilde dir.conf ```
- In the file, we want to edit it so that the ``` index.php ``` displays before the ``` index. html ```
- Now to check our changes, use ``` apachectl configtest ``` to display configtest commands
- We want to check the config file's syntax, so use ``` apachectl -t ```, which should display ``` Syntax Ok ``` if everything was done correctly.
-Lastly, we want to reload Apache and check it's status using ``` sudo systemctl reload apache2 ``` and ``` systemctl status apache2 ```

## Browser Detector
- We will turn our default .php page into a browser detector.
- To do so, navigate to the root and create a file entitled ``` index.php ```
- Refer to the textbook for the browser detector's code.
- Save the file, then use a text- or web-based browser to see the page display.

# Reflections
- I had issues with the initial server info code for ``` index.php ```. I kept forgetting to use ``` sudo ``` so when I noticed I incorrectly used a colon instead of a semicolon, I was being denied access. Eventually I noticed my error, changed the colon, and the browser displayed the page properly.
- For some reason, only using ``` w3m ``` displays the browser detector correctly at default. I can access the ``` index.php ``` using the browser, but it doesn't show as the default like it does using ``` w3m ```. To troubleshoot this, I checked the file using tilde to ensure the code saved, which it had. Then, I ran ``` sudo apt update ``` and found a few packages needed upgrading, including one related to google console. After the installations, I tried to access the default page through the external ip again and nothing had changed. Next, I checked the dir.config file I editted to configure the server to PHP. Although I had recieved a ``` Syntax Ok ``` message, I figured there might have been an error still. Turns out, the dir.config file was blank, and I had accidently editted the dir.config.bak. So, instead of typing the config text, I copied it straight from the textbook to ensure no human error occured there this time. After I confirmed that had saved, I ran the ``` apachectl configtest ``` which showed the syntax was okay. However, it still wasn't working on the browser. I went ahead and restarted Apache2 and checked the status. Still no success. Then, I checked the index.php file to ensure the code there had saved, and it did. In the end, I did eventually get the browser to display the correct page by hitting the refrech button (admittedly, out of frustration) about 5 times. Not sure why this seemed to work, but the page displayed my browser and OS (though, the browser did not register correctly).

