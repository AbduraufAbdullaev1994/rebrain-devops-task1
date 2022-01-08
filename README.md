# What is nginx and How to install it

Nginx (pronounced as “Engine-X”) is an open source web server that is often used as reverse proxy or HTTP cache. It is available for Linux for free.

In this tutorial we’ll install Nginx and set up a basic site.
## What you’ll learn
  + How to set up Nginx
  + Some basic Nginx configuration
## What you’ll need
  + A computer running Ubuntu Server 18.04 LTS
  + Some basic knowledge of command line use
## Installing Nginx
To install Nginx, use following command:

```
sudo apt update
sudo apt install nginx
```
After installing it, you already have everything you need.

You can point your browser to your server IP address. You should see this page:

![image](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/optimized/2X/7/7504d83a9fe8c09d861b2f7c49e144ac773f0c0d_2_690x288.png)

If you see this page, you have successfully installed Nginx on your web server.

## Creating our own website
Default page is placed in **/var/www/html/** location. You can place your static pages here, or use virtual host and place it other location.

Let’s create simple HTML page in **/var/www/tutorial/** (it can be anything you want). Create index.html file in this location.
```
cd /var/www
sudo mkdir tutorial
cd tutorial
sudo "${EDITOR:-vi}" index.html
```
Paste the following to the **index.html** file:
```html
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>Hello, Nginx!</title>
</head>
<body>
    <h1>Hello, Nginx!</h1>
    <p>We have just configured our Nginx web server on Ubuntu Server!</p>
</body>
</html>
```
Save this file. In next step we are going to set up virtual host to make Nginx use pages from this location.
## Setting up virtual host
To set up virtual host, we need to create file in **/etc/nginx/sites-enabled/** directory.

For this tutorial, we will make our site available on 81 port, not the standard 80 port. You can change it if you would like to.
```
cd /etc/nginx/sites-enabled
sudo "${EDITOR:-vi}" tutorial
```
```
server {
       listen 81;
       listen [::]:81;

       server_name example.ubuntu.com;

       root /var/www/tutorial;
       index index.html;

       location / {
               try_files $uri $uri/ =404;
       }
}
```




