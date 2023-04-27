# Web server

In this project, I learned how web servers work and began using one. I was
provided a personal server by ALX. I learned how to use `scp`
and Fabric to transfer files to my server. Additionally, I completed a basic
configuration of the server using Nginx.

The server is accessible at [bdbnb.site](http://bdbnb.site).

## Tasks :page_with_curl:

* **0. Transfer a file to your server**
  * [0-transfer_file](./0-transfer_file): Bash script that transfers a file
  from Holberton's client to a server.
  * Accepts four arguments:
    * The path of the file to be transferred.
    * The IP of the server to transfer the file to.
    * The username that `scp` connects with.
    * The path of the SSH privtae key that `scp` uses.
  * `scp` transfers the file to the user home directory `~/`.

* **1. Install nginx web server**
  * [1-install_nginx_web_server](./1-install_nginx_web_server): Bash script
  that configures a new Ubuntu machine with Nginx.
  * Nginx listens on port 80.
  * When querying Nginx at its root `/` with a `curl` GET request,
  it returns a page containing the string `Holberton School`.

* **2. Setup a domain name**
  * [2-setup_a_domain_name](./2-setup_a_domain_name): A text file containing
  the domain name set up for the server through Gandi.

* **3. Redirection**
  * [3-redirection](./3-redirection): Bash script that configures a new Ubuntu
  machine with Nginx.
    * Setup is identical to [1-install_nginx_web_server](./1-install_nginx_web_server)
  plus:
    * The location `/redirect_me` returns a `301 Moved Permanently` redirection
    to another page.

* **4. Not found page 404**
  * [4-not_found_page_404](./4-not_found_page_404): Bash script that configures
  a new Ubuntu machine with Nginx.
  * Setup is identical to [1-install_nginx_web_server](./1-install_nginx_web_server)
  plus:
    * Features a custom 404 page containing the string `Ceci n'est pas une page`.

* **5. Design a beautiful 404 page**
  * A custom-designed 404 error page for my server, accessible at
  [bdbnb.site/404](http://bdbnb.site/404).

* **6. Deploy fast, deploy well**
  * [fabfile.py](./fabfile.py): A Python Fabric configuration file defining
  the following functions:
  * `pack`
    * Usage: `fabric pack`
    * Creates a tar gzipped archive of the current directory named
    `holbertonwebapp.tar.gz` in the local directory.
  * `deploy`
    * Usage: `fabric -H <remote server IP> deploy`
    * Uploads the archive `holbertonwebapp.tar.gz` to the `/tmp`
    directory of the remote server.
    * Creates the directory `/tmp/holbertonwebapp` in the remote server.
    * Untars `holbertonwebapp.tar.gz` in the `/tmp/holbertonwebapp` directory
    of the remote server.
  * `clean`
    * Deletes the archive `holbertonwebapp.tar.gz` in the local directory.
    
    


* **Step 1: Install Nginx**
* sudo apt-get update
  sudo apt-get install nginx
  
* **Step 2: Adjust the Firewall**
* sudo ufw app list
* sudo ufw allow 'Nginx HTTP'
* sudo ufw status

* **Step 3: Check your Web Server**
* systemctl status nginx

* **Step 4: Manage the Nginx Process**
    * sudo systemctl stop nginx    #to stop web server
    * sudo systemctl start nginx     #to start web server if it stops
    * sudo systemctl restart nginx   #to stop and start
    * sudo systemctl reload nginx # to simply reload
    
    
    
* **How To Set Up Nginx Server Blocks (Virtual Hosts) on Ubuntu**
    *sudo mkdir -p /var/www/example.com/html   #to create the directory
    *sudo chown -R $USER:$USER /var/www/example.com/html #to assign ownership to the account
    * sudo chmod -R 755 /var/www  #to enable write access
    * vi /var/www/example.com/html/index.html
    
  **Step 3 — Creating Server Block Files for Each Domain**
    *sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.com  #copy from default file to server block file but remove "default_server" from the file and also edit "root /var/www/example.com/html;" in the file
    
* **should look like this when you are done:*
    
   server {
        listen 80;
        listen [::]:80;

        root /var/www/example.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name example.com www.example.com;

        location / {
                try_files $uri $uri/ =404;
        }
}


    *grep -R default_server /etc/nginx/sites-enabled/  # to ensure that the  default_server option is only enabled in a single active file
    
    **Step 4 — Enabling your Server Blocks and Restart Nginx**
    *sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
    *sudo nano /etc/nginx/nginx.conf (edit to "server_names_hash_bucket_size 64;") #to avoid a possible hash bucket memory problem that can arise from adding additional server names.
    *sudo nginx -t #test to make sure no syntax error
    *sudo systemctl restart nginx  #enable changes
    

