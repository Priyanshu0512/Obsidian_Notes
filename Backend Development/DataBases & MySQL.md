Problems with file-based system 
- Data Redundancy 
- Data Inconsistency 
- Difficult Data-access
- Security-issues

### Databases 
It is a collection of related data. 
- These help to solve the problem data redundancy and data inconsistency.
- easy app integration.(i.e multiple web and mobile based application can be connected to the same database)

#### DBMS 
DBMS (Database management system) is a interfacing layer between the databases and the user where processing on data to be extracted is done. A lot of DBMS understand the **SQL which stands for structured query language.** EX - mySQL, SQLite, Postgres SQL.
DBMS also provide you the functionality to put constraints on the incoming data. Ex- Type of data to be entered a particular field or length of data to be entered.

#### RDBMS
Relational DBMS is used to store data in form of tables.  
- Rows - Represents actual data of the entities.They are called tuples.
- Columns - Represents the properties of the entities.They are called attributes.

## MySQL

- `show databases;` -> List downs all the databases present in the system.
- `use <databases-name>;` ->  To select a database to run queries.
- `show tables;` -> To shows tables of the selected database.
- `create database <database-name>`- To create a new database.
- Creating new tables -
```mysql
create table <table-name>(
        <column-name-1> [datatype],
        <column-name-2> [datatype],
        .
        .
)
Ex - create table first ( Name varchar(15), DOB DATE , Salary DECIMAL);
```
 Note - Multiple values can be entered by being comma separated.
 
 Adding constraints -
```mysql
create table second( Name varchar(15) not null ,DOB date default "2002-01-01" , Gender enum("Male", "Female","Others"));
```

- `not null`-> The value cannot be empty.
- `default`-> Value is nothing is entered.
- `enum` -> Values to be entered can be only from the set of values entered in the enum set.


- `desc table-name` -> To see the structure and description of the table.
- Inserting a Row -> 
```mysql
insert into <table-name> (col1,col2,col3 ...) value( <value-1> ,<value-2>,..  )
Ex - insert into first(Name , DOB , Salary) values("Priyanshu" ,"2002-12-05", 0.0);
```

- `select <name-of-column> from <name-of_table>` ->  To see the contents of the mentioned columns from the required table.
- `select * from <name-of-table` -> To display the entire content of the table.

#### Adding Constraints 

- `select * from <table-name> where(condition);`-> This displays all the datapoints which meet the required conditions .
```mysql
1. select * from second where Gender ='Male'N;
2. select * from second where DOB =  "2002-01-01" and Gender = "Female";
3. select * from second where not Gender = "Female";
4. select * from second where DOB = "2023--9-06" or Gender = "Female";
```
 - `and` keyword can be used to add multiple conditions to the query. 
 - `or` keyword can be used to give results if either condition is satisfied.
 - `not` keyword can be used to exclude a certain value.

- `select * from <table-name> where name like = "<condtion>"`
     - `"%a%"` - Shows all the data in the tables which has letter a in it.
     - `"_a%"` - Shows all the data in tables which have one letter in-front of a and zero of more letter after a

```mysql
 1. select * from second where Name like "%m%";
 2. select * from second where Name like "_a%";
```

**Sorting Data  & Limiting Outputs Displayed**

- `select * from <table-name> order by <column-name> keyword` 
```mysql 
1.select * from second order by Name desc;//Desceding 
2.select * from second order by Name; //Ascending
3.select * from second order by Name desc Limit 3;
```

`Limit <no.-of-rows to display>`-> This limits the number of rows to be displayed after the query condition are evaluated.

```mysql 
select * from second where Gender = "Male" order by DOB desc Limit 2; //combining all the conditions mentioned above
```

**Deletion of Data** 

- `delete` -> Use the delete keyword to delete data form the table.
```mysql
delete from second where DOB = "2002-01-01" order by name desc limit 1;
```
- `delect *  from <table-name` -> Deletes all the data form the table.

**Updation of Data** 

- `update <table-name> set <column-name>=value where ={condition}`  -> Used to update the dataset in the tables.

```mysql
update second set Name = "Sam" , Gender = "Others" where Name = "Sameer";
```

**Altering Contents** 
- `alter table <table-name> change <old-column-name> <new-column-name> [new constraint(datatype or constraint)]` -> Used this command to alter the column names an its constraints.

```mysql
alter table first change Salary AnnualSalary Decimal(10,2);
```

**Difference between Update and Alter** 
Update is used to change the specific data in the table where conditions are met wherein alter is used to change the fundamental structure of the table like renaming columns or updating constraints.

**Adding Columns**

- `alter table <table-name> add <column-name> [datatype] default "default-value";`

```mysql
alter table second add Sports varchar(10) default "Cricket";
update second set Sports = "Badminton" where Note Gender ="Male";// using update to change the default value of some entries.
```
Note - By adding column in the above way adds them to the last of the table.

- `alter table <table-name> add <column-name> [datatype] after <column-name>;` -> This command adds the columns after the mentioned column name.

```mysql
alter table second add middlename varchar(10) after Name;
```

**Removing Columns** 
- `alter table <table-name> drop <column-name>` -> This drops or removes the mentioned columns from the table.

```mysql
alter table second drop middlename;
```

- `select <column-name> as "Message" from <table-name>` -> This Display the message instead of column-name. Useful when Abbreviations need to written in full form for sake of clarity.

```mysql 
select DOB as "Date of birth" from second;
```

**Concatenating columns** 
- `select concat(<column-name-1>,'-',<column-name-2>,'-'..) as <name of concatenated columns> from <table-name>` -> This query is used to concatenate multiple columns under one column.

```mysql
select concat(Name,' ',DOB,' ',Gender) as Details from second;
```

**Counting Data Entries** 
- `select count(*) as "message" from <table-name> where (condition);` -> Counts the entires in the table which meet the required conditions.

```mysql
select count(*) as "Males" from second where Gender = "Male";
```

### Miscellaneous functions 

- `select distinct <column-name> from <table-name>;` -> This command is used to select distinct entries from column mentioned.
```mysql
select distinct DOB from second;
```

- `select sum(<column-name> from <table-name> where (condition)` -> This command is used to perform mentioned operations on the entire columns. Ex - more functions are avg, min, max etc. 
```mysql
select sum(score) as "Total" from second where Sports = "Cricket";
```

- `select <column-name>, count(*) from <table-name> group by <column-name>` -> This command is used to group the data from the mentioned column and display the count of entities.
```mysql
select Sports,count(*) from second group by Sports;
```

- `select <column-name>,avg(column-name) as "message" from <table-name> group by <column-name> having {condition};`-> This command is grouping data entries from the mentioned column fulfilling required condition and then performing an operation on the column mentioned for the same set of data entries.
```mysql
select Sports ,avg(score) as average from second group by Sports having Sports ="Cricket";
```

### Joins 
Types of Joins -
- `Inner join`  -> It display all the overlapping data of both the joined tables.
- `Left join` -> It displays all the overlapping data of both the joined tables along with the data of the left table or the table with which another table was joined.
- `Right join` -> It displays all the overlapping data of both the joined tables along with the data of the right table or the table joined to an another table.
- `Outer join `-> It displays all the data if any overlapping part is found in the tables to be joined.
- `Natural join `-> In joins the tables automatically if column-names are same in both the tables.It nothing matches it returns a cartesian product.

- `select * from <table-1> <type-of-join> <table-2> on (condition);`
```mysql
select * from Actors inner join DigitalAssets on Actors.id=DigitalAssets.id;

Another way of inner-join

select * from Actors,DigitalAssets where Actors.id = DigitalAssets.id;

Nautual join 
select FirstName URL from Actors natural join DigitalAssets;

```

```mysql
select 
	o.status,
	o.orderDate,
    od.orderNumber,
	od.quantityOrdered,
	p.productName,
	p.productLine
from orderDetails od 
JOIN products p ON od.productCode = p.productCode
JOIN orders o ON o.orderNumber = od.orderNumber
where od.orderNumber ='10101';
```
If column names are same then we can use the keyword using.Ex- using(id)

Note - If joining condition is not mentioned then it will return the cartesian product(i.e. it will match the given data entries from the first table to the all the data entries of the second table). This should be avoided as if the tables contain a large amount of data then it might/will cause the system to crash or go down. 
Total No of rows in cartesian product is 
     no.of rows of first table  X no. of rows in the second table.

**Union in Data entries** 
 - `(select * from <table-1> union (select * from <table-2>`    -> This will merge the two tables column-wise irrespective of the fact whether the data entries in a table match or not if column counts matches.
 - It executes the first query and appends the result of the second query to the result of the first query.
 Ex - 
 ```mysql
select orderNumber ,orderDate from orders where orderNumber = '10101'
UNION
select orderNumber, productCode from orderDetails where orderNumber = '10101';
```

**Database Schema** - It is like a blueprint of the database which is going to be created. It stores how data is going to be stored, structure of label etc. are defined in it.

**Functional Dependency** - It defines relationship between 2 attributes.
Ex - If Y depends on X then we can uniquely identify Y for every value of X.
  - Axioms or Rules for Functional Dependency
      - Reflexivity -> If one attribute is a sub-set of another attribute it is functional dependent on it. Ex- State is a subset of address.
      - Augmentation(Partial Dependency) -> It states that if suppose  Y is dependent of X then if we combine two attributes YZ then it is partially dependent of XZ for some attribute Z.
         Note - The problem with Partial Dependency is that if changes are to be made to one entry then it has to be changes in all the places which stores its redundant data.
    - Transitivity -> It state that if Y is dependent on X and Z is dependent on Y then Z is also dependent on X.

**Database Keys** - Keys are a set of attributes that help us to uniquely identify a record in different situations.Different types of keys - 
 - Super Key -> A **set** of attributes within a table which can uniquely identify a record. 
 ```mysql
{
(employee-id,employee-name),
employee-id,
employee-Phone-no,
.
.
}
```

 - Candidate Key -> It is the minimum set of attributes which can uniquely identify a record. In the above example employee-id is in itself sufficient to uniquely identify the tuples.
 - Composite Key -> A key which consists of two or more attributes which together can uniquely identify a record.These attributes are not keys independently.
 - Primary Key -> A none Null Candidate key is chosen to be a primary key. 
 - Alternate Key -> All candidate keys except the primary key are alternate key.
 - Foreign Key ->  A key attribute which is a primary key in some other table.
```mysql
R={A,B,C,D}
AB ->C
BC ->D
CD ->A
Here candidate keys are AB AND BC Both

R={A,B,C,D,E}
A ->B
A ->E
C ->B
C ->E
B ->D

Here the candidate key is (A,C).
```

**Functional Dependency Closure or f** ** -> It contains all the rules implied by Functional Dependencies.
**Attribute Closure** -> It defines all the attributes which can be determined using an attribute.

***
### Normalisation
It is the process of determining how much redundancy is there in a table and it gives techniques to reduce it.

- **First Normal Form** -> In this form any attribute must contain atomic values.
- **Second Normal Form** -> In this form the tables must not have partial dependencies and table should already be in 1NF form.
   This can be achieved by splitting the table into multiple tables.
- **Third Normal Form** -> In this form the tables must not have transitive dependencies and table should already by in 2NF form.
- **Boyce Codd Normal Form** -> In this form the tables must already be in 3NF form. For any dependencies like A -> B , A should be the super key.
     - Prime Attributes - Keys which can be used to obtain data of keys.
     - Non-Prime Attributes - Keys which are dependent of some other keys and their data can be obtained its dependency.
    Basically what happens in BCNF form is that the candidate key should only contain Prime attributes
- **Fourth Normal Form** - In this form the tables must already be in BCNF form and should not have multi-value dependencies.
Note - In case of many to many relation the join table created is called a **Through Table**.

**View Table** - Also known as virtual table.It is usually created from the result other queries and this results can be accessed by the end user for various operation. It is important from the perspective of security as it sends the user these virtual tables instead of the actual tables in the database.
Ex - 
```mysql 
CREATE OR REPLACE VIEW orderprouctview as
select 
	o.status,
	o.orderDate,
    od.orderNumber,
	od.quantityOrdered,
	p.productName,
	p.productLine
from orderDetails od 
JOIN products p ON od.productCode = p.productCode
JOIN orders o ON o.orderNumber = od.orderNumber
where od.orderNumber ='10101';
```

Note - If values are updated either in the database or in the view table they are reflected at both the places.

#### Stored Procedure - 
These are the set of queries which can be executed as and when required in the the databases. They are the functions in normal programming languages which can be called upon need.
Syntax - 
```mysql 
Ex-1 
use classicmodels
DELIMITER #
create PROCEDURE showLimitedOrder()
BEGIN
     select * from orders limit 10;
END #
DELIMITER ;

call showLimitedOrder();

Ex-2

use classicmodels
DELIMITER #
create PROCEDURE countingOrders(
IN orderNo varchar(255) ,OUT cnt int )
BEGIN
     select count(*) from orders where orderNumber= orderNo;
END #
DELIMITER ;

call countingOrders('10101',@cnt);
select @cnt;

Ex-3 Looping statements 
use classicmodels
DELIMITER #
create PROCEDURE proc()
BEGIN
     declare x INT;
     set x = 1;
     while x<=5 do
     SELECT x;
     set x=x+1;
     end while;
END #
DELIMITER ;

call proc();

```
Note - A Stored Procedure cannot be updated. In order to makes changes to a stored procedure you need to create a new one with a different naming.

### Triggers 
- Using Triggers we can add event-listeners to the databases which will be executed upon certain specified action.
```mysql
use classicmodels

Ex-1
DELIMITER $
CREATE trigger setprice
Before Insert On products
for each row 
    set NEW.MSRP=1;
$
Delimiter ;

Ex-2
use classicmodels

DELIMITER $
CREATE trigger Logger
Before Insert On products
for each row 
    set @log= "adding new product";
$
Delimiter ;

```

- New -> New keywords represents a new entry in the table. 
Note -> Just like stored procedure triggers once created cannot be updated. To. make changes to the triggers create a new one with a different name.

**Displaying Triggers and Procedures**
```mysql 
show triggers;
show procedure status where db='classicmodels';
```