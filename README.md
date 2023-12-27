WordPress VPS Deployment with Nginx Caching
This repository contains the setup instructions and necessary files for deploying a WordPress website on a Virtual Private Server (VPS) using AWS EC2. The deployment process involves configuring Nginx as the web server, MySQL/MariaDB as the database, PHP for processing dynamic content, and enhancing website performance with Nginx caching. Additionally, the website is secured with Let's Encrypt SSL/TLS certificates.

Table of Contents:-
Server Provisioning
Website Configuration
SSL/TLS Certificate
Nginx Server Optimization
GitHub Repository Setup
Server Provisioning
Provision a Virtual Private Server (VPS):

Create an EC2 instance on AWS with Ubuntu 22.04 LTS.
Later, modify SSH traffic to allow only your IP.
Configure Secure Linux Distribution:

Ensure that you have a secure Linux distribution, such as Ubuntu 22.04.
Apply necessary firewall rules for security.
Website Configuration
Install and Configure Nginx, MySQL, and PHP:

Update packages: sudo apt-get update
Install Nginx: sudo apt-get install -y nginx
Install MySQL server: sudo apt-get install -y mysql-server
Install PHP and required modules: sudo apt-get install -y php-fpm php-mysql php-curl php-mbstring php-imagick php-xml php-zip
Configure Nginx:

Adjust the try_files list in Nginx configuration.
Enable caching:
nginx
Copy code
proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=my_cache:10m max_size=1g inactive=60m use_temp_path=off;
proxy_cache my_cache;
proxy_cache_valid 200 30m;
proxy_cache_valid 404 1m;
add_header X-Proxy-Cache $upstream_cache_status;
Set Up WordPress:

Install WordPress on the server.
Configure WordPress with the provided admin credentials.
Install security plugins and update WordPress, plugins, and themes regularly.
Use wp-rocket cache plugin for better performance.
Generate WordPress Secret Keys:

Use the command: curl -s https://api.wordpress.org/secret-key/1.1/salt/
SSL/TLS Certificate
Implement Let's Encrypt SSL/TLS Certificate:
Register a domain and create an Elastic IP on AWS.
Associate the Elastic IP with the EC2 instance.
Update DNS records with the domain registrar.
Install Certbot: sudo apt install certbot python3-certbot-nginx
Obtain and install SSL certificate: sudo certbot --nginx -d linuxisfun.ddns.net
Nginx Server Optimization
Optimize Nginx Configuration:
Enable gzip compression in Nginx for enhanced performance.
GitHub Repository Setup
Create GitHub Repository:

GitHub Repository
GitHub Actions Workflow:

Set up a GitHub Actions workflow for automated deployment.
Ensure the workflow includes necessary steps to install dependencies, build the project, and transfer files securely to the server.
