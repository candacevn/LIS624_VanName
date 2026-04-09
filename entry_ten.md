# Entry Ten
This is going to be a long one.

## Omeka Installation

1. Check for system updates ``` sudo apt update ```
2. Check PHP and MySQL versions ``` php --version ``` and ``` mysql --version ```
3. Install Image Magick ``` sudo apt install imagemagick ```
4. Enable Apache mod_rewrite ``` sudo a2enmod rewrite ```
5. Restart system after mod_rewrite ``` sudo systemctl restart apache2 ```

6. Run MySQL ``` sudo mysql -u root ```
7. Create Omeka user ``` create user 'omeka'@'localhost' identified by 'XXXXXXXXX'; ```
8. Create Omeka database ``` create database omeka; ```
9. Set Omeka user permissions ``` grant all privileges on omeka.* to 'omeka'@'localhost'; ```
10. Check databases for omeka and quit ``` show databases; ``` ``` \q ```

11. Download Omeka Classic ``` sudo wget https://github.com/omeka/Omeka/releases/download/v3.2/omeka-3.2.zip ```
12. Unzip the Omeka download ``` sudo unzip https://github.com/omeka/Omeka/releases/download/v3.2/omeka-3.2.zip ```
13. Rename the directory to omeka ``` mv /var/www/html/omeka-3.2 /var/www/html/omeka ```
14. Edit the db.ini file in the omeka directory, adding our user, host, database, and password information ``` sudo tilde /var/www/html/omeka/db.ini ```
15. Give Apache group access to write files ``` cd /var/www/html/omeka ``` ``` sudo chmod -R g+w * ```
16. Restart system after changing the group access ``` sudo systemctl restart apache2 ```
17. Finish installation via the web browser.

## Troubleshooting Omeka Installation
At step 17, I hit an error message from Omeka. It tells me to do the following to enable detailed error reporting:

1. ``` sudo tilde /var/www/html/omeka/.htaccess ```
2. Uncomment the following line ``` SetEnv APPLICATION_ENV development ```

After this, I boot up the website again to a different error "Installation Error mod_rewrite is not enabled."
My first instinct is to check if my mod_rewrite is actually not enabled:

3. ``` sudo a2enmod rewrite ```
The output lets me know "Module rewrite already enabled". So, where do I go from there?
Well, I start consulting the Omeka Classic forums and Stack Overflow. I tried the following advice:

4. Open .htaccess again
5. Uncomment ``` RewriteBase ``` and add our omeka root directory ``` /var/www/html/omeka ```
6. Edit the apache2.conf file ``` sudo tilde /etc/apache2/apache2.conf ```
7. Add the following 
``` <Directory /var/www/html/omeka>
	Options Indexes FollowsSymLInks
	AllowOverride All
	Require all granted
</Directory> ```
8. Check the error logs ``` sudo tilde /var/log/apache2/error.log ```
The error logs showed this: "/var/www/html/omeka/.htaccess: SetEnv not allowed here".
After seeing this, I was almost positive that the issue was with the server configuration, not the omeka installation.

Finally, after many painstaking hours of trial-and-error, the last two things I tried before the installation was successful:

9. I had accidentally commented out Rewrite Engine in .htaccess, so I uncommented that
10. In apache2.conf, I changed the 'AllowOverride None' to 'AllowOverride All' under '<Directory /var/www/>'

After all of that work, I was finally able to complete the omeka installation.

## Troubleshooting Wordpress
Funny thing happens after my Omeka installation issues... My VM is running pretty slow, so I think it might be best to stop and start it via gcloud.
Well, once I get the VM up and running, I mysteriously cannot access my wordpress site anymore. The stop/start process changes the external IP of the VM, which I knew, but I didn't realize that Wordpress would reroute me to the old IP every time I try to login under wp-admin.
This was kind of a pickle, because I need to get my Omeka linked onto my Wordpress site! So, I decided I would uninstall and reinstall wordpress. The process was simple:

Uninstall
1. sudo rm -rf /var/www/html/wordpress

Reinstall following last week's steps

This was a pretty easy issue to resolve, mostly because I didn't have much in the way of a nicely designed wordpress site I was afraid to destroy.

## Troubleshooting VM instance Issues
But that isn't were the issues end! The next day, I try to log into the VM through gcloud via the SSH browser access and I get hit with an error: "Connection via Cloud Identity-Aware Proxy Failed".
Oh boy. The first thing I do is hit the "Retry without Cloud Identity-Aware Proxy," which fails.
Next, I follow Google's directions to set up a firewall rule allowing TCP ingress traffic from the IP range and port specified in the error. No lukc there, either.

At this point, I'm afraid I might have to create an entirely new VM, which had me imagining re-doing an entire semester's worth of work in the few days before this assignment is due. Not fun.
But, instead of jumping the gun, I try one last thing: hit thr troubleshoot button. This showed that my VM status, Network status, and User permissions were all a-OK.
From there, it gave me a link to accessing the serial console. I was hesitant to mess with this because I'm not really familiar with working in google console besides firing up the VM, but I gave it a shot.

The serial console logs pointed to one thing: my server was running out of memory!
I knew this was on the horizon, but didn't realize it would grind everything to a halt like this!

Once I could identify the problem, the solution was pretty simple. I followed the directions devised by the professor and Amanda Bailey to create a new instance from a snapshot of my VM.
Now, I'm running the new instance, with more storage, so the problem has been remedied.

## Reflection
I feel like I've done quite a bit of reflection on the issues I've encountered, but in all honesty I'm really proud of myself. I don't say that often, but I really tried to troubleshoot and problem-solve my way out of these issues, and it worked!
I suppose this troubleshooting and on-your-feet problem-solving is a large part of working with systems like this!
