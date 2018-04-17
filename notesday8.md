### SQL Operators

<p>
* Different sql operators are

	* in
	* between
	* is null
	* is not null	
	* not in
	* not between
</p><br>
<p>
Q.1 Write a query to display student id and student first name whos last name is null.
	
	* select ID,f_name,l_name from student where l_name is null;

	+------+------------+--------+
	| ID   | f_name     | l_name |
	+------+------------+--------+
	| 4004 | Akashya    | NULL   |
	| 4005 | sugumar    | NULL   |
	| 4009 | uma        | NULL   |
	| 4010 | amar preet | NULL   |
	+------+------------+--------+
	4 rows in set (0.00 sec)
</p><br>
<p>
Q.2 Write a query to display student first name and last name whos name starts with a-m?
	
	* select ID,f_name,l_name from student where f_name between 'A' and 'N';

	+------+------------+---------+
	| ID   | f_name     | l_name  |
	+------+------------+---------+
	| 4001 | Amit       | singh   |
	| 4002 | harshit    | chauhan |
	| 4003 | Manish     | kumar   |
	| 4004 | Akashya    | NULL    |
	| 4008 | kiran      | kumar   |
	| 4010 | amar preet | NULL    |
	+------+------------+---------+
	6 rows in set (0.00 sec)
</p><br>
<p>
Q.3 give the list of id and name who is born between  jan and march?
	
	* select ID,f_name,dob from student where month(dob) between 01 and 03;

	+------+---------+------------+
	| ID   | f_name  | dob        |
	+------+---------+------------+
	| 4001 | Amit    | 1994-02-10 |
	| 4002 | harshit | 1994-03-11 |
	| 4003 | Manish  | 1994-03-21 |
	| 4006 | rajesh  | 1994-02-26 |
	| 4009 | uma     | 1994-02-10 |
	+------+---------+------------+
	5 rows in set (0.00 sec)
</p><br>
<p>
Q.4 Write a query to dispaly name where the first name delimited by hiphen - lastname and alias should be name?
	
	* select ID,concat(f_name,'-',l_name) NAME from student;

	+------+-----------------+
	| ID   | NAME            |
	+------+-----------------+
	| 4001 | Amit-singh      |
	| 4002 | harshit-chauhan |
	| 4003 | Manish-kumar    |
	| 4004 | NULL            |
	| 4005 | NULL            |
	| 4006 | rajesh-kumar    |
	| 4008 | kiran-kumar     |
	| 4009 | NULL            |
	| 4010 | NULL            |
	+------+-----------------+
	9 rows in set (0.03 sec)
	
	* select ID,concat(f_name,'-',ifnull(l_name,' ')) NAME from student; 

	+------+-----------------+
	| ID   | NAME            |
	+------+-----------------+
	| 4001 | Amit-singh      |
	| 4002 | harshit-chauhan |
	| 4003 | Manish-kumar    |
	| 4004 | Akashya-        |
	| 4005 | sugumar-        |
	| 4006 | rajesh-kumar    |
	| 4008 | kiran-kumar     |
	| 4009 | uma-            |
	| 4010 | amar preet-     |
	+------+-----------------+
	9 rows in set (0.01 sec)
</p><br>
<p>
Q.5 Write a query to dispaly mr or mrs for the gender?
	
	* select ID,case when gender='M' then concat('Mr.',f_name,'-',ifnull(l_name,' ')) else concat('Miss.',f_name,'-',ifnull(l_name,' ')) end NAME from student;

	+------+--------------------+
	| ID   | NAME               |
	+------+--------------------+
	| 4001 | Mr.Amit-singh      |
	| 4002 | Mr.harshit-chauhan |
	| 4003 | Mr.Manish-kumar    |
	| 4004 | Mr.Akashya-        |
	| 4005 | Mr.sugumar-        |
	| 4006 | Mr.rajesh-kumar    |
	| 4008 | Mr.kiran-kumar     |
	| 4009 | Miss.uma-          |
	| 4010 | Miss.amar preet-   |
	+------+--------------------+
	9 rows in set (0.00 sec)
</p><br>
<p>
Q.6 Write a query to dispaly student id,total marks and result for first test?

	* Note:If the student is failed in any one of the subject he/she should be treated as failed. 
 	* select ID,(M1+M2+M3+M4+M5) TOTAL ,
	* case when M1<35 or M2<35 or M3<35 or M4<35 or M5<35 then 'Failed'
	* when (M1+M2+M3+M4+M5)/5 between 35 and 49 then 'Pass'
	* when (M1+M2+M3+M4+M5)/5 between 50 and 59 then 'II Class Pass'
	* when (M1+M2+M3+M4+M5)/5 between 60 and 75 then 'I Class Pass'
	* else 'Distinction pass' end RESULT from marks where testno=1;
	* // Sum is used for columns not for rows.

	+------+-------+------------------+
	| ID   | TOTAL | RESULT           |
	+------+-------+------------------+
	| 4001 |   235 | Distinction pass |
	| 4002 |   152 | Failed           |
	| 4003 |   162 | I Class Pass     |
	| 4004 |   100 | Failed           |
	| 4005 |   182 | Distinction pass |
	| 4006 |   212 | Distinction pass |
	| 4007 |   145 | I Class Pass     |
	| 4008 |   236 | Distinction pass |
	+------+-------+------------------+
	8 rows in set (0.00 sec)</p>,<br>

<p>// display the name
 
	* select s.ID,s.f_name,(m.M1+m.M2+m.M3+m.M4+m.M5) TOTAL ,
	* case when M1<35 or M2<35 or M3<35 or M4<35 or M5<35 then 'Failed'
	* when (M1+M2+M3+M4+M5)/5 between 35 and 49 then 'Pass'
	* when (M1+M2+M3+M4+M5)/5 between 50 and 59 then 'II Class Pass'
	* when (M1+M2+M3+M4+M5)/5 between 60 and 75 then 'I Class Pass'
	* else 'Distinction pass' end RESULT from marks m,student s where m.id=s.id and testno=1;

	+------+---------+-------+--------+
	| ID   | f_name  | TOTAL | RESULT |
	+------+---------+-------+--------+
	| 4001 | Amit    |   235 | Pass   |
	| 4002 | harshit |   152 | Failed |
	| 4003 | Manish  |   162 | Failed |
	| 4004 | Akashya |   100 | Failed |
	| 4005 | sugumar |   182 | Failed |
	| 4006 | rajesh  |   212 | Pass   |
	| 4008 | kiran   |   236 | Pass   |
	+------+---------+-------+--------+
	7 rows in set (0.01 sec)</p><br>
<p>
// Add city
	
	*  select s.ID,s.f_name,c.cname from student s,city c,connect1 c1 where c1.ID=s.ID and c1.cid=c.cid;

	+------+---------+-----------+
	| ID   | f_name  | cname     |
	+------+---------+-----------+
	| 4001 | Amit    | bangalore |
	| 4002 | harshit | KR puram  |
	| 4003 | Manish  | hebbal    |
	| 4004 | Akashya | Nagawara  |
	| 4005 | sugumar | Henoor    |
	| 4006 | rajesh  | avadi     |
	| 4008 | kiran   | chromepet |
	+------+---------+-----------+
	7 rows in set (0.03 sec)
</p><br>
<p>
Q.7 Write a query to display student id ,name,first language,marks of first lang,
2nd language,marks for 2nd language,3rd lan,marks for 3rd lang,max marks and total marks for the test.
	
	* select a.ID,a.f_name,c.subname,f.M1,c1.subname,f.M2,c2.subname,f.M3,f.M4 SCIENCE,f.M5 SOCIAL
from student a,connect1 t,marks f,subject c,subject c1,subject c2 where a.ID=t.ID and a.ID=f.ID and t.L1=c.subid and 
t.L2=c1.subid and t.L3=c2.subid and testno=1;

	+------+---------+----------+------+---------+------+---------+------+---------+--------+
	| ID   | f_name  | subname  | M1   | subname | M2   | subname | M3   | SCIENCE | SOCIAL |
	+------+---------+----------+------+---------+------+---------+------+---------+--------+
	| 4001 | Amit    | hindi    |   45 | english |   46 | maths   |   47 |      48 |     49 |
	| 4002 | harshit | science  |    0 | english |   40 | maths   |   27 |      50 |     35 |
	| 4003 | Manish  | hindi    |   30 | tamil   |   40 | maths   |   37 |      20 |     35 |
	| 4004 | Akashya | sanskrit |   35 | english |   14 | maths   |    7 |      29 |     15 |
	| 4005 | sugumar | science  |   39 | english |   40 | maths   |   32 |      31 |     40 |
	| 4006 | rajesh  | tamil    |   40 | english |   40 | maths   |   47 |      40 |     45 |
	| 4008 | kiran   | tamil    |   45 | english |   49 | science |   47 |      50 |     45 |
	+------+---------+----------+------+---------+------+---------+------+---------+--------+
	7 rows in set (0.00 sec)
</p><br>