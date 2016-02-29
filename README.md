# Project 5: Linux Webserver

1. connect to the serverusing grader account:
    ```sh
     ssh -i ~/.ssh/grader grader@52.37.13.237 -p 2200
    ```
    - my ip address is 52.37.13.237
    - my port is 2200
    - password for grader is grader
1. you can access my catalog application using the url:
     http://ec2-52-37-13-237.us-west-2.compute.amazonaws.com/


### A summary of software installed and configuration changes made.
- Creating user named grader and generated the  key pair to access the server and grant the sudo access.
- run sudo apt-get update to update all
- Configure to utc using:
    - sudo dpkg-reconfigure tzdata
    - choose from the list none of that
    - choose UTC
- change the port to 2200
    - nano /etc/ssh/sshd_config
    - change port from 22 to 2200
    - save and close
    - service ssh restart
- Install and configure appache:
    - sudo apt-get install apache2
    - sudo apt-get install libapache2-mod-wsgi
    - sudo nano /etc/apache2/sites-enabled/000-default.conf
    - add the following line in <VirtualHost *:80> block
        - WSGIScriptAlias / /var/www/html/myapp.wsgi
    - sudo apache2ctl restart
- Install postgresql
    - sudo apt-get install postgresql
    - create user name catalog
        - sudo -su postgres
        - psql
        - createuser catalog; (by default it has limited permission we can check by typing \du)
- install git
    -  sudo apt-get install git-all
- installing unattended-upgrades
    - sudo apt-get install unattended-upgrades
    - enable it by sudo dpkg-reconfigure --priority=low unattended-upgrades
- installing fail2ban
    - sudo apt-get install fail2ban
    - modify configuration by copying conf file
        - sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
    - sudo nano /etc/fail2ban/jail.local
    - adding ip address to ignore ip
    - change destemail to my email
    - restart the service
    - sudo service fail2ban stop
    - sudo service fail2ban start
## A list of any third-party resources to complete this project.

- http://www.postgresql.org/
- https://www.digitalocean.com/community/tutorials/how-to-use-roles-and-manage-grant-permissions-in-postgresql-on-a-vps--2
- http://docs.sqlalchemy.org/en/latest/core/engines.html
- http://www.jakowicz.com/flask-apache-wsgi/
- https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
- http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xvii-deployment-on-linux-even-on-the-raspberry-pi
- https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04
