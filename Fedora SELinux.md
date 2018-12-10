SELinux Commands

Checking the Selinux context on our new erroneously configured folder, we see this:

# ls -Z file1
drwxr-xr-x. root root unconfined_u:object_r:default_t:s0 /u01/www


https://docs.fedoraproject.org/en-US/Fedora/13/html/Security-Enhanced_Linux/sect-Security-Enhanced_Linux-Troubleshooting-Top_Three_Causes_of_Problems.html

matchpathcon -V /var/www/html/*


restorecon -R -v /srv/myweb

restorecon -v /var/www/html/index.html 

https://docs.fedoraproject.org/en-US/Fedora/13/html/Security-Enhanced_Linux/sect-Security-Enhanced_Linux-Maintaining_SELinux_Labels_-Checking_the_Default_SELinux_Context.html