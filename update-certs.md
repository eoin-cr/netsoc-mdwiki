# Updating certs
Updating certificates should be pretty easy.  The `restart-server.sh` script should renew all the certs using certbox.  To run this script do
```
$ sudo su
```
and enter your password to become the root user (the restart-server script can only be ran by a root user).  Then run the file with
```
# /root/docker-nginx-jekyll/restart-server.sh
```
The certs should now all be renewed for another 90 days.
