# Kest-Netstjornun_Lokaverkefni

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
