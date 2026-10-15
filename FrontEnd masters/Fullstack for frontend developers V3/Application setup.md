- There are two main web servers, **Apache** and **Nginx**
	- nginx is always faster than node
	- it basically handles reroutes

Steps to take:
- install nginx
	- `sudo apt install nginx`
- start nginx
	- `sudo service nginx start`
- navigate to your server in the browser
- view default nginx config
	- `less /etc/nginx/sites-available/default`
- hookup **Node.js**
	- link to newest node.js source
	- `curl https://deb.nodesource.com/setup_19.x | sudo -E bash -`
- install node.js
	- `sudo apt-get install nodejs`
- install git
	- `sudo apt install git`
- change ownership of **/www**
	- `sudo chown -R $USER:$USER /var/www`
- make an application directory
	- `mkdir /var/www/app`
- initialize empty git repo in `/app`
	- `git init`

## Setup proxy pass
- install **nodejs**
- install **git**


## Setup basic node server
- create app file
	- `touch app.js`
- init project
	- `npm init`
- create a basic node server in **app.js**
- create a new nginx server and proxy requests
	- `sudo vi /etc/nginx/sites-enabled/fsfe`
	- ```nginx
	  server {
		  listen 80 default_server;
		  listen [::]:80 default_server
		  
		  root /var/www/html;
		  index index.html;
		  
		  server_name <your_domain>;
		  
		  location / {
			  proxy_pass https://127.0.0.1:3000/;
		  }
	  }
	  ```
- start your app