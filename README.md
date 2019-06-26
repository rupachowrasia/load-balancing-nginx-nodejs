# Load Balancing with Nginx and Nodejs
## To see load-balancing in action we need 4 vagrant box and using nginx and node.js to show the same.

### Box1(192.168.31.101): Installed nginx and configure it for load balancing:
1. sudo apt-get update
2. sudo apt-get install nginx
3. systemctl status nginx
4. ls /etc/nginx/
5. vi /etc/nginx/nginx.conf (just to see all config)
6. sudo vi /etc/nginx/sites-available/default
```sh
upstream project {
       server 192.168.31.102:3000;
       server 192.168.31.103:3000;
       server 192.168.31.104:3000;
}
server {
        listen 80;

        location / {
                proxy_pass http://project;
        }
}
```
7. sudo systemctl reload nginx

### Box2(192.168.31.102), Box3(192.168.31.103), Box4(192.168.31.104): Install node.js in all box and build app using express generator:
1. sudo apt-get update
2. sudo apt-get install build-essential libssl-dev
3. curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh -o install_nvm.sh
4. vi install_nvm.sh
5. bash install_nvm.sh
6. source ~/.profile
```sh
NVM Commands:
nvm ls-remote
nvm install 10.16.0
nvm use 10.16.0
nvm list
nvm alias default 10.16.0
nvm use default
```

### Box1(192.168.31.101): Load test with apachebench(ab):
1. sudo apt-get install apache2-utils
2. sudo vi /etc/nginx/sites-available/default (comment out 2 server to check the load in 1 server only)
3. sudo systemctl reload nginx
4. ab -c 40 -n 1000 http://192.168.31.101/ (took 13 sec to finish)
5. sudo vi /etc/nginx/sites-available/default (revert the changes and uncomment all to check load in all the server)
6. sudo systemctl reload nginx
7. ab -c 40 -n 1000 http://192.168.31.101/ (took 8 sec to finish)

### Box1(192.168.31.101): Testing cache using ngnix:
1. sudo vi /etc/nginx/sites-available/default
```sh
upstream node_cluster {
    server 192.168.31.102:3000;      # Node.js instance 1
    server 192.168.31.103:3000;      # Node.js instance 2
    server 192.168.31.104:3000;      # Node.js instance 3
}
server {
    listen 80;
    server_name mynodedomain.dev www.mynodedomain.dev;

    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;

        proxy_pass http://node_cluster/;
        proxy_redirect off;
    }
    location ~* \.(css|js|gif|jpe?g|png)$ {
        expires 168h;
    }
}
```
2. sudo systemctl reload nginx
3. ab -c 40 -n 1000 http://192.168.31.101/stylesheets/style.css (took  0.215 sec to finish)

**Note:** All four boxes are running on ubuntu machine. I install nginx on 192.168.31.101 and all 3 node.js app is running on 192.168.31.102, 192.168.31.103 and 192.168.31.104  machine resp. Port is same for all 3 node app i.e 3000.
After configuration we can see it in action from box1(192.168.31.101).
