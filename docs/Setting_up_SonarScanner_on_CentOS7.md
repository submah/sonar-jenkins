<img src="../images/c4logo.png">

## =========================================================

## Install and configure Sonar on Centos 7

## =========================================================

## Sonarqube requirements
1. Server with minimum 2GB/1 vcpu capacity
2. PostgreSQL version 9.3 or greater.
3. OpenJDK 11 or JRE 11
4. All sonarquber process should run as a non-root ## sonarqube ## user.

## Update: MySQL for Sonarqube is depricated


**Prep the Server With Required Softwares**
```bash
yum install wget unzip -y

yum install java-11-openjdk-devel -y

sysctl -w vm.max_map_count=524288

sysctl -w fs.file-max=131072

ulimit -n 131072

ulimit -u 8192

```

**Setup PostgreSQL 10 Database For SonarQube**
```bash
#Install PostgreSQL 10 repo
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm -y

#Install PostgreSQL 10 repo
yum install postgresql10-server postgresql10-contrib -y

#Initialize the database
/usr/pgsql-10/bin/postgresql-10-setup initdb

#Open /var/lib/pgsql/10/data/pg_hba.conf file to change the authentication to md5.

vi /var/lib/pgsql/10/data/pg_hba.conf

Find the following lines at the bottom of the file and change peer to trust and idnet to md5
```
<img src="../images/peer-to-trust.JPG">

**Start and enable PostgreSQL**
```bash
systemctl start postgresql-10
systemctl enable postgresql-10
```
>**Note** You can verify the installation using the following version select query.
```bash
sudo -u postgres /usr/pgsql-10/bin/psql -c "SELECT version();"
```

## Setup Sonar User and Database
```bash
#Change the default password of the Postgres user. All Postgres commands have to be executed from this user.

sudo passwd postgres #set the password as postgres

#Login as postgres user with the new password.

su - postgres

#create user sonar

createuser sonarqube

#Login to the PostgreSQL CLI.
psql

#Create a sonarqubedb database

create database sonarqubedb;

#Create the sonarqube DB user with a strongly encrypted password. Replace your-strong-password with a strong password.

create user sonarqube with encrypted password 'your-strong-password'; 

#Next, grant all privileges to sonrqube user on sonarqubedb.

grant all privileges on database sonarqubedb to sonarqube

#Exit the psql prompt using the following command.

\q
exit
```

## Setup Sonarqube Web Server









