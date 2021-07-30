/*
Creating Company Database
*/

create table Employee (
    emp_id int primary key,
    first_name varchar(20),
    last_name varchar (20),
    birth_day date,
    sex varchar(1),
    salary int,
    super_id int,
    branch_id int
);

create table Branch (
    branch_id int primary key,
    branch_name varchar(20),
    mgr_id int,
    mgr_start_date date,
    foreign key (mgr_id) references Employee(emp_id) on delete set NULL
);

-- ON DELETE SET NULL - A foreign key with "set null on delete" means that if a record in the parent table is deleted,
-- then the corresponding records in the child table will have the foreign key fields set to null. The records in the
-- child table will not be deleted.

alter table Employee
add foreign key (super_id) references Employee(emp_id) on delete set NULL;

alter table Employee
add foreign key (branch_id) references Branch (branch_id) on delete set NULL;

create table client(
    client_id int primary key,
    client_name varchar (20),
    branch_id int,
    foreign key (branch_id) references Branch (branch_id) on delete set NULL
);

create table works_with (
    emp_id int,
    client_id int,
    total_sales int,
    primary key(emp_id,client_id),
    foreign key (emp_id) references Employee(emp_id) on delete cascade,
    foreign key (client_id) references client (client_id) on delete cascade
);

-- ON DELETE CASCADE - A foreign key with "set null cascade" is used to automatically remove the matching records from
-- the child table when we delete the rows from the parent table. The records in the child table will be deleted automatically.

-- NOTE - If there is a situation where a foreign ley is also a primary key

create table branch_supplier (
    branch_id int,
    supplier_name varchar (20),
    supply_type varchar (20),
    primary key (branch_id, supplier_name),
    foreign key (branch_id) references Branch (branch_id) on delete cascade
);

--Corporate
insert into Employee values (100,'David','Wallace','1967-11-17','M',250000,NULL,NULL);

insert into Branch VALUES (1, 'Corporate', 100, '2006-02-09');

update Employee
set branch_id = 1
where emp_id = 100;

insert into Employee values (101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, 1);

-- Scranton
insert into Employee VALUES(102, 'Michael', 'Scott', '1964-03-15', 'M', 75000, 102, NULL);

insert into Branch VALUES(2, 'Scranton', 102, '1992-02-13');

update Employee
set branch_id = 2
where emp_id = 102;

insert into Employee VALUES(103, 'Angela', 'Martin', '1971-06-25', 'F', 63000, 102, 2);
insert into Employee VALUES(104, 'Kelly', 'Kappor', '1980-02-05', 'F', 55000, 102, 2);
insert into Employee VALUES(105, 'Stanley', 'Hudson', '1958-02-19', 'M', 69000, 102, 2);

--Stamford
insert into Employee VALUES(106, 'Josh', 'Porter', '1969-09-05', 'M', 78000, 100, null);

insert into Branch VALUES(3, 'Stamford', 106, '1998-02-13');

update Employee
set branch_id = 3
where emp_id = 106;

insert into Employee VALUES(107, 'Andy', 'Bernard', '1973-07-22', 'M', 65000, 106, 3);
insert into Employee VALUES(108, 'Jim', 'Halpert', '1978-10-01', 'M', 71000, 106, 3);

--branch supplier
insert into branch_supplier VALUES(2, 'Hammer Mill', 'Paper');
insert into branch_supplier VALUES(2, 'Uni-ball', 'Writing Utensils');
insert into branch_supplier VALUES(3, 'Patriot Paper', 'Paper');
insert into branch_supplier VALUES(2, 'J.T. Forms & Labels', 'Custom Forms');
insert into branch_supplier VALUES(3, 'Uni-ball', 'Writing Utensils');
insert into branch_supplier VALUES(3, 'Hammer Mill', 'Paper');
insert into branch_supplier VALUES(3, 'Stamford Labels', 'Custom Forms');

-- Client
insert into client VALUES(400, 'Dunmore Highschool', 2);
insert into client VALUES(401, 'Lackawama Country', 2);
insert into client VALUES(402, 'FedEx', 3);
insert into client VALUES(403, 'John Daily Law, LLC', 3);
insert into client VALUES(404, 'Scranton Whitepages', 2);
insert into client VALUES(405, 'Times Newspaper', 3);
insert into client VALUES(406, 'FedEx', 2);

--Works With
insert into works_with VALUES(105, 400, 55000);
insert into works_with VALUES(102, 401, 267000);
insert into works_with VALUES(108, 402, 22500);
insert into works_with VALUES(107, 403, 5000);
insert into works_with VALUES(108, 403, 12000);
insert into works_with VALUES(105, 404, 33000);
insert into works_with VALUES(107, 405, 26000);
insert into works_with VALUES(102, 406, 15000);
insert into works_with VALUES(105, 406, 130000);

-- Find all Employee
select * from Employee;

-- Find all employees ordered by salary
select * from Employee
order by salary;

-- Find all the employees ordered by sex and then name
select * from Employee
order by sex, first_name, last_name;

-- Find the first 5 employees in the tasble
select * from Employee
limit 5;

--Find the first and last names of all the employees
select first_name, last_name from Employee;

--Find the Forename & Surnames of all the employees
select first_name as Forename, last_name as Surname from Employee;

--Find all the different genders
select distinct sex
from Employee;

-- Find the number of employees
select COUNT (emp_id)
from Employee;

--Count the employees who have supervisors
select COUNT(super_id)
from Employee;

--Find the number of female employees born after 1970
select COUNT(sex) from Employee
where sex = 'F' AND birth_day > '1970-01-01';

-- Find the average of all the employee salary
select AVG(salary)
from Employee;

-- Find the average of all the male employee salary
select AVG(salary)
from Employee
where sex = 'M';

-- Find the sum of all employee salary
select SUM(salary)
from Employee;

-- find out how many males and females are there
select COUNT(sex) as total, sex
from Employee
group by sex
order by total;

-- Find the total sales of each salesman
select SUM(total_sales), emp_id
from works_with
group by emp_id;

-- Find how much amount each client spend
select SUM(total_sales), client_id
from works_with
group by client_id;

-- WILDCARDS
-- % = any no of characters
-- _ = ine character

-- Find any branch suppliers who are in the label business
select * 
from branch_supplier
where supplier_name LIKE '%label%';

-- Find all supliers supplying anything starting with "P" followed by any character, followed by "per"
select * 
from branch_supplier
where supply_type LIKE 'p_per';

-- Find any employee born in February
select *
from Employee
where birth_day LIKE '%02___';

-- Find all the employee whose first name starts with either "a" or "j"
select *
from Employee
where first_name like 'a%' or first_name like 'j%';


-- Find any clients who are school
select *
from client
where client_name LIKE '%school%';

-- Find the employee who has salary between 70000 and 100000
select salary, emp_id
from Employee
where salary BETWEEN 70000 AND 100000
order by salary;

-- Combine all the employee first and last name
select CONCAT(first_name,' ',last_name) as name
from Employee;

-- Create the list of employee and branch name in a single table named as List
select first_name as List
from Employee
UNION
select branch_name
from Branch;

-- Create a list of all clients and branch supploers names along with the branch id associated with the respected table
select client_name, client.branch_id
from client
UNION
select supplier_name, branch_supplier.branch_id
from branch_supplier;

-- Find the list of all money spend or earned by the company
select salary
from Employee
UNION
select total_sales
from works_with;

-- Find all branches and the names of their managers
select branch.branch_name, CONCAT(Employee.first_name,' ',Employee.last_name) as Emp_Name
from Employee
JOIN branch
on Employee.emp_id = branch.mgr_id;

-- Find all the employees along with the branch they are currently manager in (If any)
select CONCAT(Employee.first_name,' ',Employee.last_name) as Emp_Name, branch.branch_name as Manager_in
from Employee
LEFT JOIN branch
on Employee.emp_id = branch.mgr_id;

-- Insert New York branch with branch id "4" in branch table and find the employees along with the branch they are currently manager in. [NOTE - include all the branches no matter if they don't have any manager]
insert into branch (branch_id, branch_name) VALUES(4, 'New York') ;

select CONCAT(Employee.first_name,' ',Employee.last_name) as Emp_Name, branch.branch_name as Manager_in
from Employee
RIGHT JOIN branch
on Employee.emp_id = branch.mgr_id;

delete from branch
where branch_id = 4;

select * from branch;

-- Find all the employees and the branch to which they belong respectively
select CONCAT(Employee.first_name,' ',Employee.last_name) as Emp_Name, branch.branch_name
from Employee
JOIN branch
on Employee.branch_id = branch.branch_id;

-- Nested query
--Find all the employees who earn the minimum salary in a particular branch and arrange the list in ascending order on salary
select *
from Employee
where salary in
    (select min(salary)
    from Employee
    group by branch_id)
order by salary;

-- Find the names of all the employees who have sold over 30000 to a single client
select CONCAT(Employee.first_name,' ',Employee.last_name) as Emp_Name
from Employee
where Employee.emp_id in (
    select emp_id
    from works_with
    where total_sales > 30000
);

-- Find all the clients who are handled by the branch that Michael Scott manages [Assume you know Michael ID]
select client.client_name
from client
where client.branch_id = (
    select branch.branch_id
    from branch
    where branch.mgr_id = 102
    limit 1
);
