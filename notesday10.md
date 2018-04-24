Types of Function

1. Single row (non aggregate function example upper,lower,abs)
2.Multi row (aggregate function example sum,max,min)

String function

1. String conversion of uppercase and lowercase.

Select ucase(f_name) from student;

Q.1 Display the name with first char as capital and remaining as small?

2.Select concat(ucase(substring(f_name,1,1)),lcase(substring(f_name,2))) NAME from student;

Q.2 Display Only specific feild/string in the formate given below?

'bangalore-karnataka-india'
* select substring_index((substring_index('bangalore-karnataka-india','-',2)),'-',-1);
