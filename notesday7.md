### Creating , Using and Quering the data

<p>
create the database with name called 'name'.

	* create database name; 
</p><br>
<p>
	* show databases;</p><br>
<p>
	* use name;</p><br>
<p>
	* create table state;</p><br>
<p>
	* insert into state vlaues(101,'tamilnadu');//single cot denotes it is a data which is constant

	* insert into state (sname,sid) vlaues('kerala',102);

	* insert into state (sname,sid) values('Ap',104);

	* insert into state (sname,sid) values('punjab',105);

	* insert into state (sname,sid) values('karnataka',106);

</p><br>

<p>
	* create table district(

	* did int primary key,

	* dname varchar(20),

	* sid int references state(sid));//this will create foreign key</p><br>

<p>
	* insert into district values(1001,'bangalore',103);

	* insert into district values(1002,'chittoor',101);

	* insert into district values(1003,'Mysore',103);

	* insert into district values(1004,'vellore',102);

	* insert into district values(1005,'chennai',102);

	* insert into district values(1006,'vizag',101);

</p><br>
<p>
	* create table city(

	* cid int primary key,

	* cname varchar(20),

	* did int references district(did));//reference name of primary and foreign key can be different but the width should be same 

</p><br>
<p>
	* insert into district values(5001,'bangalore',1001);

	* insert into district values(5002,'hebal',1001);

	* insert into district values(5003,'k r puram',1001);

	* insert into district values(5004,'nagawara',1001);

	* insert into district values(5005,'henoor',1001);

	* insert into district values(5006,'chittoor',1002);

	* insert into district values(5007,'madanapalle',1002);

	* insert into district values(5008,'tirupati',1002);

	* insert into district values(5009,'punganur',1002);

	* insert into district values(5010,'palamner',1002);

	* insert into district values(5011,'mysore',1003);

	* insert into district values(5012,'vellore',1004);

	* insert into district values(5013,'katpadi',1004);

	* insert into district values(5014,'chennai',1005);

	* insert into district values(5015,'ranipet',1005);

	* insert into district values(5016,'vizag',1006);
</p><br>

<p>
	* create table student(

	* id int primary key,

	* f_name varchar(20),

	* l_name varchar(20),

	* dob date,

	* dno varchar(10),

	* street varchar(35),

	* street2 varchar(30),

	* gender varchar(2) check(gende='M' or grnder='F'));
</p><br>


<p>
	* insert into student values(4001,'rajesh','kumar','1994-05-01','250-a-3-3','rajanagar','NGV palli','M');</p><br>
<p>
	* create table connect1(

	* id int references student(id),

	* cid int references city(cid),

	* l1 int references subject(subid),

	* l2 int references subject(subid),

	* l3 int references subject(subid));
</p><br>
<p>
	* insert into connect1(4001,5001,4,2,1);
</p><br>
<p>
	* create table marks(

	* id int references student(id),

	* m1 int check(m1 between 0 and 50),

	* m2 int check(m2 between 0 and 50),

	* m3 int check(m3 between 0 and 50),

	* m4 int check(m4 between 0 and 50),

	* m5 int check(m5 between 0 and 50),

	* testno int check(testno between 1 and 10),

	* primary key(id,testno));
</p><br>
<p>
	* insert into marks values(4001,45,46,47,48,49,1),

	* insert into marks values(4002,0,45,40,44,42,1),

	* insert into marks values(4003,47,45,40,44,42,1),

	* insert into marks values(4002,35,30,20,34,32,1),
</p><br>
create table sate1 as select sid from state;

Only for DDL commands it is automatically commited.

For DML commands we have to commit manually. 

<p>
# QUery

	* Query is made up of two things selection(sigma symbol) and projection(pi symbol).
	* select all from table_name
	* distict ca be used only in select call.
	* Age is computed or derived data with key word current_date() or now() or today().
	* In select call we have
		* where
		* subqueries
		* order by
		* group by
</p><br>		
<p>
	* write a command to create a table from existing table without transfer of data?
</p><br>