# Kest-Netstjornun_Lokaverkefni

## Hostname og Domain

server1: 

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/3ba43a64-8e8e-4d2a-92f7-da923095c19e)


client1:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/92f857e1-dc14-4202-86bf-b11d0fd88468)


client2:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/e0eb738f-f4dd-460f-81fa-3dd8fa2e7771)



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
![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/2ed34774-fe83-46c5-a797-d1556a2f0ae6)



Foreign key tengingar milli tafla: 
![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/26b609bf-7ad9-4a3e-becc-c6e5798329ea)

## Vikulegar Backup
crontab config:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/1bcbb05f-fc27-4b87-8f5d-676ca322ff99)

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

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/3795f572-9066-48a9-a620-58c8c8e6e960)

clientar synca bara við server1

client1:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/b4fb8e17-35d9-4e8f-94de-a67bd445f63e)

client2:

![image](https://github.com/bjartur2004/Kest-Netstjornun_Lokaverkefni/assets/46542460/47ff98c5-af62-4917-bd14-a0bf176551b0)


