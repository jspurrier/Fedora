Create Directory Structure

Create virtual directory
`mkdir -p /var/www/dev.2daygeek.com/public_html`
`mkdir -p /var/www/support.2daygeek.com/public_html`

change ownership (not always needed)
Change the Ownership 
 `chown -R username:username /var/www/support.2daygeek.com/public_html`
 `chown -R username:username /var/www/dev.2daygeek.com/public_html`
 
 Folder permissions
 `chmod -R 755 /var/www/`
 
Create Virtual Directories
`mkdir /etc/httpd/sites-available`
`mkdir /etc/httpd/sites-enabled`

Create Virtual Host File
`touch /etc/httpd/sites-available/dev.2daygeek.com.conf`
`touch /etc/httpd/sites-available/support.2daygeek.com.conf`

Include Virtual host file into httpd.conf file
`nano /etc/httpd/conf/httpd.conf`
`IncludeOptional sites-enabled/*.conf`

Virtual Host for support.2daygeek.com
``` 
<VirtualHost *:80>
    ServerName www.support.2daygeek.com
    ServerAlias support.2daygeek.com
    DocumentRoot /var/www/support.2daygeek.com/public_html
    ErrorLog /var/www/support.2daygeek.com/error.log
    CustomLog /var/www/support.2daygeek.com/requests.log combined
</VirtualHost>
```

Virtual Host for dev.2daygeek.com 
```
<VirtualHost *:80>
    ServerName www.dev.2daygeek.com
    ServerAlias dev.2daygeek.com
    DocumentRoot /var/www/dev.2daygeek.com/public_html
    ErrorLog /var/www/dev.2daygeek.com/error.log
    CustomLog /var/www/dev.2daygeek.com/requests.log combined
</VirtualHost>
```


 Enable Virtual Hosts
`ln -s /etc/httpd/sites-available/dev.2daygeek.com.conf /etc/httpd/sites-enabled/dev.2daygeek.com.conf`
`ln -s /etc/httpd/sites-available/support.2daygeek.com.conf /etc/httpd/sites-enabled/support.2daygeek.com.conf`

**##### Disable Default Virtual Hosts (Just delete the corresponding symbolic link file)**
`rm -Rf /etc/httpd/sites-enabled/dev.2daygeek.com.conf`


`apachectl configtest`
`systemctl reload httpd.service`
`systemctl restart httpd.service`