# Making changes to the site

## Using Git
In your terminal create a new directory and `cd` into it. Make sure you have your ssh key added to your GitHub account 
(tutorial [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). Then go to the GitHub repo [here](https://github.com/ucdnetsoc/homepage)
and click the green code button and copy the link in the Clone section. Then run the following commands:
```
$ git init
$ git remote add origin [link you copied]
$ git pull origin master
```
Then you can create a new branch by doing `$ git branch [name]` and then doing `$ git checkout [name]`.
Now you can make your changes (note that the pages are written in markdown, so if you're changing formatting make sure you know how that works).
Once your changes are made run the following commands:
```
$ git add [files changed]
$ git commit -m "[message briefly explaining what you changed]"
$ git push
```
(If you get an error saying to set upstream origin master, simply copy the command given, e.g. `git push --set-upstream origin addCommittee`)
Now you can go back to the GitHub page and [create a Pull Request(PR)](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).
You can then merge your PR. 

## Updating the website from Git
Now that you've made your changes to the Git repo, if you have access to the server, you can navigate to `/root/docker-nginx-jekyll/` and then run `$ ./restart-website.sh`, and the changes will automatically be pulled
and deployed. Don't worry if you don't have server access though, as a cronjob automatically runs the script every day at midnight.


## Making a redirect subdomain
Just like for changing the website, change the subdomain files by cloning the [nginx config repo](https://github.com/ucdnetsoc/docker-nginx-jekyll/tree/master/_conf) locally, and then pushing your changes to git.

To make a new subdomain create a new file by doing `nano subdomain.netsoc.com.conf`. The code for a subdomain which redirects to a different site is as follows:
```
server {
    listen 443;
    server_name subdomain.netsoc.com;

    rewrite ^(.*) https://whatever.com permanent;
}
```

### Restarting nginx
You must restart nginx to update your domain changes by doing
```
# docker container exec dockernginxjekyll_nginx_1 nginx -s reload
```
in order to apply any changes to the site.

## Manually changing the website
It is not recommended to manually edit this files, due to the risk of up configuration files and the like, and also the inability to merge to git (thereby saving your changes).
However, if you must manually edit the files for whatever reason, note that the site files (including subdomain config files) are located in `/root/docker-nginx-jekyll/`, *not* in `/etc/nginx/sites-available`.
Also note, there is a cronjob which runs every day at midnight which pulls the docker jekyll netsoc repo, so any changes you make to files which are in that repo without pushing will be reset at midnight (although creating new config files and the like should be fine).
