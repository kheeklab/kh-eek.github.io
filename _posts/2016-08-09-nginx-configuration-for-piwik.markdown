---
published: true
title: NGINX Configuration for Piwik
layout: post
categories: [NGINX, PIWIK]
---
After long time googling for using Piwlk with NGINX at last I found the best one.

This configuration file was provided by Seph. You can see the complete information [here](https://github.com/perusio/piwik-nginx) .


```
server 
   ## This is to avoid the spurious if for sub-domain name rewriting.
   listen [::]:80
   server_name www.stats.example.com
   rewrite  $scheme://stats.example.com$request_uri? permanent

server 
    listen [::]:80
    limit_conn arbeit 
    server_name stats.example.com

    # Parameterization using hostname of access and log filenames.
    access_log  /var/log/nginx/stats.example.com_access.log
    error_log   /var/log/nginx/stats.example.com_error.log

    # Disable all methods besides HEAD, GET and POST.
     $request_method  ^(GET|HEAD|POST)$  
        return 
    

      /var/www/sites/stats.example.com/
    index  index.php index.html

    # Disallow any usage of piwik assets if referer is non valid.
    location  ^.+\.(?:jpg|png|css|gif|jpeg|js|swf)$ 
             # Defining the valid referers.
             valid_referers  blocked *.mysite.com othersite.com
              $invalid_referer  
                return 
             
             expires 
             break
    

    # Support for favicon. Return a 204 (No Content) if the favicon
    # doesn't exist.
    location  /favicon.ico 
             try_files /favicon.ico 
    

    # Try all locations and relay to index.php as a fallback.
    location  
             try_files  /index.php
    

    # Relay all index.php requests to fastcgi.
    location  ^/(?:index|piwik)\.php$ 
            fastcgi_pass unix:/tmp/php-cgi/php-cgi.socket
    

    # Any other attempt to access PHP files returns a 404.
    location  ^.+\.php$ 
              return 
    

    # Return a 404 for all text files.
    location  ^/(?:README|LICENSE[^.]*|LEGALNOTICE)(?:\.txt)*$ 
             return 
    

    # # The 404 is signaled through a static page.
    # error_page  404  /404.html;

    # ## All server error pages go to 50x.html at the document root.
    # error_page 500 502 503 504  /50x.html;
    # location = /50x.html {
    #       root   /var/www/nginx-default;
    
 # server
```