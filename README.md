# proxy_useing_apache2

```
sudo apt-get update -y
sudo apt-get install apache2 -y

```

2 - Enable Required Apache Modules:
```
sudo a2enmod proxy
sudo a2enmod proxy_http

```
3 - Configure Apache Virtual Host:
```
sudo nano /etc/apache2/sites-available/jenkins.conf

```
4 - Add the following configuration to the file. Replace your_server_domain_or_ip with your server's actual domain or IP address:

```
<VirtualHost *:80>
    ServerName your_server_domain_or_ip

    ProxyPass / http://localhost:8080/
    RequestHeader set X-Forwarded-proto "https"
    ProxyPassReverse / http://localhost:8080/

    ErrorLog ${APACHE_LOG_DIR}/jenkins-error.log
    CustomLog ${APACHE_LOG_DIR}/jenkins-access.log common
</VirtualHost>

```
 5 - Enable the New Virtual Host:
```
sudo a2ensite jenkins
sudo systemctl reload apache2

```
