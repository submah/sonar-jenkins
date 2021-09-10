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









