# Kest-Netstjornun_Lokaverkefni

## Hostname og Domain

server1: 

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/15b77f8e-df3a-4493-a4e6-a7066b6651a2)

client1:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/e56e7da1-a6ef-47ac-936c-1fd0968fdd36)

client2:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/c5cb1328-22da-4aaa-9488-9bb73f3c995f)


## DHCP setup

server 1 er með static ip 192.168.100.254, seinasta nothæfa ip talan á þessu subneti
![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/b76a4a92-7280-47b6-ab06-7d8eebef5cac)
// img af client 1 og 2
// put /etc/dhcp/dhcpd.conf og /etc/default/isc-dhcp-server (after dns fonf)

## Database
```sql
create database HrDatabase;
use HrDatabase;

create table jobs(
jobID int,
jobTitle varchar(30),
minSalary int,
maxSalary int,

constraint jobID_PK primary key (jobID)
);

create table location(
locationID int,
city varchar(25),
address varchar(35),
zipcode varchar(3),

constraint locationID_PK primary key (locationID)
);

create table department(
departmentID int,
departmentName varchar(55),
managerKennitala varchar(10),
locationID int,

constraint departmentID_PK primary key (departmentID),
constraint locationID_FK foreign key (locationID) references location(locationID)
);

create table employees(
kennitala varchar(10),
firtsname varchar(55),
lastname varchar(55),
email varchar(100), 
phone varchar(15),
dateOfHire date,
salary int,
departmentID int,
jobID int,

constraint kennitala_PK primary key (kennitala),
constraint department_FK foreign key (departmentID) references department(departmentID),
constraint jobID_FK foreign key (jobID) references jobs(jobID)
);
```

Töflurnar í databaseinum: 
![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/895bd88d-d370-42b6-b843-ef1c139e98a5)



Foreign key tengingar milli tafla: 
![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/14fa1966-f848-489e-bc1b-829c6cf0bdda)

## Vikulegar Backup
crontab config:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/197709f7-036f-46fe-a7e3-6418260bc6be)

backup script:
``` bash
#!/bin/bash

backup_dir="/backups"
mkdir -p "$backup_dir"

current_date=$(date +%F)

backup_subdir="$backup_dir/$current_date"
mkdir -p "$backup_subdir"

for user_dir in /home/*; do
    if [ -d "$user_dir" ]; then
        username=$(basename "$user_dir")
        tar -czvf "$backup_subdir/$username.tar.gz" -C "$user_dir" .
    fi
done
```
## NTP server

server1 syncar við ýmsa servera

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/27bb9fdb-0956-4d4d-82f1-5c3aeff54c24)

clientar synca bara við server1

client1:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/032dc31f-e13a-4a19-a498-1d14f88b3fd8)

client2:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/da79dc02-72ed-4f4c-89db-f9cc22608960)


