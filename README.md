## INSTALLATION GUIDE: https://www.cyberciti.biz/faq/how-to-install-docker-on-amazon-linux-2/


#### Mysql configuration on docker

#### PULL MYSQL IMAGE
```sql  
docker pull mysql/mysql-server:latest
```

#### RUN IMAGE
```sql
docker run -d --name=mysql-container -p 3306:3306 mysql/mysql-server
```

#### COPY DEFAULT PASSWORD
```sql
docker logs mysql-container
 ```

#### IF NO PASSWORD FOUND
```sql 
docker logs mysql-container 2>&1 | grep GENERATED
```

#### EXECUTE THE CONTAINER
```sql  
docker exec -it mysql-container sh
```

#### LOGIN
```sql
cd var/lib
mysql -u root -p
```

#### CHANGE ROOT USER PASSWORD
```sql 
ALTER USER 'root'@'localhost' IDENTIFIED BY '[newpassword]';
```

#### SQL COMMANDS

```sql 
show databases
use mysql;
\s // MYSQL INFORMATION
```

#### CREATE TABLE
```sql 
create table employee (id int not null primary key auto_increment, name varchar(255), gender varchar(255));
```

#### INSERT SINGLE RECORD
```sql 
insert into employee (id, name, gender) values (null, "John", "Male");
```

#### INSERT MULTIPLE RECORDS
```sql 
insert into employee (id, name, gender) values (), ();
```

#### UPDATE RECORD 
```sql 
update employee set gender = "Male"; // updates gender to all rows.
update employee set gender = "Male" where name = "John"; // updates gender of John
update employee set gender = "Male", city = "New Delhi" where name "John" // updates multiple columns
```
 
#### ALTER TABLE
#### ADD COLUMN
```sql 
alter table employee add column gender varchar(255);
```

#### MODIFY COLUMN
```sql 
alter table employee modify column customerName varchar(15);
```

#### RENAME COLUMN
```sql
alter table employee rename column gender to customerGender; 
```

#### DROP COLUMN
```sql 
alter table employee drop column gender;
```

#### ORDER BY
```sql 
select * from employee order by name asc | desc;
 ```

#### LIMIT
```sql 
select * from employee order by name asc limit 3;
```

#### OFFSET - ignore first n
```sql 
select * from employee order by name asc limit 3 offset 2;
 ```

#### ALIAS
```sql 
select name as employeeName from employee;
select name "employeeName" from employee;
```


#### CREATE FOREIGN KEY - DURING TABLE CREATION
```sql 
create table department (id not null primary key auto_increment, deptName varchar(200), cid int,
foreign key(cid) references employee(id));
```

#### CREATE FOREIGN KEY - AFTER TABLE IS CREATED
```sql 
create table department (id not null primary key auto_increment, deptName varchar(200)); 
alter table add column cid int;
```

```sql
alter table department add constraint fk_employee01 foreign key (cid) references customer(id); // WITH CONSTRAINT
```
```sql
alter table department add foreign key(cid) references customer(id); // WITHOUT CONSTRAINT
```

#### DROP FOREIGN KEY
```sql 
alter table department drop foreign key [constraint_name]
 ```

#### JOIN TABLES - FETCH DATA FROM MULTIPLE TABLES
#### Normal join
```sql
SELECT employee.name, employee.city, department.name
FROM employee, department
WHERE employee.id = department.eid
```

```sql  
SELECT e.name, e.city, d.name
FROM employee e, department d
WHERE e.id = d.eid
```


#### Functions
#### Sum
```sql 
select sum(salary) from employee where city = "New Delhi"; // total salary goes to new delhi employees
```

#### Avg
```sql 
select avg(salary) from employee where city = "New Delhi"; // average salary goes to new delhi employees
```

#### Count
```sql 
select count(name) from employee where city = "New Delhi"; // total count of employees from New Delhi location;
```
```sql 
select count(gender) from employee;
```

#### STRING FUNCTIONS
```sql 
length("str")
concate(str1, str2)
lcase(str)
ucase(str)
substring(str, start, length)
trim(str)
```

#### MORE FUNCTIONS
```sql 
database()
version()
user()
select DATABASE() "DB", VERSION() "version" USER() "user";
```

#### MATH FUNCTIONS
```sql 
sin
cos
tan
```

#### CREATE PROCEDURE
```sql 
delimiter //
```

```sql
DELIMITER //
create procedure CREATE_CUSTOMER ()
begin
create table customer (customerId int primary key auto_increment, customerName varchar(255));
insert into customer values (null, "John Doe");
insert into customer values (null, "James Smith");
insert into customer values (null, "David Doe");
insert into customer values (null, "Elenor Shellstrop");
insert into customer values (null, "Gustavo Gaviria");
end//

```
```sql
DELIMITER ;
```
```sql
 call CreateUserTable();
```


#### CREATE PROCEDURE WITH PARAMETER
```sql
delimiter //
```
```sql
create procedure COUNT_BY_LAST_NAME(IN last_name varchar(255), OUT count int);
begin
select count(*) into count from customer where customerName like concat('%', last_name, '%');
end //
delimiter ;

call COUNT_BY_LAST_NAME('Smith', @Result);
select @Result;
```
```sql
delimiter ;
```

#### LIST PROCEDURE
```sql
show procedure status where db = "db5";
```

#### DROP PROCEDURE
```sql
drop procedure PROCEDURE_NAME
```

#### CREATE USER 'admin' PASSWORD 'admin'
````sql
select host, user from user;

CREATE USER 'admin'@'%' IDENTIFIED BY 'admin';   // Create a new user account with a desired username and password: 

GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%';   // Grant appropriate privileges to the new user account:

FLUSH PRIVILEGES;   // to apply all changes

````

#### NODE JS CONNECTION

```js
// app.ts
import mysql from 'mysql2';

const connectDB = async() => {
  const credentials = {host: 'localhost', user: 'admin', password: 'admin'};
  try {
    const connection = await mysql.createConnection(credentials)
    connection.connect((error: any) => { 
      if(error) throw Error('connection failed.'+ error.message)
      console.log('==> Database connected');
    })
  } catch (error: any) {
    throw Error(error);
  }
}

export {connectDB};
```





#### PRIVILLAGES

#### Optional
Check the list of users

```
use mysql; 
select user from user;
```

#### CREATE A USER

```
CREATE USER 'dbeaver'@'%' IDENTIFIED BY 'dbeaver';
GRANT ALL PRIVILEGES ON *.* TO 'dbeaver'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```


