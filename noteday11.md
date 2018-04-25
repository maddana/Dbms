### Numbers
<p>
	* select round(456.6,0),round(456.222,2),round(456.2222,-1),round(456.2222,-2),round(456.2222,-3);

	+----------------+------------------+--------------------+--------------------+--------------------+
	| round(456.6,0) | round(456.222,2) | round(456.2222,-1) | round(456.2222,-2) | round(456.2222,-3) |
	+----------------+------------------+--------------------+--------------------+--------------------+
	|            457 |           456.22 |                460 |                500 |                  0 |
	+----------------+------------------+--------------------+--------------------+--------------------+
	1 row in set (0.02 sec)
	* If we use positive inround function the decimal parts will be(0<5,1>5).
</p><br>
<p>
	* truncate remove the digits.

	*  select truncate(456.6,0) T1,truncate(456.222,2) T2,truncate(456.2222,-1) T3,truncate(456.2222,-2) T4,truncate(456.2222,-3) T5;

	+-----+--------+-----+-----+----+
	| T1  | T2     | T3  | T4  | T5 |
	+-----+--------+-----+-----+----+
	| 456 | 456.22 | 450 | 400 |  0 |
	+-----+--------+-----+-----+----+
	1 row in set (0.00 sec)

</p><br>
<p>
* Ceil
	* select ceil(456.6,0) T1,ceil(456.222,2) T2,ceil(456.2222,-1) T3,ceil(456.2222,-2) T4,ceil(456.2222,-3) T5;
</p><br>
<p>
* floor
	* select floor(456.6) T1,floor(456.222) T2,floor(456.2222) T3,floor(456.2222) T4,floor(456.2222) T5;

	+-----+-----+-----+-----+-----+
	| T1  | T2  | T3  | T4  | T5  |
	+-----+-----+-----+-----+-----+
	| 456 | 456 | 456 | 456 | 456 |
	+-----+-----+-----+-----+-----+
	1 row in set (0.01 sec)
</p><br>
<p>
* mod()
	* select mod(5,2) T1;
	+------+
	| T1   |
	+------+
	|    1 |
	+------+
</p><br>

## Date Function
<p>
	* select current_date();

	+----------------+
	| current_date() |
	+----------------+
	| 2018-04-24     |
	+----------------+
	1 row in set (0.03 sec)
</p><br>
<p>
Q.2 year(),month(),day() // specified feilds

	* select year(current_date()) Y,month(current_date()) M,day(current_date()) D;

	+------+------+------+
	| Y    | M    | D    |
	+------+------+------+
	| 2018 |    4 |   24 |
	+------+------+------+
	1 row in set (0.01 sec)
</p><br>
<p>
Q.3 select DATE_FORMAT(current_date(),'%d %b %y') DATE;

	+-----------+
	| DATE      |
	+-----------+
	| 24 Apr 18 |
	+-----------+
	1 row in set (0.02 sec)
</p><br>
<p>
Q.4 We need comma between feilds?

	*  select DATE_FORMAT(current_date(),'%D,%b,%y') DATE;

	+-------------+
	| DATE        |
	+-------------+
	| 24th,Apr,18 |
	+-------------+
	1 row in set (0.00 sec)
</p><br>
<p>
Q.5 write a query to display date difference in terms of days months and year?

	* select datediff(current_date(),'2017-02-27') diff;

	+------+
	| Diff |
	+------+
	|  421 |
	+------+
	1 row in set (0.00 sec)

	* select floor((datediff(current_date(),'2017-02-27')/30)/12) Year_diff;
	
	+-----------+
	| Year_diff |
	+-----------+
	|         1 |
	+-----------+
	1 row in set (0.00 sec)
	
	* select floor((datediff(current_date(),'2017-02-27')/30)/12) Year_diff,floor((datediff(current_date(),'2017-02-27')/30)%12) Month_diff;

	+-----------+------------+
	| Year_diff | Month_diff |
	+-----------+------------+
	|         1 |          2 |
	+-----------+------------+
	1 row in set (0.00 sec)
<p>
Q.6 print the first not null values in the columns

	* select coalesce(l_name,dob,f_name) from student;

	+-----------------------------+
	| coalesce(l_name,dob,f_name) |
	+-----------------------------+
	| singh                       |
	| chauhan                     |
	| kumar                       |
	| 1994-05-15                  |
	| 1994-10-10                  |
	| kumar                       |
	| kumar                       |
	| 1994-02-10                  |
	| 1994-06-11                  |
	+-----------------------------+
	9 rows in set (0.00 sec)
</p><br>
<p>
Q.6 Write a query to display student id ,name,and number of test he has taken?

	* select ID,count(*) N_TEST from marks group by ID;
	* select a.ID,a.f_name,b.N_TEST from student a inner join (select ID,count(*) N_TEST from marks group by ID)b on a.ID=b.ID;
	
	+------+------------+--------+
	| ID   | f_name     | N_TEST |
	+------+------------+--------+
	| 4001 | Amit       |      3 |
	| 4002 | harshit    |      3 |
	| 4003 | Manish     |      2 |
	| 4004 | Akashya    |      3 |
	| 4005 | sugumar    |      3 |
	| 4006 | rajesh     |      1 |
	| 4008 | kiran      |      3 |
	| 4009 | uma        |      2 |
	| 4010 | amar preet |      2 |
	+------+------------+--------+
	9 rows in set (0.13 sec)
	
	* select s.ID,s.f_name,count(*) N_TEST from student s,marks m where s.ID=m.ID group by s.ID;
	
	*  select s.ID,s.f_name,count(*) N_TEST from student s,marks m where s.ID=m.ID group by s.ID having count(*)>2 order by count(*);

	*  select a.ID,a.f_name,b.N_TEST from student a inner join (select ID,count(*) N_TEST from marks group by ID having count(*)>2)b on a.ID=b.ID order by b.N_TEST,a.ID desc;
</p><br>
<p>
Q.7 Least city name along with the number of people are there?

	* select cid,count(*) cno from conneect1 group by cid;
	
	* select a.cid,a.cname,b.cno from city a inner join(select cid,count(*) cno from connect1 group by cid) b on(a.cid=b.cid);

	+------+-----------+-----+
	| cid  | cname     | cno |
	+------+-----------+-----+
	| 5001 | bangalore |   1 |
	| 5002 | hebbal    |   1 |
	| 5003 | KR puram  |   1 |
	| 5004 | Nagawara  |   1 |
	| 5005 | Henoor    |   1 |
	| 5006 | avadi     |   2 |
	| 5009 | chromepet |   1 |
	+------+-----------+-----+
	7 rows in set (0.06 sec)
</p><br>
<p>
Q.8 Least city name along with the number of people are there in each city and if no one stays in the city give null?

	* select a.cid,a.cname,ifnull(b.cno,'null') from city a left outer join(select cid,count(*) cno from connect1 group by cid) b on(a.cid=b.cid);

	+------+-----------+----------------------+
	| cid  | cname     | ifnull(b.cno,'null') |
	+------+-----------+----------------------+
	| 5001 | bangalore | 1                    |
	| 5002 | hebbal    | 1                    |
	| 5003 | KR puram  | 1                    |
	| 5004 | Nagawara  | 1                    |
	| 5005 | Henoor    | 1                    |
	| 5006 | avadi     | 2                    |
	| 5007 | T nagar   | null                 |
	| 5008 | Guindy    | null                 |
	| 5009 | chromepet | 1                    |
	| 5010 | meerut    | null                 |
	| 5011 | agra      | null                 |
	+------+-----------+----------------------+
	11 rows in set (0.01 sec)

	* Using In-line view
		
		* 

</p><br>

<p>

Q.9 Aggregate and non aggregate

	* select count(*),count(ID),sum(M1) from student;
	* count() is aggregate .
	* select ID,count(*),count(ID),sum(M1), from marks group by ID;
	* ID is non aggregate which can be used only group by when we have to use both aggr and non-aggre functions.
	* When using aggregate we have to use having function instead of where ,where is used for non-aggre functions.
	* ex.select ID,count(*),count(ID),sum(M1),avg(M1) from marks where ID between 4001 and 4005 group by ID having count(*) >1;
	
	+------+----------+-----------+---------+---------+
	| ID   | count(*) | count(ID) | sum(M1) | avg(M1) |
	+------+----------+-----------+---------+---------+
	| 4001 |        3 |         3 |      95 | 31.6667 |
	| 4002 |        3 |         3 |      40 | 13.3333 |
	| 4003 |        2 |         2 |      60 | 30.0000 |
	| 4004 |        3 |         3 |     106 | 35.3333 |
	| 4005 |        3 |         3 |     107 | 35.6667 |
	+------+----------+-----------+---------+---------+
	5 rows in set (0.06 sec)
</p><br>
<p>
Q.10 Write a query to display day name along with no of students born in each day?
	
	* select date_format(dob,'%a'),count(*) from student group by date_format(dob,'%a'); 

	+-----------------------+----------+
	| date_format(dob,'%a') | count(*) |
	+-----------------------+----------+
	| Fri                   |        1 |
	| Mon                   |        2 |
	| Sat                   |        3 |
	| Sun                   |        1 |
	| Thu                   |        2 |
	+-----------------------+----------+
	5 rows in set (0.03 sec)
</p><br>
<p>
Q.11 Dispaly the date which has highest students?

	* select date_format(dob,'%a'),count(*) from student group by date_format(dob,'%a') having count(*) in(select max(b.x) from (select count(*) x from student group by date_format(dob,'%a'))b);

	+-----------------------+----------+
	| date_format(dob,'%a') | count(*) |
	+-----------------------+----------+
	| Sat                   |        3 |
	+-----------------------+----------+
	1 row in set (0.00 sec)
</p><br>
<p>
Q.12 write a query to to show month wise no students born?Write a query whose birthday lies in next week?

	*  select date_format(dob,'%M'),count(*) from student group by date_format(dob,'%M');

	+-----------------------+----------+
	| date_format(dob,'%M') | count(*) |
	+-----------------------+----------+
	| December              |        1 |
	| February              |        3 |
	| June                  |        1 |
	| March                 |        2 |
	| May                   |        1 |
	| October               |        1 |
	+-----------------------+----------+
	
	* select date_format(dob,'%M'),count(*) from student group by date_format(dob,'%M') having count(*) in(select max(b.x) from (select count(*) x from student group by date_format(dob,'%M'))b);

	+-----------------------+----------+
	| date_format(dob,'%M') | count(*) |
	+-----------------------+----------+
	| February              |        3 |
	+-----------------------+----------+
	1 row in set (0.00 sec)

	* 