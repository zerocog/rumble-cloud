# Apache2 for Ubuntu

## apt update

```
#!/bin/bash
sudo apt update
sudo apt upgrade -y
sudo apt list --upgradable
```

Note:

if you get a message of packages kept back, try

`sudo apt-get install <list of packages kept back>`

## Install Apache2 

```
sudo apt-get install apache2
sudo apt-get install apache2-dev
wget https://github.com/GrahamDumpleton/mod_wsgi/archive/refs/tags/5.0.2.tar.gz
tar xvfz 5.0.2.tar.gz
cd mod_wsgi-5.0.2
```

## Configure mod_wsgi

```
conda activate ptcenv
./configure
```

## Enable WSGI

After installing mod_wsgi, you need to enable it in Apache.
You can do this by creating a symbolic link to the mod_wsgi configuration file:

On Ubuntu/Debian:

`sudo ln -s /etc/apache2/mods-available/wsgi.conf /etc/apache2/mods-enabled/`

## configure mod_wsgi

Create a new file in the Apache configuration directory
(e.g. /etc/apache2/conf.d/ or /etc/httpd/conf.d/) to configure mod_wsgi.
For example, create a file called wsgi.conf with the following contents:

```
WSGIDaemonProcess myapp processes=2 threads=15
WSGIProcessGroup myapp
WSGIScriptAlias / /path/to/myapp/wsgi.py
```

Replace myapp with the name of your Python web application,
and /path/to/myapp/wsgi.py with the path to your application's WSGI script.
