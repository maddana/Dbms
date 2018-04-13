### DATABASE MANAGEMENT SYSTEM(DBMS)
<p>
`````
DBMS-- Database Management System

*Create
*Insert
*Delete
*Query  
MainFrame is used to store the data.
And sql is used to mainpulate the data.</p>
<br>
<p>
Q.1 What is Backend and Frontend process

BackEnd Engine

* Not reachable by user.
* MRP - Memory Resident program.
* DB2,oracle.
* Multi-user.

FrontEnd Process

* Sql is a frontend process.
* It is a language which allow the user to interact with the backend process.
</p><br>
<p>
Q.2 What is database?

* Database-collection of table spaces.
* Table is a collection of rows.
* Rows are collection of columns.
* Columns are collection of attributs and domains.</p><br>
<p>
Q.3 What are attributes and domains?

* Attributes are the name of the feild
* Domain is the set of data stored.(ex numeric data if it is storing integer values).</p><br>
<p>
Q.4 What are different names for tables,rows and columns?

* Tables -- Relation,Table,Entity Set.
* Rows -- Records,Rows and Entity.
* Columns -- Attributes,Domain and Columns.
</p><br>
<p>
Q.5 What is freezing data?

* The data which can't accept no more changes is called freezing.</p><br>
<p>
Q.6 What is Masterdata and Transition data?

* Masterdata -- Data which is permanent and won't change is called masterdata.
* ex.name,city.

* Transition data -- Data that occurs based on the event.
* Data occurs only when a perticular event happens.
* ex.Only when the event(month end) happens the data(salary)
will be credited or initiated. 
</p><br>

<p>
 ## Example Student_details
s.no    name              dob          fname  mname    address                        gender f.occ f.sal	
1    sachin Tendulkar   18/09/2000     raj   devi   f.no:2d,mayflower.coimbatore      male   

ID     f_name  l_name  dob    d.no   street  street2   city   district   pin  state   gender


  
ID     f_name  l_name       dob    d.no   street  street2   city        gender
1      sachin   tendulkar   ...     ...                      mumbai     male
2      sachin1  tendulkar    ...    ...   ....     ....      mumbai     male

ID    district  state
1     mumbai     maharashtra
2     mumbai     maharashtra

state
sid   sname
01    maharashtra
02    karnataka
03   tamilnadu
district
did dname sid
101 mumbai 01
102 pune   01
cid   cname    did
1001  mumbai   101


ID     f_name  l_name       dob    d.no   street  street2      gender
1      sachin   tendulkar   ...     ...                        male
2      sachin1  tendulkar    ...    ...   ....     ....        male

l1
ID   cid   s1    s2 
1   1001   02    04
2   1001   04    06



subject
subid   subname
01       maths
02       english
03       science
04       hindi
05	 sanskrit
06	 tamil
primary key(subid)

Academy
ID     Marks1  Marks2	Marks3    Marks4  Marks5   testno
1      20      00       10         11       22        01
2       33     44      55            66      77       01
1        ..     ..       ..         ..      ..        02 
primary key(id,testno)
where id =101 and marks=40;


`````