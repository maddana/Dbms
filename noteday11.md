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

	* select ID,f_name,testno 
</p><br>
<p>
Q.7 Least city name along with the number of people are there?
</p><br>
<p>
Q.8 Least city name along with the number of people are there in each city and if no one stays in the city give null?

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

