# Firewall
##### Add to Fireall
```
$ sudo firewall-cmd --add-port=80/tcp --permanent
$ sudo firewall-cmd --add-service=https --permanent
$ sudo firewall-cmd --reload
```
##### Show Rules
```
$ sudo firewall-cmd --list-all
$ sudo firewall-cmd --list-ports
$ sudo firewall-cmd --list-services
```
##### Delete Rules
```
$ sudo firewall-cmd --remove-port=80/tcp
$ sudo firewall-cmd --remove-service=http
$ sudo firewall-cmd --reload
```

##### Customized Service
```
$ cat <<EOF | sudo tee /usr/lib/firewalld/services/test.xml
<?xml version="1.0" encoding="utf-8"?>
<service>
  <short>test</short>
  <description>Test for firewalld</description>
  <port protocol="tcp" port="100"/>
</service>
EOF
$ sudo firewall-cmd --reload > /dev/null


$ sudo firewall-cmd --add-service=test --permanent > /dev/null
$ sudo firewall-cmd --reload > /dev/null

```
