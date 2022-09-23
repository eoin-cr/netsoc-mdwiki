# Making changes to the site
Note that the site files (including subdomain config files) are located in `/root/docker-nginx-jeckyll/`, *not* in `/etc/nginx/sites-available`.  This means you will have to use the command `sudo su` to switch to the root user to access/make changes to the site.

Also note, there is a cronjob which runs every day at midnight which pulls the docker jekyll netsoc repo, so any changes you make to files which are in that repo will be reset at midnight (although creating new config files and the like should be fine).

## Making a redirect subdomain
Subdomain files are stored in `/root/docker-nginx-jeckyll/_conf`.  To make a new subdomain create a new file by doing `nano subdomain.netsoc.com.conf`. The code for a subdomain which redirects to a different site is as follows:
```
server {
    listen 443;
    server_name subdomain.netsoc.com;

    rewrite ^(.*) https://whatever.com permanent;
}
```

## Restarting nginx
You must restart nginx by doing
```
docker container exec dockernginxjekyll_nginx_1 nginx -s reload
```
in order to apply any changes to the site.
