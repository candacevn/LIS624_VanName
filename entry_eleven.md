#Entry Eleven

## Koha Installation
1. Set up VM instance- my instance had already been upgraded to a larger storage size previously, so I just added the network tages and created the firewall rules for staff and public access to the opac.
2. Update and Upgrade the server's packages
3. Save disk space using ``` sudo apt autoremove -y && sudo apt clean ```
4. Sync with the Koha ILS using
``` sudo apt install apt-transport-https ca-certificates curl
sudo mkdir -p --mode=0755 /etc/apt/keyrings
sudo curl -fsSL https://debian.koha-community.org/koha/gpg.asc -o /etc/apt/keyrings/koha.asc
```
5. Use the root user ``` sudo su ``` then copy and paste the following:
```
tee /etc/apt/sources.list.d/koha.sources <<EOF
Types: deb
URIs: https://debian.koha-community.org/koha/
Suites: 25.05
Components: main
Signed-By: /etc/apt/keyrings/koha.asc
EOF
```
6. Use ``` cat /etc/apt/sources.list.d/koha.sources ``` to verify information matches the textbook.
7. Exit out of the root user ``` exit ```
8. Install MariaDB, a fork of MySQL Koha defaults to, ``` sudo apt install mariadb-server ```
9. Review and install koha-common ``` apt show koha-common ``` and ``` sudo apt install koha-common ```
10. Configure the two ports to allow access between the two user types, staff and public, by first making a copy of the file: ``` sudo cp /etc/koha/koha-sites.conf /etc/koha/koha-sites.conf.backup ```
* Then, edit the file to include ```INTRAPORT="8080" OPACPORT="8081" ```
11. Install the following module ``` sudo a2enmod rewrite cgi headers proxy_http ``` then restart the server.
12. Make a copy of the following file: ``` sudo cp /etc/apache2/ports.conf /etc/apache2/ports.conf.backup ```
* Then, edit the file to include the following lines at the top ``` Listen 8080 Listen 8081 ```
* (Note for self: Might have to change the virtual host directory in 000-default)
13. Create the Koha library using ``` sudo koha-create --create-db kohalibrary ```
14. Restart the server.
15. run the following commands to configure apache2: ``` sudo a2dissite 000-default ``` ```asuo a2enmod deflate ``` and ``` sudo a2ensite kohalibrary ```
16. Reload and restart the server.
17. Get the user name and password for koha using ``` sudo koha-passwd kohalibrary ```
18. Visit the website using the staff port to complete the installation process.

## Reflection
I feel like I ran into significantly less problems this time around, which felt good. I was a bit hesitant to mess with the ports, but the instructions helped me navigate the console settings correctly and I thankfully haven't had any issues with the ports (yet).
One thing I did notice is that I can't access my wordpress or omeka sites through the koha instance VM because of the port settings, which I hadn't expected. I suppose there is a way to configure these websites to function through different ports like we did with Koha, probably in the configuration files of the software.

