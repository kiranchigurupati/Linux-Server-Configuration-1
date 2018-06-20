# Linux-Server-Configuration

## About
  This is the Udacity project 6 about the Configuring the Linux the server.

## Server Details
Server IP Address 13.232.120.119

Hosted site Url [http://13.232.120.119.xip.io/](http://13.232.120.119.xip.io/)

## Grader Password

unix

## Grader Key

-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAzWjQFkash6auMRk5tw2yJNRSTANOWMWnbxXqAL/bMsWdqfAb
qbqg6mRzOeYPSLbbJ7LGia49qU/qlN3x6XIlbcMwMjKbhLY01MLab7h7Qv0nOTKZ
whEHjl2K2a8txPvZa6+U5kfDWMl97yz4G9F6QWv0Pz5goO8a26aMT3Jv4AeJKBcy
a2uY12Exwatv+9mGT0gcw0c2Aad5m0oqKq7tA7F6O6DgkcdoO70JQPrJLnXH/+pj
+eLgCdNyrfZf1TdgfPzc8GxeVd2T/mbHRwP3iMsH4r65NQ3zQU0PHgK1KyIN2hiG
Yh+rf2g87GfgWzJYl9QAa1wNz7xUz8MkFOblDwIDAQABAoIBAQCpNxA9Wall8q0L
a5F9OH4qEvNdBVg0j1eYjsAAMA0+rUduKIxRbZqEnY3DA8BRkbnG4WLnJzBK27gP
PSu9ubgVzTdWExTE5mltYLwcTyjUDcKTPxklo2vLH0p0e/jDjwoUyUdr0XCfIxZo
w239VLtXS7yhoRxvV6qTioeKJ2b8cR3yXWEDIVeayO40hciBb4zP6I5vz8nKkIAw
ttuvSQpDaBbHgZ8KTWNlFfIsdDSUw2bKM6OSLjBMqr+oLKmCsgGGYPDhBVbgvtww
TfvLFf3Hqa+w6YlX3+yD9om5KUAtHFPRB6nPLeVJcONxDZA1ZsSizRJp51TVCFek
fy4LNqjxAoGBAPb/vk4Y3KEkMaDi44RVviNT2rId7b2vqoYrxZiteFtJ3dX19dOI
vorx0J2Ka2BqGvMhzuJ3Lk6cXwiAGcnqNrPmN+pafAODR7yYg50aS5QF+DIP4HTU
Adm6aAkpeqhQHiSZsXVjUk3rb5OwKRhs/dbV74zdnGE4aZU26SLbE6SXAoGBANTl
FHBWgukiAG7yJ9XqpLIg53PG1GG0lL0llIbqF/HXyH0CC3dYP18r3T3HP8u7N7Y5
TXrVyTJsZHKplKykrkC2mloESDgVnry1/Ppm039oey7hLXirLr2jT7j+dfCmb9Ut
oL7KAmsUryMArNbo4pC0jiuWxMcLGcTVKrwJq3pJAoGAGolVZ8yR/5oE3vUhXnlb
yS3cJCDFBwkVd/7B5upUMPKZq8AWHhjl58WdFR/m81/S72YldP0682UnbKFeo+vO
3rsQLNR12GbFUUTNdxZ5IjkV9kLwaXzRihPV044qSGT7KBF/GE6IbCisPyDA+YfU
Kb2oU+kHQQaviUFyALWqwZcCgYAchK9POReCOU7Ljd6uNidnwSagCLNsfy8pgz45
MGSSvfAaZsq4avbaPdr+KpGuLd8Rpu1tFfREr+ZowbSrx8eb3Zohks9FzAeeidZg
iKOuPoW5yuo3bt7tAlJsmpGb8f+rE9ijlhXq2DN5wd5lT38CGV2uEx06+I60IkX+
OGFjGQKBgQDrRS4P68PxGgMD0mNkXlZ7ZnNsafewtgt1sgs+hk4tFAR4kB77JKBv
248dTvAvRK6UAqywc2AgqGsVqfT0XPxKqICNbWJ+UEAwfMafMuCSPB2yMR5PNLLl
2fDqZrienVzarLPLLwmKQqOfwNQfYwgjBXI2Bt+wY31TJLPBzeaZPA==
-----END RSA PRIVATE KEY-----

## How to connect as grader:
  save private key provided in your local machine and run the following command
  ```
  ssh -i path/to/privatekey -p 2200 grader@13.232.120.119
    
  ```
## Configuring Linux Server

### Updating all packages
```
sudo apt-get update
sudo apt-get upgrade
```

### Creating grader User:
  ```
  sudo adduser grader
  ```
  This will add new user
  ```
  sudo nano /etc/sudoers
  ```
  Below the Root user append the following line
  ```
  grader  ALL=(ALL:ALL) ALL
  ```
  This will grant sudo permission to grader
  ### Creating a ssh key pair for grader
   On your local machine in terminal/command prompt
   ```
   ssh-keygen
   ```
   This will generate public and private ssh keys which is saved to .ssh folder
   
   Then in your virtual machine change to newly created user
   ```
   sudo su - grader
   ```
   Create a new directory .ssh and new file authorized_keys in that directory
   ```
   mkdir .ssh
   sudo nano .ssh/authorized_keys
   ```
   Copy the public key with .pub extension to authorized_keys and save the file
   ```
   chmod 700 .ssh
   chmod 644 .ssh/authorized_keys
   ```
   - 700 will give read write and execute permission to user.
   - 644 prevent other user from writting in to file.
   Then restart ssh server
   ```
   sudo service ssh restart
   ```
   
   Now from your log in to grader with private key generated 
   ```
   ssh -i .ssh/id_rsa grader@ipaddress 
   ```
  ### Changing the ssh port to 2200
   ```
   sudo nano /etc/ssh/sshd_config
   ```
   Change port 22 to port 2200
    
   Restart the ssh server
   
   ```
   service ssh restart
   ```
   
   >Note: Before Logging using ssh add custom TCP port 2200 under lightsaail firewall in networking tab in lightsail instance console  
   
   Now Login using command like this
   ```
   ssh -i .ssh/id_rsa -p 2200 grader@ipaddress
   ```
   
  ### Disabling ssh login as root
  `sudo nano /etc/ssh/sshd_config`
  
  make change `PermitRootLogin no`
  
  ### Configurating  Ufw firewall
  ```
  sudo ufw allow 2200/tcp
  sudo ufw allow 80/tcp
  sudo ufw allow 123/udp
  sudo ufw enable
  ```
  This will allow all required ports and enables the ufw
  
  After that 
  ```
  sudo ufw status
  ```
  It will display all allowed ports
  
  ### Changing time Zone
  `sudo dpkg-reconfigure tzdata`
  
  select none from list and then select utc.
  
  ### Installing Apache2 
  In terminal 
  
  ```sudo apt-get install apache2```
  
  Now mod_wsgi
  
  ```sudo apt-get install python-setuptools libapache2-mod-wsgi```
  
  Enable mod_wsgi
  
  ```sudo a2enmod wsgi ```
  #### Setting up your flask application to work with apache2
   Creating a flask app
   
   In /var/www directory create a new folder
   `sudo mkdir FlaskApp`
   
   Install git 
   
   `sudo apt-get install git`
   
   move to the FlaskApp `cd FlaskApp`
   
   In that direcory clone your github repository
   
   `sudo git clone https://github.com/username/catalog.git`
   
   Rename your repository to FlaskApp
   
   Then rename your project file to `__init__.py`
   
   >Error : While accesssing the client_secrets.json file 
   ```
   PROJECT_ROOT = os.path.realpath(os.path.dirname(__file__))
   json_url = os.path.join(PROJECT_ROOT, 'client_secrets.json')
   CLIENT_ID = json.load(open(json_url))['web']['client_id']
   ```
   Use json_url instead client_secrets.json in script
   
   Reffered from [stack overflow](https://stackoverflow.com/questions/44742566/wsgi-cant-find-file-in-same-directory-in-app)
   
  #### Install and configuring postgresql for project
   Install Postgres `sudo apt-get install postgresql`
   
   login to postgres `sudo su - postgres`
   
   postgres shell `psql`
   
   create user `CREATE USER catalog WITH PASSWORD 'password';`
   
   permit user to createdb `ALTER USER catalog CREATEDB;`
   
   Create a db name  catalog with user catalog `CREATE DATABASE catalog WITH OWNER catalog;`
   
   connect to db `\c catalog`
   
   revoke all permission to public `REVOKE ALL ON SCHEMA public FROM public;`
   
   Give schema permission to user catalog `GRANT ALL ON SCHEMA public TO catalog;`
   
   exit from db  `\q`
   exit from postgres `exit`
   
   Change the database connection in both db_setup.py and __init__.py as `engine =       create_engine('postgresql://catalog:password@localhost/catalog')`
   
   Now you are ready with your applicatiom
  ### Configure and Enable a New Virtual Host
   `sudo nano /etc/apache2/sites-available/FlaskApp.conf`
   
   In this add the following code
   ```
   <VirtualHost *:80>
		ServerName mywebsite.com
		ServerAdmin admin@mywebsite.com
		WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
		<Directory /var/www/FlaskApp/FlaskApp/>
			Order allow,deny
			Allow from all
		</Directory>
		Alias /static /var/www/FlaskApp/FlaskApp/static
		<Directory /var/www/FlaskApp/FlaskApp/static/>
			Order allow,deny
			Allow from all
		</Directory>
		ErrorLog ${APACHE_LOG_DIR}/error.log
		LogLevel warn
		CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
   ```
   Enable the virtual host 
   `sudo a2ensite FlaskApp`
   
   Disabling the default apache2 page
   `sudo a2dissite 000-default.conf`
   
  ### Create the .wsgi File
    ```
    cd /var/www/FlaskApp
    sudo nano flaskapp.wsgi 
    ```
   Add the following code
   
   ```
   #!/usr/bin/python
    import sys
    import logging
    logging.basicConfig(stream=sys.stderr)
    sys.path.insert(0,"/var/www/FlaskApp/")

    from FlaskApp import app as application
    application.secret_key = 'Add your secret key'
   ```
   save and exit
   
   Deploying flask app with apache2 is referred from [Digital ocean](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
  
   ### Installing require modules
   You can either install all modules on your machine or create a virtual environment for the project and install the modules
   To Create virtual environment: sudo virtualenv venv
   To activate virtual environment: source venv/bin/activate
   ` pip install flask sqlalchemy psycopg2 requests oauth2client`

   To deactivate virtual environment: deactivate
   
   ### Setting up your Google Oauth2
   Login to your [developer console](https://console.developers.google.com) and select your project and edit OAuth details as following
   
   Javascript origin
   `http://ip.xip.io`
   
   redirect URI
   
   `http://ip.xip.io\callback`
   
   `http://ip.xip.io\gconnect`
   
   `http://ip.xip.io\login`
   
   [xip.io](xip.io) is a free DNS which will be the same as using IP address
   
   ### Final Step
   Restart your apache2 server
   
   `sudo service apache2 restart`
   
   ### References used
        https://www.digitalocean.com
        some git hubs to get an idea 
