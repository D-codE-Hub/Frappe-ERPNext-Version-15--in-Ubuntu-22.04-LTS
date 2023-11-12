# Frappe-ERPNext Version-15 in Ubuntu 22.04 LTS
A complete Guide to Install Frappe/ERPNext version 15  in Ubuntu 22.04 LTS

#### Refer this for default python 3.11 setup

- [D-codeE Video Tutorial](https://youtu.be/TReR0I0O1Xo)

### Pre-requisites 

      Python 3.11+
      Node.js 18+
      
      Redis 5                                       (caching and real time updates)
      MariaDB 10.3.x / Postgres 9.5.x               (to run database driven apps)
      yarn 1.12+                                    (js dependency manager)
      pip 20+                                       (py dependency manager)
      wkhtmltopdf (version 0.12.5 with patched qt)  (for pdf generation)
      cron                                          (bench's scheduled jobs: automated certificate renewal, scheduled backups)
      NGINX                                         (proxying multitenant sites in production)


------
### Steps to Install python 3.11.xx
------

> ## `Note: If you are using ubuntu 23.xx or latest  the default python version is 3.11.xx. So you can skip the python 3.11 installation steps`
    
#### First, import the Python repository with the most up-to-date stable releases.

      sudo apt install software-properties-common
      sudo add-apt-repository ppa:deadsnakes/ppa -y
      sudo apt update
      
#### install Python 3.11 by executing the following command in your terminal:

      sudo apt install python3.11
      python3.11 --version

    
#### To install all the extras in one go, run the following command.

      sudo apt install python3.11-full



#### Refer this for default python 3.11 setup

- [www.linuxcapable.com](https://www.linuxcapable.com/how-to-install-python-3-11-on-ubuntu-linux/#google_vignette)
- [ubuntuhandbook.org](https://ubuntuhandbook.org/index.php/2022/10/python-3-11-released-how-install-ubuntu)

-----


### STEP 1 Install git
    sudo apt-get install git

### STEP 2 install python-dev

    sudo apt-get install python3-dev

### STEP 3 Install setuptools and pip (Python's Package Manager).

    sudo apt-get install python3-setuptools python3-pip

### STEP 4 Install virtualenv
    
    sudo apt install python3.11-venv
    

### STEP 5 Install MariaDB

    sudo apt-get install software-properties-common
    sudo apt install mariadb-server
    sudo mysql_secure_installation
    
    
      In order to log into MariaDB to secure it, we'll need the current
      password for the root user. If you've just installed MariaDB, and
      haven't set the root password yet, you should just press enter here.

      Enter current password for root (enter for none): # PRESS ENTER
      OK, successfully used password, moving on...
      
      
      Switch to unix_socket authentication [Y/n] Y
      Enabled successfully!
      Reloading privilege tables..
       ... Success!
 
      Change the root password? [Y/n] Y
      New password: 
      Re-enter new password: 
      Password updated successfully!
      Reloading privilege tables..
       ... Success!

      Remove anonymous users? [Y/n] Y
       ... Success!
 
       Disallow root login remotely? [Y/n] Y
       ... Success!

       Remove test database and access to it? [Y/n] Y
       - Dropping test database...
       ... Success!
       - Removing privileges on test database...
       ... Success!
 
       Reload privilege tables now? [Y/n] Y
       ... Success!

 
    
    
    
### STEP 6  MySQL database development files

    sudo apt-get install libmysqlclient-dev

### STEP 7 Edit the mariadb configuration ( unicode character encoding )

    sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf

add this to the 50-server.cnf file

    
    [server]
    user = mysql
    pid-file = /run/mysqld/mysqld.pid
    socket = /run/mysqld/mysqld.sock
    basedir = /usr
    datadir = /var/lib/mysql
    tmpdir = /tmp
    lc-messages-dir = /usr/share/mysql
    bind-address = 127.0.0.1
    query_cache_size = 16M
    log_error = /var/log/mysql/error.log
    
    [mysqld]
    innodb-file-format=barracuda
    innodb-file-per-table=1
    innodb-large-prefix=1
    character-set-client-handshake = FALSE
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci      
     
    [mysql]
    default-character-set = utf8mb4

Now press (Ctrl-X) to exit

    sudo service mysql restart

### STEP 8 install Redis
    
    sudo apt-get install redis-server

### STEP 9 install Node.js 18.X package

    sudo apt install curl 
    curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
    source ~/.profile
    nvm install 18

### STEP 10  install Yarn

    sudo apt-get install npm

    sudo npm install -g yarn

### STEP 11 install wkhtmltopdf

    sudo apt-get install xvfb libfontconfig wkhtmltopdf
    

### STEP 12 install frappe-bench

    sudo -H pip3 install frappe-bench
    
    bench --version
    
### STEP 13 initilise the frappe bench & install frappe latest version 

    bench init frappe-bench --frappe-branch version-15 --python python3.11
    
    cd frappe-bench/
    bench start
    
### STEP 14 create a site in frappe bench 
    
    bench new-site dcode.com
    
    bench --site dcode.com add-to-hosts

Open url http://dcode.com:8000 to login 


### STEP 15 install ERPNext latest version in bench & site

    
    bench get-app erpnext --branch version-15
    ###OR
    bench get-app https://github.com/frappe/erpnext --branch version-15

    bench --site dcode.com install-app erpnext
    
    bench start
    
    


    
