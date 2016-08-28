---
published: true
title: installing MariaDB with yum CentOS 6
layout: post
---
### Adding the MariaDB YUM repository

MariaDB have YUM repositories for several YUM-based Linux distributions. To easily generate the appropriate MariaDB.repo entry for your distribution, use [MariaDB online repository generator](https://downloads.mariadb.org/mariadb/repositories/).

Once you have your ```MariaDB.repo``` entry, add it to a file under ```/etc/yum.repos.d/``` with following command: 

    vim etc/yum.repos.d/MariaDB.repo

Here example ```MariaDB.repo``` file for CentOS 6 is:

    # MariaDB 10.1 CentOS repository list - created 2016-08-28 10:35 UTC
    # http://downloads.mariadb.org/mariadb/repositories/
    [mariadb]
    name = MariaDB
    baseurl = http://yum.mariadb.org/10.1/centos6-amd64
    gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
    gpgcheck=1

### Installing MariaDB with YUM

With the repo file in place you can now install MariaDB like so:

    sudo yum install MariaDB-server MariaDB-client

### After Installation

After the installation completes, start MariaDB with:

   sudo /etc/init.d/mysql start
   chkconfig mysql on

### Secure MariaDB after installation to

– Set (Change) root password
– Remove anonymous users
– Disallow root login remotely
– Remove test database and access to it
– Reload privilege tables

    mysql_secure_installation

### Check the new root password and databases

    mysql  -u root -p

    Welcome to the MariaDB monitor.  Commands end with ; or \g.
    Your MariaDB connection id is 13
    Server version: 5.5.34-MariaDB MariaDB Server
    Copyright (c) 2000, 2013, Oracle, Monty Program Ab and others.
    
    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

    MariaDB [(none)]> show  databases;
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | mysql              |
    | performance_schema |
    +--------------------+
    3 rows in set (0.00 sec)
    
    MariaDB [(none)]>