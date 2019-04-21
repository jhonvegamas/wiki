# How To Install Apache Tomcat 8 on Debian 9.md

```Shell
sudo apt-get install tomcat8
sudo apt-get install tomcat8-admin tomcat8-examples tomcat8-docs
```

## Change port

### Edit configuration file 

### Stop service

```Shell
service tomcat8 stop
```
Edit file

```Shell
sudo nano /etc/tomcat8/server.xml
```

```XML
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```

```XML
<Connector port="[NEW PORT]" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```

### Restart service

```Shell
service tomcat8 start
```

or

```Shell
service tomcat8 restart
```
### Verify status
```Shell
service tomcat8 status
```

## Aditional Configuration
### Add users

```Shell
service tomcat8 stop
```

sudo nano /etc/tomcat8/tomcat-users.xml

```XML
<role rolename="manager-gui" />
<user username="manager" password="password-manager" roles="manager-gui" />
<role rolename="admin-gui" />
<user username="admin" password="admin123" roles="admin-gui" />
```

```Shell
service tomcat8 start
```
