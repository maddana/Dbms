Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 4
Server version: 5.0.45-community-nt MySQL Community Edition (GPL)

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql> use name;
Database changed
mysql> insert into state (sname,sid) values('AP',101);
Query OK, 1 row affected (0.03 sec)

mysql> insert into state (sname,sid) values('TN',102);
Query OK, 1 row affected (0.01 sec)

mysql> insert into state (sname,sid) values('Karnataka',103);
Query OK, 1 row affected (0.02 sec)

mysql> insert into state (sname,sid) values('Kerala',104);
Query OK, 1 row affected (0.02 sec)

mysql> insert into state (sname,sid) values('JK',105);
Query OK, 1 row affected (0.01 sec)

mysql> show state;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'state' at line 1
mysql> select from state;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'from state' at line 1
mysql> select *from state;
+-----+-----------+
| sid | sname     |
+-----+-----------+
| 101 | AP        |
| 102 | TN        |
| 103 | Karnataka |
| 104 | Kerala    |
| 105 | JK        |
+-----+-----------+
5 rows in set (0.00 sec)

mysql> create table state1 as select sid from state;
Query OK, 5 rows affected (0.06 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> select *from state1;
+-----+
| sid |
+-----+
| 101 |
| 102 |
| 103 |
| 104 |
| 105 |
+-----+
5 rows in set (0.00 sec)

mysql> create table district(
    -> did int primary key,
    -> dname varchar(20),
    -> sid int references state(sid));
Query OK, 0 rows affected (0.05 sec)

mysql> desc state1;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| sid   | int(11) | NO   |     |         |       |
+-------+---------+------+-----+---------+-------+
1 row in set (0.02 sec)

mysql> show tables;
+----------------+
| Tables_in_name |
+----------------+
| district       |
| state          |
| state1         |
+----------------+
3 rows in set (0.00 sec)

mysql> drop table state1;
Query OK, 0 rows affected (0.05 sec)

mysql> select *from district;
Empty set (0.00 sec)

mysql> select *from state;
+-----+-----------+
| sid | sname     |
+-----+-----------+
| 101 | AP        |
| 102 | TN        |
| 103 | Karnataka |
| 104 | Kerala    |
| 105 | JK        |
+-----+-----------+
5 rows in set (0.00 sec)

mysql> insert into district values(1001,'bangalore',103);
Query OK, 1 row affected (0.03 sec)

mysql> insert into district values(1002,'chittoor',101);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(1001,'Mysore',103);
ERROR 1062 (23000): Duplicate entry '1001' for key 1
mysql> insert into district values(1001,'vellore',102);
ERROR 1062 (23000): Duplicate entry '1001' for key 1
mysql> insert into district values(1001,'chennai',102);
ERROR 1062 (23000): Duplicate entry '1001' for key 1
mysql> insert into district values(1001,'vizag',101);
ERROR 1062 (23000): Duplicate entry '1001' for key 1
mysql> insert into district values(1003,'Mysore',103);
Query OK, 1 row affected (0.05 sec)

mysql> insert into district values(1004,'vellore',102);
Query OK, 1 row affected (0.00 sec)

mysql> insert into district values(1005,'chennai',102);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(1006,'vizag',101);
Query OK, 1 row affected (0.03 sec)

mysql> select *from district;
+------+-----------+------+
| did  | dname     | sid  |
+------+-----------+------+
| 1001 | bangalore |  103 |
| 1002 | chittoor  |  101 |
| 1003 | Mysore    |  103 |
| 1004 | vellore   |  102 |
| 1005 | chennai   |  102 |
| 1006 | vizag     |  101 |
+------+-----------+------+
6 rows in set (0.00 sec)

mysql> create table city(
    -> cid int primary key,
    -> cname varchar(20),
    -> did int reference district(did));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'reference district(did))' at line 4
mysql> create table city(
    -> cid int primary key,
    -> cname varchar(20),
    -> did int references district(did));
Query OK, 0 rows affected (0.05 sec)

mysql> insert into district values(5001,'bangalore',1001);
Query OK, 1 row affected (0.03 sec)

mysql> insert into district values(5002,'hebal',1001);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(5003,'k r puram',1001);
Query OK, 1 row affected (0.01 sec)

mysql> insert into district values(5004,'nagawara',1001);
Query OK, 1 row affected (0.01 sec)

mysql> insert into district values(5005,'henoor',1001);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(5006,'chittoor',1002);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(5007,'madanapalle',1002);
Query OK, 1 row affected (0.00 sec)

mysql> insert into district values(5008,'tirupati',1002);
Query OK, 1 row affected (0.00 sec)

mysql> insert into district values(5009,'punganur',1002);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(5010,'palamner',1002);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(5011,'mysore',1003);
Query OK, 1 row affected (0.01 sec)

mysql> insert into district values(5012,'vellore',1004);
Query OK, 1 row affected (0.00 sec)

mysql> insert into district values(5013,'chennai',1005);
Query OK, 1 row affected (0.00 sec)

mysql> insert into district values(5014,'vizag',1006);
Query OK, 1 row affected (0.05 sec)

mysql> insert into district values(5013,'katpadi',1004);
ERROR 1062 (23000): Duplicate entry '5013' for key 1
mysql> create table student(
    -> id int primary key,
    -> f_name varchar(20),
    -> l_name varchar(20),
    -> dob date,
    -> dno varchar(10),
    -> street varchar(35),
    -> street2 varchar(30),
    -> gender varchar(2) check(gender in ('M','F'));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '' at line 9
mysql> create table student(
    -> id int primary key,
    -> f_name varchar(20),
    -> l_name varchar(20),
    -> dob date,
    -> dno varchar(10),
    -> street varchar(35),
    -> street2 varchar(30),
    -> gender varchar(2) check(gender in('M','F'));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '' at line 9
mysql> create table student(
    -> id int primary key,
    -> f_name varchar(20),
    -> l_name varchar(20),
    -> dob date,
    -> dno varchar(10),
    -> street varchar(35),
    -> street2 varchar(30),
    -> gender varchar(2) check(gende='M' or grnder='F'));
Query OK, 0 rows affected (0.11 sec)

mysql> insert into student values(4001,'rajesh','kumar','1994-05-01','II-250-a-3-3','rajanagar','NGV palli','M');
ERROR 1406 (22001): Data too long for column 'dno' at row 1
mysql> insert into student values(4001,'rajesh','kumar','1994-05-01','250-a-3-3','rajanagar','NGV palli','M');
Query OK, 1 row affected (0.01 sec)

mysql> insert into student values(4002,'atif','imam','1995-24-12','250-b-3-3','nagar','palli','M');
ERROR 1292 (22007): Incorrect date value: '1995-24-12' for column 'dob' at row 1
mysql> insert into student values(4002,'atif','imam','1995-12-24','250-b-3-3','nagar','palli','M');
Query OK, 1 row affected (0.01 sec)

mysql> show tables
    -> ;
+----------------+
| Tables_in_name |
+----------------+
| city           |
| district       |
| state          |
| student        |
+----------------+
4 rows in set (0.00 sec)

mysql> select *from student;
+------+--------+--------+------------+-----------+-----------+-----------+--------+
| id   | f_name | l_name | dob        | dno       | street    | street2   | gender |
+------+--------+--------+------------+-----------+-----------+-----------+--------+
| 4001 | rajesh | kumar  | 1994-05-01 | 250-a-3-3 | rajanagar | NGV palli | M      |
| 4002 | atif   | imam   | 1995-12-24 | 250-b-3-3 | nagar     | palli     | M      |
+------+--------+--------+------------+-----------+-----------+-----------+--------+
2 rows in set (0.00 sec)

mysql> drop tables;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '' at line 1
mysql> create database studentrecord;
Query OK, 1 row affected (0.03 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| name               |
| schooldb           |
| studentrecord      |
| test               |
+--------------------+
6 rows in set (0.00 sec)

mysql> use studentrecords;
ERROR 1049 (42000): Unknown database 'studentrecords'
mysql> use studentrecord;
Database changed
mysql> create table state(
    -> sid int unique NOT NULL,
    -> sname varchar(20) NOT NULL);
Query OK, 0 rows affected (0.06 sec)

mysql> insert into state values(101,'tamilnadu');
Query OK, 1 row affected (0.03 sec)

mysql> insert into state (sname,sid) values('kerla',102);
Query OK, 1 row affected (0.03 sec)

mysql> insert into state (sname,sid) values('karnataka',103);
Query OK, 1 row affected (0.02 sec)

mysql> insert into state (sname,sid) values('AP',104);
Query OK, 1 row affected (0.02 sec)

mysql> insert into state (sname,sid) values('punjab',105);
Query OK, 1 row affected (0.01 sec)

mysql> insert into state (sname,sid) values('delhi',106);
Query OK, 1 row affected (0.02 sec)

mysql> create table district(
    -> did int primary key,
    -> dname varchar(20),
    -> sid int references state(sid));
Query OK, 0 rows affected (0.05 sec)

mysql> insert into district values(1001,'bangalore',103);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(1002,'chennai',101);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(1003,'mandya',103);
Query OK, 1 row affected (0.02 sec)

mysql> insert into district values(1004,'mysore',103);
Query OK, 1 row affected (0.00 sec)

mysql> insert into district values(1005,'delhi',106);
Query OK, 1 row affected (0.02 sec)

mysql> create table city(
    -> cid int primary key,
    -> cname varchar(20),
    -> did int references district(did));
Query OK, 0 rows affected (0.05 sec)

mysql> insert into city values(5001,'bangalore',1001);
Query OK, 1 row affected (0.05 sec)

mysql> insert into city values(5002,'hebbal',1001);
Query OK, 1 row affected (0.01 sec)

mysql> insert into city values(5003,'KR puram',1001);
Query OK, 1 row affected (0.02 sec)

mysql> insert into city values(5004,'Nagawara',1001);
Query OK, 1 row affected (0.02 sec)

mysql> insert into city values(5005,'Henoor',1001);
Query OK, 1 row affected (0.02 sec)

mysql> insert into city values(5006,'avadi',1002);
Query OK, 1 row affected (0.01 sec)

mysql> insert into city values(5007,'T nagar',1002);
Query OK, 1 row affected (0.00 sec)

mysql> insert into city values(5008,'Guindy',1002);
Query OK, 1 row affected (0.02 sec)

mysql> insert into city values(5009,'chromepet',1002);
Query OK, 1 row affected (0.02 sec)

mysql> insert into city values(5010,'meerut',1005);
Query OK, 1 row affected (0.01 sec)

mysql> insert into city values(5011,'agra',1005);
Query OK, 1 row affected (0.03 sec)

mysql> create table student(
    -> ID int primary key,
    -> f_name varchar(20),
    -> l_name varchar(10),
    -> dob date,
    -> dno varchar (10),
    -> street varchar(35),
    -> street2 varchar(30),
    -> gender varchar(2) check(gender='M' or gender='F'));
Query OK, 0 rows affected (0.05 sec)

mysql> insert into student values(4001,'Amit','singh','1994-02-10',null,'manyata road',null, 'M');
Query OK, 1 row affected (0.03 sec)

mysql> insert into student values(4002,'harshit','chauhan','1994-03-11',null,'nagawara road',null, 'M');
Query OK, 1 row affected (0.03 sec)

mysql> insert into student values(4003,'Manish','kumar','1994-03-21','25','mysore road',null, 'M');
Query OK, 1 row affected (0.02 sec)

mysql> insert into student values(4004,'Akashya',null,'1994-05-15',null,'hebbal out ring',null, 'M');
Query OK, 1 row affected (0.02 sec)

mysql> insert into student values(4005,'sugumar',null,'1994-10-10',null,'vellore road',null, 'M');
Query OK, 1 row affected (0.01 sec)

mysql> insert into student values(4006,'rajesh','kumar','1994-02-26',16,'kuppam road',null, 'M');
Query OK, 1 row affected (0.02 sec)

mysql> insert into student values(4007,'kayal','vizhi','1994-04-28',1/25,'maduarai road',null, 'F');
ERROR 1406 (22001): Data too long for column 'dno' at row 1
mysql> insert into student values(4008,'kiran','kumar','1994-12-10',null,'vkotta road',null, 'M');
Query OK, 1 row affected (0.02 sec)

mysql> insert into student values(4009,'uma',null,'1994-02-10',null,'ap road',null, 'F');
Query OK, 1 row affected (0.00 sec)

mysql> insert into student values(4010,'amar preet',null,'1994-06-11',11,'mysore road',null, 'F');
Query OK, 1 row affected (0.01 sec)

mysql> create table subject(
    -> subid  int primary key,
    -> subname varchar(15));
Query OK, 0 rows affected (0.08 sec)

mysql> insert into subject values(01,'maths');
Query OK, 1 row affected (0.02 sec)

mysql> insert into subject values(02,'english');
Query OK, 1 row affected (0.01 sec)

mysql> insert into subject values(03,'science');
Query OK, 1 row affected (0.01 sec)

mysql> insert into subject values(04,'hindi');
Query OK, 1 row affected (0.02 sec)

mysql> insert into subject values(05,'sanskrit');
Query OK, 1 row affected (0.00 sec)

mysql> insert into subject values(06,'tamil');
Query OK, 1 row affected (0.01 sec)

mysql> insert into subject values(07,'social studies');
Query OK, 1 row affected (0.01 sec)

mysql> create table connect1(
    -> ID int references student(ID),
    -> cid int references city(cid),
    -> l1 int references subject(subid),
    -> l2 int references subject(subid),
    -> l3 int references subject(subid));
Query OK, 0 rows affected (0.05 sec)

mysql> insert into connect1 values(4001,5001,04,02,01);
Query OK, 1 row affected (0.02 sec)

mysql> insert into connect1 values(4002,5003,03,02,01);
Query OK, 1 row affected (0.01 sec)

mysql> insert into connect1 values(4003,5002,04,06,01);
Query OK, 1 row affected (0.02 sec)

mysql> insert into connect1 values(4004,5004,05,02,01);
Query OK, 1 row affected (0.02 sec)

mysql> insert into connect1 values(4005,5005,03,02,01);
Query OK, 1 row affected (0.02 sec)

mysql> insert into connect1 values(4006,5006,06,02,01);
Query OK, 1 row affected (0.00 sec)

mysql> insert into connect1 values(4007,5006,06,02,01);
Query OK, 1 row affected (0.01 sec)

mysql> insert into connect1 values(4008,5009,06,02,03);
Query OK, 1 row affected (0.03 sec)

mysql> create table marks(
    -> ID int references student(ID),
    -> M1 int check(M1 between 0 and 50),
    -> M2 int check(M2 between 0 and 50),
    -> M3  int check(M3 between 0 and 50),
    -> M4  int check(M4 between 0 and 50),
    -> M5  int check(M5 between 0 and 50),
    -> testno int check(testno between 1 and 10),
    -> primary key(ID,testno));
Query OK, 0 rows affected (0.03 sec)

mysql> insert into marks values(4001,45,46,47,48,49,1);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4003,30,40,37,20,35,1);
Query OK, 1 row affected (0.01 sec)

mysql> insert into marks values(4002,0,40,27,50,35,1);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4004,35,14,07,29,15,1);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4005,39,40,32,31,40,1);
Query OK, 1 row affected (0.01 sec)

mysql> insert into marks values(4006,40,40,47,40,45,1);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4007,30,40,30,20,25,1);
Query OK, 1 row affected (0.00 sec)

mysql> insert into marks values(4008,45,49,47,50,45,1);
Query OK, 1 row affected (0.02 sec)

mysql>
mysql> insert into marks values(4001,35,36,37,38,39,2);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4003,30,40,37,30,45,2);
Query OK, 1 row affected (0.01 sec)

mysql> insert into marks values(4002,0,40,17,50,35,2);
Query OK, 1 row affected (0.00 sec)

mysql> insert into marks values(4004,36,14,07,29,15,2);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4005,29,10,32,31,20,2);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4009,10,40,17,40,45,2);
Query OK, 1 row affected (0.01 sec)

mysql> insert into marks values(4008,30,40,30,20,25,2);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4010,15,19,47,50,45,2);
Query OK, 1 row affected (0.00 sec)

mysql>
mysql> insert into marks values(4010,45,46,47,48,49,3);
Query OK, 1 row affected (0.01 sec)

mysql> insert into marks values(4009,30,40,37,20,31,3);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4008,0,40,27,50,35,3);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4004,35,14,47,29,15,3);
Query OK, 1 row affected (0.00 sec)

mysql> insert into marks values(4005,39,43,32,31,40,3);
Query OK, 1 row affected (0.00 sec)

mysql> insert into marks values(4002,40,42,47,40,45,3);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4007,31,40,34,28,25,3);
Query OK, 1 row affected (0.02 sec)

mysql> insert into marks values(4001,15,19,37,25,45,3);
Query OK, 1 row affected (0.00 sec)

mysql> show tables;
+-------------------------+
| Tables_in_studentrecord |
+-------------------------+
| city                    |
| connect1                |
| district                |
| marks                   |
| state                   |
| student                 |
| subject                 |
+-------------------------+
7 rows in set (0.00 sec)

mysql> drop student;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'student' at line 1
mysql> drop table student;
Query OK, 0 rows affected (0.03 sec)

mysql> create table student(
    -> ID int primary key,
    -> f_name varchar(20),
    -> l_name varchar(10),
    -> dob date,
    -> dno varchar (10),
    -> street varchar(35),
    -> street2 varchar(30),
    -> gender varchar(2) check(gender='M' or gender='F')));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ')' at line 9
mysql> gender varchar(2) check(gender='M' or gender='F'));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'gender varchar(2) check(gender='M' or gender='F'))' at line 1
mysql> gender varchar(2) check(gender='M' or gender='F'));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'gender varchar(2) check(gender='M' or gender='F'))' at line 1
mysql> create table student(
    -> ID int primary key,
    -> f_name varchar(20),
    -> l_name varchar(10),
    -> dob date,
    -> dno varchar (10),
    -> street varchar(35),
    -> street2 varchar(30),
    -> gender varchar(2) check(gender='M' or gender='F'));
Query OK, 0 rows affected (0.05 sec)

mysql> insert into student values(4001,'Amit','singh','1994-02-10',null,'manyata road',null, 'M');
Query OK, 1 row affected (0.03 sec)

mysql> insert into student values(4002,'harshit','chauhan','1994-03-11',null,'nagawara road',null, 'M');
Query OK, 1 row affected (0.01 sec)

mysql> insert into student values(4003,'Manish','kumar','1994-03-21','25','mysore road',null, 'M');
Query OK, 1 row affected (0.02 sec)

mysql> insert into student values(4004,'Akashya',null,'1994-05-15',null,'hebbal out ring',null, 'M');
Query OK, 1 row affected (0.02 sec)

mysql> insert into student values(4005,'sugumar',null,'1994-10-10',null,'vellore road',null, 'M');
Query OK, 1 row affected (0.01 sec)

mysql> insert into student values(4006,'rajesh','kumar','1994-02-26',16,'kuppam road',null, 'M');
Query OK, 1 row affected (0.00 sec)

mysql> insert into student values(4007,'kayal','vizhi','1994-04-28',1/25,'maduarai road',null, 'F');
ERROR 1406 (22001): Data too long for column 'dno' at row 1
mysql> insert into student values(4008,'kiran','kumar','1994-12-10',null,'vkotta road',null, 'M');
Query OK, 1 row affected (0.02 sec)

mysql> insert into student values(4009,'uma',null,'1994-02-10',null,'ap road',null, 'F');
Query OK, 1 row affected (0.02 sec)

mysql> insert into student values(4010,'amar preet',null,'1994-06-11',11,'mysore road',null, 'F');
Query OK, 1 row affected (0.00 sec)

mysql> select distinct id from state;
ERROR 1054 (42S22): Unknown column 'id' in 'field list'
mysql> select distinct id from student;
+------+
| id   |
+------+
| 4001 |
| 4002 |
| 4003 |
| 4004 |
| 4005 |
| 4006 |
| 4008 |
| 4009 |
| 4010 |
+------+
9 rows in set (0.03 sec)

mysql> select f_name FIRSTname from student;
+------------+
| FIRSTname  |
+------------+
| Amit       |
| harshit    |
| Manish     |
| Akashya    |
| sugumar    |
| rajesh     |
| kiran      |
| uma        |
| amar preet |
+------------+
9 rows in set (0.00 sec)

mysql> select f_name "FIRST name" from student;
+------------+
| FIRST name |
+------------+
| Amit       |
| harshit    |
| Manish     |
| Akashya    |
| sugumar    |
| rajesh     |
| kiran      |
| uma        |
| amar preet |
+------------+
9 rows in set (0.00 sec)

mysql> select f_name,dob,(now()-dob)/365 Age from student;
+------------+------------+-----------------+
| f_name     | dob        | Age             |
+------------+------------+-----------------+
| Amit       | 1994-02-10 | 55288756724.386 |
| harshit    | 1994-03-11 |  55288756724.11 |
| Manish     | 1994-03-21 | 55288756724.082 |
| Akashya    | 1994-05-15 | 55288756723.551 |
| sugumar    | 1994-10-10 | 55288756722.195 |
| rajesh     | 1994-02-26 | 55288756724.342 |
| kiran      | 1994-12-10 | 55288756721.647 |
| uma        | 1994-02-10 | 55288756724.386 |
| amar preet | 1994-06-11 | 55288756723.288 |
+------------+------------+-----------------+
9 rows in set (0.03 sec)

mysql> select f_name,dob,(now()-dob) Age from student;
+------------+------------+----------------+
| f_name     | dob        | Age            |
+------------+------------+----------------+
| Amit       | 1994-02-10 | 20180396204422 |
| harshit    | 1994-03-11 | 20180396204321 |
| Manish     | 1994-03-21 | 20180396204311 |
| Akashya    | 1994-05-15 | 20180396204117 |
| sugumar    | 1994-10-10 | 20180396203622 |
| rajesh     | 1994-02-26 | 20180396204406 |
| kiran      | 1994-12-10 | 20180396203422 |
| uma        | 1994-02-10 | 20180396204422 |
| amar preet | 1994-06-11 | 20180396204021 |
+------------+------------+----------------+
9 rows in set (0.00 sec)

mysql> select curdate();
+------------+
| curdate()  |
+------------+
| 2018-04-16 |
+------------+
1 row in set (0.00 sec)

mysql> select f_name,dob,(curdate()-dob) Age from student;
+------------+------------+--------+
| f_name     | dob        | Age    |
+------------+------------+--------+
| Amit       | 1994-02-10 | 240206 |
| harshit    | 1994-03-11 | 240105 |
| Manish     | 1994-03-21 | 240095 |
| Akashya    | 1994-05-15 | 239901 |
| sugumar    | 1994-10-10 | 239406 |
| rajesh     | 1994-02-26 | 240190 |
| kiran      | 1994-12-10 | 239206 |
| uma        | 1994-02-10 | 240206 |
| amar preet | 1994-06-11 | 239805 |
+------------+------------+--------+
9 rows in set (0.00 sec)

mysql> select f_name,dob,(curdate()-dob)/12 Age from student;
+------------+------------+-----------------+
| f_name     | dob        | Age             |
+------------+------------+-----------------+
| Amit       | 1994-02-10 | 20017.166666667 |
| harshit    | 1994-03-11 |        20008.75 |
| Manish     | 1994-03-21 | 20007.916666667 |
| Akashya    | 1994-05-15 |        19991.75 |
| sugumar    | 1994-10-10 |         19950.5 |
| rajesh     | 1994-02-26 | 20015.833333333 |
| kiran      | 1994-12-10 | 19933.833333333 |
| uma        | 1994-02-10 | 20017.166666667 |
| amar preet | 1994-06-11 |        19983.75 |
+------------+------------+-----------------+
9 rows in set (0.00 sec)

mysql> select f_name,dob,(curdate()-dob)/(365*12) Age from student;
+------------+------------+-----------------+
| f_name     | dob        | Age             |
+------------+------------+-----------------+
| Amit       | 1994-02-10 | 54.841552511416 |
| harshit    | 1994-03-11 | 54.818493150685 |
| Manish     | 1994-03-21 | 54.816210045662 |
| Akashya    | 1994-05-15 | 54.771917808219 |
| sugumar    | 1994-10-10 | 54.658904109589 |
| rajesh     | 1994-02-26 | 54.837899543379 |
| kiran      | 1994-12-10 | 54.613242009132 |
| uma        | 1994-02-10 | 54.841552511416 |
| amar preet | 1994-06-11 |           54.75 |
+------------+------------+-----------------+
9 rows in set (0.01 sec)

mysql>