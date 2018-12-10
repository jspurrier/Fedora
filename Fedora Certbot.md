Lets Encrypt Fedora Apache

`sudo dnf install certbot`

change to root
`sudo -i`

Run Command
`certbot certonly --webroot -w /var/www/html -d www.srv.world`


Should tell you where it installs too after answering the questions. Put into .conf files as needed.

to renew as root

`certbot renew`



