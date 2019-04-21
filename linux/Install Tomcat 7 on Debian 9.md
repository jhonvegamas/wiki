# Verify JAVA
java -version

## Download Tomcat 7 Archive
```Shell
cd /opt
wget https://www-eu.apache.org/dist/tomcat/tomcat-7/v7.0.94/bin/apache-tomcat-7.0.94.tar.gz
```

Verify url in https://tomcat.apache.org/download-70.cgi

Extract
```Shell
sudo tar xzf apache-tomcat-7.0.94.tar.gz
```

Rename directory
```Shell
sudo mv apache-tomcat-7.0.94 tomcat7
```

## Setup Environment Variable
```Shell
echo "export CATALINA_HOME="/opt/tomcat7"" >> ~/.bashrc
source ~/.bashrc
```

## Start Tomcat

```Shell
cd /opt/tomcat7
sudo ./bin/startup.sh
```

Verify 
http://ip-or-domain:8080 

## Setup User Accounts

conf/tomcat-users.xml
inside <tomcat-users> </tomcat-users> tags.

```XML
# user manager can access only manager section.
<role rolename="manager-gui" />
<user username="manager" password="_SECRET_PASSWORD_" roles="manager-gui" />

# user admin can access manager and admin section both.
<role rolename="admin-gui" />
<user username="admin" password="_SECRET_PASSWORD_" roles="manager-gui,admin-gui" />
```

# Create Tomcat7 Init Script
Create a init file /etc/init.d/tomcat7 using following content.

```Shell
#!/bin/bash

### BEGIN INIT INFO
# Provides:        tomcat7
# Required-Start:  $network
# Required-Stop:   $network
# Default-Start:   2 3 4 5
# Default-Stop:    0 1 6
# Short-Description: Start/Stop Tomcat server
### END INIT INFO

PATH=/sbin:/bin:/usr/sbin:/usr/bin

start() {
 sh /opt/tomcat7/bin/startup.sh
}

stop() {
 sh /opt/tomcat7/bin/shutdown.sh
}

case $1 in
  start) start;;
  stop)  stop;;
  restart) stop; start;;
  *) echo "Run as $0 "; exit 1;;
esac
```

Now execute following commands to set proper permissions and symbolic links for init script.

```Shell
chmod 755 /etc/init.d/tomcat7
update-rc.d tomcat7 defaults
```
## References

https://tecadmin.net/install-tomcat-7-on-ubuntu/
https://packages.debian.org/jessie/tomcat7
https://www.howtoinstall.co/es/debian/jessie/tomcat7
