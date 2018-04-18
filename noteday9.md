### Joints in Dbms

# Inner join

* If the tables have same column data then inner join is used to refer the data.
* It give the data of similar data in different tables. 
* In inner join alias is important.

# Outer join

* If we have nagation(~) then it is outer join.

# left outer join

* Primary key data present and in the foreign key there is no data then it is left outer join.

# right outer join


# self join

* If both primary and foreign key are present in same table it is refered as self join.
<p>
Q.1 Write a query to display id,name and marks1?

// Natural join
* select ID,f_name,m1 from student natural join marks; 
* select ID,f_name,m1 from student natural join marks where testno=1;
// Inner join
* select a.ID,a.f_name,b.m1 from student a inner join marks b on(a.id=b.id);
* select a.ID,a.f_name,b.m1 from student a inner join marks b on(a.id=b.id and testno=1);
//Left outer join
* select a.ID,a.f_name,b.m1 from student a left outer join marks b on(a.id=b.id);
* select a.ID,a.f_name,b.m1 from student a left outer join marks b on(a.id=b.id and b.testno=1);
* select a.ID,a.f_name,b.m1 from student a left outer join marks b on(a.id=b.id and b.testno=1) where b.m1 is null;
</p><br>
<p>
Q.2 Write a inner join display name,city name?

* select a.f_name,b.cname from student a inner join connect1 c on(a.id=c.id) inner join city b on(b.cid=c.cid);
</p><br>
<p>
Q.3 Write student name,city,district,state?

* select a.ID,a.f_name,b.cname,d.dname,s.sname from student a inner join connect1 c on(a.ID=c.ID)
inner join city b on(b.cid=c.cid) inner join district d on(d.did=b.did)
inner join state s on(s.sid=d.sid);
</p><br>
<p>
Q.4 Write a query name,id and marks and dispaly details if he is not taken?

* select a.ID,a.f_name, case when b.M1 is null or b.M2 is null then
'Absent'
else
(b.M1+b.M2+b.M3+b.M4+b.M5) end TOTAL from student a left outer join marks b on(a.id=b.id and testno=1); 

* select a.ID,a.f_name, ifnull((b.M1+b.M2+b.M3+b.M4+b.M5),'Absent') from student a left outer join marks b on(a.id=b.id and testno=1); 


</p><br>
<p>
Q.5 Write a query to dispaly ho are from bangalore if he is from bangalore print from bangalore and if he is not out of bangalore?

* select a.ID,a.f_name, case when c.cname='bangalore' then 'From Bangalore'
else 'Not from Bangalore' end RES from student a left outer join connect1 c1 on(a.ID=c1.ID)
left outer join city c on(c.cid=c1.cid);
</p><br>
<p>
# Sub-Query

* 1. In-Line View
	* A subquery written 'from' clause instead of using a table name.
	* select id,(M1+M2+M3+M4+M5) total,testno from marks
	* select id,total,total/5 avg from(select id,(M1+M2+M3+M4+M5) total,testno from marks) A;
//print name and total avg
	* select a.id,a.f_name,b.total,b.total/5 avg from student a inner join (select id,(M1+M2+M3+M4+M5) total,testno from marks)b on(a.id=b.id);
//print name and city name
	* select x1.id,x1.f_name,y1.cname from student x1 inner join (select a.id,b.cname from connect1 a inner join city b on(a.cid=b.cid))y1 on (x1.id=y1.id);

* 2. Normal subquery
	* A subquery written 'where' clause instead of giving a value for comparison, that query wriiten.
	* A normal subquery is of type 1. Single column subquery. 2. Multi cloumn subquery.
	* 3. Sinle row subquery
		* '=','>','<'
	* 4. Multiple row subquery
		* 'in','> all','> any','< all','< any' (also sinle row operators)
</p><br>































