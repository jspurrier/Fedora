##### Install Samba
`sudo dnf install samba`
##### Enable Samba
`sudo systemctl enable smb nmb`
##### Start Samba
`sudo systemctl start smb nmb`
##### Permit firewall Samba
`sudo firewall-cmd --add-service=samba --permanent`
##### Reload Firewall
`sudo firewall-cmd --reload`
#####SELinux for home Directories
`sudo setsebool -P samba_enable_home_dirs on`
##### Must add a user
`sudo pdbedit -a username`
##### Restart after adding
`sudo systemctl restart smb nmb`
##### Set SE Linux samba perms
`sudo setsebool -P samba_export_all_ro 1`
##### Restart samba
`sudo systemctl restart smb nmb`
