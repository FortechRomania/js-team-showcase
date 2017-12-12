## Nginx

### Getting familiar with nginx
Nginx is a free, open-source, high-performance HTTP server and reverse proxy. We use their official [website](http://nginx.org/en/) to read about their latest updates. We use also [Digital Ocean](https://www.digitalocean.com) for learning purposes.
This [link](https://www.digitalocean.com/community/tutorials/understanding-nginx-server-and-location-block-selection-algorithms) might help you start your work in this direction. This [beginner's guide](http://nginx.org/en/docs/beginners_guide.html) might also come in handy;

We choose nginx servers because:
* Open-Source & Free.
* Addresses [C10k problem](http://www.kegel.com/c10k.html)
* Easy to install. Easy to  configure.
* Designed for big apps but also suitable for small ones.
* Scales in all directions: from the smallest VPS to large clusters of servers.
* Not threaded to handle requests.
* Small and predictable amounts of memory under load

#### How to install
Depending on the operating system: installation steps described [here](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/).
##### Installation example for Ubuntu 16.04
```
deb http://nginx.org/packages/ubuntu/ xenial nginx
deb-src http://nginx.org/packages/ubuntu/ xenial nginx
sudo apt-get update
sudo apt-get install nginx
```

#### Server Configuration Structure
* /etc/nginx: contains all configuration files.
* /etc/nginx/nginx.conf: the main/universal nginx configuration file.
* /etc/nginx/sites-available/: the directory where all "server blocks" can be stored. nginx will not use the configuration files found in this directory unless they are linked to the sites-enabled directory. Typically, all server block configuration is done in this directory, and then enabled by linking to the other directory.
* /etc/nginx/sites-enabled/: The directory where all enabled "server blocks" are stored. Typically, these are created by linking to configuration files found in the sites-available directory.


#### How to use - Main commands
* Start server
```
sudo /etc/init.d/nginx start
    or
sudo systemctl start nginx
```
* Check Status
```
systemctl status nginx
```
* Stop server
This stop option implies that a fast/forced shutdown is applied i.e. the process is killed instantly even if there is a current request in progress.
```
nginx -s stop  
    or
kill - s processId ( ps aux | grep nginx )
```
* Quit server
This stop option graceful shuts down the server. That means that it waits for the worker processes to finish serving current requests.
```
nginx -s quit
```
* Test/Check for correct syntax the configuration from the nginx config file.
```
nginx -t
```
* Restart service
```
sudo systemctl restart nginx
```
* Reload the configuration file
```
sudo systemctl reload nginx
    or
nginx -s reload
```
* (Re)open log files
```
nginx -s reopen
```

#### Main configuration blocks
* http - main configuration from the `nginx.conf` file; in this block the universal configuration is done.
* server - block that contains all the configuration for the virtual server;
* listen - describes addresses and ports that accept connection with the server. In this block can be defined one of the following:

** an ip/address/port combination,

** a lone IP what will listen the default port 80,

** a lone port that will listen every address on that port,

** a path to other unix socket.

* server_name - indicates all server names. With this block you can define several names for your server. Keep in mind that the  1st name listed is the primary name. The server can be a string that can contain `*`, `~`, or regex;
* ssl_certificate & ssl_certificate_key - blocks applicable for https; they indicate the paths to ssl certificates;
* error_log, access_log - blocks used to indicate the path where logs will be stored;
* location - block with config used for handling requests for different resources and URIs for the parent server;
* gzip - block used for on-the-fly gzip compression to limit the amount of bandwidth used and speed up some transfers. This block can be configured in such matter that only files bigger than a certain size are included in the gzip compression - only relevant compression is done and the transfer process is done rapidly.
* root - sets the root directory for requests;
* index - defines what will be used as index; it is nested inside location for internal redirect;
* proxy_pass - if specified inside a location, this directive passed a request to an HTTP proxied server;
* try_files - checks the existence of files in the specified order and uses the first found file for request processing; the processing is performed in the current context;
* alias: defines a replacement for the specified location.

#### Configuration example
The following configuration example is used for two UI applications - an user app and an admin dashboard. The applications were built with create-react-app package do the deploy process was done following the instructions from this [link](https://medium.com/@johnbrett/create-react-app-push-state-nginx-config-a9f7530621c1).
On HTTP, the server will listen to the default port `80`. When on HTTPS, the `443` port will be listened and the ssl certificates will be checked. The server's name can be is called `myserver`. For logging the errors, I setup the path from my local storage. Access logs could have been added but it is not in the purpose of this app. The `root` block points to the folder where the user app is stored. There are two `location` blocks used in this configuration file. The first one (`location /api/`) handles the requests to an HTTP proxied server - in this case the backend server. The second one(`location /admin`) handles the requests to the dashboard app.

```
server {
    listen         80;
    server_name    myserver.ro www.myserver.ro;
    return         301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    server_name    myserver.ro www.myserver.ro;
    ssl_certificate /etc/nginx/ssl/myserver_ro.crt;
    ssl_certificate_key /etc/nginx/ssl/myserver.key;

    error_log /var/log/myserver/error.log;

    root /home/work/ui/build_final;
    try_files $uri /index.html;

    location /api/ {
        proxy_pass http://127.0.0.1:3000;
    }

    location /admin {
        alias /home/work/dash/build_final;
        try_files $uri /admin/index.html;
    }
}
```
