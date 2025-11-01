📦 Nextcloud Hosting Setup

This repository contains setup files and configuration details for hosting Nextcloud — a powerful open-source platform for file sharing and collaboration.

🧠 What is Nextcloud?

Nextcloud is a self-hosted productivity platform that lets you:

Store, access, and share files securely

Sync your data across devices

Collaborate with others using integrated apps like calendars, contacts, and chat

Official website: https://nextcloud.com/

⚙️ Installation Steps (based on YouTube tutorial)

You can follow the complete installation guide here:
🎥 YouTube Video Tutorial

If you want to set it up manually, here’s a quick outline:

Update and upgrade your system

sudo apt update && sudo apt upgrade -y


Install Apache, MariaDB, and PHP

sudo apt install apache2 mariadb-server libapache2-mod-php php php-mysql php-xml php-mbstring php-curl php-gd php-zip unzip -y


Create a Nextcloud database

sudo mysql -u root -p
CREATE DATABASE nextcloud;
CREATE USER 'nextclouduser'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextclouduser'@'localhost';
FLUSH PRIVILEGES;
EXIT;


Download and extract Nextcloud

wget https://download.nextcloud.com/server/releases/latest.zip
unzip latest.zip
sudo mv nextcloud /var/www/html/
sudo chown -R www-data:www-data /var/www/html/nextcloud


Enable Apache configuration

sudo nano /etc/apache2/sites-available/nextcloud.conf


Add:

<VirtualHost *:80>
    DocumentRoot /var/www/html/nextcloud
    ServerName your-domain.com

    <Directory /var/www/html/nextcloud/>
        Require all granted
        AllowOverride All
        Options FollowSymLinks MultiViews
    </Directory>
</VirtualHost>


Then:

sudo a2ensite nextcloud.conf
sudo a2enmod rewrite headers env dir mime
sudo systemctl restart apache2


Complete setup in browser

Open your browser → http://localhost/nextcloud

Enter admin credentials, database info, and finish installation.
------------------------------------------------------------------------------------------------------------------------------------------
IF ANYTHING IS NOT WORKING THEN I GAVE YOU A LINK THERE YOU CAN CAREFULLY LISTEN AND EXECUTE 
(MAKE CHANGES IN PHP FILE[IN THAT YOU HAVE TO ADD LOCALHOST SO THAT IT WILL WORK ANYWHERE YOU WANT TO USE])

📘 Reference

For full installation guidance, watch the original YouTube video:
▶️ https://youtu.be/Wh7Qo63EGJk?si=UcJa8uHUEm8zTTWL
